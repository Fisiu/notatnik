+++
banner = ""
categories = ["openSUSE"]
date = "2012-01-25T22:22:22+02:00"
description = ""
images = []
menu = ""
tags = ["fontconfig", "openSUSE"]
title = "Priorytety fontów a fontconfig"
slug = "priorytety-fontow-a-fontconfig"

+++
[Fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig) jest biblioteką służącą do konfiguracji dostępu do fontów. Cała konfiguracja jest przechowywana w plikach [xml](http://pl.wikipedia.org/wiki/XML), dzięki czemu są one czytelne i łatwe w modyfikacji. Wyczerpujące informacje można znaleźć w podręczniku man fonts-conf bądź bezpośrednio na [stronie](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html).

Domyślna konfiguracja jest wystarczająca dla przeciętnego użytkownika jednak ma pewien mankament. Otóż rodzina fontów MS ma większy priorytet niż fonty domyślne. Dla przykładu, mając ustawione fonty z rodziny **DejaVu Sans** jako domyślne instalujemy font **Consolas** (dostępny np. w [PowerPointViewer](http://download.microsoft.com/download/E/6/7/E675FFFC-2A6D-4AB0-B3EB-27C9F8C8F696/PowerPointViewer.exe) - wypakować za pomocą cabextract). Okazuje się, że po instalacji staje się on domyślnym fontem monospace. Czy aby tego chcieliśmy?

Jeśli nie chcemy aby zainstalowane fonty MS stały się domyślnymi, wystarczy zmienić konfigurację fontconfig. Tworzymy kopię zapasową i edytujemy plik:

{{< kbd "su" >}}
{{< kbd "cp /etc/fonts/suse-post-user.conf /etc/fonts/suse-post-user.conf.backup" >}}
{{< kbd "vim /etc/fonts/suse-post-user.conf" >}}

Odszukujemy odpowiednie fonty które wg. nas nie powinny panoszyć się w systemie (np. Consolas, Verdana, etc.) i przenosimy je o kilka linii w dół. Po zapisaniu pliku pozostaje nam odświeżenie pamięci podręcznej fontconfig:

{{< kbd "su" >}}
{{< kbd "rm /var/cache/fontconfig/*" >}}
{{< kbd "fc-cache -r" >}}

Od teraz, fonty którym obniżyliśmy priorytet nie będą 'ustawiać' się jako domyślne choć nadal można będzie z nich korzystać.

Przykładowy plik konfiguracyjny z obniżonym priorytetem fontów MS: {{< gist Fisiu 9403085 >}}
