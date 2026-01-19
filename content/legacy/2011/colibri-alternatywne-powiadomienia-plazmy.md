+++
banner = ""
categories = []
date = "2011-02-10T13:25:44+02:00"
description = ""
images = []
menu = ""
tags = ["kde", "openSUSE", "colibri", "plazma"]
title = "Colibri - alternatywne powiadomienia plazmy"
slug = "colibri-alternatywne-powiadomienia-plazmy"

+++
Aby skorzystać z alternatywnych powiadomień plazmy konieczne jest posiadanie KDE SC w wersji minimum 4.5. Potrzebny nam pakiet znajduje się w repozytorium Extra - stosownym dla naszej wersji KDE. Instalujemy go za pomocą:

{{< kbd"su" >}}
{{< kbd"zypper install colibri" >}}

Następnie usuwamy widżet domyślnych powiadomień plazmy.

!["Usuwanie powiadomień plazmy"](/img/2011/remove_plazma_notification.png)

Teraz wystarczy włączyć nowe powiadomienia. W tym celu uruchamiamy Ustawienia Systemowe → Powiadomienia programów i systemu → Colibri Notifications.
Oto jak prezentuje się nowy styl powiadomień:

!["Powiadomienia Colibri"](/img/2011/colibri_notification.png)
