+++
banner = ""
categories = []
date = "2008-11-06T18:25:49+02:00"
description = ""
images = []
menu = ""
tags = []
title = "openSUSE Beta 4 jeszcze nie dla mnie"

+++
W poniedziałek, 2008-11-03, [ukazała](http://news.opensuse.org/2008/11/03/development-release-opensuse-111-beta-4-now-available/) się kolejna testowa wersja systemu openSUSE, oznaczona jako Beta 4. Spragniony testów przystąpiłem do pobierania obrazu [Delta ISO](http://pl.opensuse.org/Download_Help#Aplikowanie_delta_ISO). Po pomyślnym utworzeniu pełnego obrazu iso nadszedł moment instalacji. Sam proces instalcji przebiegł w sposób standardowy. Miejscem docelowym nowej instalacji miała być mała partycja (~12GB) utworzona na macierzy "[fake RAID](http://en.wikipedia.org/wiki/RAID#Firmware.2Fdriver_based_RAID)".
<!-- more -->
Instalacja przebiegła pomyślnie, nawet z zainstalowaniem [Gruba](http://pl.wikipedia.org/wiki/Grub) nie było problemów. Po ponownym uruchomieniu komputera okazało się, że nie można uruchomić dopiero co zainstalowanego systemu.

Komunikat, który mnie przywitał wyglądał tak:

```
(...)
usbcore: registered new interface driver usbhid
usbhid: v2.6:USB HID core driver
...........................Could not find /dev/mapper/nvidia_ifjaecch_part2.
Want me to fall back to /dev/mapper/nvidia_ifjaecch_part2? (Y/n)
y
Waiting for device /dev/mapper/nvidia_ifjaecch_part2 to appear: ...........................not found -- exiting to /bin/sh
$_
```

Po chwili postanowiłem zajrzeć na bugzillę Novell'a, gdzie znalazłem stosowne informacje na ten temat. Całe szczęście, że problem został już rozwiązany. Po szczegóły odsyłam do [źródła](https://bugzilla.novell.com/show_bug.cgi?id=439439).
Jak dla mnie wersja Beta 4 jest bezużyteczna. Pozostaje czekanie na kolejne wydanie deweloperskie, które ma się ukazać już niebawem.
