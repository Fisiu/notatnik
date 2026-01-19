+++
banner = ""
categories = []
date = "2009-02-13T10:26:12+02:00"
description = ""
images = []
menu = ""
tags = ["openSUSE", "kde", "plazma", "widzet"]
title = "Plazma i widżety - zapisywanie ustawień"
slug = "plazma-i-widzety-zapisywanie-ustawien"

+++
Po migracji GNOME → KDE 4.2 napotkałem na pewien dość irytujący mnie problem. O ile z ustawieniami  _Plazmy_ nie było problemów, to jeden z jej  _widżetów_ sprawiał mi psikusy. Chodzi o  _Szybkie uruchamianie_ i brak zapisywania ustawień. Skutkowało to tym, że przy każdym uruchomieniu komputera czy też zalogowaniu się,  _widżet_ ten zawsze uruchamiał się z domyślnymi ustawieniami. Poradziłem sobie z tym w sposób następujący.

1. Po uruchomieniu systemu i zalogowaniu się, usunąłem plik z ustawieniami  _Plazmy_.
{{< kbd "cd .kde4/share/config/" >}}
{{< kbd "rm plasma*" >}}
2. Stworzyłem pusty plik z ustawieniami plazmy za pomocą edytora nano.
{{< kbd "nano .kde4/share/config/plasmarc" >}}
3. Zabiłem sesję X, poprzez kombinację klawiszy [Ctrl + Alt + Backspace].
4. Ponownie zalogowałem się, i zacząłem zmieniać ustawienia  _Plazmy_ oraz jej  _widżetów_.

Po dokonanych zmianach, ustawienia pulpitu zapisywane są już poprawnie.
