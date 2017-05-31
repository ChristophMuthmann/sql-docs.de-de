---
title: "Löschen ein Auftragsschrittprotokolls | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server Agent]
- deleting job step logs
- logs [SQL Server], jobs
- removing job step logs
ms.assetid: ee20c6cd-0258-4550-bdb0-71e86a0fb330
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e3ddfb6b7c76014732bb12c2d33f337af683dade
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="delete-a-job-step-log"></a>Löschen eines Auftragsschrittprotokolls
In diesem Thema wird beschrieben, wie Sie ein Auftragsschrittprotokoll des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents löschen.  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So löschen Sie ein Auftragsschrittprotokoll des SQL Server-Agents mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
Wenn Auftragsschritte gelöscht werden, werden auch die entsprechenden Ausgabeprotokolle gelöscht.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Sie können nur Aufträge ändern, die in Ihrem Besitz sind, es sei denn, Sie sind ein Mitglied der festen Serverrolle **sysadmin** .  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>So löschen Sie ein Auftragsschrittprotokoll des SQL Server-Agents  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**, erweitern Sie **Aufträge**, klicken Sie mit der rechten Maustaste auf den Auftrag, den Sie ändern möchten, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Löschen Sie im Dialogfeld **Auftragseigenschaften** den ausgewählten Auftragsschritt.  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>So löschen Sie ein Auftragsschrittprotokoll des SQL Server-Agents  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- removes the job step log for step 2 in the job Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobsteplog  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 2;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_delete_jobsteplog (Transact-SQL)](http://msdn.microsoft.com/en-us/e9ef4c99-abde-4038-b6a3-a25dcbaf0958).  
  
## <a name="SMO"></a>Verwendung von SQL Server Management Objects  
Verwenden Sie die **DeleteJobStepLogs** -Methode der **Job** -Klasse in einer Programmiersprache Ihrer Wahl, z. B. Visual Basic, Visual C# oder PowerShell. Weitere Informationen finden Sie unter[SQL Server Management Objects (SMO)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
```  
-- Uses PowerShell to delete all job step log files that have ID values larger than 5.  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = $srv.JobServer.Jobs["Test Job"]  
$jb.DeleteJobStepLogs(5)  
```  
  

