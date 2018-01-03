---
title: "Erste Schritte mit SQL Server-2017 für SUSE Linux Enterprise Server | Microsoft Docs"
description: Dieser Schnellstart veranschaulicht das Installieren von SQL Server-2017 auf SUSE Linux Enterprise Server und erstellen und Abfragen einer Datenbank mit Sqlcmd.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.workload: On Demand
ms.openlocfilehash: b92036d4b706b5e76165708438d350c1883db912
ms.sourcegitcommit: 73043fe1ac5d60b67e33b44053c0a7733b98bc3d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Installieren von SQL Server, und erstellen Sie eine Datenbank auf SUSE Linux Enterprise Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Schnellstart installieren Sie zunächst SQL Server 2017 unter SUSE Linux Enterprise Server (SLES) v12 SP2. Verbinden Sie dann mit **Sqlcmd** Ihre erste Datenbank zu erstellen und Ausführen von Abfragen.

> [!TIP]
> Dieses Lernprogramm erfordert Benutzereingaben und eine Internetverbindung. Wenn Sie interessiert sind die [unbeaufsichtigte](sql-server-linux-setup.md#unattended) oder [offline](sql-server-linux-setup.md#offline) Installationsverfahren, finden Sie unter [-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Voraussetzungen

Sie benötigen einen SLES v12 SP2-Computer mit **mindestens 2 GB** des Arbeitsspeichers. Das Dateisystem muss **XFS** oder **EXT4**. Andere Dateisysteme, z. B. **BTRFS**, werden nicht unterstützt.

Um SUSE Linux Enterprise Server auf dem eigenen Computer zu installieren, wechseln Sie zu [https://www.suse.com/products/server](https://www.suse.com/products/server). Sie können auch SLES virtuelle Computer in Azure erstellen. Finden Sie unter [erstellen und Verwalten von Linux-VMs mit der Azure-CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm), und verwenden Sie `--image SLES` im Aufruf von `az vm create`.

> [!NOTE]
> Zu diesem Zeitpunkt die [Windows-Subsystem für Linux](https://msdn.microsoft.com/commandline/wsl/about) für Windows 10 als Installationsziel für eine wird nicht unterstützt.

Weitere Informationen zu Systemanforderungen, finden Sie unter [Systemanforderungen für SQL Server on Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Installieren von SQLServer

Um SQL Server auf SLES konfigurieren möchten, führen Sie die folgenden Befehle in einem abschließenden zum Installieren der **Mssql Server** Paket:

> [!IMPORTANT]
> Wenn Sie eine CTP bzw. RC-Version von SQL Server-2017 zuvor installiert haben, müssen Sie zuerst die alte Repository entfernen, vor der Registrierung eines den GA-Repositorys. Weitere Informationen finden Sie unter [ändern Repositorys aus dem Repository Vorschau in GA-Repository](sql-server-linux-change-repo.md).

1. Herunterladen der Microsoft SQL Server-SLES Repository-Konfigurationsdatei an:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   sudo zypper --gpg-auto-import-keys refresh
   ```

   > [!NOTE]
   > Dies ist das kumulative Update (CU)-Repository. Weitere Informationen zu Ihrem Repository-Optionen und deren Unterschiede finden Sie unter [ändern quellrepositorys](sql-server-linux-setup.md#repositories).

1. Führen Sie die folgenden Befehle zum Installieren von SQL Server:

   ```bash
   sudo zypper install -y mssql-server
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

1. Wenn Sie eine Remoteverbindung herstellen möchten, müssen Sie möglicherweise auch die SQL Server-TCP-Port (Standardport: 1433) in Ihrer Firewall öffnen. Wenn Sie die SuSE-Firewall verwenden, müssen Sie bearbeiten die **/etc/sysconfig/SuSEfirewall2** Konfigurationsdatei. Ändern der **FW_SERVICES_EXT_TCP** Eintritt in die SQL Server-Portnummer einschließen.

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

An diesem Punkt wird SQL Server ausgeführt wird, auf dem Computer SLES und ist einsatzbereit!

## <a id="tools"></a>Installieren Sie die SQL Server-Befehlszeilentools

Um eine Datenbank erstellen zu können, müssen Sie die Verbindung mit einem Tool, das auf dem SQL Server Transact-SQL-Anweisungen ausgeführt werden kann. Die folgenden Schritte aus der SQL Server-Befehlszeilentools zu installieren: [Sqlcmd](../tools/sqlcmd-utility.md) und [Bcp](../tools/bcp-utility.md).

1. Fügen Sie das Microsoft SQL Server-Repository hinzu Zypper.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Installieren Sie **Mssql-Tools** mit dem UnixODBC Developer-Paket.

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
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
> * [Visual Studio-Code](sql-server-linux-develop-use-vscode.md).
> * [MSSQL-Cli (Vorschau)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
