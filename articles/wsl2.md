# WSL2 w Windows 10

## Spis treści

* [Czym jest WSL2?](#part1)
* [Konfiguracja WSL2 w Windows 10](#part2)
* [Konfiguracja Ubuntu](#part3)
* [Dostęp do plików WLS2 <-> Windows](#part4)
* [docker.io w Windows :)](#part5)
* [Aplikacje z interfejsem graficznym](#part6)
* [Dźwięk w WSL2](#part7)
* [USB w WSL2](#part8)

## Czym jest WSL2?<a name="part1"></a>

WSL2 jest zaktualizowaną wersją środowiska WSL, udostępnioną w Maju 2020, dla wszystkich (nie tylko uczesntników programu Windows Insider),
służącą do uruchamiana pełnych dystrybucji Linuxa takich jak min. Ubuntu z poziomu systemu Windows. [What's New in WSL2?'](https://docs.microsoft.com/en-us/windows/wsl/wsl2-index)

### Troche historii

W sierpniu 2016 Microsoft zaprezentował WSL (Windows Subsystem for Linux), warstwę kompatybliności pozwalającą na uruchamianie plików wykonywalnych dla systemu GNU/Linux a dokładnie ELF. 
Początkowo w WSL dostępna była tylko jedna dystrybucja, Ubuntu Linux. WSL 1 bazował na wartwie pośredniczącej przez co brakowało wsparcia dla pewnych funkcjonalności, np. docker-a. 
Również operacje I/O były dosyć wolne. WSL1 nie wspiera aplikacji 32-bitowych.

Technologia stojąca za WSL bazuje na porzuconym projekcie [Astoria](https://arstechnica.com/information-technology/2016/02/microsoft-confirms-android-on-windows-astoria-tech-is-gone/), 
którego celem było uruchamianie aplikacji dla systemu Android w Windows 10 Mobile.

### Najwieksze zalety WSL2 w porównaniu do WSL1

* Bazuje na prawdziwym kernelu Linuxa a nie jak dotychczas interfejsie pośredniczącym
* Pełne wsparcie sys-calli Linuxa
* Niektóre operacje I/O są teraz nawet 20x szybsze. Kompilacja czy wypakowywanie plików znacznie przyspieszyło
* Pliki przechowywane są na partycji ext4 (domyślny romiar dysku WSL2 to 250 GB)

## Konfiguracja WSL2 w Windows 10<a name="part2"></a>

WSL2 dostępny jest tylko na Windows 10 Pro w wersji co najmniej 1909 a poniższe kroki były uruchamiane na wersji 2004.

Wersje sytstemu Windows można sprawdzić wpisująć w terminalu komendę 

```
winver.exe
```

![Terminal as Admin](https://arturfog.github.io/articles/wsl2/47.png)

1 Instalacja Windows Terminal z Microsoft Store.

Ten krok jest opcjonalny jednak użycie Windows Terminal znacznie uławia pracę 
w konsoli systemu Windows oraz późniejszą pracę z dystrybucjami Linuxa

![Store](https://arturfog.github.io/articles/wsl2/1.png)

2 Uruchom Windows Terminal jako administrator

![Terminal as Admin](https://arturfog.github.io/articles/wsl2/4.png)

3 Instalacja Windows Subsystem for Linux 

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

![WSL installation](https://arturfog.github.io/articles/wsl2/5.png)

4 Aktywacja ‘Virtual Machine Platform’ 

```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

![WSL installation](https://arturfog.github.io/articles/wsl2/6.png)

5 W tym momencie należy wykonać restart sysetemu Windows

6 Aktualizacja kernela Linuxa dla WSL2

Pobieramy i instalujemy następujący plik

[https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

![WSL Kernel update](https://arturfog.github.io/articles/wsl2/7.png)

7 Ustaw WSL2 jako domyślne

Warto ustawić WSL2 jako domyślne dla nowych instalacji dystrybucji Linuxa

```
wsl --set-default-version 2
```

![WSL set version](https://arturfog.github.io/articles/wsl2/8.png)

8 Zainstaluj Ubuntu z Microsoft Store

![Search Ubuntu Microsoft Store](https://arturfog.github.io/articles/wsl2/9.png)
![Ubuntu Microsoft Store](https://arturfog.github.io/articles/wsl2/10.png)
![Ubuntu downloading](https://arturfog.github.io/articles/wsl2/11.png)

9 Po zainstalowaniu uruchamiamy Ubuntu

![Ubuntu downloading](https://arturfog.github.io/articles/wsl2/12.png)

10 Podczas pierwszego uruchomienia, zostanie utworzone konto użytkownika

![Ubuntu downloading](https://arturfog.github.io/articles/wsl2/15.png)

11 Po utworzeniu konta, uzyskujemy dostęp do konsoli Ubuntu

![Ubuntu downloading](https://arturfog.github.io/articles/wsl2/16.png)

Po zakończeniu instalacji i konfiguracji zestawu WSL2 + Ubuntu możemy rozpocząć korzytanie 
z zainstalowanej dystrybucji Linuxa

## Podstawowa konfiguracja Ubuntu<a name="part3"></a>

Domyślna instalacja Ubuntu posiada zainstalowane tylko podstawowe aplikacje, przed rozpoczęciem instalacji kolejnych
warto przeprowadić aktualizacje pakietów do najnowszych wersji

1 Aktualizujemy listę dostępnych pakietów

```
sudo apt get update
```

2 Pobieramy i instalujemy aktualizacje

```
sudo apt get upgrade
```

W tym momencie możemy przystąpić do dalszej koniguracji w zależności od potrzeb, 
np. zainstalować serwer www (nginx lub apache) lub kompilator C++. W dalszej częsci 
artykułu znajdują się instrukcje insttalacji min. dockera oraz obsługi aplikacji z graficznym
interfejsem użytkownika.

![Ubuntu upgrade](https://arturfog.github.io/articles/wsl2/18.png)

## Dostęp do plików WLS2 <-> Windows<a name="part4"></a>

### Dostęp z Linuxa do dysków systemu Windows 

Dostęp do plików został rozwiązany bardzo wygodnie. W kontenerze WSL2 
automatycznie zostają podmontowane wszystkie dyski widoczne w systemie Windows. 

Z poziomu Linuxa możemy uzyskać dostęp do plików i dysków widocznych w systemie Windows

![Ubuntu disk access](https://arturfog.github.io/articles/wsl2/20.png)

Dysk C: (i wszystkie inne) dostępne są z katalogu */mnt*

![Ubuntu disk access](https://arturfog.github.io/articles/wsl2/22.png)

### Dostęp z Windows do plików Ubuntu

Dostęp z Windows do plików w konetenerach WSL2 róznież jest bardzo łatwy, poprzez 'Eksplorator plików' i 
specjaną ścieżke

Aby uzyskać dostęp do plików Ubuntu z poziomu Windows należy w "Eksploratorze plików" wpisać 
ścieżke

```
\\wsl$
```

![Windows disk access](https://arturfog.github.io/articles/wsl2/21.png)

W tym mijescu widoczne są wszystkie zainstalowane dystrybucje Linuxa i możemy uzyskać dostęp do plików
przechowywanych w Ubuntu, w wygodny sposób

![Windows disk access](https://arturfog.github.io/articles/wsl2/19.png)

## Docker.io w Windows<a name="part5"></a>

Największą wg. mnie zaletą WSL2 jest pełne wsparcie dla [docker-a](https://www.docker.com/)

Jego obsługa bez dużego narzutu sprzętowego (jak w przypdaku pełnej wirtualizacji), 
pozwala na wygodną obsługę zaawansowanych kontenerów.

Umożliwia to pracę z projektami wymagającymi Linuxa, osobą, które z różnych wzgledów nie 
chciały/mogły zainstalować na komputerze Linuxa.

Zacznijmy od instalacji docker-a

```
sudo apt install docker.io
```

![Install docker](https://arturfog.github.io/articles/wsl2/23.png)

Uruchamiamy docker-a (uruchomienie przez systemd nie jest możliwe)

```
sudo dockerd&
```

Instalujemy testowy kontener "hello-world"

```
sudo docker pull hello-world
```

![Install docker](https://arturfog.github.io/articles/wsl2/25.png)

Sprawdźmy czy nowy kontener działa ? 

```
sudo docker run hello-world
```

![Install docker](https://arturfog.github.io/articles/wsl2/26.png)

Działa !

## Aplikacje z interfejsem graficznym <a name="part6"></a>

Obecnie WSL2 nie pozwalaa na natywnie uruchamianie aplikacji z interfejsem graficznym. Microsoft zapowiedział
udostępnienie tej funkcji w przyszłości.

Natomiast po instalacji jednego z dostępnych portów serwera X-ów dla systemu Windows, aplikacje z graficznym 
interfejsem można uruchamiać.

1 Należy zacząć od instalacji wybranego serwera X-ów. Na przykład vcxsrv

[https://sourceforge.net/projects/vcxsrv/](https://sourceforge.net/projects/vcxsrv/)

2 Instalacja przebiega standardowo, nie wymaga jakiejkolwiek konfiguracji

![Install docker](https://arturfog.github.io/articles/wsl2/27.png)

3 Uruchamiamy aplikacje, podczas uruchomienia pojawi się kreator, który pozwala wybrać parametery
serwera X-ów

![Install docker](https://arturfog.github.io/articles/wsl2/48.png)
![Install docker](https://arturfog.github.io/articles/wsl2/45.png)
![Install docker](https://arturfog.github.io/articles/wsl2/46.png)

4 W ostatnim kroku należy zaznaczyć opcje 'Disable access control'

![Install docker](https://arturfog.github.io/articles/wsl2/31.png)

5 Po uruchomienia serwera, już w środowisku Ubuntu, należy zadeklarować dwie zmienne środowiskowe i 
możemy już uruchamiać aplikacje graficzne. 

```
export DISPLAY=$(awk '/nameserver / {print $2; exit}' /etc/resolv.conf 2>/dev/null):0
export LIBGL_ALWAYS_INDIRECT=1
```

5 Zainstalujmy Firefox-a i sprawdźmy czy działa

```
sudo apt install firefox
```

![Install docker](https://arturfog.github.io/articles/wsl2/32.png)

6 Pozostaje uruchomić firefoxa i sprawdzić czy działa

```
firefox
```

Działa !

![Install docker](https://arturfog.github.io/articles/wsl2/33.png)

## Dźwięk w WSL2 <a name="part7"></a>

Natywnie WSL2 nie obsługuje jeszcze dzwięku. Jednak używająć rozwiązania używanego obecnie domyślnie w Linuxie (PulseAudio) a dokładnie 
jego portu na Windows, można odtwarzać dzwięki w Ubuntu działającym wewnątrz WSL2.

1 Pobieramy server PulseAudio dla Windows [https://www.freedesktop.org/wiki/Software/PulseAudio/Ports/Windows/Support/](https://www.freedesktop.org/wiki/Software/PulseAudio/Ports/Windows/Support/)

Aktualna wersja portu dla Windows to 1.1
[http://bosmans.ch/pulseaudio/pulseaudio-1.1.zip](http://bosmans.ch/pulseaudio/pulseaudio-1.1.zip)

2 Po pobraniu należy wypakować pliki i możemy przystąpić do konfiguracji serwera audio

![Install docker](https://arturfog.github.io/articles/wsl2/35.png)


W plikach konfiguracyjnch należy podać adres IP Windowsa, można go pobrać używając następującej komendy w konsoli Ubuntu

3 Adres IP Windows pobierzemy tą komendą

```
cat /etc/resolv.conf | grep nameserver
```

4 Edytujemy plik 'etc\pulse\default.pa'

Wyłączamy obłsugę przechwytywania dzwięku, ze względu na problemy z kompatyblinością z Windows

![Install docker](https://arturfog.github.io/articles/wsl2/38.png)

Dodajemy adres IP kontenera Ubuntu do listy wyjątków, aby pozowlić mu na połączenie z serwerem PulseAudio

![Install docker](https://arturfog.github.io/articles/wsl2/41.png)

5 Edytujemy plik 'etc\pulse\daemon.conf'

W pliku wyłączamy automatyczne zamykanie serwera po 20 minutach bez podłączenia klienta, zmieniajać wartość na -1

![Install docker](https://arturfog.github.io/articles/wsl2/37.png)

6 Teraz możemy uruchomić server pulseaudio

Przy pomocy terminala Windows przechodzimy do podkatalogu bin w katalogu z wypakowanymi plikami PulseAudio
```
pulseaudio.exe
```

![Install docker](https://arturfog.github.io/articles/wsl2/44.png)

7 Podczas pierwszego uruchomienia należy dodać pulseaudio do listy wyjątków Windows Firewall

![Install docker](https://arturfog.github.io/articles/wsl2/40.png)

8 PulseAudio powinno sie uruchomic i w konsoli pojawią się logi z aplikacji

![Install docker](https://arturfog.github.io/articles/wsl2/43.png)

9 Następnie musimy wyexportowć zmienną z adresem IP serwera PulseAudio aby Ubuntu mogło się z nim połaczyć
(należy pamiętać aby podmienić poniższy adres IP na ten pobrany w kroku nr 3)

```
export PULSE_SERVER=tcp:172.26.112.1
```

10 Pozostaje sprawdzić czy dzwięk działa np. odtwarzając film na youtube poprzez przeglądarke.

## USB w WSL2 <a name="part8"></a>

USB jest kolejną funkcjonalnością nie dostępną obecnie w WSL2. Jego obsługa jest 
zapowiedziana w kolejnych aktualizacjach.

Poniewż WSL2 bazuje na krenelu Linuxa, użytkownicy próbują dodać obsługę USB poprzzez rekompilacje Linuxa i 
wykorzystanie aplikacji USB/IP [http://usbip.sourceforge.net/](http://usbip.sourceforge.net/)

Jedną z takich prób jest następujący pull request

[https://github.com/microsoft/WSL2-Linux-Kernel/pull/45](https://github.com/microsoft/WSL2-Linux-Kernel/pull/45)

Niestety USB/IP nie pozwala na udostępnienie portów USB z systemu Windows, natomiast pozwala udostępniać porty USB 
kiedy serwerem jest Linux.
