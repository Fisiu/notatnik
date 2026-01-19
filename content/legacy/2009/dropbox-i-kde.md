+++
banner = ""
categories = ["openSUSE"]
date = "2009-02-26T16:41:20+02:00"
description = ""
images = []
menu = ""
tags = ["dropbox", "kde", "linux"]
title = "Dropbox i KDE"

+++

Dropbox jest usługą pozwalającą nam na synchronizację plików pomiędzy komputerami. Nasze dane są przesyłane na serwer a z niego na inne nasze komputery. O cały proces dba aplikacja działająca w tle, która monitoruje nasze pliki i w razie potrzeby dokonuje ich aktualizacji. Darmowa wersja konta udostępnia nam 2GB przestrzeni dyskowej. Aczkolwiek istnieje sposób na powiększenie jej do 6GB bez wydawania nawet złotówki. Po więcej informacji na ten temat zapraszam na [https://www.getdropbox.com/referrals](https://www.getdropbox.com/referrals).

Twórcy usługi nie ograniczają się tylko do użytkowników _jedynie słusznego systemu_ i dlatego udostępnili aplikację zarówno dla Windows, MacOSX jak i Linux. Oficjalna wersja dla  _pingwina_ jest zintegrowana z nautilusem, elementem środowiska Gnome. Jednak cóż począć, jeśli korzystamy z KDE? A i na to jest rada ;)
<!-- more -->
Najpierw musimy pobrać aplikację stosowną do wersji naszego systemu.
  * [Dropbox](http://www.getdropbox.com/download?plat=lnx.x86) dla wersji 32-bit
  * [Dropbox](http://www.getdropbox.com/download?plat=lnx.x86_64) dla wersji 64-bit

Załóżmy, że archiwum z aplikacją zostanie zapisane w naszym katalogu domowym, `~/`.

Następnie musimy je rozpakować. W tym celu możemy użyć menu kontekstowego menedżera plików bądź wydając polecenie w konsoli:
{{< kbd "tar -xvf dropbox-lnx.x86*" >}}

Archiwum zostnie wypakowane do naszego katalogu domowego. Następnie przechodzimy do miejsca, gdzie zostało ono rozpakowane:
{{< kbd "cd ~/.dropbox-dist" >}}

Teraz pozostaje nam już tylko uruchomić program, wydając polecenie:
{{< kbd "./dropboxd" >}}

Dalej postępujemy zgodnie z kreatorem pierwszego uruchomienia, gdzie możemy określić m.in. katalog, którego zawartość będzie synchronizowana.

Jeśli chcemy, aby  _Dropbox_ był uruchamiany razem z KDE, wystarczy dodać go do aplikacji auto startu. W tym celu wybieramy z menu systemowego _Ustawienia Systemowe → Zaawansowane → Automatyczne Uruchomienie_. W oknie konfiguracji wybieramy przycisk  **Add Program** i podajemy ścieżkę do programu:
{{< kbd "~/.dropbox-dist/dropboxd" >}}

Zaznaczamy jeszcze opcję **Enabled**, aby aktywować automatyczne uruchamianie dopiero co skonfigurowanego programu.

Od tej pory _Dropbox_ będzie czuwał nad stanem naszych plików po każdym uruchomieniu komputera.

!["Dropbox w tacce Systemowej"](/img/2009/dropbox_tray-300x55.png)
