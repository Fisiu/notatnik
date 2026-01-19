+++
banner = ""
categories = ["openSUSE"]
date = "2016-07-13T00:38:54+02:00"
description = ""
images = []
menu = ""
tags = ["drukarka", "skaner", "brother"]
title = "Brother DCP-J140W w openSUSE Leap 42 1"
slug = "brother-dcp-j140w-w-opensuse-leap-42-1"

+++
openSUSE Leap 42.1 zagościł u mnie stosunkowo późno, chyba dopiero około pół roku po premierze. I to tylko na jednym komputerze. Do tej pory wykonywałem uaktualnienie, wykonując nadzwyczaj magiczne polecenie
{{< kbd "su" >}}
{{< kbd "zypper dup" >}}

O ile mnie pamięc nie myli, to ta historia powtarzała się od kilku już lat. Począwszy od wersji 12.1, który była instalowana "na czysto". Jednak przy wersji 42.1 ponownie postanowiłem zainstalować system na czysto. A jak wiadomo, wiąże się to zawsze za kopią i przywracaniem plików. Dodatkowo jest to dobra okazja aby nieco posprzątać, zwłaszcza w miejscach, gdzie dawno nie zaglądaliśmy...
<!--more-->
Sama instalacja openSUSE Leap 42.1 nie stanowiła żadnego problemu. Pliki również udało się przywrócić dość sprawnie, konfiguracja vima i powłoki leży w repozytorium gita - więc i tu poszło gładko. I tak przez jakiś czas system pracował, wydawało mi się, że o niczym nie zapomniałem. Aż do czasu kiedy chciałem coś przeskanować i wydrukować. Wszak Brother DCP-J140W działał przez sieć, choć było to jeszcze na starym systemie. Więc zabrałem się za instalację, choć sama [dokumentacja](http://support.brother.com/g/s/id/linux/en/index.html?c=us_ot&lang=en&comple=on&redirect=on) mówi, że to bułka z masłem. Na pierwszy ogień poszedł skaner. Po instalacji sterownika z pakietu rpm konieczne było dodadnie skanera. Poszło gładko.
{{< kbd "su" >}}
{{< kbd "zypper in ~/Pobrane/brscan4-0.4.3-3.x86_64.rpm" >}}
{{< kbd "brsaneconfig4 -a name=DCP-J140W model=DCP-J140W ip=192.168.1.10" >}}

W razie czego pomagamy sobie `brsaneconfig4 -h`.

Niestety, pomimo tego, że polecenie
{{< kbd "brsaneconfig4 -q" >}}

informowało, że urządzenie jest dostępne:
```terminal
Devices on network
  0 DCP-J140W           "DCP-J140W"         I:192.168.1.10
```
to żadna aplikacja do skanowania nie mogła ze skanerem się połączyć. Dokumentacja milczy na ten tema, jednak rozwiązanie okazło się całkiem proste. Wystarczy dodać na końcu pliku `/etc/sane.d/dll.conf` linię `brother4`.

Za skanerem poszła drukarka. Bez większych przygód. Instalacja sterownika ograniczała się do:
{{< kbd "su" >}}
{{< kbd "zypper in ~/Pobrane/dcpj140wcupswrapper-1.1.3-6.i386.rpm ~/Pobrane/dcpj140wlpr-1.1.3-6.i386.rpm" >}}

Potem zostało już tylko dodanie drukarki w [CUPS](http://www.cups.org/). Ja w tym celu wykorzystałem interfejs www pod adresem [http://localhost:631](http://localhost:631). W sekcji `Administration` → `Add printer` → `LPD/LPR` i jako połączenie wpisujemy `lpd://192.168.1.10/binary_p1`. Następnie podajemy nazwę i opis a później wskazujemy plik .ppd. W moim przypadku był to plik `/opt/brother/Printers/dcpj140w/cupswrapper/brother_dcpj140w_printer_en.ppd`. Na samym końcu zostało wybranie domyślnych ustawień drukowania.

Tadam! Można drukować i skanować.

UWAGA. W odpowiednich miejscach użyj adresu IP który odpowiada twojemu urządzeniu ;-)
