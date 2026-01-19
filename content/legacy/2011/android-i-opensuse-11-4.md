+++
banner = ""
categories = []
date = "2011-03-24T13:33:44+02:00"
description = ""
images = []
menu = ""
tags = ["android", "openSUSE"]
title = "Android i openSUSE 11.4"
slug = "android-i-opensuse-11-4"

+++
Po instalacji i konfiguracji openSUSE 11.4 okazało się, że po instalacji [SDK Androida](http://developer.android.com/sdk/index.html) nie można połączyć się z zewnętrznym urządzeniem. Efekt jest taki:

{{< kbd "adb devices" >}}
```terminal
List of devices attached
????????????     no permissions
```

Rozwiązanie jest bardzo proste. Należy najpierw sprawdzić, jak identyfikuje się nasz sprzęt.

{{< kbd "lsusb" >}}
```terminal
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 002: ID 0dda:2005 Integrated Circuit Solution, Inc. Datalux DLX-1611 16in1 Card Reader
Bus 001 Device 004: ID 04e8:681c Samsung Electronics Co., Ltd ← Moje urządzenie
```

Istotną informacją jest ID producenta, w moim wypadku **04e8**.
Teraz pozostało stworzyć odpowiednią regułę udev. Bez zagłębiania się w szczegóły reguł udev, można to zrobić tak:

{{< kbd "su" >}}
{{< kbd "echo 'SUBSYSTEM==\"usb\", ATTRS{idVendor}==\"04e8\", ATTRS{idProduct}==\"681c\", MODE=\"0660\" GROUP=\"users\"' > /etc/udev/rules.d/51-android.rules" >}}

Od teraz urządzenie powinno już prawidłowo działać z naszym systemem.
