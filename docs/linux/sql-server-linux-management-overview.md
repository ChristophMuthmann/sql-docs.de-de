---
title: Verwalten von SQLServer on Linux | Microsoft Docs
description: Dieser Artikel enthält Links zu allgemeinen Verwaltungsaufgaben und Tools für SQL Server auf Linux ausgeführt wird.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: sql-linux
ms.workload: On Demand
ms.openlocfilehash: de19f1952465c62bf026dbd3d92666b7a1b968ae
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Wählen Sie das richtige Tool zum Verwalten von SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Es gibt verschiedene Methoden zum Verwalten von SQL Server-2017 unter Linux. Der folgende Abschnitt enthält eine kurze Übersicht über unterschiedliche Management-Tools und Techniken mit Zeigern auf Weitere Ressourcen.

## <a name="mssql-conf"></a>mssql-conf 
Die **Mssql-Conf** Tool konfiguriert die SQL Server unter Linux. Weitere Informationen finden Sie unter [konfigurieren Sie SQL Server unter Linux mit Mssql-Conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Nahezu jede Option in einem Clienttool ausführen kann auch mit Transact-SQL-Anweisungen ausgeführt werden. SQL Server bietet [dynamische Verwaltungssichten (DMVs)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) Status und Konfiguration von SQL Server-Abfrage. Es gibt auch [Transact-SQL-Befehle](https://msdn.microsoft.com/library/bb510741.aspx) Datenbankverwaltungsaufgaben. Führen Sie diese Befehle in jedem Clienttool, das Herstellen einer Verbindung mit SQL Server und Ausführen von Transact-SQL-Abfragen, z. B. unterstützt [Sqlcmd](sql-server-linux-setup-tools.md) oder [Visual Studio Code](sql-server-linux-develop-use-vscode.md).

## <a name="sql-server-operations-studio-preview"></a>SQL Server Operationen Studio (Vorschau)

Die neue Microsoft SQL Operations Studio (preview) ist eine plattformübergreifende-Tool zum Verwalten von SQL Server. Weitere Informationen finden Sie unter [Microsoft SQL Operations Studio (preview)](../sql-operations-studio/what-is.md).

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio unter Windows

SQL Server Management Studio (SSMS) ist eine Windows-Anwendung, die eine grafische Benutzeroberfläche bereitstellt, für die Verwaltung von SQL Server. Obwohl es zurzeit nur unter Windows ausgeführt wird, können es Sie Ihre Linux SQL Server-Instanzen herstellen. Weitere Informationen zur Verwendung von SSMS zum Verwalten von SQL Server finden Sie unter [Verwenden von SSMS zum Verwalten von SQL Server on Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>MSSQL-Cli (Vorschau)

Microsoft hat ein neues Skripts plattformübergreifende-Tool für SQL Server veröffentlicht [Mssql-Cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Dieses Tool ist derzeit als Vorschau verfügbar.

## <a name="powershell"></a>PowerShell

PowerShell bietet eine umfangreiche befehlszeilenumgebung zum Verwalten von SQL Server on Linux. Weitere Informationen finden Sie unter [Verwenden von PowerShell zum Verwalten von SQL Server on Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu SQL Server unter Linux finden Sie unter [SQL Server on Linux](sql-server-linux-overview.md).
