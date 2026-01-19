+++
banner = ""
categories = ["openSUSE"]
date = "2014-03-23T19:12:19+02:00"
description = ""
images = []
menu = ""
tags = ["openSUSE", "zypper", "zsh"]
title = "Uzupełnianie poleceń zyppera w zsh"
slug = "uzupelnianie-polecen-zyppera-w-zsh"

+++
Narzędzie uzupełniania poleceń w zsh jest na prawdę potężne. Po zainstalowaniu ZSH w openSUSE 13.1 za pomocą {{< kbd"sudo zypper in zsh" >}} przyszła pora na poprawę wyglądu i zachowania powłoki.
Zamiast tworzyć wszystko od podstaw skorzystałem z gotowego rozwiązania jakim jest [oh-my-zsh](http://ohmyz.sh/). Jednak zamiast korzystać z wbudowanych motywów, użyłem [powerline](https://powerline.readthedocs.org/en/latest/) i dostosowałem wygląd do swoich potrzeb. Aktualnie wygląda to tak:

![konsola_powerline_prompt](/img/2014/zsh-konsole-powerline-prompt.png)

<!-- more -->

Domyślna dystrybucja ZSH zawiera sporą ilość rozszerzeń, jednym z nich jest uzupełnianie poleceń zyppera. Jednak zaraz po instalacji ZSH, uzupełnianie są tylko globalne opcje zyppera, bez listy poleceń. Można się spytać po co nam takie uzupełnianie które nie działa? A no po to żeby je naprawić ;-) Najpierw uruchomiłem ZSH z parametrami `-xv`, dzięki temu widziałem jaka funkcja i skąd jest uruchamiana. Okazało się, że lista poleceń zyppera była źle filtrowana, i w efekcie wszystkie polecenia były pomijane na liście podpowiedzi. Rozwiązanie okazało się całkiem proste i wygląda dokładnie jak w poniższym kodzie:

```patch
From 08c2443e5722b578943d2eccfca708e54dea5d20 Mon Sep 17 00:00:00 2001
From: Mariusz Fik <fisiu@opensuse.org>
Date: Sat, 15 Mar 2014 20:23:51 +0100
Subject: [PATCH] Fix zypper commands completion [zypper <TAB>].

Signed-off-by: Mariusz Fik <fisiu@opensuse.org>
---
 Completion/openSUSE/Command/_zypper | 5 ++++-
 1 file changed, 4 insertions(+), 1 deletion(-)

diff --git a/Completion/openSUSE/Command/_zypper b/Completion/openSUSE/Command/_zypper
index ef8ca20..25a32c3 100644
--- a/Completion/openSUSE/Command/_zypper
+++ b/Completion/openSUSE/Command/_zypper
@@-2,6 +2,7 @@
 #
 # Copyright (C) 2009 Holger Macht <holger@homac.de>
 # Copyright (C) 2014 Thomas Mitterfellner <thomas.mitterfellner@gmail.com>
+# Copyright (C) 2014 Mariusz Fik <fisiu@opensuse.org>
 #
 # This file is released under the GPLv2.
 #
@@-45,8 +46,10 @@ _zypper() {
             # start parsing with "Global Options:"
             [[ $hline =~ "^Global Options:" ]] && tag=1
             [[ $tag = 0 ]] && continue
+            # skip empty lines
+            [[ $hline =~ ^\s*$ ]] && continue
             # all commands have to start with lower case letters
-            [[ $hline[1] =~ ^[A-Z] ]] && continue
+            [[ $hline == [[:upper:]]* ]] && continue
             (( ${#hline} < 2 )) && continue

             # cut comma at end of command
--
1.8.4.5﻿
```

Powyższa łatka została już [włączona](https://sourceforge.net/p/zsh/code/ci/2dcf05310612d9bc9980d57f15d500fcf220a974/) do rozwojowej wersji ZSH i tym samym będzie dostępna wraz z kolejnym wydaniem (5.0.6) ZSH. Jednak nic nie stoi na przeszkodzie aby samodzielnie poprawić funkcję uzupełniania, wystarczy tylko zmodyfikować plik `/usr/share/zsh/functions/Completion/openSUSE/_zypper`.
Od teraz, wpisując w terminalu np. {{< kbd"zypper s[tab]" >}} zobaczymy wszystkie możliwe opcje zaczynające się na literę s:

```terminal
search           -- se Search for packages matching a pattern.
services         -- ls List all defined services.
shell            -- sh Accept multiple commands at once.
source-download  -- Download source rpms for all installed packages to a local directory.
source-install   -- si Install source packages and their build dependencies.
```
