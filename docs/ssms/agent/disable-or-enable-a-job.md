---
title: Deaktivieren oder Aktivieren eines Auftrags | Microsoft-Dokumentation
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
- stopping jobs
- disabling jobs
- SQL Server Agent jobs, disabling
- jobs [SQL Server Agent], disabling
ms.assetid: 5041261f-0c32-4d4a-8bee-59a6c16200dd
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 63ab17f3ac8fb0de122b8553d2f5ce536ef3701c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="disable-or-enable-a-job"></a>Deaktivieren oder Aktivieren eines Auftrags
In diesem Thema wird beschrieben, wie Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftrag in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]deaktivieren können. Beim Deaktivieren eines Auftrags wird dieser nicht gelöscht, und kann gegebenenfalls wieder aktiviert werden.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So aktivieren oder deaktivieren Sie einen Auftrag mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-disable-or-enable-a-job"></a>So aktivieren oder deaktivieren Sie einen Auftrag  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **SQL Server-Agent**.  
  
3.  Erweitern Sie **Aufträge**, und klicken Sie dann mit der rechten Maustaste auf den Auftrag, den Sie deaktivieren bzw. aktivieren möchten.  
  
4.  Klicken Sie auf **Deaktivieren**, um einen Auftrag zu deaktivieren. Klicken Sie auf **Aktivieren**, um einen Auftrag zu aktivieren.  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
  
#### <a name="to-disable-or-enable-a-job"></a>So aktivieren oder deaktivieren Sie einen Auftrag  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- changes the name, description, and disables status of the job NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @new_name = N'NightlyBackups -- Disabled',  
        @description = N'Nightly backups disabled during server migration.',  
        @enabled = 0 ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_update_job (Transact-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623).  
  

