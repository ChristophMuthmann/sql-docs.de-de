---
title: Verzögerte Transaktionen (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- I/O [SQL Server], database recovery
- restoring pages [SQL Server]
- deferred transactions
- modifying transaction deferred state
ms.assetid: 6fc0f9b6-d3ea-4971-9f27-d0195d1ff718
caps.latest.revision: 45
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ebdce0b5f382f30437ee0fa78cb9d9bdba4ed2c4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="deferred-transactions-sql-server"></a>Markierte Transaktionen [SQL Server]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise kann eine beschädigte Transaktion verzögert werden, wenn für das Rollback (Rückgängig machen) erforderliche Daten während des Starts der Datenbank offline sind. Bei einer *verzögerten Transaktion* handelt es sich um eine Transaktion, für die kein Commit ausgeführt wird, wenn die Rollforwardphase beendet wird, und bei der ein Fehler auftritt, sodass für die Transaktion kein Rollback ausgeführt werden kann. Da kein Rollback ausgeführt werden kann, wird die Transaktion verzögert.  
  
> [!NOTE]  
>  Beschädigte Transaktionen werden nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise verzögert. In anderen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kann eine beschädigte Transaktion nicht gestartet werden.  
  
 Eine verzögerte Transaktion tritt normalerweise dann auf, wenn für eine Datenbank ein Rollforward ausgeführt wird und durch einen E/A-Fehler verhindert wird, dass eine Seite, die für die Transaktion erforderlich ist, gelesen werden kann. Doch auch ein Fehler auf Dateiebene kann verzögerte Transaktionen zur Folge haben. Eine verzögerte Transaktion kann auch auftreten, wenn eine Teilwiederherstellungssequenz an einem Punkt angehalten wird, an dem ein Transaktionsrollback erforderlich ist und für eine Transaktion Daten erforderlich sind, die offline sind.  
  
 Bei Benutzertransaktionen, bei denen während des Rollbacks ein E/A-Fehler auftritt, wird die gesamte Datenbank in den Offlinezustand versetzt. Wird die Datenbank zurück in den Onlinezustand versetzt, werden beim Wiederherstellungsvorgang alle vorherigen Sperren wiederhergestellt, und es wird versucht, für alle Transaktionen, für die kein Commit ausgeführt wurde, ein Rollback auszuführen. Alle durch eine Transaktion geänderten Daten bleiben entsprechend gesperrt, bis für die Transaktion ein Rollback ausgeführt werden kann. Für Transaktionen, für die kein Rollback ausgeführt werden kann, werden die Sperren freigegeben, sobald der Fehler behoben und die Datenbank neu gestartet wurde, oder nachdem eine Onlinewiederherstellung erfolgt, wenn die verzögerten Transaktionen gelöst werden, während die Datenbank online bleibt. Bis zu diesem Zeitpunkt können die Sperren von einer verzögerten Transaktion aufrecht erhalten werden, wodurch bestimmte Vorgänge in der gesamten Datenbank verhindert werden. Wenn eine verzögerte Transaktion beispielsweise eine CREATE TABLE-Anweisung enthält, können Benutzer Tabellen erst nach dem Auflösen der verzögerten Transaktion erstellen.  
  
 Eine verzögerte Transaktion kann auch auftreten, weil eine Datenbank mit einer schrittweisen Wiederherstellung bis zu einem Zeitpunkt wiederhergestellt wird, an dem sich eine oder mehrere aktive Transaktionen auf eine Dateigruppe auswirken, die bislang nicht wiederhergestellt wurde und offline ist. Da kein Rollback ausgeführt werden kann, werden die Transaktionen verzögert.  
  
 In der folgenden Tabelle sind die Aktionen aufgeführt, die einen Wiederherstellungsvorgang der Datenbank verursachen. Die Tabelle veranschaulicht außerdem das Ergebnis von E/A-Fehlern.  
  
|Aktion|Lösung (bei E/A-Fehlern oder wenn erforderliche Daten offline sind)|  
|------------|-----------------------------------------------------------------------|  
|Serverstart|verzögerten Transaktion|  
|Wiederherstellung|Verzögerte Transaktion|  
|Anfügen|Anfügen erzeugt einen Fehler|  
|AutoNeustart|verzögerten Transaktion|  
|Erstellen einer Datenbank oder einer Datenbankmomentaufnahme|Erstellen erzeugt einen Fehler|  
|Wiederholen bei Datenbankspiegelung|verzögerten Transaktion|  
|Dateigruppe ist offline|verzögerten Transaktion|  
  
## <a name="moving-a-transaction-out-of-the-deferred-state"></a>Beenden des VERZÖGERTEN Zustands einer Transaktion  
  
> [!IMPORTANT]  
>  Das Transaktionsprotokoll bleibt bei verzögerten Transaktionen aktiv. Eine virtuelle Protokolldatei, in der verzögerte Transaktionen enthalten sind, kann erst abgeschnitten werden, wenn sich diese Transaktionen nicht mehr im Verzögerungsmodus befinden. Weitere Informationen zu Protokollkürzung finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Damit der verzögerte Zustand der Transaktion beendet wird, muss die Datenbank ordnungsgemäß und ohne E/A-Fehler gestartet werden. Falls verzögerte Transaktionen vorhanden sind, müssen Sie die Ursache der E/A-Fehler beheben. Die verfügbaren Lösungen werden nachfolgend in der Reihenfolge aufgelistet, in der sie normalerweise versucht werden:  
  
-   Starten Sie die Datenbank neu. Wenn es sich um ein vorübergehendes Problem gehandelt hat, sollte die Datenbank ohne verzögerte Transaktionen gestartet werden.  
  
-   Wenn die Transaktionen verzögert wurden, weil eine Dateigruppe offline war, schalten Sie die Dateigruppe wieder online.  
  
     Mithilfe der folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung können Sie eine Offlinedateigruppe wieder in den Onlinezustand versetzen:  
  
    ```  
    RESTORE DATABASE database_name FILEGROUP=<filegroup_name>  
    ```  
  
-   Stellen Sie die Datenbank wieder her. Nach einer Onlinewiederherstellung werden alle verzögerten Transaktionen aufgelöst.  
  
     Wurden die verzögerten Transaktionen im Rahmen des Modells der vollständigen oder massenprotokollierten Wiederherstellung von einigen wenigen beschädigten Seiten verursacht, können die Fehler möglicherweise durch eine Onlinewiederherstellung der entsprechenden Seiten behoben werden (sofern diese unterstützt wird).  
  
-   Wenn keine Dateigruppe mehr erforderlich ist, deren Offlinestatus zu verzögerten Transaktionen führt, setzen Sie die offline geschaltete Dateigruppe außer Kraft. Transaktionen, die sich verzögert haben, weil eine Dateigruppe offline ist, befinden sich, nachdem eine Dateigruppe außer Kraft gesetzt wird, nicht mehr im Verzögerungsmodus.  
  
    > [!IMPORTANT]  
    >  Eine außer Kraft gesetzte Dateigruppe kann nicht wiederhergestellt werden.  
  
     Weitere Informationen finden Sie unter [Entfernen von veralteten Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md).  
  
-   Wenn Transaktionen aufgrund einer beschädigten Seite verzögert wurden und keine gute Sicherung der Datenbank vorhanden ist, müssen Sie zum Reparieren der Datenbank wie folgt vorgehen:  
  
    -   Versetzen Sie die Datenbank zunächst in den Notfallmodus. Führen Sie dazu die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung aus:  
  
        ```  
        ALTER DATABASE <database_name> SET EMERGENCY  
        ```  
  
         Informationen zum Notfallmodus finden Sie unter [Database States](../../relational-databases/databases/database-states.md).  
  
    -   Reparieren Sie anschließend die Datenbank, indem Sie die Option DBCC REPAIR_ALLOW_DATA_LOSS in einer der folgenden DBCC-Anweisungen verwenden: [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md), [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)oder [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).  
  
         Sobald DBCC auf die beschädigte Seite stößt, wird ihre Zuordnung aufgehoben, und es werden alle damit verbundenen Fehler repariert. Durch diesen Ansatz kann die Datenbank in einem physisch konsistenten Status wieder online geschaltet werden. Allerdings können dabei weitere Daten verloren gehen. Aus diesem Grund sollte dieser Ansatz nur als letzte Möglichkeit verwendet werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Entfernen von veralteten Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)   
 [Dateiwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Dateiwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
