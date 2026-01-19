+++
banner = ""
categories = ["openSUSE"]
date = "2009-04-06T20:20:04+02:00"
description = ""
images = []
menu = ""
tags = ["build service", "kadu", "sled"]
title = "home:Fisiu także dla SLED11"
slug = "home-fisiu-takze-dla-sled11"

+++
Dotychczas [openSUSE Build Service](https://build.opensuse.org/) wykorzystywałem do budowania pakietów dla openSUSE. Jak pokazuje życie, również użytkownicy [SUSE Linux Enterpsrise Desktop](http://www.novell.com/linux/) chcieliby korzystać z aplikacji takich jak [kadu](http://www.kadu.net) czy [qnapi](http://krzemin.iglu.cz/software/qnapi). Więc postanowiłem stworzyć repozytorium również dla nich. Jako, że wersja SLED/SLES 11 bazuje na openSUSE 11.1, stworzenie repozytorium i przebudowanie pakietów zajęło tylko kilka chwil. Dostępne jest ono pod adresem:

`http://download.opensuse.org/repositories/home:/Fisiu/SLE_11/`

Wystarczy dodać adres repozytorium za pomocą Yast lub terminala:

{{< kbd "su" >}}
{{< kbd "zypper ar http://download.opensuse.org/repositories/home:/Fisiu/SLE_11/home:Fisiu" >}}
