---
title: Überwachung und Problembehandlung bei der Datenmigration (Stretch Database) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: stretch-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: fe99413e2181ac50f2f64b8d895335ea37779eef
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>Überwachung und Problembehandlung bei der Datenmigration (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Wählen Sie zum Überwachen der Datenmigration in der Stretch Database-Überwachung **Aufgaben | Stretch | Überwachen** für eine Datenbank in SQL Server Management Studio aus.  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>Überprüfen des Status der Datenmigration in der Stretch Database-Überwachung  
 Wählen Sie **Aufgaben | Stretch | Überwachen** für eine Datenbank in SQL Server Management Studio aus, um die Stretch Database-Überwachung zu öffnen und die Datenmigration zu überwachen.  
  
-   Im oberen Bereich der Überwachung werden allgemeine Informationen über die SQL Server-Datenbank mit aktivierter Funktion Stretch-Datenbank und die Azure-Remotedatenbank angezeigt.  
  
-   Im unteren Bereich der Überwachung wird der Status der Datenmigration für jede Tabelle mit aktivierter Funktion Stretch-Datenbank in der Datenbank angezeigt.  
  
 ![Stretch Database-Überwachung](../../sql-server/stretch-database/media/stretch-monitor.PNG "Stretch Database-Überwachung")  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwalten und Problembehandlung von Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  
