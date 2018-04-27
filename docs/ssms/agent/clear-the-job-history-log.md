---
title: Löschen des Auftragsverlaufsprotokolls | Microsoft-Dokumentation
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
- jobs [SQL Server Agent], history
- clearing job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 34b9398a-c409-4040-8ea1-0deceb18f961
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d260975cf8801bed8a7d7cda26033c30ea384a34
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="clear-the-job-history-log"></a>Clear the Job History Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie der Inhalt des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftragsverlaufprotokolls in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)], oder SQL Server Management Objects gelöscht werden kann.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So löschen Sie das Auftragsverlaufsprotokoll mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-clear-the-job-history-log"></a>So löschen Sie das Auftragsverlaufsprotokoll  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**, und klicken Sie auf **Aufträge**.  
  
3.  Klicken Sie mit der rechten Maustaste auf einen Auftrag, und klicken Sie dann auf **Verlauf anzeigen**.  
  
4.  Wählen Sie im **Protokolldatei-Viewer**den Auftrag aus, dessen Verlauf gelöscht werden soll, und führen Sie dann einen der folgenden Schritte aus:  
  
    -   Klicken Sie auf **Löschen**, und klicken Sie dann im Dialogfeld **Verlauf löschen** auf **Gesamten Verlauf löschen** . Sie können wahlweise den gesamten Auftragsverlauf löschen oder auch nur den Verlauf, der vor einem bestimmten Datum angefallen ist. Soll der gesamte Auftragsverlauf gelöscht werden, klicken Sie auf **Gesamten Verlauf löschen**. Um nur ältere Einträge im Auftragsverlauf zu löschen, klicken Sie auf **Verlauf löschen vor**, und geben Sie das gewünschte Datum an.  
  
    -   Klicken Sie auf **Auftragsstatus** , wenn Sie das Verlaufsprotokoll eines Multiserverauftrags löschen möchten. Klicken Sie auf **Auftrag**und auf einen Auftragsnamen, und klicken Sie dann auf **Remoteauftragsverlauf anzeigen**.  
  
5.  Klicken Sie auf **Löschen**.  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-clear-the-job-history-log"></a>So löschen Sie das Auftragsverlaufsprotokoll  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- example removes the history for a job named NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_purge_jobhistory  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
## <a name="SMO"></a>Verwendung von SQL Server Management Objects  
**So löschen Sie das Auftragsverlaufsprotokoll**  
  
Verwenden Sie die **PurgeJobHistory** -Methode der **JobServer** -Klasse in einer Programmiersprache Ihrer Wahl, z. B. Visual Basic, Visual C# oder PowerShell. Weitere Informationen finden Sie unter [SQL Server Management Objects (SMO)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
