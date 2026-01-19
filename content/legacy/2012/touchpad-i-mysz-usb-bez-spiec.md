+++
banner = ""
categories = ["openSUSE"]
date = "2012-04-25T14:24:23+02:00"
description = ""
images = []
menu = ""
tags = ["touchpad", "openSUSE"]
title = "Touchpad i mysz usb bez spięć"
slug = "touchpad-i-mysz-usb-bez-spiec"

+++
Często pracując na laptopie korzystam z zewnętrznej myszki na usb. Jednak po jej podłączeniu touchpad nadal działa a "magiczny" skrót do jego obsługi Fn + F3 **\*** zdaje się być bezużyteczny. Z pomocą przychodzi nam udev i wszechstronność jego reguł. Aby wyłączyć touchpad po podłączeniu myszy do portu usb i automatycznie go włączyć po jej odłączeniu wystarczy, że utworzymy 2 proste reguły. Tworzymy plik `/etc/udev/rules.d/01-touchpad.rules` z zawartością zamieszczoną poniżej. W miejsce `$user` wstawiamy nazwę użytkownika.

```bash
ACTION=="add", SUBSYSTEM=="input", KERNEL=="mouse[1-9]", ENV{DISPLAY}=":0.0", ENV{XAUTHORITY}="/home/$user/.Xauthority", ENV{ID_CLASS}="mouse", RUN+="/usr/bin/synclient TouchpadOff=1"
ACTION=="remove", SUBSYSTEM=="input", KERNEL=="mouse[1-9]", ENV{DISPLAY}=":0.0", ENV{XAUTHORITY}="/home/$user/.Xauthority", ENV{ID_CLASS}="mouse", RUN+="/usr/bin/synclient TouchpadOff=0"
```

**\*** Dell Vostro 3450 + Linux 3.3.2-1-desktop

Pozwoliłem sobie na edycję posta z bardzo prostego powodu. Człowiek pisze reguły udev zamiast uruchomić `synaptiks` i zaznaczyć żądaną opcję. Zdecydowanie szybciej i wygodniej. Powyższy plik można spokojnie usunąć :wink:

!["Konfiguracja touchpada w KDE"](/img/2012/synaptiks-with-mouse.png)
