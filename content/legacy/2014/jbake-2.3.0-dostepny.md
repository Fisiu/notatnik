+++
banner = ""
categories = []
date = "2014-06-15T21:07:47+02:00"
description = ""
images = []
menu = ""
tags = ["java", "jbake", "blog"]
title = "JBake 2.3.0 dostępny"
slug = "jbake-2-3-0-dostepny"

+++
Całkiem niedawno ukazała się nowa wersja [jbake](http://jbake.org/) - 2.3.0. Lista zmian dla tego wydania przedstawia się nastepująco:

* Wsparcie dla przyrostowego renderowania stron (w tym wydaniu jeszcze domyślnie wyłączone, funkcja eksperymentalna)
* Dodano wsparcie dla projektów w podkatalogach
* Kod odpowiedzialny za parsowanie i renderowanie został przepisany, dzięki czemu łatwiejsze jest jego utrzymanie i dodawanie nowych funkcjonalności
* Domyślny status może być teraz zdefiniowany w pliku konfiguracyjnym
* Naprawiono błąd URI występujący na platformie Windows
* Dodano opcję wiersza polceń realizującą opcje bake+serve
* Dostęp do opcji konfiguracyjnych z plików w formacie AsciiDoc
* Dodano wsparcie dla frameworka logowania
* Dodano obsługę szablonów Groovy oraz Thymeleaf
* Rozszerzony model danych jest dostępny w szablonach
* Usprawniono raportowanie błędów
* Startowy szablon został zaktualizowany i używa teraz Bootstrap 3.1.1 oraz jQuery 1.11.1

Jbake [jest](http://search.maven.org/#browse|523103791) już dostępny w centralnym repozytorium maven. Można także użyć [jbake-maven-plugin](https://github.com/ingenieux/jbake-maven-plugin) do szybkiego generowania stron i podglądu na żywo. Lista celów: `mvn jbake:help` w głównym katalogu projektu.
