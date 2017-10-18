# Collection of Developer Notes

## Intellij

#### Setup
- Update bin\idea64.exe.vmoptions
```
-Xms512m
-Xmx2048m
```

- Update bin\idea64.exe.vmoptions
```
-Xms512m
-Xmx2048m
```

- Update bin\idea.properties
```
idea.config.path=${idea.home}/../IntelliJIdea/config
idea.system.path=${idea.home}/../IntelliJIdea/system
```

- Tools -> Terminal -> Set path

Cygwin
```
"c:\cygwin64\bin\sh.exe" -c "/bin/xhere /bin/bash"
```

#### Network Neighbourhood plugin launching bash
- Edit ${IntelliJIdeaHome}\config\plugins\NativeNeighbourhood\classes\org\intellij\plugins\nativeNeighbourhood\icons\windows\cmd.bat
```
C:\cygwin64\bin\mintty.exe -e /bin/xhere /bin/bash.exe
```


## Cygwin

### Bash prompt here
```
$ chere -i -t mintty
```

Registry should be:
```
[HKEY_CLASSES_ROOT\Directory\Background\shell\cygwin64_bash\command]
REG_EXPAND_SZ  C:\cygwin64\bin\mintty.exe -e /bin/xhere /bin/bash.exe "%V"
```

## WSL (Windows Linux Subsystem Tweaks)

- Remove windows path from wsl (prevents BSODS?):
```
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Lxss]
"AppendNtPath"=dword:00000000
```

#### Mintty + WSL (Requires cygwin + wslbridge!)
- Update wsl shortcut

Download [wslbridge](https://github.com/rprichard/wslbridge/releases) ﻿and copy binaries into **C:\Cygwin64\bin**
Edit your wsl shortcut to be C:\cygwin64\bin\mintty.exe C:\cygwin64\bin\wslbridge.exe -C ~ -t /bin/bash --login
```
C:\cygwin64\bin\mintty.exe C:\cygwin64\bin\wslbridge.exe -C ~ -t /bin/bash --login
```

- Enable right-click Explorer context with mintty+wsl

Make a wsl.reg file, the commands included in here are: **C:\cygwin64\bin\mintty.exe C:\cygwin64\bin\wslbridge.exe -t /bin/bash --login** 

Opening into dir location doesn't work exactly, but is close enough. Once installed, regedit to suit.
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\wsl_bash\command]
@=hex(2):43,00,3a,00,5c,00,63,00,79,00,67,00,77,00,69,00,6e,00,36,00,34,00,5c,\
  00,62,00,69,00,6e,00,5c,00,6d,00,69,00,6e,00,74,00,74,00,79,00,2e,00,65,00,\
  78,00,65,00,20,00,43,00,3a,00,5c,00,63,00,79,00,67,00,77,00,69,00,6e,00,36,\
  00,34,00,5c,00,62,00,69,00,6e,00,5c,00,77,00,73,00,6c,00,62,00,72,00,69,00,\
  64,00,67,00,65,00,2e,00,65,00,78,00,65,00,20,00,2d,00,74,00,20,00,2f,00,62,\
  00,69,00,6e,00,2f,00,62,00,61,00,73,00,68,00,20,00,2d,00,2d,00,6c,00,6f,00,\
  67,00,69,00,6e,00,20,00,00,00

[HKEY_CLASSES_ROOT\Directory\shell\wsl_bash\command]
@=hex(2):43,00,3a,00,5c,00,63,00,79,00,67,00,77,00,69,00,6e,00,36,00,34,00,5c,\
  00,62,00,69,00,6e,00,5c,00,6d,00,69,00,6e,00,74,00,74,00,79,00,2e,00,65,00,\
  78,00,65,00,20,00,43,00,3a,00,5c,00,63,00,79,00,67,00,77,00,69,00,6e,00,36,\
  00,34,00,5c,00,62,00,69,00,6e,00,5c,00,77,00,73,00,6c,00,62,00,72,00,69,00,\
  64,00,67,00,65,00,2e,00,65,00,78,00,65,00,20,00,2d,00,74,00,20,00,2f,00,62,\
  00,69,00,6e,00,2f,00,62,00,61,00,73,00,68,00,20,00,2d,00,2d,00,6c,00,6f,00,\
  67,00,69,00,6e,00,20,00,00,00

