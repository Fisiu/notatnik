+++
banner = ""
categories = []
date = "2009-04-20T21:59:28+02:00"
description = ""
images = []
menu = ""
tags = ["openSUSE", "ajax", "aptana", "eclipse", "ide", "php"]
title = "Aptana IDE i openSUSE x86_64"

+++
[Aptana](http://www.aptana.com/) - to zintegrowane środowisko programistyczne zbudowane na bazie [Eclipse](http://www.eclipse.org/). Służy głównie do tworzenia aplikacji sieciowych w technologii [AJAX](http://pl.wikipedia.org/wiki/AJAX). Środowisko oferuje wsparcie dla _JavaScript_, _HTML_, _DOM_, _CSS_, uzupełnianie kodu oraz debugger JavaScript. Dzięki mechanizmowi wtyczek możemy w łatwy sposób dodać wsparcie dla _Ruby on Rails_, _PHP_, _Python_, _Perl_, _Adobe AIR_ oraz _Apple iPhone_. Aplikacja dostępna jest na wiele platform, jak i również w formie wtyczki do _Eclipse_. Aptana, jako samodzielna aplikacja dostępna jest na platformę 32 bitową. Jednak po kilku prostych zabiegach możliwe jest jej uruchomienie w systemie x86_64.
<!--more-->
Najpierw musimy pobrać główną aplikację Aptana Studio ze [strony domowej](http://www.aptana.com/). W tym opisie wszystkie pobierane pliki znajdują się w katalogu domowym, `~/`.

{{< kbd "wget http://update.aptana.com/studio-standalone/Aptana_Studio_Setup_Linux_1.2.6.zip" >}}

Następnie tworzymy katalog `/opt/aptana`, zmieniamy jego właściciela i rozpakowujemy tam pobrany przed momentem plik.

{{< kbd "su" >}}
{{< kbd "mkdir /opt/aptana" >}}
{{< kbd "chown użytkownik:users /opt/aptana>" >}}
{{< kbd "exit" >}}
{{< kbd "unzip ~/Aptana_Studio_Setup_Linux_1.2.6.zip -d /opt" >}}

Kolejno pobieramy i rozpakowujemy mozilla-xulrunner w wersji 32bit.
{{< kbd "wget http://releases.mozilla.org/pub/mozilla.org/xulrunner/releases/1.8.1.3/contrib/linux-i686/xulrunner-1.8.1.3.en-US.linux-i686-20080128.tar.gz" >}}
{{< kbd "tar -xvf ~/xulrunner-1.8.1.3.en-US.linux-i686-20080128.tar.gz -C /opt/aptana" >}}

Teraz pozostało nam jeszcze doinstalowanie środowiska Javy 32bit. Uruchamiamy YaST → Oprogramowanie → Zarządzanie oprogramowaniem. Wybieramy pakiet widoczny na obrazku poniżej i akceptujemy zmiany.

!["sun_java_i586"](/img/2009/sun_java_i586.png)

Kolejną czynnością jaką musimy wykonać jest napisanie prostego skryptu o nazwie np. _RunAptana.sh_. Można użyć dowolnego edytora. Ja posłużę się vi.

{{< kbd "vi /opt/aptana/RunAptana.sh" >}}

Kod skryptu powinien wyglądać tak:

```bash
#!/bin/bash
MOZILLA_FIVE_HOME=/opt/aptana/xulrunner
if [ $LD_LIBRARY_PATH ]; then
LD_LIBRARY_PATH=$MOZILLA_FIVE_HOME:$LD_LIBRARY_PATH
else
LD_LIBRARY_PATH=$MOZILLA_FIVE_HOME
fi
export MOZILLA_FIVE_HOME LD_LIBRARY_PATH
/opt/aptana/AptanaStudio -vm /usr/lib/jvm/java-1.6.0-sun-1.6.0/jre/bin/java
```

I teraz już możemy zacząć korzystać z Aptany, uruchamiając ją za pomocą tego skryptu:

{{< kbd "/opt/aptana/RunAptana.sh" >}}

Bardziej wymagający użytkownicy mogą sobie stworzyć jeszcze skrót w menu aplikacji.
