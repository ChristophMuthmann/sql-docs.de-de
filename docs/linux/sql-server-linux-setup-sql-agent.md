---
title: "Installieren von SQL Server-Agent für Linux | Microsoft Docs"
description: Dieses Thema beschreibt, wie der SQL Server-Agent unter Linux zu installieren.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 83f6e12a38d5fef4ab27cc39257906c4263aa846
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="install-sql-server-agent-on-linux"></a>Installieren von SQL Server-Agent für Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Führen Sie die folgenden Schritte aus, um den SQL Server-Agent (**Mssql-Server-Agent**) unter Linux zu installieren. Der [SQL Server-Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) führt geplante SQL Server-Aufträge aus. Informationen zu Features, die für diese Version von SQL Server-Agent unterstützt werden, finden Sie in den [Release Notes](sql-server-linux-release-notes.md).

> [!NOTE]
> [Installieren Sie den SQL Server-2017](sql-server-linux-setup.md#platforms), bevor Sie den SQL Server-Agent installieren. Dadurch werden die Schlüssel und Repositories konfiguriert, die zur Installation des **Mssql-Server-Agent** Pakets benötigt werden.

Installieren Sie SQL Server-Agent für Ihre Plattform:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Installieren Sie auf RHEL</a>

Verwenden Sie die folgenden Schritte zum Installieren des **Mssql-Server-Agent** unter Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls der **Mssql-Server-Agent** bereits installiert ist, können Sie mit den folgenden Befehlen das Update auf die aktuellste Version durchführen:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie eine Offline-Installation durchführen möchten, finden Sie den SQL Server-Agent-Paketdownload in den [Release Notes](sql-server-linux-release-notes.md). Verwenden Sie zum installieren anschließend die in [Installieren von SQL Server](sql-server-linux-setup.md#offline) beschriebenen Installationsschritte. 

## <a name="ubuntu">Installieren Sie auf Ubuntu</a>

Verwenden Sie die folgenden Schritte zum Installieren des **Mssql-Server-Agent** auf Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls der **Mssql-Server-Agent** bereits installiert ist, können Sie mit den folgenden Befehlen das Update auf die aktuellste Version durchführen:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie eine Offline-Installation durchführen möchten, finden Sie den SQL Server-Agent-Paketdownload in den [Release Notes](sql-server-linux-release-notes.md). Verwenden Sie zum installieren anschließend die in [Installieren von SQL Server](sql-server-linux-setup.md#offline) beschriebenen Installationsschritte. 

## <a name="SLES">Installieren Sie auf SLES</a>

Verwenden Sie die folgenden Schritte zum Installieren des **Mssql-Server-Agent** für SUSE Linux Enterprise Server. 

Installieren Sie **Mssql-Server-Agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Falls der **Mssql-Server-Agent** bereits installiert ist, können Sie mit den folgenden Befehlen das Update auf die aktuellste Version durchführen:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Falls Sie eine Offline-Installation durchführen möchten, finden Sie den SQL Server-Agent-Paketdownload in den [Release Notes](sql-server-linux-release-notes.md). Verwenden Sie zum installieren anschließend die in [Installieren von SQL Server](sql-server-linux-setup.md#offline) beschriebenen Installationsschritte. 

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Verwendung von SQL Server-Agent zum erstellen, planen und ausführen von Aufträgen finden Sie unter [Erstellen und Ausführen von SQL Server-Agent-Aufträge unter Linux](sql-server-linux-run-sql-server-agent-job.md).

