+++
banner = ""
categories = []
date = "2010-11-04T10:37:56+02:00"
description = ""
images = []
menu = ""
tags = ["factory", "openSUSE"]
title = "11.4 M3 spóźnione - wina KDE SC?"
slug = "11-4-m3-spoznione-wina-kde-sc"

+++
Według [planu wydania](http://en.opensuse.org/Roadmap) jutro powinien ukazać się kolejny, trzeci kamień milowy openSUSE 11.4. Jak zapowiedział wczoraj Stephan Kulow, na liście [opensuse-factory](http://lists.opensuse.org/opensuse-factory/2010-11/msg00036.html), M3 zostaje opóźniony. Powodem takie decyzji jest nadal niepoprawiony błąd w menadżerze okien KWin który skutkuje crashami serwera X przy włączonych efektach pulpitu. Jeśli błąd zostanie naprawiony szybko, M3 ujrzy światło dzienne w przyszłym tygodniu. Jednak dość prawdopodobne jest to, że tak się nie stanie. Wówczas M3 będzie miał wyłączoną opcję efektów pulpitu. Czas pokaże w jakim stanie dostaniemy M3 do testów ;)

Będąc przy temacie "factory" warto wspomnieć o szerszych testach [systemd](http://lists.opensuse.org/opensuse-factory/2010-10/msg00244.html) - który być może zastąpi w oS 11.4 SysVinit. A najlepsze w tym wszystkim jest to, że aktualne wydanie oS 11.3 dostało działającego upstarta. Choć nie jest nawet domyślnie włączony i zanim to nastąpi jego miejsce może zająć systemd.

Jeśli jednak ktoś chce przełączyć się w openSUSE 11.3 z SysVinit na upstart wystarczy zainstalować pakiet 'upstart':

{{< kbd "su" >}}
{{< kbd "zypper in upstart" >}}

Od teraz każdy następny uruchomienie systemu będzie zarządzane i kontrolowane przez upstart.
