---
title: "Überwachung und Problembehandlung bei der Datenmigration (Stretch-Datenbank) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/14/2016
ms.prod: stretch-database
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, monitoring
- monitoring Stretch Database
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 91c10b51a3fec9ccc96c3aa23100abdf2a60ba81
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>Überwachung und Problembehandlung bei der Datenmigration (Stretch-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Wählen Sie zum Überwachen der Datenmigration in der Stretch-Datenbanküberwachung **Aufgaben | Stretch | Überwachen** für eine Datenbank in SQL Server Management Studio aus.  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>Überprüfen des Status der Datenmigration in der Stretch-Datenbanküberwachung  
 Wählen Sie **Aufgaben | Stretch | Überwachen** für eine Datenbank in SQL Server Management Studio aus, um die Stretch-Datenbanküberwachung zu öffnen und die Datenmigration zu überwachen.  
  
-   Im oberen Bereich der Überwachung werden allgemeine Informationen über die SQL Server-Datenbank mit aktivierter Funktion Stretch-Datenbank und die Azure-Remotedatenbank angezeigt.  
  
-   Im unteren Bereich der Überwachung wird der Status der Datenmigration für jede Tabelle mit aktivierter Funktion Stretch-Datenbank in der Datenbank angezeigt.  
  
 ![Überwachung der Stretch-Datenbank](../../sql-server/stretch-database/media/stretch-monitor.PNG "Überwachung der Stretch-Datenbank")  
  
##  <a name="Migration"></a> Überprüfen des Status der Datenmigration in einer dynamischen Verwaltungsansicht  
 Öffnen Sie die dynamische Verwaltungssicht **sys.dm_db_rda_migration_status** , um anzuzeigen, wie viele Batches und Datenzeilen migriert wurden. Weitere Informationen finden Sie unter [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
##  <a name="Firewall"></a> Problembehandlung der Datenmigration  
 **Zeilen aus meiner Tabelle mit aktivierter Funktion Stretch werden nicht zu Azure migriert. Wo liegt das Problem?**  
 Es gibt mehrere Probleme, die die Migration beeinflussen können. Überprüfen Sie folgende Aspekte.  
  
-   Überprüfen Sie die Netzwerkkonnektivität für den SQL Server-Computer.  
  
-   Stellen Sie sicher, dass die Azure-Firewall Ihren SQL-Server nicht daran hindert, sich mit dem Remoteendpunkt zu verbinden.  
  
-   Überprüfen Sie die dynamische Verwaltungssicht **sys.dm_db_rda_migration_status** für den Status des aktuellen Batches. Wenn ein Fehler aufgetreten ist, überprüfen Sie die Werte „error_number“, „error_state“ und „error_severity“ für den Batch.  
  
    -   Weitere Informationen zu dieser Sicht finden Sie unter [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
    -   Weitere Informationen zum Inhalt einer SQL Server-Fehlermeldung finden Sie unter [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md).  
  
 **Die Azure-Firewall blockiert Verbindungen von meinem lokalen Server.**  
 Möglicherweise müssen Sie eine Regel zu den Azure-Firewalleinstellungen des Azure-Servers hinzufügen, damit SQL Server mit dem Azure-Remoteserver kommunizieren kann.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten und Problembehandlung von Stretch-Datenbank](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  

