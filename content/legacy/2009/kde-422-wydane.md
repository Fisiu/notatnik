+++
banner = ""
categories = ["openSUSE"]
date = "2009-04-02T16:43:50+02:00"
description = ""
images = ["img/2009/desktop_kde42.png"]
menu = ""
tags = ["openSUSE", "kde", "plazma", "widzet"]
title = "KDE 4.2.2 wydane!"
slug = "kde-4-2-2-wydane"

+++
Bez większego rozgłosu wydana została dzisiaj, tj 02.04.2009 kolejna wersja środowiska KDE 4.2.2. Nazwa kodowa tego wydanie to "_**Cano**_". Aktualizacja wnosi sporo poprawek, zwłaszcza w silniku przeglądarki Konqueror – [KHTML](http://pl.wikipedia.org/wiki/KHTML) oraz w programie pocztowym - [KMail](http://pl.wikipedia.org/wiki/KMail). Dodano także sporo poprawek zwiększających stabilność KRunner. Pełna lista zmian, w porównaniu do wydania 4.2.1, dostępna jest na stronach  [http://www.kde.org](http://www.kde.org/announcements/changelogs/changelog4_2_1to4_2_2.php).

!["desktop_kde42"](/img/2009/desktop_kde42.png)

Pakiety dla openSUSE są już dostępne w repozytorium KDE4:Factory. Aby zainstalować aktualną wersję KDE w openSUSE 11.1,  wystarczy dodać poniższe repozytoria za pomocą Yast:

`http://download.opensuse.org/repositories/KDE:/KDE4:/Factory:/Desktop/openSUSE_11.1/`
`http://download.opensuse.org/repositories/KDE:/KDE4:/Factory:/Extra-Apps/openSUSE_11.1/`
`http://download.opensuse.org/repositories/KDE:/KDE4:/Community/openSUSE_11.1_KDE4_Factory_Desktop/`

Dla poprzednich edycji openSUSE repozytoria są także dostępne. Wystarczy w adresie repozytorium zmienić 11.1 na odpowiedni numerek posiadanego przez nas systemu.

Następnie przeprowadzić standardową aktualizację lub wykonać w konsoli:

{{< kbd "su" >}}
{{< kbd "zypper up" >}}
