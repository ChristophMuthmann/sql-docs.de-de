---
title: "Installieren von SQL Server-Agent für Linux | Microsoft Docs"
description: Dieser Artikel beschreibt, wie der SQL Server-Agent unter Linux zu installieren.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.workload: On Demand
ms.openlocfilehash: 7db50a59a4a6ce9ab7aa416e4ac8d597449541b7
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="install-sql-server-agent-on-linux"></a>Installieren von SQL Server-Agent für Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Führen Sie die folgenden Schritte aus, um den SQL Server-Agent (**Mssql-Server-Agent**) unter Linux zu installieren. Der [SQL Server-Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) führt geplante SQL Server-Aufträge aus. Informationen zu Features, die für diese Version von SQL Server-Agent unterstützt werden, finden Sie in den [Release Notes](sql-server-linux-release-notes.md).

> [!NOTE]
> Installieren Sie vor dem SQL Server-Agent zunächst [SQL Server-2017](sql-server-linux-setup.md#platforms). Auf diese Weise werden die Schlüssel und Repositorys konfiguriert, die bei der Installation des **mssql-server-agent**-Pakets verwendet werden.

Installieren Sie SQL Server-Agent für Ihre Plattform:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Installation unter RHEL</a>

Gehen Sie wie folgt vor, um **mssql-server-agent** unter Red Hat Enterprise Linux zu installieren. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls **mssql-server-agent** bereits installiert ist, können Sie mit den folgenden Befehlen auf die neueste Version aktualisieren:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie eine Offline-Installation durchführen möchten, finden Sie den Downloadlink für das SQL Server-Agent-Paket in den [Anmerkungen zur Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte, die im Artikel beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="ubuntu">Installieren Sie auf Ubuntu</a>

Gehen Sie wie folgt vor, um **mssql-server-agent** unter Ubuntu zu installieren. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls **mssql-server-agent** bereits installiert ist, können Sie mit den folgenden Befehlen auf die neueste Version aktualisieren:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie eine Offline-Installation durchführen möchten, finden Sie den Downloadlink für das SQL Server-Agent-Paket in den [Anmerkungen zur Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte, die im Artikel beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="SLES">Installieren Sie auf SLES</a>

Gehen Sie wie folgt vor, um **mssql-server-agent** unter SUSE Linux Enterprise Server zu installieren. 

Installieren Sie **Mssql-Server-Agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls **mssql-server-agent** bereits installiert ist, können Sie mit den folgenden Befehlen auf die neueste Version aktualisieren:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie eine Offline-Installation durchführen möchten, finden Sie den Downloadlink für das SQL Server-Agent-Paket in den [Anmerkungen zur Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte, die im Artikel beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zum Erstellen, Planen und Ausführen von Aufträgen mithilfe des SQL Server-Agents finden Sie unter [„Erstellen und Ausführen von SQL Server-Agent-Aufträgen unter Linux“](sql-server-linux-run-sql-server-agent-job.md).
