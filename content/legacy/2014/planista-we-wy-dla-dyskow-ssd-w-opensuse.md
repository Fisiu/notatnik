+++
banner = ""
categories = []
date = "2014-03-11T18:10:19+02:00"
description = ""
images = []
menu = ""
tags = ["openSUSE", "ssd", "wydajność"]
title = "Planista We/Wy dla dysków SSD w openSUSE"

+++
Domyślnym planistą We/Wy w openSUSE jest <abbr title="Complete Fairness Queueing">CFQ</abbr> i radzi on sobie z klasycznymi dyskami talerzowymi całkiem dobrze. Więcej informacji o samym planiście CFQ można znaleźć w [dokumentacji kernela](https://www.kernel.org/doc/Documentation/block/cfq-iosched.txt) a przegląd planistów dostępnych w dystrybucji openSUSE dostępny jest w [podręczniku openSUSE, rozdział 13](http://activedoc.opensuse.org/book/opensuse-system-analysis-and-tuning-guide/chapter-13-tuning-io-performance). Dla dysków <abbr title="Solid State Drive">SSD</abbr> lepszym wyborem zdaje się być planista Deadline bądź Noop.

Sprawdzić aktualnie używanego planistę można za pomocą:
{{< kbd "cat /sys/block/sda/queue/scheduler" >}}

```terminal
noop deadline [cfq]
```

Jako `root` możemy zmienić planistę w 'locie':
{{< kbd "echo noop > /sys/block/sda/queue/scheduler" >}}

Skoro już wiemy jak zmienić planistę po uruchomieniu systemu, pozostaje tylko ten proces zautomatyzować. Jeśli posiadamy w komputerze tylko jeden dysk, i jest nim dysk SSD (lub kilka, lecz wszystkie są SSD), najprostszym rozwiązaniem będzie dodanie parametru `elevator` (nazwa planisty jako wartość) do listy wywołania jądra. W tym celu edytujemy plik:
{{< kbd "sudo vi /etc/default/grub" >}}

I dodajemy nasz parametr do pozostałych dla opcji `GRUB_CMDLINE_LINUX_DEFAULT`. Przykładowy fragment ww. pliku może wyglądać tak:

```config
GRUB_CMDLINE_LINUX_DEFAULT=" video=1680x1050 resume=/dev/disk/by-id/ata-Hitachi_HDS721050CLA362_JP1521HN0MUHTA-part5 splash=silent quiet showopts radeon.audio=0 radeon.dpm=1 elevator=deadline"
```

Pozostaje nam jeszcze zaktualizowanie menu rozruchowego, za pomocą:
{{< kbd "grub2-mkconfig -o /boot/grub2/grub.cfg" >}}

A co gdy mamy kilka dysków, różnego typu, zarówno talerzowe jak i SSD? Wówczas nie ruszamy menu gruba, tylko korzystamy z dobrodziejstw `udev`. Tworzymy zestaw prostych reguł, dzięki którym przydzielimy planistę w zależności od typu dysku. Tworzymy plik `/etc/udev/rules.d/50-io-schedulers.rules` z zawartością:

```config
# set deadline scheduler for non-rotating disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="deadline"

# set cfq scheduler for rotating disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="cfq"
```

Reguły będą mieć zastosowanie po ponownym uruchomieniu komputera. Dla przykładu, w komputerze dysk `/dev/sda` jest dyskiem SSD a `/dev/sdb` jest dyskiem talerzowym. Wyjście polecenia `cat /sys/block/sd{a,b}/queue/scheduler` zwróci:

```terminal
noop [deadline] cfq
noop deadline [cfq]
```
