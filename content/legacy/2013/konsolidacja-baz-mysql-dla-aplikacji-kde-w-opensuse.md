+++
banner = ""
categories = ["openSUSE"]
date = "2013-11-21T16:50:33+02:00"
description = ""
images = []
menu = ""
tags = ["openSUSE", "KDE"]
title = "Konsolidacja baz mysql dla aplikacji KDE w openSUSE"

+++
Pulpit plazmy korzysta z akonadi, które w domyślnej konfiguracji używa własnej instancji mysql/mariadb. Amarok przechowuje informacje o naszej bibliotece (notowania, teksty, oceny) również w bazie mysql. W tym celu korzysta również z własnej instancji. DigiKam domyślnie przechowuje informacji o kolekcji obrazów w bazie sqlite. Przy większych kolekcjach, może okazać się, że wydajność sqlite jest niewystarczająca. Nic nie stoi na przeszkodzie, aby wszystkie bazy przenieść do systemowej instancji mariadb. Dzięki temu unikniemy dublowania instancji baz dla akonadi i amaroka oraz przyspieszymy działanie digiKama.

I krótka legenda dla kodów użytych w tym wpisie.Kody zaczynające się od:

* \# - należy wykonać jako root
* $ - należy wykonać jako zwykły użytkownik
* \> - należy wykonać w konsoli mysql/mariadb

Zanim zaczniemy migrować bazy, należy zainstalować serwer mysql/mariadb i uruchomić go:

{{< kbd "# zypper in mariadb" >}}
{{< kbd "# systemctl enable mysql" >}}
{{< kbd "# systemctl start mysql" >}}

<!-- more -->

### Akonadi

Upewniamy się, że akonadi działa:

{{< kbd "$ akonadictl status" >}}

Tworzymy zrzut aktualnej bazy akonadi za pomocą:

{{< kbd "$ mysqldump --socket=~/.local/share/akonadi/socket-$HOSTNAME/mysql.socket akonadi > ~/akonadi-backup.sql" >}}

Zatrzymujemy serwer akonadi:

{{< kbd "$ akonadictl stop" >}}

Zmieniamy konfigurację bazy danych akonadi, tak aby korzystała z zewnętrznego serwera mysql. Możemy edytować plik `~/.config/akonadi/akonadiserverrc` by jego zawartość wyglądała następująco:

```
[%General]
Driver=QMYSQL
SizeThreshold=4096
ExternalPayload=false

[QMYSQL]
Name=akonadi
Host=localhost
Options=
ServerPath=/usr/sbin/mysqld
StartServer=false
User=akonadi
Password=akonadi

[Debug]
Tracer=null
```

Lub możemy uruchomić:

{{< kbd "$ kcmshell4 akonadi" >}}

Odznaczamy 'Używaj wewnętrznego serwera MySQL' i uzupełniamy dane jak na rysunku poniżej.

![akonadi-system-mariadb](/img/2013/akonadi-system-mariadb.png)

Następnie konieczne jest dodanie bazy danych i użytkownika.

{{< kbd "> CREATE USER 'akonadi'@'localhost' IDENTIFIED BY 'akonadi';" >}}
{{< kbd "> CREATE DATABASE `akonadi`;" >}}
{{< kbd "> GRANT ALL PRIVILEGES ON akonadi.* to 'akonadi'@'localhost' IDENTIFIED BY 'akonadi';" >}}

Następnie należy przywrócić nasz zrzut bazy akonadi za pomocą:

{{< kbd "$ mysql akonadi < akonadi-backup.sql" >}}

Teraz pozostało nam już tylko uruchomić serwer akonadi za pomocą:

{{< kbd "$ akonadictl start" >}}

Jeśli spotkamy się z błędem:

```mysql
Sql error: Table 'akonadi.SchemaVersionTable' doesn't exist QMYSQL: Unable to execute query
```

