---
title: "Erste Schritte mit SQL Server-2017 für SUSE Linux Enterprise Server | Microsoft Docs"
description: Dieser Schnellstart-Tutorial wird gezeigt, wie installieren Sie SQL Server-2017 auf SUSE Linux Enterprise Server und erstellen und Abfragen einer Datenbank mit Sqlcmd wird.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 09/07/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: d454dca437f64a73879ed689fce1100c74a6fcde
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>Installieren von SQL Server, und erstellen Sie eine Datenbank auf SUSE Linux Enterprise Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Schnellstart-Tutorial installieren Sie zuerst SQL Server 2017 RC2 unter SUSE Linux Enterprise Server (SLES) v12 SP2. Verbinden Sie dann mit **Sqlcmd** Ihre erste Datenbank zu erstellen und Ausführen von Abfragen.

> [!TIP]
> Dieses Lernprogramm erfordert Benutzereingaben und eine Internetverbindung. Wenn Sie interessiert sind die [unbeaufsichtigte](sql-server-linux-setup.md#unattended) oder [offline](sql-server-linux-setup.md#offline) Installationsverfahren, finden Sie unter [-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Sie benötigen einen SLES v12 SP2-Computer mit **mindestens 3,25 GB** des Arbeitsspeichers. Das Dateisystem muss **XFS** oder **EXT4**. Andere Dateisysteme, z. B. **BTRFS**, werden nicht unterstützt.

Um SUSE Linux Enterprise Server auf dem eigenen Computer zu installieren, wechseln Sie zu [https://www.suse.com/products/server](https://www.suse.com/products/server). Sie können auch SLES virtuelle Computer in Azure erstellen. Finden Sie unter [erstellen und Verwalten von Linux-VMs mit der Azure-CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm), und verwenden Sie `--image SLES` im Aufruf von `az vm create`.

Weitere Informationen zu Systemanforderungen, finden Sie unter [Systemanforderungen für SQL Server on Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Installieren von SQLServer

Um SQL Server auf SLES konfigurieren möchten, führen Sie die folgenden Befehle in einem abschließenden zum Installieren der **Mssql Server** Paket:

1. Herunterladen der Microsoft SQL Server-SLES Repository-Konfigurationsdatei an:

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. Führen Sie die folgenden Befehle zum Installieren von SQL Server:

   ```bash
   sudo zypper install -y mssql-server
   ```

1. Nach der Paket-Installation abgeschlossen ist, führen Sie **Mssql-Conf Setup** und befolgen Sie die Anweisungen, um das SA-Kennwort festlegen, und wählen die Version.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > Stellen Sie sicher, dass ein sicheres Kennwort für das SA-Konto (minimale Länge von 8 Zeichen, einschließlich Groß- und Kleinbuchstaben, Ziffern der Basis 10 und/oder nicht alphanumerische Symbole) angeben.

   > [!TIP]
   > Bei der Installation von RC2 sind keine erworbenen Lizenzen erforderlich, um eine der Editionen versuchen. Da es sich um ein Release Candidate handelt, wird die folgende Meldung angezeigt, unabhängig von der Edition, die Sie auswählen:
   >
   > `This is an evaluation version.  There are [175] days left in the evaluation period.`
   >
   > Diese Meldung reflektiert nicht die Edition, die Sie ausgewählt haben. Er bezieht sich auf die Preview-Zeitraums für RC2.

1. Sobald die Konfiguration abgeschlossen ist, stellen Sie sicher, dass der Dienst ausgeführt wird:

   ```bash
   systemctl status mssql-server
   ```

1. Wenn Sie eine Remoteverbindung herstellen möchten, müssen Sie möglicherweise auch die SQL Server-TCP-Port (Standardport: 1433) in Ihrer Firewall öffnen.

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
> **Sqlcmd** ist nur ein Tool zum Herstellen einer Verbindung mit SQL Server zum Ausführen von Abfragen und Verwaltungs- und Entwicklungstools Aufgaben ausführen. Andere Tools umfassen [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md) und [Visual Studio Code](sql-server-linux-develop-use-vscode.md).

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]

