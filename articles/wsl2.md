# WSL2 w Windows 10

## Spis treści

[Czym jest WSL2?](https://arturfog.github.io/articles/wsl2.md)
[Konfiguracja WSL2 w Windows 10](https://arturfog.github.io/articles/wsl2.md)
[Konfiguracja Ubuntu](https://arturfog.github.io/articles/wsl2.md)

## Czym jest WSL2? 

WSL2 jest zaprezentowanym w Maju 2020 zaktualizowanym środowiskiem do uruchamiana pełnych dystrybucji Linuxa takich jak min. Ubuntu 
z poziomu systemu Windows. [What's New in WSL2?'](https://docs.microsoft.com/en-us/windows/wsl/wsl2-index)

### Konfiguracja WSL2 w Windows 10

1. Instalacja Windows Terminal z Microsoft Store

![Store](https://arturfog.github.io/articles/wsl2/1.png)

2. Uruchom Windows Terminal jako administrator

![Terminal as Admin](https://arturfog.github.io/articles/wsl2/4.png)

3. Instalacja Windows Subsystem for Linux 

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

![WSL installation](https://arturfog.github.io/articles/wsl2/5.png)

4. Aktywacja ‘Virtual Machine Platform’ 

```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

![WSL installation](https://arturfog.github.io/articles/wsl2/6.png)


5. Restart sysetemu

6. Aktualizacja kernela Linuxa dla WSL2

[https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

![WSL Kernel update](https://arturfog.github.io/articles/wsl2/7.png)

7. Ustaw WSL2 jako domyślne

```
wsl --set-default-version 2
```

![WSL set version](https://arturfog.github.io/articles/wsl2/8.png)

8. Zainstaluj Ubuntu z Microsoft Store

![Search Ubuntu Microsoft Store](https://arturfog.github.io/articles/wsl2/9.png)
![Ubuntu Microsoft Store](https://arturfog.github.io/articles/wsl2/10.png)
![Ubuntu downloading](https://arturfog.github.io/articles/wsl2/11.png)

9. Po zainstalowaniu uruchamiamy Ubuntu

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).


### Konfiguracja Ubuntu

1. Aktualizujemy listę dostępnych pakietów

```
sudo apt get update
```

2. Pobieramy aktualizacje

```
sudo apt get upgrade
```

![Ubuntu upgrade](https://arturfog.github.io/articles/wsl2/18.png)