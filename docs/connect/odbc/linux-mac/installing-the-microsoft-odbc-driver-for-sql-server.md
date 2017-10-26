---
title: "Installieren von Microsoft ODBC Driver für SQL Server unter Linux und MacOS | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8a12dec078ada9d029a70edbe1c35a608c85a538
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Installieren von Microsoft ODBC Driver für SQL Server unter Linux und macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

In diesem Thema wird erläutert, wie zum Installieren der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] für Linux und MacOS sowie die optionalen-Befehlszeilentools für SQL Server (`bcp` und `sqlcmd`) und den UnixODBC-Header-Entwicklung.

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

### <a name="redhat-enterprise-server-6"></a>Red Hat Enterprise Server 6
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

### <a name="redhat-enterprise-server-7"></a>Red Hat Enterprise Server 7
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
brew install --no-sandbox msodbcsql mssql-tools
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQLServer

### <a name="redhat-enterprise-server-6"></a>Red Hat Enterprise Server 6
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

### <a name="redhat-enterprise-server-7"></a>Red Hat Enterprise Server 7
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
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools-14.0.2.0-1
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
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools-14.0.2.0-1
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
- Red Hat: Glibc, e2fsprogs, krb5-Bibliotheken, Openssl, unixODBC
- SuSE: Glibc, libuuid1, krb5, Openssl, unixODBC

Jede dieser Pakete hat wiederum ihre eigenen Abhängigkeiten, die nicht unbedingt auf dem System vorhanden. Eine allgemeine Lösung für dieses Problem, finden Sie in Ihren verteilungspunktcomputern Paket-Manager-Dokumentation: [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](http://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian), und [SUSE](https://en.opensuse.org/Portal:Zypper)

Es ist auch für alle abhängigen Pakete manuell herunterladen gemeinsam auf dem Installationscomputer zu platzieren, und installieren jedes Paket manuell wiederum Schlichten mit der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13-Paket.

#### <a name="redhat-linux-enterprise-server-7"></a>RedHat Linux Enterprise Server 7
  - Die neuesten Msodbcsql entsprechende hier herunterladen: http://packages.microsoft.com/rhel/7/prod/
  - Installieren von Abhängigkeiten und der Treiber
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- Die neuesten Msodbcsql .deb hier herunterladen: http://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- Installieren von Abhängigkeiten und der Treiber 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- Die neuesten Msodbcsql entsprechende hier herunterladen: http://packages.microsoft.com/sles/12/prod/
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

Bevor Sie den Treiber verwenden können, installieren Sie den UnixODBC Treiber-Manager. Weitere Informationen finden Sie unter [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) .  

**Installationsschritte**  

> [!IMPORTANT]  
> Diese Anleitung bezieht sich auf `msodbcsql-11.0.2270.0.tar.gz`, also die Installationsdatei für Red Hat Linux. Wenn Sie die Vorschau für SUSE Linux installieren, wird der Dateiname `msodbcsql-11.0.2260.0.tar.gz`.  
  
Den Treiber installieren:

1.  Stellen Sie sicher, dass Sie die Root-Berechtigung besitzen.  

2.  Wechseln Sie zum Verzeichnis, in dem der Download die Datei platziert `msodbcsql-11.0.2270.0.tar.gz`. Stellen Sie sicher, dass Sie die zu Ihrer Linux-Version passende Datei „ \*.tar.g“ besitzen. Führen Sie den folgenden Befehl aus, um die Dateien zu extrahieren **tar xvzf msodbcsql-11.0.2270.0.tar.gz**.  
  
3.  Ändern Sie in der `msodbcsql-11.0.2270.0` Verzeichnis, und es wird eine Datei namens angezeigt **"Install.sh" angezeigt**.  
  
4.  Um eine Liste aller verfügbaren Installationsoptionen zu erhalten, führen Sie den folgenden Befehl aus: **./install.sh**.  
  
5.  Führen Sie eine Sicherung von **odbcinst.ini**mittels Backup durch. Die Treiberinstallation aktualisiert **odbcinst.ini**. „odbcinst.ini“ beinhaltet die Liste der Treiber, die beim unixODBC-Treiber-Manager registriert sind. Um den Speicherort von „odbcinst.ini“ auf Ihrem Computer zu finden, führen Sie den folgenden Befehl aus: **odbc_config --odbcinstini**.  
  
6.  Führen Sie den folgenden Befehl aus, bevor Sie den Treiber installieren: **./install.sh verify**. Die Ausgabe von **./install.sh verify** berichtet, ob Ihr Computer über die erforderliche Software verfügt, um den ODBC-Treiber unter Linux zu unterstützen.  
  
7.  Wenn Sie bereit sind, den ODBC-Treiber unter Linux zu installieren, führen Sie diesen Befehl aus: **./install.sh install**. Falls Sie einen Installationsbefehl angeben müssen (**bin-dir** oder **lib-dir**), geben Sie den Befehl nach der **install** -Option an.  
  
8.  Lesen Sie die Lizenzvereinbarung und geben Sie **YES** ein, um mit der Installation fortzufahren.  
  
Die Installation platziert den Treiber in `/opt/microsoft/msodbcsql/11.0.2270.0`. Der Treiber und seine Unterstützungsdateien muss `/opt/microsoft/msodbcsql/11.0.2270.0`.  
  
Um zu überprüfen, ob der Microsoft OBCD-Treiber unter Linux erfolgreich registriert wurde, führen Sie den folgenden Befehl aus: **odbcinst -q -d -n "ODBC Driver 11 for SQL Server"**.  
  
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
  
-   [Fehlerdetails (http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    Die in der URL spezifizierte Fehlernummer (11001) sollte geändert werden, damit sie mit dem Ihnen angezeigten Fehler übereinstimmt.  
  
## <a name="see-also"></a>Siehe auch

[Installieren des Treiber-Managers](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Versionsanmerkungen](../../../connect/odbc/linux-mac/release-notes.md)

[Systemanforderungen](../../../connect/odbc/linux-mac/system-requirements.md)

