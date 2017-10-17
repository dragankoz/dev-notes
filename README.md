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

Linux Subsystem
```
"C:\Windows\System32\bash.exe" "--login"
```

#### Network Neighbourhood plugin launching bash
- Edit ${IntelliJIdeaHome}\config\plugins\NativeNeighbourhood\classes\org\intellij\plugins\nativeNeighbourhood\icons\windows\cmd.bat
```
C:\cygwin64\bin\mintty.exe -e /bin/xhere /bin/bash.exe
```


## Cygwin

### Bash propmt here
```
$ chere -i -t mintty
```

Registry should be:
```
[HKEY_CLASSES_ROOT\Directory\Background\shell\cygwin64_bash\command]
REG_EXPAND_SZ  C:\cygwin64\bin\mintty.exe -e /bin/xhere /bin/bash.exe "%V"
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