należy zmienić nazwy table naszej bazy na format [CamelCase](http://en.wikipedia.org/wiki/CamelCase).


{{< kbd "> RENAME TABLE schemaversiontable TO SchemaVersionTable;" >}}
{{< kbd "> RENAME TABLE resourcetable TO ResourceTable;" >}}
{{< kbd "> RENAME TABLE collectionattributetable TO CollectionAttributeTable;" >}}
{{< kbd "> RENAME TABLE collectionmimetyperelation TO CollectionMimeTypeRelation;" >}}
{{< kbd "> RENAME TABLE collectionpimitemrelation TO CollectionPimItemRelation;" >}}
{{< kbd "> RENAME TABLE collectiontable TO CollectionTable;" >}}
{{< kbd "> RENAME TABLE flagtable TO FlagTable;" >}}
{{< kbd "> RENAME TABLE mimetypetable TO MimeTypeTable;" >}}
{{< kbd "> RENAME TABLE parttable TO PartTable;" >}}
{{< kbd "> RENAME TABLE pimitemflagrelation TO PimItemFlagRelation;" >}}
{{< kbd "> RENAME TABLE pimitemtable TO PimItemTable;" >}}

Od teraz akonadi będzie korzystało z systemowej instancji mysql/mariadb.
Możliwe są dalsze [optymalizacje](http://cgbdx.wordpress.com/2011/07/21/how-to-setup-your-external-sql-server-for-akonadi/) bazy danych, adekwatne do [konfiguracji](https://projects.kde.org/projects/kdesupport/akonadi/repository/revisions/master/entry/server/src/storage/mysql-global.conf) używanej przez dedykowaną instancję bazy.


### Amarok

Zatrzymujemy serwer mysql/mariadb:

{{< kbd "# systemctl stop mysql" >}}

Uruchamiamy serwer tylko z bazą amaroka:

{{< kbd "$ cd ~/.kde4/share/apps/amarok" >}}
{{< kbd "$ /usr/sbin/mysqld --defaults-file=`pwd`/my.cnf --default-storage-engine=MyISAM --datadir=`pwd`/mysqle --socket=`pwd`/sock --skip-grant-tables" >}}

Teraz pozostaje utworzyć zrzut bazy amaroka:

{{< kbd "$ mysqldump -S sock amarok > amarok.sql" >}}

Po wykonaniu zrzuty możemy już zatrzymać serwer z bazą amarok i uruchomić serwer z konfiguracją globalną.

{{< kbd "# systemctl start mysql" >}}

Następnie konieczne jest utworzenie bazy danych, do której zaimportujemy dane z zrzutu.
Tworzymy bazę i użytkownika:

{{< kbd "> CREATE USER 'amarok'@'localhost' IDENTIFIED BY 'amarok';" >}}
{{< kbd "> CREATE DATABASE `amarok`;" >}}
{{< kbd "> GRANT ALL PRIVILEGES ON amarok.* to 'amarok'@'localhost' IDENTIFIED BY 'amarok';" >}}

Importujemy zrzut do nowej bazy:

{{< kbd "$ mysql -u amarok -p amarok < amarok.sql" >}}

Teraz pozostaje tylko skonfigurować amaroka, aby korzystał z zewnętrznej bazy danych. Dane muszą być oczywiście takie jakich użyliśmy przed chwilą.

![Konfiguracja amaroka i zewnętrznej bazy](/img/2013/amarok-system-mariadb.png)


### digiKam

Zaczniemy od utworzenia 2 nowych baz dla digiKama i użytkownika dla tych baz.

{{< kbd "> CREATE USER 'digikam'@'localhost' IDENTIFIED BY 'digikam';" >}}
{{< kbd "> CREATE DATABASE `digikam`;" >}}
{{< kbd "> CREATE DATABASE `thumbnails-digikam`;" >}}
{{< kbd "> GRANT ALL PRIVILEGES ON digikam.* to 'digikam'@'localhost' IDENTIFIED BY 'digikam';" >}}
{{< kbd "> GRANT ALL PRIVILEGES ON thumbnails-digikam.* to 'digikam'@'localhost' IDENTIFIED BY 'digikam';" >}}

Następnie korzystamy z wbudowanego w digiKam narzędzia do migracji bazy danych. W tym celu uruchamiamy digiKam i z menu `Ustawienienia` wybieramy `Migracja bazy danych`. W lewej części okna wybieramy sqlite i podajemy ścieżkę gdzie są aktualnie bazy przechowywane. Domyślnie jest to `~/Obrazy`. W prawej części okna uzupełniamy dane niezbędne do połączenia z bazą mysql/mariadb.

![Migracja sqlite do mariadb w digiKam](/img/2013/digikam-system-mariadb.png)

Pozostaje sprawdzić połączenie i zmigrować naszą bazę sqlite do mysql/mariadb przez naciśnięcie przycisku `Migruj ->`.
Czas migracji zależny jest od wielkości naszej kolekcji oraz wydajności naszego sprzętu, zwłaszcza dysku twardego i procesora. Po migracji ostatnim krokiem jest skonfigurowanie digiKama, aby korzystał z bazy mysql/mariadb. Z menu `Ustawienia` wybieramy `Konfiguracja: digiKam...` i w sekcji `Baza danych` należy wybrać MySQL i uzupełnić dane połączenia.

![Konfiguracja mysql w digiKam](/img/2013/digikam-use-system-mariadb.png)

UWAGA! Jeśli z komputera korzysta kilku użytkowników, należy dla każdego użytkownika utworzyć osobną bazę. Jako nazwę dla baz, można użyć schematu `$USER_akonadi`, `$USER_amarok` i `$USER_digikam`.
