+++
banner = ""
categories = ["openSUSE"]
date = "2013-03-03T13:19:19+02:00"
description = ""
images = []
menu = ""
tags = ["openSUSE", "chromium", "flash", "ppapi"]
title = "Chromium i flash via PPAPI"

+++
Ady korzystać z najnowszego flasha w openSUSE konieczne jest zainstalowanie pakietu `chromium-pepper-flash`. Dostępny jest on w repozytorium **packmana**. Instalacja ogranicza się tylko do wykonania:

{{< kbd "zypper in chromium-pepper-flash" >}}

Jednak aby chromium współpracowało z nową wtyczką, konieczne jest dodanie odpowiednich flag do globalnego pliku konfiguracyjnego chromium. Jako root edytujemy plik **/etc/default/chromium** i dodajemy poniższe flagi. Jeśli już korzystamy z innych flag, wystarczy je dopisać na końcu.

```config
CHROMIUM_FLAGS="--ppapi-flash-path=/usr/lib/chromium/PepperFlash/libpepflashplayer.so"
```

Jeśli korzystamy z openSUSE w wersji x86_64, ścieżka do wtyczki zawiera **lib64** zamiast **lib**.

Po ponownym uruchomieniu przeglądarki chromium, odwiedzamy adres `chrome://plugins`. Szukamy wtyczek flasha i wyłączamy wersję NPAPI. Od teraz chromium będzie korzystało z nowego flasha, aktualnie w wersji 11.6. Dzięki temu, karta graficzna działająca na otwartym sterowniku radeon czy intel wykorzystywana jest do renderowania obrazu. Zapewne podobna sytuacja będzie mieć miejsce w przypadku korzystania z innego sprzętu i sterowników, choć sam na innych konfiguracjach tego nie testowałem.