[HKEY_CLASSES_ROOT\Drive\Background\Shell\wsl_bash\command]
@=hex(2):43,00,3a,00,5c,00,63,00,79,00,67,00,77,00,69,00,6e,00,36,00,34,00,5c,\
  00,62,00,69,00,6e,00,5c,00,6d,00,69,00,6e,00,74,00,74,00,79,00,2e,00,65,00,\
  78,00,65,00,20,00,43,00,3a,00,5c,00,63,00,79,00,67,00,77,00,69,00,6e,00,36,\
  00,34,00,5c,00,62,00,69,00,6e,00,5c,00,77,00,73,00,6c,00,62,00,72,00,69,00,\
  64,00,67,00,65,00,2e,00,65,00,78,00,65,00,20,00,2d,00,74,00,20,00,2f,00,62,\
  00,69,00,6e,00,2f,00,62,00,61,00,73,00,68,00,20,00,2d,00,2d,00,6c,00,6f,00,\
  67,00,69,00,6e,00,00,00

[HKEY_CLASSES_ROOT\Drive\shell\wsl_bash\command]
@=hex(2):43,00,3a,00,5c,00,63,00,79,00,67,00,77,00,69,00,6e,00,36,00,34,00,5c,\
  00,62,00,69,00,6e,00,5c,00,6d,00,69,00,6e,00,74,00,74,00,79,00,2e,00,65,00,\
  78,00,65,00,20,00,43,00,3a,00,5c,00,63,00,79,00,67,00,77,00,69,00,6e,00,36,\
  00,34,00,5c,00,62,00,69,00,6e,00,5c,00,77,00,73,00,6c,00,62,00,72,00,69,00,\
  64,00,67,00,65,00,2e,00,65,00,78,00,65,00,20,00,2d,00,74,00,20,00,2f,00,62,\
  00,69,00,6e,00,2f,00,62,00,61,00,73,00,68,00,20,00,2d,00,2d,00,6c,00,6f,00,\
  67,00,69,00,6e,00,00,00
  
```

## Hyper-V
### Install (Powershell - Admin)
```
> Enable-WindowsOptionalFeature -Online -FeatureName:Microsoft-Hyper-V -All
```

### Disable/Enable Hyper-V (cmd - Admin)
```
bcdedit /set hypervisorlaunchtype off
bcdedit /set hypervisorlaunchtype auto
```

## Windows 10 Linux Subsystem
### Install (Powershell - Admin)
```
> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```


## Oracle 10g XE

### Installing
- Install
- Reboot (if sqlplus is not available on cmd line)
- Change default http port since 8080 is wildly popular
```
$ sqlplus /nolog
 
SQL*Plus: Release 10.2.0.1.0 - Production on Mon Jul 24 10:36:17 2017
 
Copyright (c) 1982, 2005, Oracle.  All rights reserved.
 
SQL> connect
Enter user-name: system
Enter password: welcome123
Connected.
SQL> exec DBMS_XDB.SETHTTPPORT(18080);
 
PL/SQL procedure successfully completed.
 
SQL> quit
Disconnected from Oracle Database 10g Express Edition Release 10.2.0.1.0 - Production
```

## Docker for Windows
### Installing
- Enable Hyper-V
- Make sure port 2375 is enabled (Settings → General → "Expose Daemon on tcp://localhost:2375" )
- Add to System Environment (May need to reboot)
```
DOCKER_HOST=tcp://localhost:2375
```

## Kubernetes
### Installing
- See http://www.collegemajorsnews.com/news/Setting-up-Kubernetes-on-Windows10-Laptop-with-Minikube/

(Using cmd.exe - adminstrator)
```
> minikube config set profile minikube-dk
> minikube config set vm-driver hyperv
> minikube.exe start --kubernetes-version="v1.7.0" --memory=3096 --hyperv-virtual-switch=External1 --v=7 --alsologtos
```

### Hyper-V + Minikube settings tweaks
- Disable dynamic memory
- Turn off time synchronization (Hyper-V integration service) - makes systemd-udevd cpu spike
- Disable Hyper-V checkpoints
- Turn off auto-start
- Assign static MAC (dhcp becomes more predictable?)