---
title: Installieren von Microsoft ODBC Driver für SQL Server unter Linux und MacOS | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9819122fd8a0ca50a31d3a97465aaa2f32e37b56
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Installieren von Microsoft ODBC Driver for SQL Server unter Linux und macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

In diesem Artikel wird erläutert, wie zum Installieren der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] für Linux und MacOS sowie die optionalen Command-Line-Tools für SQL Server (`bcp` und `sqlcmd`) und den UnixODBC-Header-Entwicklung.

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 für SQLServer 

> [!IMPORTANT]
> Bei der Installation der v17 `msodbcsql` Paket, das kurz verfügbar war, sollten Sie dies entfernen sie vor der Installation von die `msodbcsql17` Paket. Dadurch werden Konflikte vermieden. Die `msodbcsql17` Paket kann installiert werden, parallel zu den `msodbcsql` v13-Paket.

### <a name="debian-8-and-9"></a>Debian 8 und 9
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6-and-7"></a>RedHat Unternehmensserver 6 und 7
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11sp4-and-12"></a>SUSE Linux Enterprise Server 11SP4 und 12

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

exit
sudo ACCEPT_EULA=Y zypper install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu-1404-1604-and-1710"></a>Ubuntu 14.04, 16.04 und 17.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 14.04
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 17.10
curl https://packages.microsoft.com/config/ubuntu/17.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="os-x-1011-el-capitan-macos-1012-sierra-and-macos-1013-high-sierra"></a>OS X 10.11 (El Capitan), MacOS 10.12 (Sierra) und MacOS 10,13 (hohe Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql17 mssql-tools
```

## <a name="microsoft-odbc-driver-131-for-sql-server"></a>Microsoft ODBC Driver 13.1 for SQLServer 

### <a name="debian-8"></a>Debian 8
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11"></a>SUSE Linux Enterprise Server 11

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1610"></a>Ubuntu 16.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="os-x-1011-el-capitan-and-macos-1012-sierra"></a>OS X 10.11 (El Capitan) und MacOS 10.12 (Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQLServer

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su 
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo 
zypper update 
sudo ACCEPT_EULA=Y zypper install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
zypper install unixODBC-utf16-devel
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="offline-installation"></a>Offlineinstallation
Wenn Sie lieber/erfordern die [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Odbcdriver 13 auf einem Computer ohne Internetzugang installiert werden, müssen Sie manuell Auflösen von paketabhängigkeiten. Die [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 gelten die folgenden direkte Abhängigkeiten:
- Ubuntu: libc6 (> = 2.21), Libstdc ++ 6 (> = 4.9), libkrb5 3 "," libcurl3 "," Openssl "," Debconf (> = 0,5), Unixodbc (> = 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

Jedes dieser Pakete wiederum ihre eigenen Abhängigkeiten aufweist, die nicht unbedingt auf dem System vorhanden. Eine allgemeine Lösung für dieses Problem, finden Sie in Ihren verteilungspunktcomputern Paket-Manager-Dokumentation: [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](http://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian), und [SUSE](https://en.opensuse.org/Portal:Zypper)

Es ist auch für alle abhängigen Pakete manuell herunterladen gemeinsam auf dem Installationscomputer zu platzieren, und installieren jedes Paket manuell wiederum Schlichten mit der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13-Paket.

#### <a name="redhat-linux-enterprise-server-7"></a>RedHat Linux Enterprise Server 7
  - Laden Sie das aktuelle `msodbcsql` `.rpm` von hier aus: http://packages.microsoft.com/rhel/7/prod/
  - Installieren von Abhängigkeiten und der Treiber
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- Laden Sie das aktuelle `msodbcsql` `.deb` von hier aus: http://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- Installieren von Abhängigkeiten und der Treiber 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- Laden Sie das aktuelle `msodbcsql` `.rpm` von hier aus: http://packages.microsoft.com/sles/12/prod/
- Installieren Sie die Abhängigkeiten und der Treiber

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

Wenn Sie die Installation des Pakets abgeschlossen haben, können Sie sicherstellen, dass die [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 können alle abhängigen Elemente suchen, indem Ldd ausgeführt, und überprüfen die Ausgabe für fehlende Bibliotheken:
```
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-linux"></a>Microsoft ODBC Driver 11 for SQLServer on Linux

Bevor Sie den Treiber verwenden können, installieren Sie den UnixODBC Treiber-Manager. Weitere Informationen finden Sie unter [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md).

**Installationsschritte**  

> [!IMPORTANT]  
> Diese Anleitung bezieht sich auf `msodbcsql-11.0.2270.0.tar.gz`, also die Installationsdatei für Red Hat Linux. Wenn Sie die Vorschau für SUSE Linux installieren, wird der Dateiname `msodbcsql-11.0.2260.0.tar.gz`.  
  
