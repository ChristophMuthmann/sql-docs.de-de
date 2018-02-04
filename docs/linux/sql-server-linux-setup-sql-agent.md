---
title: "Installieren von SQL Server-Agent für Linux | Microsoft Docs"
description: Dieses Thema beschreibt, wie der SQL Server-Agent unter Linux zu installieren.
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
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.workload: On Demand
ms.openlocfilehash: 873c2da961db577889a3fca4139e325083d609e9
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="install-sql-server-agent-on-linux"></a>Installieren von SQL Server-Agent für Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Die folgenden Schritte installieren Sie SQL Server-Agent (**Mssql-Server-Agent**) unter Linux. Die [SQL Server-Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) geplante SQL Server-Aufträge ausgeführt. Informationen zu Funktionen, die für diese Version von SQL Server-Agent unterstützt, finden Sie unter der [Release Notes](sql-server-linux-release-notes.md).

> [!NOTE]
> Vor der Installation von SQL Server-Agent zuerst [installieren Sie SQL Server-2017](sql-server-linux-setup.md#platforms). Konfiguriert, um die Schlüssel und Repositorys, die Sie verwenden, bei der Installation der **Mssql-Server-Agent** Paket.

Installieren Sie SQL Server-Agent für Ihre Plattform:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Installieren Sie auf dem RHEL</a>

Verwenden Sie die folgenden Schritte zum Installieren der **Mssql-Server-Agent** unter Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie noch **Mssql-Server-Agent** installiert haben, können Sie auf die neueste Version mit den folgenden Befehlen aktualisieren:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Wenn Sie eine Offlineinstallation benötigen, suchen Sie in der SQL Server-Agent-Paketdownload der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte in diesem Thema beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="ubuntu">Installieren Sie auf Ubuntu</a>

Verwenden Sie die folgenden Schritte zum Installieren der **Mssql-Server-Agent** auf Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie noch **Mssql-Server-Agent** installiert haben, können Sie auf die neueste Version mit den folgenden Befehlen aktualisieren:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Wenn Sie eine Offlineinstallation benötigen, suchen Sie in der SQL Server-Agent-Paketdownload der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte in diesem Thema beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="SLES">Installieren Sie auf SLES</a>

Verwenden Sie die folgenden Schritte zum Installieren der **Mssql-Server-Agent** für SUSE Linux Enterprise Server. 

Installieren Sie **Mssql-Server-Agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie noch **Mssql-Server-Agent** installiert haben, können Sie auf die neueste Version mit den folgenden Befehlen aktualisieren:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Wenn Sie eine Offlineinstallation benötigen, suchen Sie in der SQL Server-Agent-Paketdownload der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte in diesem Thema beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Verwendung von SQL Server-Agent erstellen, Planen und Ausführen von Aufträgen finden Sie unter [führen Sie einen SQL Server-Agent-Auftrag unter Linux](sql-server-linux-run-sql-server-agent-job.md).
