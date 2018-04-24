---
title: Entfernen der Datenbankspiegelung (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], removing
- stopping database mirroring [SQL Server]
- removing database mirroring [SQL Server]
ms.assetid: 40c72091-8f03-4037-8b55-5e95309fe145
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f0f3e6d7f9d2c635daa81c90e468f560da98b92
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="removing-database-mirroring-sql-server"></a>Entfernen der Datenbankspiegelung (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Datenbankbesitzer kann eine Datenbankspiegelungssitzung jederzeit bei jedem Partner manuell beenden.  
  
## <a name="impact-of-removing-mirroring"></a>Auswirkungen aus dem Entfernen der Spiegelung  
 Durch das Entfernen der Spiegelung tritt folgende Situation ein:  
  
-   Die Beziehung zwischen den Partnern sowie zwischen den einzelnen Partnern und dem Zeugen werden, sofern vorhanden, dauerhaft abgebrochen.  
  
     Falls die Partner miteinander kommunizierten, als die Sitzung beendet wurde, wird die Beziehung unmittelbar auf beiden Computern abgebrochen. Wenn die Partner nicht miteinander kommunizierten (die Datenbank besaß zum Beendigungszeitpunkt den Status DISCONNECTED), wird die Beziehung unmittelbar bei dem Partner abgebrochen, von dem aus die Spiegelung beendet wurde. Sobald der andere Partner versucht, die Verbindung wiederherzustellen, wird für diesen Partner ersichtlich, dass die Datenbankspiegelungssitzung beendet wurde.  
  
-   Die Informationen zur Spiegelungssitzung werden gelöscht, im Gegensatz zum Anhalten einer Sitzung. Die Spiegelung wird sowohl aus der Prinzipaldatenbank als auch aus der Spiegelungsdatenbank entfernt. In **sys.databases** werden die**mirroring_state**-Spalte und alle anderen Spiegelungsspalten auf NULL festgelegt. Weitere Informationen finden Sie unter [sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md).  
  
-   Jede Partnerserverinstanz behält eine separate Kopie der Datenbank.  
  
-   Die Spiegeldatenbank verbleibt im Status RESTORING (siehe Spalte für den **Status** in **sys.databases**), weil die Spiegeldatenbank mit RESTORE WITH NORECOVERY erstellt wurde. Zu diesem Zeitpunkt können Sie die bisherige Spiegelungsdatenbank löschen oder auch mit WITH RECOVERY wiederherstellen. Wenn Sie die Datenbank wiederherstellen, weicht sie von der früheren Prinzipaldatenbank ab, weil mit der Wiederherstellung eine neue Wiederherstellungsverzweigung gestartet wird.  
  
> [!NOTE]  
>  Um die Spiegelung nach dem Anhalten einer Sitzung fortzusetzen, müssen Sie eine neue Datenbankspiegelungssitzung einrichten. Wenn Sie nach dem Beenden der Spiegelung eine Protokollsicherung erstellt haben, müssen Sie diese Sicherung auf die Spiegelungsdatenbank anwenden, bevor Sie die Spiegelung erneut starten.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So entfernen Sie die Datenbankspiegelung**  
  
-   [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
 **So starten Sie die Datenbankspiegelung**  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE-Datenbankspiegelung &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Anhalten und Fortsetzen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  
