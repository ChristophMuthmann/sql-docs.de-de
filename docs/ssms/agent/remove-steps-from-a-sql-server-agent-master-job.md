---
title: Entfernen von Schritten aus einem Masterauftrag für den SQL Server-Agent |Microsoft-Dokumente
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 871e6162-1221-464d-8f7f-7e454dcd9edb
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fe0690955bcc1b8312672cdd965a1d2631389445
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="remove-steps-from-a-sql-server-agent-master-job"></a>Remove Steps from a SQL Server Agent Master Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie Schritte aus einem Masterauftrag für den SQL Server-Agent in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]entfernen.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **Entfernen von Schritten aus einem Masterauftrag für den SQL Server-Agent mit:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
Ein Masterauftrag für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent kann nicht gleichzeitig lokale Server und Remoteserver als Ziel haben.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Sie können nur Aufträge ändern, die in Ihrem Besitz sind, es sei denn, Sie sind ein Mitglied der festen Serverrolle **sysadmin** . Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-remove-steps-from-a-sql-server-agent-master-job"></a>So entfernen Sie Schritte aus einem Masterauftrag für den SQL Server-Agent  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, der den Auftrag mit den zu löschenden Schritten enthält.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um den Ordner **Aufträge** zu erweitern.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Auftrag, dessen Schritte Sie löschen möchten, und wählen Sie **Eigenschaften**aus.  
  
5.  Klicken Sie im Dialogfeld **Auftragseigenschaften >***Auftragsname* unter **Seite auswählen** auf die Option **Schritte**.  
  
6.  Wählen Sie unter **Auftragsschrittliste**den zu löschenden Auftragsschritt aus, und klicken Sie auf **Löschen**.  
  
7.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-remove-steps-from-a-sql-server-agent-master-job"></a>So entfernen Sie Schritte aus einem Masterauftrag für den SQL Server-Agent  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- removes job step 1 from the job Weekly Sales Data Backup   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1 ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_delete_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/421ede8e-ad57-474a-9fb9-92f70a3e77e3).  
  
