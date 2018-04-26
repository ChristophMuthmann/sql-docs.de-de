---
title: Unbeaufsichtigte Installation für SQL Server unter SUSE Linux Enterprise Server | Microsoft Docs
description: SQL Server-Skript-Beispiel - unbeaufsichtigte Installation für SUSE Linux Enterprise Server
author: edmacauley
ms.author: edmaca
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 8f783244a2bcfab915453929636433c92160a177
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sample-unattended-sql-server-installation-script-for-suse-linux-enterprise-server"></a>Beispiel: Für die unbeaufsichtigte SQL Server-Installationsskript für SUSE Linux Enterprise Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieses Beispielskript für die Bash installiert 2017 von SQL Server unter SUSE Linux Enterprise Server (SLES) v12 SP2 ohne interaktiver Eingabe. Er bietet Beispiele für die Installation des Datenbankmoduls, die SQL Server-Befehlszeilentools, SQL Server-Agent, und führt nach der Installation Schritte aus. Optional können Sie einen Administrator zu erstellen und Installieren der Volltextsuche.

> [!TIP]
> Wenn Sie ein Skript für die unbeaufsichtigte Installation nicht benötigen, ist die schnellste Möglichkeit zum Installieren von SQL Server, führen die [Schnellstart für SLES](quickstart-install-connect-suse.md). Weitere Informationen zum Setup finden Sie unter [-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

- Sie benötigen mindestens 2 GB Arbeitsspeicher zum Ausführen von SQL Server unter Linux.
- Das Dateisystem muss **XFS** oder **EXT4**. Andere Dateisysteme, z. B. **BTRFS**, werden nicht unterstützt.
- Weitere Informationen zu Systemanforderungen, finden Sie unter [Systemanforderungen für SQL Server on Linux](sql-server-linux-setup.md#system).

> [!IMPORTANT]
> SQL Server-2017 erfordert libsss_nss_idmap0, das nicht von der Standardeinstellung SLES Repositorys bereitgestellt wird. Sie können ihn aus dem SLES v12 SP2-SDK installieren.

## <a name="sample-script"></a>Beispielskript

```bash
#!/bin/bash -e

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_INSTALL_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
sudo zypper --gpg-auto-import-keys refresh

#Add the SLES v12 SP2 SDK to obtain libsss_nss_idmap0
sudo SUSEConnect -p sle-sdk/12.2/x86_64

echo Installing SQL Server...
sudo zypper install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y zypper install -y mssql-tools unixODBC-devel

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo zypper install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo zypper install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring SuSEfirewall2 to allow traffic on port 1433...
sudo SuSEfirewall2 open INT TCP 1433
sudo SuSEfirewall2 stop
sudo SuSEfirewall2 start

# Example of setting post-installation configuration options
# Set trace flags 1204 and 1222 for deadlock tracing:
# echo Setting trace flags...
# sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after making configuration changes:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 5s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

### <a name="running-the-script"></a>Ausführen des Skripts

So führen Sie das Skript aus

1. Fügen Sie das Beispiel in Ihrem bevorzugten Text-Editor, und speichern Sie sie z. B. mit einem einprägsamen Namen `install_sql.sh`.

1. Anpassen `MSSQL_SA_PASSWORD`, `MSSQL_PID`, und die anderen Eigenschaften, die Sie ändern möchten.

1. Markieren Sie das Skript als ausführbare Datei

   ```bash
   chmod +x install_sql.sh
   ```

1. Führen Sie das Skript

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>Grundlegendes zum Skript
Im ersten Schritt des Bash-Skripts, die einige Variablen festgelegt ist. Dabei kann es sich um Umgebungsvariablen oder Skriptvariablen wie im Beispiel handeln. Die Variable ``` MSSQL_SA_PASSWORD ``` ist **erforderlichen** von SQL Server-Installation, die die anderen sind benutzerdefinierte Variablen, die für das Skript erstellt. Das Beispielskript führt die folgenden Schritte aus:

1. Importieren Sie die öffentlichen Microsoft-GPG-Schlüssel.

1. Registrieren Sie den Microsoft-Repositorys für SQL Server und die Befehlszeilenprogramme.

1. Aktualisieren Sie den lokalen Repositorys

1. Installieren von SQL Server

1. Konfigurieren von SQL Server mit der ```MSSQL_SA_PASSWORD``` und die automatische Annahme der Endbenutzer-Lizenzvertrag.

1. Automatisch akzeptieren der Endbenutzer-Lizenzvertrag für die SQL Server-Befehlszeilentools, installieren Sie sie und installieren Sie das Unixodbc-Dev-Paket.

1. Der Pfad für die einfache Verwendung der SQL Server-Befehlszeilentools hinzugefügt.

1. Installieren Sie SQL Server-Agent aus, wenn die Skriptvariable ```SQL_INSTALL_AGENT``` standardmäßig festgelegt ist, auf.

1. Installieren Sie SQL Server-Volltextsuche, optional, wenn die Variable ```SQL_INSTALL_FULLTEXT``` festgelegt ist.

1. Entsperren Sie Port 1433 für TCP auf dem System-Firewall von einem anderen System eine Verbindung mit SQL Server erforderlich.

1. Legen Sie optional Ablaufverfolgungsflags für die Ablaufverfolgung Deadlock fest. (erfordert die auskommentierung der Zeilen)

1. SQL Server ist jetzt installiert werden, um betriebsbereit zu machen, den Prozess erneut starten.

1. Stellen Sie sicher, dass SQL Server ordnungsgemäß installiert ist, und gleichzeitig alle Fehlermeldungen.

1. Erstellen Sie einen neuen Benutzer des Server-Administrator, wenn ```SQL_INSTALL_USER``` und ```SQL_INSTALL_USER_PASSWORD``` sind beide festgelegt.

## <a name="next-steps"></a>Nächste Schritte

Mehrere unbeaufsichtigte Installationen zu vereinfachen, und Erstellen eines eigenständigen Bash-Skripts, durch die die entsprechenden Umgebungsvariablen festgelegt. Sie können Variablen einen entfernen, die das Beispielskript verwendet, und fügen Sie sie in ihren eigenen Bash-Skripts.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

Führen Sie dann die Bash-Skripts wie folgt:
```bash
. ./my_script_name.sh
```

Weitere Informationen zu SQL Server unter Linux finden Sie unter [SQL Server on Linux – Übersicht](sql-server-linux-overview.md).