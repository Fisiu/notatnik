+++
banner = ""
categories = ["openSUSE"]
date = "2014-06-22T19:31:45+02:00"
description = ""
images = []
menu = ""
tags = ["openSUSE", "bash", "pliki"]
title = "Jak okiełznać bałagan w zdjęciach?"
slug = "jak-okielznac-balagan-w-zdjeciach"

+++
Zbieramy fotki z jakiegoś wydarzenia na przestrzeni kilku lat. W tym czasie używamy różnych aparatów, telefonów czy kamer. Każde z tych urządzeń ma inny schemat nazywania plików, różne formaty daty i/lub czasu. Dochodzimy do momentu, że w katalogu mamy setki czy tysiące zdjęć. Jak zatem zapanować na takim bałaganem? Ano w 2 prostych krokach.
Po pierwsze, kopiujemy wszystkie zdjęcia do nowego katalogu. W międzyczasie sprawdzamy czy mamy zainstalowany program `jhead` np. za pomocą {{< kbd "which jhead" >}}

Jeśli programu brak, to w openSUSE szybko instalujemy za pomocą YaST bądź w konsoli {{< kbd "sudo zypper in jhead" >}}

Program zainstalowany, zdjęcia skopiowane - czas ogarnąć bałagan.
W konsoli przechodzimy do katalogu ze zdjęciami i uruchamiamy:

{{< kbd "jhead -autorot -ft -nfIMG_%Y.%m.%d-%H.%M.%S *.jpg" >}}

Użyte parametry oznaczają:

* -autorot Automatyczne obracanie zdjęcia na podstawie danych Exif
* -ft Ustawia datę modyfikacji pliku na podstawie daty z danych Exif
* -nf Zmienia nazwę pliku, zgodnie z podanym wzorcem (`man date`), data i czas ustawiane na podstawie danych Exif

I tak przykładowy plik `20130801_144642.jpg` zmieni nazwę na `IMG_2013.08.01-14.46.41.jpg`.

PS. Jeśli wcześniej usunęliśmy dane Exif z plików, niestety nic z tego nie wyjdzie.
