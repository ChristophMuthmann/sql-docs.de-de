---
title: Erste Schritte mit SQL Server-2017 unter Red Hat Enterprise Linux | Microsoft Docs
description: Dieser Schnellstart-Tutorial wird gezeigt, wie 2017 von SQL Server unter Red Hat Enterprise Linux installieren und dann zu erstellen und Abfragen einer Datenbank mit Sqlcmd wird.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 6d18cbe5b20882581afa731ce5d207cbbc69be6c
ms.openlocfilehash: d5f7a249e43619e0730da0a30fd5597788441bb8
ms.contentlocale: de-de
ms.lasthandoff: 10/21/2017

---
# <a name="install-sql-server-and-create-a-database-on-red-hat"></a>Installieren von SQL Server, und erstellen Sie eine Datenbank auf Red Hat

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Schnellstart-Tutorial installieren Sie zuerst SQL Server 2017 für die Red Hat Enterprise Linux (RHEL) 7.3 +. Verbinden Sie dann mit **Sqlcmd** Ihre erste Datenbank zu erstellen und Ausführen von Abfragen.

> [!TIP]
> Dieses Lernprogramm erfordert Benutzereingaben und eine Internetverbindung. Wenn Sie interessiert sind die [unbeaufsichtigte](sql-server-linux-setup.md#unattended) oder [offline](sql-server-linux-setup.md#offline) Installationsverfahren, finden Sie unter [-Installationsleitfaden für SQL Server on Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Sie benötigen eine RHEL 7.3 oder 7.4 Computer mit **mindestens 3,25 GB** des Arbeitsspeichers.

Wechseln Sie zu um Red Hat Enterprise Linux auf Ihrem eigenen Computer zu installieren, [http://access.redhat.com/products/red-hat-enterprise-linux/evaluation](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation). Sie können auch RHEL virtuelle Computer in Azure erstellen. Finden Sie unter [erstellen und Verwalten von Linux-VMs mit der Azure-CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm), und verwenden Sie `--image RHEL` im Aufruf von `az vm create`.

Weitere Informationen zu Systemanforderungen, finden Sie unter [Systemanforderungen für SQL Server on Linux](sql-server-linux-setup.md#system).

## <a id="install"></a>Installieren von SQLServer

Um SQL Server auf RHEL konfigurieren möchten, führen Sie die folgenden Befehle in einem abschließenden zum Installieren der **Mssql Server** Paket:

> [!IMPORTANT]
> Wenn Sie eine CTP bzw. RC-Version von SQL Server-2017 zuvor installiert haben, müssen Sie zuerst die alte Repository entfernen, vor der Registrierung eines den GA-Repositorys. Weitere Informationen finden Sie unter [ändern Repositorys aus dem Repository Vorschau in GA-Repository](sql-server-linux-change-repo.md).

1. Herunterladen der Microsoft SQL Server-Red Hat-Repository-Konfigurationsdatei an:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!NOTE]
   > Dies ist das kumulative Update (CU)-Repository. Weitere Informationen zu Ihrem Repository-Optionen und deren Unterschiede finden Sie unter [ändern quellrepositorys](sql-server-linux-setup.md#repositories).

1. Führen Sie die folgenden Befehle zum Installieren von SQL Server:

   ```bash
   sudo yum install -y mssql-server
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
   
1. Um Remoteverbindungen zuzulassen, öffnen Sie den SQL Server-Dienstport für die Firewall auf dem RHEL. Der SQL Server-Standardport ist TCP 1433. Bei Verwendung von **FirewallD** für Ihre Firewall können Sie die folgenden Befehle verwenden:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

An diesem Punkt wird SQL Server auf dem RHEL-Computer ausgeführt wird, und ist einsatzbereit!

## <a id="tools"></a>Installieren Sie die SQL Server-Befehlszeilentools

Um eine Datenbank erstellen zu können, müssen Sie die Verbindung mit einem Tool, das auf dem SQL Server Transact-SQL-Anweisungen ausgeführt werden kann. Die folgenden Schritte aus der SQL Server-Befehlszeilentools zu installieren: [Sqlcmd](../tools/sqlcmd-utility.md) und [Bcp](../tools/bcp-utility.md).

1. Herunterladen der Microsoft Red Hat-Repository-Konfigurationsdatei an.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. Wenn Sie eine frühere Version des mussten **Mssql-Tools** installiert haben, entfernen Sie alle älteren UnixODBC-Paketen.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Führen Sie die folgenden Befehle zum Installieren **Mssql-Tools** mit dem UnixODBC Developer-Paket.

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
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

