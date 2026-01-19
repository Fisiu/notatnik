+++
banner = ""
categories = ["openSUSE"]
date = "2014-03-27T13:12:27+02:00"
description = ""
images = []
menu = ""
tags = ["openSUSE", "java", "eclipse", "tomcat"]
title = "Biblioteka Apache Tomcat Native w Eclipse"

+++
Po dodaniu serwera aplikacji Apache Tomcat w Eclipse, podczas startu widzimy w logach:

```java
INFO: The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path: /usr/java/packages/lib/amd64:/usr/lib64:/lib64:/lib:/usr/lib
```

Jak dodać bibliotekę Apache Tomcat Native do `java.library.path`? Najpierw trzeba ją skompilować.

No potrzeby tego postu, zakładam, że tomcat znajduje w katalogu `/opt/java/servers/tomcat7`. Jeśli zmienna CATALINA_HOME nie jest ustawiona, warto ją dodać do np. `~/.profile`:

```bash
# Export tomcat home
export CATALINA_HOME=/opt/java/servers/tomcat7
```

### Instalacja zależności
Zanim zaczniemy kompilować, konieczne jest przygotowanie systemu. Na podstawowy zestaw narzędzi do kompilacji kodu w języku `c` składa się `gcc` i `make`. Indywidualne pakiety można zainstalować za pomocą:
{{< kbd "zypper in make gcc" >}}

Można także skorzystać z dostępnych wzorców i zainstalować `pattern devel_C_C++` za pomocą:
{{< kbd "zypper in -t pattern devel_C_C++" >}}

Do kompilacji samej zaś biblioteki potrzebujemy pakiety `libopenssl-devel` oraz `libapr1-devel`. Jeśli jeszcze ich nie mamy w systemie, to instalujemy:
{{< kbd "zypper in libopenssl-devel libapr1-devel" >}}

<!-- more -->

### Kompilacja biblioteki
1. Przechodzimy do katalogu `bin` w katalogu tomcata i rozpakowujemy źródła.

{{< kbd "cd $CATALINA_HOME/bin" >}}
{{< kbd "tar xf tomcat-native.tar.gz" >}}

2. Przechodzimy do katalogu `tomcat-native-1.1.29-src/jni/native`
Uwaga! Wersja biblioteki może się różnić, zależnie od użytej wersji tomcata. W wersji tomcat-7.0.52 biblioteka natywna jest w wersji 1.1.29.

{{< kbd "cd tomcat-native-1.1.29-src/jni/native" >}}

3. Konfiguracja i kompilacja
Aby przygotować źródła do kompilacji, wywołujemy skrypt `configure`. W liście parametrów dostarczamy ścieżkę do plików nagłówkowych `apr` oraz ustawiamy `prefix` - ścieżka gdzie biblioteka zostanie zainstalowana po wywołaniu `make install` z zachowaniem struktury katalogów. Po skonfigurowaniu, wystarczy skompilować i zainstalować bibliotekę.

{{< kbd "./configure --with-apr=$(which apr-1-config) --prefix=$CATALINA_HOME/native" >}}
{{< kbd "make && make install" >}}

Jako potwierdzenie, że biblioteka została zainstalowana, wyświetlona zostanie informacja:

```terminal
Libraries have been installed in:
   /opt/java/servers/tomcat7/native/lib
```

Na powyższą ścieżkę składa się użyty `prefix` podczas konfiguracji i katalog `lib`.

### java.library.path

Podczas próby uruchomienia tomcata z poziomy eclipse, nadal dostajemy informację, że biblioteka natywna nie jest dostępna. Pomimo, że przed chwilą zostało skompilowana i zainstalowana. Trzeba jeszcze dać ją do ściżki, z której będzie dostępna dla Javy. Aby nie modyfikować ustawień systemowych, można to osiągnąć w eclipse.
Otwieramy konfigurację uruchamiania. PPM na naszym projekcie → Run configurations wybieramy konfigurację dla Apache Tomcat a z niej kartę `Environment`. Dodajemy nowy parametr o nazwie `LD_LIBRARY_PATH` i wartości takiej jak ścieżka, gdzie nasza biblioteka została zainstalowana, czyli `/opt/java/servers/tomcat7/native/lib`.

![java.library.path](/img/2014/tomcat-native-lib-eclipse.png)

Po zastosowaniu zmian i uruchomieniu serwera, w dzienniku uruchamiania możemy zobaczyć:

```java
INFO: Loaded APR based Apache Tomcat Native library 1.1.29 using APR version 1.4.8.
```
