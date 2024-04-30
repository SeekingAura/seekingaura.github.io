---
title: Cloudflared-Install
---
<!-- omit from toc -->
# Cloudflared Install on device
To use cloudflare tunnel the device where the service that you want to expose the service or connection (server-side demon), the [official guide](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/create-local-tunnel/#1-download-and-install-cloudflared) have a detailed steps, but on this guide will have more examples and more detailed cases.

<!-- omit from toc -->
# TOC
- [Windows - With Winget](#windows---with-winget)
  - [Install winget](#install-winget)
  - [Use winget to install](#use-winget-to-install)
- [Windows - Manually](#windows---manually)
  - [Download executable](#download-executable)
  - [Move to anywhere you want](#move-to-anywhere-you-want)
  - [Set to environment PATH](#set-to-environment-path)
- [Linux - Ubuntu](#linux---ubuntu)


<!-- omit from toc -->
# TL;DR - Windows
Run a CMD with admin privilegies install with winget (that can installed from Microsoft Store have the name ["App Installer"](https://www.microsoft.com/store/productId/9NBLGGH4NNS1?ocid=pdpshare)):
```shell
winget install --id Cloudflare.cloudflared
```

For limited permission case use executable [Windows 64 bits](https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-windows-amd64.exe)


# Windows - With Winget
According to [official guide](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/#windows) Easy way to install is with [winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/) 

## Install winget
To [install winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/#install-winget) download form the Microsoft Store the app with name ["App Installer"](https://www.microsoft.com/store/productId/9NBLGGH4NNS1?ocid=pdpshare), once this is installed open a new *CMD* and try command 

```shell
winget --info
```

if output something like this, winget was installed ok

```txt
Windows Package Manager v1.7.10661
Copyright (c) Microsoft Corporation. All rights reserved.

Windows: Windows.Desktop v10.0.19045.4170
System Architecture: X64
Package: Microsoft.DesktopAppInstaller v1.22.10661.0

Winget Directories
...
```

If something is wrong try reboot system and try again run command info again

## Use winget to install
Run this command on cmd
```shell
winget install --id Cloudflare.cloudflared
```

Admin privileges may required, once installation process finish check in a new console with the next command:

```shell
cloudflared --version
```

output should be something like this
```
cloudflared version 2024.3.0 (built 2024-03-20-1009 UTC)
```

If something is wrong try reboot system and try again run command info again

# Windows - Manually
This method is more used if you have a limited permissions, but if you want to call process from anywhere is required to modify environment var `PATH`
## Download executable
Just download the executable [Windows 64 bits](https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-windows-amd64.exe) from [official site](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/#windows)

## Move to anywhere you want
Once you download the .exe file may have name of specific source like `cloudflared-windows-amd64.exe` should rename to `cloudflared` and move into a easy access folder for example `C:\cloudflared\cloudflared.exe`. In this way if you need to run cloudflared tunnels can access quickly with

```shell
cd /cloudflared
```

and then run cloduflared commands
```shell
cloudflared --version
```

## Set to environment PATH

To run command cloduflared from anywhere add the folder where the *cloudflared.exe* is on this example **.exe** are at `C:\cloudflared\cloudflared.exe` so then add to env var PATH the value `C:\cloudflared`, and open new termianl and try, if does not work reboot.


# Linux - Ubuntu
ToDo

---

[Next](/docs/cloudflared/local/auth)

<!-- omit from toc -->
# Navigation
* [Cloudflared local index](/docs/cloudflared/local)
* [Cloudflared index](/docs/cloudflared)
* [Docs index](/docs)

