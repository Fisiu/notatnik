+++
banner = ""
categories = []
date = "2011-02-25T13:20:44+02:00"
description = ""
images = []
menu = ""
tags = []
title = "Koniec spamowania ;)"

+++
Jako, że cały czas poszukiwałem wtyczki odpowiedzialnej za kolorowane składni w WordPressie dzisiaj przyszła pora na zmianę... Aktualnie ustawiłem <del>CodeColorer</del> SyntaxHighlighter. Wtyczka ta korzysta z tagów code a nie z pre tak jak poprzednia. W związku z tym zmodyfikowałem kilka postów aby zastosować style nowej wtyczki. Niestety spowodowało to zaśmiecenie planety openSUSE więc dalszych edycji zaniechałem.
Przepraszam czytelników za spam :)

W ramach przypomnienia, chciałem napisać o zmianie struktury repozytorium Packman. Wraz z [aktualizacją OBS do 2.1](http://lists.links2linux.de/pipermail/packman/2011-February/009422.html) na serwerach Packmana zmieniono układ repozytoriów. Do tej pory dostępne było jedno repozytorium w którym znajdowały się wszystkie pakiety. Aktualnie trwa przebudowywanie wszystkich pakietów więc nowy układ repozytoriów nie jest jeszcze kompletny. Jednak w efekcie końcowym, Packman będzie miał 4 repozytoria:

* Essentials - podstawowe kodeki, MPlayer, SMPlayer
* Multimedia - dodatkowe multimedia
* Games - gry
* Extra - wszystko co nie weszło w skład trzech powyższych

Więc każdy będzie mógł dodać to co mu pasuje. Jednak jeśli ktoś będzie chciał mieć tylko jedno repozytorium zawierające wszystkie powyższe, dostępny będzie plik .repo. Tym sposobem będzie można korzystać z Packmana tak jak dotychczas.