Den Treiber installieren:

1.  Stellen Sie sicher, dass Sie die Root-Berechtigung besitzen.  

2.  Wechseln Sie zum Verzeichnis, in dem der Download die Datei platziert `msodbcsql-11.0.2270.0.tar.gz`. Stellen Sie sicher, dass Sie die zu Ihrer Linux-Version passende Datei „ \*.tar.g“ besitzen. Extrahieren Sie die Dateien, führen Sie den folgenden Befehl `tar xvzf msodbcsql-11.0.2270.0.tar.gz`.  
  
3.  Ändern Sie in der `msodbcsql-11.0.2270.0` Verzeichnis, und es wird eine Datei namens angezeigt **"Install.sh" angezeigt**.  
  
4.  Um eine Liste aller verfügbaren Installationsoptionen zu erhalten, führen Sie den folgenden Befehl aus: **./install.sh**.  
  
5.  Führen Sie eine Sicherung von **odbcinst.ini**mittels Backup durch. Die Treiberinstallation aktualisiert **odbcinst.ini**. „odbcinst.ini“ beinhaltet die Liste der Treiber, die beim unixODBC-Treiber-Manager registriert sind. Um den Speicherort von "Odbcinst.ini" auf Ihrem Computer zu ermitteln, führen Sie den folgenden Befehl: ```odbc_config --odbcinstini```.  
  
6.  Bevor Sie den Treiber installieren, führen Sie den folgenden Befehl: `./install.sh verify`. Die Ausgabe des `./install.sh verify` meldet, ob Ihr Computer über die erforderliche Software zur Unterstützung des ODBC-Treibers unter Linux verfügt.  
  
7.  Wenn Sie den ODBC-Treiber unter Linux zu installieren möchten, führen Sie den Befehl: `./install.sh install`. Wenn Sie einen Installationsbefehl angeben müssen (`bin-dir` oder `lib-dir`), geben Sie den Befehl nach der **installieren** Option.  
  
8.  Lesen Sie die Lizenzvereinbarung und geben Sie **YES** ein, um mit der Installation fortzufahren.  
  
Die Installation platziert den Treiber in `/opt/microsoft/msodbcsql/11.0.2270.0`. Der Treiber und seine Unterstützungsdateien muss `/opt/microsoft/msodbcsql/11.0.2270.0`.  
  
Um sicherzustellen, dass der Microsoft ODBC-Treiber unter Linux erfolgreich registriert wurde, führen Sie den folgenden Befehl: ```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```.  
  
[Verwende bestehende MSDN C++ ODBC-Beispiele für den ODBC-Treiber unter Linux](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) zeigt ein Beispiel, das mittels des ODBC-Treibers unter Linux eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] herstellt.  
  
**Deinstallieren**  
  
Sie können den odbcdriver 11 unter Linux deinstallieren, indem Sie die folgenden Befehle ausführen:  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>Beheben von Verbindungsproblemen  
Wenn Sie nicht zum Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mit dem ODBC-Treiber verwenden Sie die folgenden Informationen, um das Problem zu identifizieren.  
  
Das häufigste Verbindungsproblem besteht darin, dass der unixODBC-Treiber-Manager doppelt installiert wurde. Durchsuchen Sie „/usr“ nach „libodbc\*.so\*“. Falls Sie mehr als eine Version der Datei sehen, haben Sie (möglicherweise) mehr als einen Treiber-Manager installiert. Ihre Anwendung verwendet eventuell die falsche Version.
  
Aktivieren Sie das Verbindungsprotokoll, indem Sie die Bearbeitung Ihrer `/etc/odbcinst.ini` Datei, die im folgenden Abschnitt mit diesen Elementen enthalten:

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
Falls der Verbindungsversuch wieder fehlschlägt und Ihnen keine Protokolldatei angezeigt wird, gibt es (möglicherweise) zwei Kopien des Treiber-Managers auf Ihrem Computer. Andernfalls sollte die Ausgabe des Protokolls etwa so aussehen:  
  
```  
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
Ist der ASCII-zeichencodierung nicht UTF-8, zum Beispiel: 
  
```  
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
Es ist mehr als ein Treiber-Manager installiert und die Anwendung verwendet die falsche, die eine oder der Treiber-Manager nicht korrekt erstellt wurde.  
  
Weitere Informationen zum Beheben von Verbindungsproblemen finden Sie hier:  
  
