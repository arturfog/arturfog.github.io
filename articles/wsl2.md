# WSL2 w Windows 10

## Spis treści

* [Czym jest WSL2?](#part1)
* [Konfiguracja WSL2 w Windows 10](#part2)
* [Konfiguracja Ubuntu](#part3)
* [Dostęp do plików WLS2 <-> Windows](#part4)
* [docker.io w Windows :)](#part5)

## Czym jest WSL2?<a name="part1"></a>

WSL2 jest zaprezentowanym w Maju 2020 zaktualizowanym środowiskiem do uruchamiana pełnych dystrybucji Linuxa takich jak min. Ubuntu 
z poziomu systemu Windows. [What's New in WSL2?'](https://docs.microsoft.com/en-us/windows/wsl/wsl2-index)

## Konfiguracja WSL2 w Windows 10<a name="part2"></a>

1 Instalacja Windows Terminal z Microsoft Store

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


5 Restart sysetemu

6 Aktualizacja kernela Linuxa dla WSL2

[https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

![WSL Kernel update](https://arturfog.github.io/articles/wsl2/7.png)

7 Ustaw WSL2 jako domyślne

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

Po zakończeniu instalacji i konfiguracji zestawu WSL2 + Ubuntu uzyskujemy dostęp do 
pełnej funkcjonalności tej dystrybucji Linuxa. 

## Konfiguracja Ubuntu<a name="part3"></a>

1 Aktualizujemy listę dostępnych pakietów

```
sudo apt get update
```

2 Pobieramy aktualizacje

```
sudo apt get upgrade
```

![Ubuntu upgrade](https://arturfog.github.io/articles/wsl2/18.png)

## Dostęp do plików WLS2 <-> Windows<a name="part4"></a>

### Dostęp z Linuxa do dysków systemu Windows 

Z poziomu Linuxa możemy uzyskać dostęp do plików i dysków widocznych w systemie Windows

![Ubuntu disk access](https://arturfog.github.io/articles/wsl2/20.png)

Dysk C: (i wszystkie inne) dostępne są z katalogu */mnt*

![Ubuntu disk access](https://arturfog.github.io/articles/wsl2/22.png)

### Dostęp z Windows do plików Ubuntu

Aby uzyskać dostęp do plików Ubuntu z poziomu Windows należy w "Eksploratorze plików" wpisać 
ścieżke 

![Windows disk access](https://arturfog.github.io/articles/wsl2/21.png)

W tym mijescu widoczne są wszystkie zainstalowane dystrybucje Linuxa

![Windows disk access](https://arturfog.github.io/articles/wsl2/19.png)

## Docker.io w Windows<a name="part5"></a>

Największą nowością i wg. mnie zaletą WSL2 jest możliwość uruchamian docker-a