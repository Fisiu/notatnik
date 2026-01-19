+++
banner = ""
categories = []
date = "2014-03-10T14:49:19+02:00"
description = ""
images = []
menu = ""
tags = ["github", "blog", "wordpress"]
title = "Z wordpressa do html"

+++
Wiosna za pasem więc czas po porządki. Z racji, że ciągłe powiadomienia o kolejnych aktualizacjach wordpressa czy jego wtyczek zaczęły mnie dość mocno irytować a samo utrzymywanie tego bloga wymagało systematycznego nakładu pracy. Postanowiłem wyeliminować źródło problemów, czyli wordpressa. Więc zacząłem się rozglądać za "czymś" do generowania statycznych treści. Miało być to proste narzędzie, z relatywnie małymi zależnościami, umożliwiające szybki start. No i oczywiście import starych postów z wordpressa.

I tak trafiłem na system [JBake](http://www.jbake.org/). Narzędzie napisane w Javie, kilka silników do obsługi szablonów ([freemarker](http://freemarker.org/), [groovy templates](http://groovy.codehaus.org/Groovy+Templates) i [thymeleaf](http://www.thymeleaf.org/) v.2.3.0), dostępna [wtyczka mavena](https://github.com/ingenieux/jbake-maven-plugin) umożliwia podgląd postów na żywo oraz automatyczne wysyłanie treści na [githuba](http://pages.github.com/). JBake nie posiada możliwości importowania danych bezpośrednio z wordpressa. Jednak istnieje sporo narzędzi do eksportowania stron/postów z wordpressa do formatu markdown. Osobiście użyłem nieco [zmodyfikowanego](https://github.com/Fisiu/exitwp) skryptu [exitwp](https://github.com/thomasf/exitwp).

Pozostało stworzyć jakiś motyw i poprawić domyślne szablony. Podczas tego eksperymentu powstał motyw `fidbake`, zbudowany w oparciu o bootstrap 3, fontawesome i system komentarzy disqus. Całość dostępna jest na licencji MIT: [https://github.com/Fisiu/fidbake](https://github.com/Fisiu/fidbake) a demo można sprawdzić pod adresem [http://jbake-fidano.rhcloud.com/](http://jbake-fidano.rhcloud.com/).

Stara (sub)domena jeszcze działa i wskazuje na stary blog. Aktualnie nie jestem pewien czy podpiąć ją pod githuba czy dać o niej zapomnieć. Czas pokaże...