-   [Schritte zum Beheben von SQL-Konnektivitätsproblemen](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [SQL Server 2005 Beheben von Konnektivitätsproblemen – Teil I](http://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [Konnektivitätsproblembehebung in SQL Server 2008 mit dem Konnektivitätsringpuffer](http://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [Problembehebung für die SQL Server-Authentifizierung](http://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [Fehler-Details ()http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    Die in der URL spezifizierte Fehlernummer (11001) sollte geändert werden, damit sie mit dem Ihnen angezeigten Fehler übereinstimmt.  
  
## <a name="driver-files"></a>Treiberdateien
Der ODBC-Treiber unter Linux und MacOS besteht aus folgenden Komponenten:

### <a name="linux"></a>Linux

|Komponente|Description|  
|---------------|-----------------|  
|Libmsodbcsql-17. X.so.X.X oder Libmsodbcsql 13. X.so.X.X|Gemeinsam genutzte Objekt (`so`) dynamische Bibliotheksdatei, die gesamte Funktionalität des Treibers enthält. Diese Datei wird im installiert `/opt/microsoft/msodbcsql17/lib64/` für den Treiber 17 und in `/opt/microsoft/msodbcsql/lib64/` für Driver 13.|  
|`msodbcsqlr17.rll`oder`msodbcsqlr13.rll`|Die begleitende Ressourcendatei für die Treiberbibliothek. Diese Datei wird in installiert. `[driver .so directory]../share/resources/en_US/`| 
|msodbcsql.h|Die Header-Datei, die alle erforderlichen neuen Definitionen benötigt des Treibers enthält.<br /><br /> **Hinweis:**  Sie können nicht auf „msodbcsql.h“ und „odbcss.h“ im selben Programm verweisen.<br /><br /> "msodbcsql.h" wird im installiert `/opt/microsoft/msodbcsql17/include/` für Treiber 17 und in `/opt/microsoft/msodbcsql/include/` für Driver 13. |
|LICENSE.txt|Die Textdatei, die die Bedingungen des Endbenutzer-Lizenzvertrag enthält. Diese Datei befindet sich im `/usr/share/doc/msodbcsql17/` für Treiber 17 und in `/usr/share/doc/msodbcsql/` für Driver 13.|
|RELEASE_NOTES|Die Textdatei, die Anmerkungen zu dieser Version enthält. Diese Datei befindet sich im `/usr/share/doc/msodbcsql17/` für Treiber 17 und in `/usr/share/doc/msodbcsql/` für Driver 13.|


### <a name="macos"></a>MacOS

|Komponente|Description|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib oder libmsodbcsql.13.dylib|Die dynamische Bibliothek (`dylib`) Datei, die gesamte Funktionalität des Treibers enthält. Diese Datei wird im installiert `/usr/local/lib/`.|  
|`msodbcsqlr17.rll`oder`msodbcsqlr13.rll`|Die begleitende Ressourcendatei für die Treiberbibliothek. Diese Datei wird im installiert `[driver .dylib directory]../share/msodbcsql17/resources/en_US/` für Treiber 17 und in `[driver .dylib directory]../share/msodbcsql/resources/en_US/` für Driver 13. | 
|msodbcsql.h|Die Header-Datei, die alle erforderlichen neuen Definitionen benötigt des Treibers enthält.<br /><br /> **Hinweis:**  Sie können nicht auf „msodbcsql.h“ und „odbcss.h“ im selben Programm verweisen.<br /><br /> "msodbcsql.h" wird im installiert `/usr/local/include/msodbcsql17/` für Treiber 17 und in `/usr/local/include/msodbcsql/` für Driver 13. |
|LICENSE.txt|Die Textdatei, die die Bedingungen des Endbenutzer-Lizenzvertrag enthält. Diese Datei befindet sich im `/usr/local/share/doc/msodbcsql17/` für Treiber 17 und in `/usr/local/share/doc/msodbcsql/` für Driver 13. |
|RELEASE_NOTES|Die Textdatei, die Anmerkungen zu dieser Version enthält. Diese Datei befindet sich im `/usr/local/share/doc/msodbcsql17/` für Treiber 17 und in `/usr/local/share/doc/msodbcsql/` für Driver 13. |

## <a name="resource-file-loading"></a>Laden von Ressourcendateien

Der Treiber muss die Ressourcendatei zu laden, um zu funktionieren. Diese Datei heißt `msodbcsqlr17.rll` oder `msodbcsqlr13.rll` abhängig von der Version des Treibers. Der Speicherort des der `.rll` Datei ist relativ zum Speicherort des Treibers selbst (`so` oder `dylib`), wie in der obigen Tabelle aufgeführt. Ab Version 17.1 versucht der Treiber auch beim Laden der `.rll` aus der Standard-Verzeichnis, wenn das Laden von Daten aus den relativen Pfad ein Fehler auftritt. Der Standardpfad für die Ressource sind:

Linux: `/opt/microsoft/msodbcsql17/share/resources/en_US/`

MacOS: `/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>Siehe auch

[Installieren des Treiber-Managers](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Anmerkungen zu dieser Version](../../../connect/odbc/linux-mac/release-notes.md)

[Systemanforderungen](../../../connect/odbc/linux-mac/system-requirements.md)
