---
title: Schreiben des Auftragsstatus in das Windows-Anwendungsprotokoll | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- status information [SQL Server], jobs
- SQL Server Agent jobs, status
- writing job status to log
- jobs [SQL Server Agent], status
- logs [SQL Server], jobs
ms.assetid: 3b813702-8f61-40ec-bf3b-ce9deb7e68be
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 52c18177b568b73ec0508ab13c3b4f589d618c33
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="write-the-job-status-to-the-windows-application-log"></a>Write the Job Status to the Windows Application Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie den [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] konfigurieren müssen, damit der Auftragsstatus mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)], oder SQL Server Management Objects in das Windows Anwendungsereignisprotokoll geschrieben wird.  
  
Sie stellen sicher, dass Datenbankadministratoren wissen, wann Aufträge fertig gestellt sind und wie oft diese ausgeführt werden. Zu den typischen Auftragsantworten gehören folgende:  
  
-   Benachrichtigen des Operators per E-Mail, Pager oder **NET SEND** -Nachricht. Verwenden Sie eine dieser Auftragsantworten vor allem dann, wenn der Operator weitere Schritte ausführen muss. Wenn beispielsweise ein Sicherungsauftrag erfolgreich ausgeführt wurde, muss der Operator darüber informiert werden, um das Sicherungsband entfernen zu können und an einem sicheren Standort aufbewahren zu lassen.  
  
-   Schreiben einer Ereignismeldung in das Windows-Anwendungsprotokoll. Diese Art der Antwort können Sie nur bei fehlgeschlagenen Aufträgen verwenden.  
  
-   Automatisches Löschen des Auftrags. Verwenden Sie diese Auftragsantwort, wenn Sie sicher sind, dass Sie diesen Auftrag nicht erneut ausführen müssen.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So schreiben Sie den Auftragsstatus in das Windows-Anwendungsprotokoll, und zwar mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-write-job-status-to-the-windows-application-log"></a>So schreiben Sie den Auftragsstatus in das Windows-Anwendungsprotokoll  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**, erweitern Sie **Aufträge**, klicken Sie mit der rechten Maustaste auf den Auftrag, den Sie bearbeiten möchten, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Wählen Sie die Seite **Benachrichtigungen** aus.  
  
4.  Aktivieren Sie **In Windows-Anwendungsereignisprotokoll schreiben**, und wählen Sie eine der folgenden Optionen aus:  
  
    -   Klicken Sie auf**Bei erfolgreicher Auftragsausführung**, um den Auftragsstatus zu protokollieren, wenn der Auftrag erfolgreich abgeschlossen wurde.  
  
    -   Klicken Sie auf**Bei Auftragsfehler**, um den Auftragsstatus zu protokollieren, wenn der Auftrag nicht erfolgreich abgeschlossen wurde.  
  
    -   Klicken Sie auf**Beim Abschluss des Auftrags** , um den Auftragsstatus unabhängig vom Abschlussstatus zu protokollieren.  
  
## <a name="SMO"></a>Verwendung von SQL Server Management Objects  
**So schreiben Sie den Auftragsstatus in das Windows-Anwendungsprotokoll**  
  
Rufen Sie die **EventLogLevel** -Eigenschaft der **Job** -Klasse in einer Programmiersprache Ihrer Wahl auf, z. B. Visual Basic, Visual C# oder PowerShell.  
  
Im folgenden Codebeispiel wird der Auftrag so festgelegt, dass bei Abschluss der Auftragsausführung ein Betriebssystem-Ereignisprotokolleintrag generiert wird.  
  
**PowerShell**  
  
```  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = new-object Microsoft.SqlServer.Management.Smo.Agent.Job($srv.JobServer, "Test Job")  
$jb.EventLogLevel = [Microsoft.SqlServer.Management.Smo.Agent.CompletionAction]::Always  
```  
  
