+++
banner = ""
categories = []
date = "2009-02-03T12:59:08+02:00"
description = ""
images = []
menu = ""
tags = []
title = "Aktualizacja OpenOffice.org do wersji 3.0.1"
slug = "aktualizacja-openoffice-org-do-wersji-3-0-1"

+++
Kilka dni temu ukazała się najnowsza edycja pakietu biurowego – OpenOffice.org 3.0.1. Dla openSUSE 11.1 pakiety są dostępne w  _BuidService_ w repozytorium [OpenOffice.org:STABLE](http://download.opensuse.org/repositories/OpenOffice.org:/STABLE/openSUSE_11.1/)

Jednak po dokonaniu aktualizacji i próbie uruchomienia wita nas błąd. Pojawia się okienko z informacją,  że nie można uruchomić programu. Próby uruchomienia z terminala też niewiele nam pomagają, gdyż żadne dodatkowe informacje na temat błędu nie są wyświetlane. Rozwiązanie problemu jest bardzo proste i sprowadza się do usunięcia trzech, niepotrzebnych pakietów. W tym celu wystarczy otworzyć terminal, zalogować się jako  _root_ i usunąć konfliktujące biblioteki:

<kbd>su -</kbd>
<kbd>zypper rm OpenOffice_org-libs-gui OpenOffice_org-libs-core OpenOffice_org-components</kbd>

Od teraz już można spokojnie korzystać z najnowszego OpenOffice.org :)
