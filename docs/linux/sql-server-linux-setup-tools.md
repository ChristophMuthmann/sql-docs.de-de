---
title: Installieren von SQL Server-Befehlszeilentools unter Linux | Microsoft Docs
description: Dieses Thema beschreibt, wie die SQL Server-Verwaltungstools unter Linux zu installieren.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 130da2409070f0acfda0bf78fcf2c4326bbeec92
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Installieren Sie die SQL Server-Befehlszeilentools Sqlcmd und Bcp unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Die folgenden Schritte installieren Sie die Befehlszeilentools, Microsoft ODBC-Treiber und ihre Abhängigkeiten. Die **Mssql-Tools** Paket enthält:

- **Sqlcmd**: Abfrage Befehlszeilen-Hilfsprogramm.
- **BCP**: Massenkopieren Import / Export-Dienstprogramm.

Installieren von Tools für Ihre Plattform:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

In diesem Thema wird beschrieben, wie die Befehlszeilentools zu installieren. Beispiele zur Verwendung für die originale **Sqlcmd** oder **Bcp**, finden Sie unter der [Links](#next-steps) am Ende dieses Themas.

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>Installieren von Tools für RHEL 7

Verwenden Sie die folgenden Schritte zum Installieren der **Mssql-Tools** unter Red Hat Enterprise Linux. 

1. Geben Sie ein Superuser-Modus.

   ```bash
   sudo su
   ```

1. Herunterladen der Microsoft Red Hat-Repository-Konfigurationsdatei an.

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. Exit-Superuser-Modus.

   ```bash
   exit
   ```

1. Wenn Sie eine frühere Version des mussten **Mssql-Tools** installiert haben, entfernen Sie alle älteren UnixODBC-Paketen.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Führen Sie die folgenden Befehle zum Installieren **Mssql-Tools** mit dem UnixODBC Developer-Paket.

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Beim Aktualisieren auf die neueste Version der **Mssql-Tools** führen Sie die folgenden Befehle:
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **Optionale**: Hinzufügen `/opt/mssql-tools/bin/` auf Ihre **Pfad** -Umgebungsvariable in der Bash-Shell.

   Vornehmen **Sqlcmd/Bcp** zugegriffen werden kann, aus der Bash-Shell für anmeldesitzungen, Ändern der **Pfad** in der **~/.bash_profile** Datei mit dem folgenden Befehl:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Vornehmen **Sqlcmd/Bcp** zugegriffen werden kann, aus der Bash-Shell für interaktive/nicht-anmeldesitzungen, Ändern der **Pfad** in der **~/.bashrc** -Datei mit den folgenden Befehl aus:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>Installieren von Tools auf Ubuntu 16.04

Verwenden Sie die folgenden Schritte zum Installieren der **Mssql-Tools** auf Ubuntu. 

1. Importieren Sie die öffentlichen Repositorys GPG Schlüssel.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registrieren Sie die Microsoft Ubuntu-Repositorys.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. Aktualisieren Sie die Liste der Datenquellen, und führen Sie den Installationsbefehl den UnixODBC Developer-Paket aus.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > Beim Aktualisieren auf die neueste Version der **Mssql-Tools** führen Sie die folgenden Befehle:
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **Optionale**: Hinzufügen `/opt/mssql-tools/bin/` auf Ihre **Pfad** -Umgebungsvariable in der Bash-Shell.

   Vornehmen **Sqlcmd/Bcp** zugegriffen werden kann, aus der Bash-Shell für anmeldesitzungen, Ändern der **Pfad** in der **~/.bash_profile** Datei mit dem folgenden Befehl:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Vornehmen **Sqlcmd/Bcp** zugegriffen werden kann, aus der Bash-Shell für interaktive/nicht-anmeldesitzungen, Ändern der **Pfad** in der **~/.bashrc** -Datei mit den folgenden Befehl aus:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>Installieren von Tools für SLES 12

Verwenden Sie die folgenden Schritte zum Installieren der **Mssql-Tools** für SUSE Linux Enterprise Server. 

1. Fügen Sie das Microsoft SQL Server-Repository hinzu Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Installieren Sie **Mssql-Tools** mit dem UnixODBC Developer-Paket.

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > Beim Aktualisieren auf die neueste Version der **Mssql-Tools** führen Sie die folgenden Befehle:
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **Optionale**: Hinzufügen `/opt/mssql-tools/bin/` auf Ihre **Pfad** -Umgebungsvariable in der Bash-Shell.

   Vornehmen **Sqlcmd/Bcp** zugegriffen werden kann, aus der Bash-Shell für anmeldesitzungen, Ändern der **Pfad** in der **~/.bash_profile** Datei mit dem folgenden Befehl:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   Vornehmen **Sqlcmd/Bcp** zugegriffen werden kann, aus der Bash-Shell für interaktive/nicht-anmeldesitzungen, Ändern der **Pfad** in der **~/.bashrc** -Datei mit den folgenden Befehl aus:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a>Installieren von Tools auf macOS

Eine Vorschau der **Sqlcmd** und **Bcp** ist nun auf MacOS verfügbar. Weitere Informationen finden Sie unter der [Ankündigung](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/).

Verwenden Sie zum Installieren der Tools für Mac El Capitan und Sierra die folgenden Befehle ein:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
#brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox mssql-tools
#for silent install: 
#ACCEPT_EULA=y brew install --no-sandbox mssql-tools
```

## <a id="docker"></a>Docker

Beginnend mit SQL Server 2017 CTP 2.0, sind die SQL Server-Befehlszeilentools in der Docker-Images enthalten. Wenn Sie das Image mit einer interaktiven Eingabeaufforderung anfügen, können Sie die Tools lokal ausführen.

## <a name="offline-installation"></a>Offlineinstallation

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

Die folgende Tabelle enthält den Speicherort für die neuesten Tools Pakete:

| Tools-Paket | Version | Herunterladen |
|-----|-----|-----|
| Red Hat-RPM-Tools-Paket | 14.0.5.0-1 | [MSSQL-Tools-RPM-Paket](https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| SLES RPM-Tools-Paket | 14.0.5.0-1 | [MSSQL-Tools-RPM-Paket](https://packages.microsoft.com/sles/12/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian-Paket tools | 14.0.5.0-1 | [MSSQL-Tools Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |
| Ubuntu 16.10 Debian-Paket tools | 14.0.5.0-1 | [MSSQL-Tools Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |

Diese Pakete richten sich nach **Msodbcsql**, und muss zunächst installiert werden. Die **Msodbcsql** Paket besteht eine Abhängigkeit auf **UnixODBC-entwickl** (RPM) oder **Unixodbc-Dev** (Debian). Der Speicherort, der die **Msodbcsql** Pakete werden in der folgenden Tabelle aufgeführt:

| Msodbcsql-Paket | Version | Herunterladen |
|-----|-----|-----|
| Red Hat-RPM-Msodbcsql-Paket | 13.1.6.0-1 | [Msodbcsql-RPM-Paket](https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| SLES RPM-Msodbcsql-Paket | 13.1.6.0-1 | [Msodbcsql-RPM-Paket](https://packages.microsoft.com/sles/12/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Msodbcsql Debian-Paket | 13.1.6.0-1 | [Msodbcsql Debian-Paket](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |
| Ubuntu 16.10 Msodbcsql Debian-Paket | 13.1.6.0-1 | [Msodbcsql Debian-Paket](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |

Verwenden Sie die folgenden Schritte aus, um diese Pakete manuell zu installieren:

1. **Verschieben Sie die heruntergeladenen Pakete auf Linux-Computer**. Wenn Sie einen anderen Computer verwendet, um die Pakete herunterzuladen, ist eine Möglichkeit zum Verschieben der Pakete auf den Linux-Computer mit der **scp** Befehl.

1. **Installieren der Pakete und**: Installieren der **Mssql-Tools** und **Msodbc** Pakete. Wenn Sie keine Abhängigkeit Fehler erhalten, bis der nächste Schritt ignorieren.

    | Platform | Paket installieren Befehle |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | SLES | `sudo zypper install msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo zypper install mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_13.1.6.0-1_amd64.deb`<br/>`sudo dpkg -i mssql-tools_14.0.5.0-1_amd64.deb` |

1. **Alle fehlenden Abhängigkeiten müssen aufgelöst**: Sie müssen möglicherweise an diesem Punkt fehlenden Abhängigkeiten. Wenn dies nicht der Fall ist, können Sie diesen Schritt überspringen. In einigen Fällen müssen Sie manuell suchen und installieren diese Abhängigkeiten.

    Für RPM-Pakete können Sie überprüfen und die erforderlichen Abhängigkeiten mit den folgenden Befehlen:

    ```bash
    rpm -qpR msodbcsql-13.1.6.0-1.x86_64.rpm
    rpm -qpR mssql-tools-14.0.5.0-1.x86_64.rpm
    ```

    Für Pakete, Debian, wenn Sie Zugriff auf genehmigten Repositorys, enthält diese Abhängigkeiten die einfachste Lösung ist die Verwendung der **apt-Get** Befehl:

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > Dieser Befehl schließt die Installation der SQL Server-Pakete.

    Wenn dies für Ihre Debian-Paket nicht funktioniert, können Sie überprüfen und die erforderlichen Abhängigkeiten mit den folgenden Befehlen:

    ```bash
    dpkg -I msodbcsql_13.1.6.0-1_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_14.0.5.0-1_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>Nächste Schritte

Ein Beispiel zum Verwenden von **Sqlcmd** zum Herstellen einer Verbindung mit SQL Server, und erstellen Sie eine Datenbank, finden Sie in einem der folgenden Quick start Lernprogramme:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)

Ein Beispiel zum Verwenden von **Bcp** zum Massenimport und Exportieren von Daten, finden Sie unter [Massenkopieren von Daten mit SQL Server on Linux](sql-server-linux-migrate-bcp.md).

