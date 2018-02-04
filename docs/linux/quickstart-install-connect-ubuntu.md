---
title: Erste Schritte mit SQL Server-2017 auf Ubuntu | Microsoft Docs
description: Dieser Schnellstart veranschaulicht das Installieren von SQL Server-2017 auf Ubuntu und erstellen und Abfragen einer Datenbank mit Sqlcmd.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.workload: Active
ms.openlocfilehash: ac570feda5ce20ee8d255abb25b83a327c84c7f3
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="install-sql-server-and-create-a-database-on-ubuntu"></a>Installieren von SQL Server, und erstellen Sie eine Datenbank für Ubuntu

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Schnellstart installieren Sie zunächst SQL Server 2017 auf Ubuntu 16.04. Verbinden Sie dann mit **Sqlcmd** Ihre erste Datenbank zu erstellen und Ausführen von Abfragen.

> [!TIP]
> Dieses Lernprogramm erfordert Benutzereingaben und eine Internetverbindung. Wenn Sie interessiert sind die [unbeaufsichtigte](sql-server-linux-setup.md#unattended) oder [offline](sql-server-linux-setup.md#offline) Installationsverfahren, finden Sie unter [-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Sie benötigen einen Computer Ubuntu 16.04 mit **mindestens 2 GB** des Arbeitsspeichers.

Um Ubuntu auf Ihrem eigenen Computer zu installieren, wechseln Sie zu [http://www.ubuntu.com/download/server](http://www.ubuntu.com/download/server). Sie können auch Ubuntu virtuelle Computer in Azure erstellen. Finden Sie unter [erstellen und verwalten Sie virtuelle Linux-Computer mit der Azure-CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm).

> [!NOTE]
> Zu diesem Zeitpunkt die [Windows-Subsystem für Linux](https://msdn.microsoft.com/commandline/wsl/about) für Windows 10 als Installationsziel für eine wird nicht unterstützt.

Weitere Informationen zu Systemanforderungen, finden Sie unter [Systemanforderungen für SQL Server on Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Installieren von SQLServer

Um SQL Server auf Ubuntu konfigurieren möchten, führen Sie die folgenden Befehle in einem abschließenden zum Installieren der **Mssql Server** Paket.

> [!IMPORTANT]
> Wenn Sie eine CTP bzw. RC-Version von SQL Server-2017 zuvor installiert haben, müssen Sie zuerst die alte Repository entfernen, vor der Registrierung eines den GA-Repositorys. Weitere Informationen finden Sie unter [ändern Repositorys aus dem Repository Vorschau in GA-Repository](sql-server-linux-change-repo.md).

1. Importieren Sie die öffentlichen Repositorys GPG Schlüssel:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Das Microsoft SQL Server-Ubuntu-Repository zu registrieren:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!NOTE]
   > Dies ist das kumulative Update (CU)-Repository. Weitere Informationen zu Ihrem Repository-Optionen und deren Unterschiede finden Sie unter [ändern quellrepositorys](sql-server-linux-setup.md#repositories).

1. Führen Sie die folgenden Befehle zum Installieren von SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

1. Nach der Paket-Installation abgeschlossen ist, führen Sie **Mssql-Conf Setup** und befolgen Sie die Anweisungen, um das SA-Kennwort festlegen, und wählen die Version.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Wenn Sie SQL Server-2017 in diesem Lernprogramm versuchen, die folgenden Editionen kostenlos lizenziert: Evaluation, Developer und Express.

   > [!NOTE]
   > Stellen Sie sicher, dass ein sicheres Kennwort für das SA-Konto (minimale Länge von 8 Zeichen, einschließlich Groß- und Kleinbuchstaben, Ziffern der Basis 10 und/oder nicht alphanumerische Symbole) angeben.

1. Sobald die Konfiguration abgeschlossen ist, stellen Sie sicher, dass der Dienst ausgeführt wird:

   ```bash
   systemctl status mssql-server
   ```

1. Wenn Sie eine Remoteverbindung herstellen möchten, müssen Sie möglicherweise auch die SQL Server-TCP-Port (Standardport: 1433) in Ihrer Firewall öffnen.

An diesem Punkt wird SQL Server ausgeführt wird, auf dem Computer Ubuntu und ist einsatzbereit!

## <a id="tools"></a>Installieren Sie die SQL Server-Befehlszeilentools

Um eine Datenbank erstellen zu können, müssen Sie die Verbindung mit einem Tool, das auf dem SQL Server Transact-SQL-Anweisungen ausgeführt werden kann. Die folgenden Schritte aus der SQL Server-Befehlszeilentools zu installieren: [Sqlcmd](../tools/sqlcmd-utility.md) und [Bcp](../tools/bcp-utility.md).

1. Importieren Sie die öffentlichen Repositorys GPG Schlüssel:

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Registrieren Sie das Repository Microsoft Ubuntu:

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
   ```

1. Aktualisieren Sie die Liste der Datenquellen, und führen Sie den Installationsbefehl mit dem UnixODBC Developer-Paket:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-tools unixodbc-dev
   ```

1. Fügen Sie der Einfachheit halber `/opt/mssql-tools/bin/` auf Ihre **Pfad** -Umgebungsvariablen angegeben. Dadurch können Sie die Tools ausführen, ohne den vollständigen Pfad anzugeben. Führen Sie die folgenden Befehle zum Ändern der **Pfad** für anmeldesitzungen und interaktive/nicht-Anmeldung Sitzungen:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd** ist nur ein Tool zum Herstellen einer Verbindung mit SQL Server zum Ausführen von Abfragen und Verwaltungs- und Entwicklungstools Aufgaben ausführen. Andere Tools umfassen:
>
> * [SQL Server Operationen Studio (Vorschau)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * [Visual Studio Code](sql-server-linux-develop-use-vscode.md).
> * [MSSQL-Cli (Vorschau)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
