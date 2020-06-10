# WSL2 w Windows 10

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


For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).