---
title: Verwalten von Aufträgen über ein gesamtes Unternehmen | Microsoft-Dokumentation
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
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 242e93d1524891c31f9cab152401ea04f221909a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="manage-jobs-across-an-enterprise"></a>Verwalten von Aufträgen über ein gesamtes Unternehmen
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Wenn Sie Änderungen an den Definitionen von Multiserveraufträgen außerhalb von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] vornehmen, müssen Sie die Änderungen der Downloadliste bereitstellen, damit die Zielserver erneut einen Download des aktualisierten Auftrags durchführen können. Um sicherzustellen, dass die Zielserver über aktuelle Auftragsdefinitionen verfügen, führen Sie nach dem Aktualisieren des Multiserverauftrags eine INSERT-Anweisung aus:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Um Zielserver darüber zu benachrichtigen, dass ein Multiserverauftrag geändert wurde, müssen Sie den vorherigen Befehl aufrufen, nachdem Sie eine der folgenden Prozeduren verwendet haben:  
  
-   [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_update_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/e158802c-c347-4a5d-bf75-c03e5ae56e6b)  
  
-   [sp_delete_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/421ede8e-ad57-474a-9fb9-92f70a3e77e3)  
  
-   [Verwalten von Ereignissen](http://msdn.microsoft.com/en-us/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)  
  
-   [sp_detach_schedule (Transact-SQL)](http://msdn.microsoft.com/en-us/9a1fc335-1bef-4638-a33a-771c54a5dd19)  
  
    > [!NOTE]  
    > Es ist nicht notwendig, **sp_post_msx_operation** aufzurufen, nachdem Sie **sp_update_job** oder **sp_delete_job**aufgerufen haben, da diese gespeicherten Prozeduren automatisch die notwendigen Änderungen der Downloadliste bereitstellen.  
  
Mithilfe der folgenden Tasks werden häufig Aufträge über ein gesamtes Unternehmen hinweg verwaltet:  
  
**So überprüfen Sie den Status eines Zielservers**  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/f841d3bd-901a-4980-ad0b-1c6eeba3f717)  
  
-   [SQL Server Management Objects (SMO)](http://msdn.microsoft.com/en-us/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**So wechseln Sie die Zielserver für einen Auftrag**  
  
-   [SQL Server Management Studio](../../ssms/agent/modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
-   [SQL Server Management Objects (SMO)](http://msdn.microsoft.com/en-us/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**So ändern Sie den Speicherort eines Zielservers**  
  
-   [SQL Server Management Studio](../../ssms/agent/specify-a-target-server-s-location-sql-server-management-studio.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
-   [SQL Server Management Objects (SMO)](http://msdn.microsoft.com/en-us/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**So synchronisieren Sie die Uhren der Zielserver**  
  
-   [SQL Server Management Studio](../../ssms/agent/synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/40e44df7-d3e3-44ee-b149-08aba629a21f)  
  
**So erzwingen Sie, dass ein Zielserver den Masterserver abruft**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](http://msdn.microsoft.com/en-us/085deef8-2709-4da9-bb97-9ab32effdacf)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwalten von Ereignissen](../../ssms/agent/manage-events.md)  
  
