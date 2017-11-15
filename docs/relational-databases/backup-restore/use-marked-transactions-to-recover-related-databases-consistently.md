---
title: Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction marks [SQL Server]
- marked transactions [SQL Server]
- database restores [SQL Server], inserting transaction marks for
- recovery [SQL Server], related databases
- restoring databases [SQL Server], related database recovery
- database restores [SQL Server], related databases
- marked transactions [SQL Server], creating
- BEGIN TRAN...WITH MARK statement
- two-phase commit
ms.assetid: 50a73574-1a69-448e-83dd-9abcc7cb7e1a
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b8b5fd59afda45375e8258dd56a34e34138a696
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="use-marked-transactions-to-recover-related-databases-consistently"></a>Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Dieses Thema ist nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken relevant, die das vollständige oder das massenprotokollierte Wiederherstellungsmodell verwenden.  
  
 Wenn Sie Updates für zwei oder mehr Datenbanken, ( *zugehörige Datenbanken*), ausführen, können Sie diese mithilfe von Transaktionsmarkierungen bis zu einem logisch konsistenten Punkt wiederherstellen. Bei dieser Wiederherstellung gehen jedoch alle Transaktionen verloren, für die nach der Markierung, die als Wiederherstellungspunkt verwendet wird, ein Commit ausgeführt wird. Das Markieren von Transaktionen empfiehlt sich nur, wenn Sie verbundene Datenbanken prüfen oder wenn Sie in Kauf nehmen, dass Transaktionen, für die kürzlich ein Commit ausgeführt wurde, verloren gehen.  
  
 Durch das routinemäßige Markieren zugehöriger Transaktionen in allen verbundenen Datenbanken werden eine Reihe allgemeiner Wiederherstellungspunkte in den Datenbanken erstellt. Die Transaktionsmarkierungen werden im Transaktionsprotokoll aufgezeichnet und in Protokollsicherungen eingebunden. Wenn ein Notfall eintreten sollte, können Sie die einzelnen Datenbanken bis zu dieser Transaktionsmarkierung und damit bis zu einem konsistenten Zeitpunkt wiederherstellen.  
  
> [!NOTE]  
>  Protokollsicherungen für die verschiedenen Datenbanken können unabhängig voneinander erstellt werden. Sie müssen auch nicht gleichzeitig ausgeführt werden.  
  
 Für das Wiederherstellen zugehöriger Datenbanken in den folgenden Szenarien ist es erforderlich, dass in allen verbundenen Datenbanken bereits markierte Transaktionen verfügbar sind:  
  
-   Mindestens ein Transaktionsprotokoll ist beschädigt. Stellen Sie für den Datenbanksatz einen konsistenten Status zum Zeitpunkt der letzten Protokollsicherung wieder her.  
  
-   Sie müssen für den gesamten Datenbanksatz einen gegenseitig konsistenten Status zu einem früheren Zeitpunkt wiederherstellen.  
  
> [!IMPORTANT]  
>  Sie können verbundene Datenbanken nur bis zu einer markierten Transaktion wiederherstellen, nicht bis zu einem bestimmten Zeitpunkt.  
  
 Weitere Informationen zum Erstellen markierter Transaktionen finden Sie unter "Erstellen der markierten Transaktionen" weiter unten in diesem Thema.  
  
## <a name="typical-scenario-for-using-marked-transactions"></a>Typisches Szenario zum Verwenden markierter Transaktionen  
 Ein typisches Szenario zum Verwenden markierter Transaktionen umfasst die folgenden Schritte:  
  
1.  Erstellen Sie eine vollständige oder differenzielle Datenbanksicherung für die einzelnen verbundenen Datenbanken.  
  
2.  Markieren Sie in allen Datenbanken einen Transaktionsblock.  
  
3.  Sichern Sie das Transaktionsprotokoll für alle Datenbanken.  
  
4.  Stellen Sie mithilfe von WITH NORECOVERY Datenbanksicherungen wieder her.  
  
5.  Stellen Sie mithilfe von WITH STOPATMARK Protokolle wieder her.  
  
## <a name="considerations-for-using-marked-transactions"></a>Überlegungen zum Verwenden markierter Transaktionen  
 Beachten Sie Folgendes, bevor Sie benannte Markierungen in das Transaktionsprotokoll einfügen:  
  
-   Transaktionsmarkierungen belegen Protokollspeicherplatz und sollten deshalb nur für Transaktionen verwendet werden, die eine wichtige Rolle bei der Wiederherstellungsstrategie für die Datenbank spielen.  
  
-   Nachdem für eine markierte Transaktion ein Commit ausgeführt wurde, wird in die [logmarkhistory](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) -Tabelle in **msdb**eine Zeile eingefügt.  
  
-   Wenn sich eine markierte Transaktion über mehrere Datenbanken auf demselben Datenbankserver oder auf verschiedenen Servern erstreckt, müssen die Markierungen in den Protokollen aller betroffenen Datenbanken aufgezeichnet werden.  
  
## <a name="creating-the-marked-transactions"></a>Erstellen der markierten Transaktionen  
 Verwenden Sie die [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) -Anweisung und die WITH MARK [*description*]-Klausel, um markierte Transaktionen zu erstellen. Der optionale *description* -Parameter ist eine Textbeschreibung der Markierung. Ein Markierungsname für die Transaktion ist erforderlich. Ein Markierungsname kann erneut verwendet werden. Im Transaktionsprotokoll werden der Markierungsname, die Beschreibung, die Datenbank, der Benutzer, datetime-Informationen und die Protokollfolgenummer (LSN, Log Sequence Number) aufgezeichnet. Die datetime-Informationen werden zusammen mit dem Markierungsnamen für die eindeutige Identifizierung der Markierung verwendet.  
  
 **So erstellen Sie markierte Transaktionen in einem Datenbanksatz:**  
  
1.  Benennen Sie die Transaktion in der BEGIN TRAN-Anweisung, und verwenden Sie die WITH MARK-Klausel  
  
     Die BEGIN TRAN *Neuer Markierungsname* WITH MARK-Anweisung kann innerhalb einer vorhandenen Transaktion geschachtelt werden. Der Wert von *Neuer Markierungsname* stellt den Markierungsnamen für die Transaktion dar, selbst wenn die Transaktion einen Transaktionsnamen umfasst.  
  
    > [!NOTE]  
    >  Wenn Sie eine zweite geschachtelte BEGIN TRAN...WITH MARK-Anweisung ausgeben, wird diese ausgelassen, führt allerdings zu einer Warnmeldung.  
  
2.  Führen Sie ein Update für alle Datenbanken im Datenbanksatz aus.  
  
     Die Markierung für eine bestimmte Transaktion wird nur in Transaktionsprotokollen auf der Serverinstanz eingefügt, auf der die BEGIN TRAN...WITH MARK-Anweisung ausgeführt wird. Die Transaktionsmarkierung wird in das Transaktionsprotokoll der Datenbanken platziert, die von der markierten Transaktion auf dieser Serverinstanz aktualisiert wurden. Wenn sich die Datenbanken auf verschiedenen Serverinstanzen befinden, müssen auf den einzelnen Serverinstanzen identische Markierungen erstellt werden.  
  
### <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das Transaktionsprotokoll bis zur Markierung in der markierten Transaktion mit dem Namen `ListPriceUpdate`wiederhergestellt.  
  
```tsql  
USE AdventureWorks  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master  
GO  
  
RESTORE DATABASE AdventureWorks  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'ListPriceUpdate';  
```  
  
## <a name="forcing-a-mark-to-spread-to-other-servers"></a>Erzwingen einer Markierung für andere Server  
 Ein Transaktionsmarkierungsname wird nicht automatisch an einen anderen Server verteilt, wenn die Transaktion dort verteilt wird. Um die Weitergabe der Markierung an die anderen Server zu erzwingen, muss eine gespeicherte Prozedur geschrieben werden, die eine BEGIN TRAN *name* WITH MARK-Anweisung enthält. Diese gespeicherte Prozedur muss dann auf dem Remoteserver unter dem Gültigkeitsbereich der Transaktion auf dem ursprünglichen Server ausgeführt werden.  
  
 Angenommen, eine partitionierte Datenbank ist in mehreren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]vorhanden. In jeder Instanz gibt es eine Datenbank namens `coyote`. Erstellen Sie zuerst in allen Datenbanken eine gespeicherte Prozedur, z. B. `sp_SetMark`.  
  
```tsql  
CREATE PROCEDURE sp_SetMark  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION @name WITH MARK  
UPDATE coyote.dbo.Marks SET one = 1  
COMMIT TRANSACTION;  
GO  
```  
  
 Erstellen Sie anschließend die gespeicherte Prozedur `sp_MarkAll` , in der eine Transaktion enthalten ist, mit der in jeder Datenbank eine Markierung platziert wird. `sp_MarkAll` kann von jeder Instanz aus ausgeführt werden.  
  
```tsql  
CREATE PROCEDURE sp_MarkAll  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION  
EXEC instance0.coyote.dbo.sp_SetMark @name  
EXEC instance1.coyote.dbo.sp_SetMark @name  
EXEC instance2.coyote.dbo.sp_SetMark @name  
COMMIT TRANSACTION;  
GO  
```  
  
### <a name="two-phase-commit"></a>Zweiphasencommit  
 Das Ausführen eines Commits einer verteilten Transaktion verläuft in zwei Phasen: Vorbereitung und Commit. Wenn für eine markierte Transaktion ein Commit ausgeführt wird, wird der Commitprotokolleintrag für jede Datenbank in der markierten Transaktion an einem Punkt des Protokolls platziert, an dem in keinem der Protokolle zweifelhafte Transaktionen vorhanden sind. Damit wird sichergestellt, dass keine Transaktionen auftreten, für die in einem Protokoll das vollzogene Ausführen eines Commits angezeigt wird, während in einem anderen Protokoll das vollzogene Ausführen eines Commits nicht angezeigt wird.  
  
 Gehen Sie dazu während der Ausführung eines Commits für eine markierte Transaktion folgendermaßen vor:  
  
1.  Die Vorbereitungsphase einer Markierungstransaktion hält alle neuen Vorbereitungen und Commits zurück.  
  
2.  Nur Commits für bereits vorbereitete Transaktionen werden fortgesetzt.  
  
3.  Die Markierungstransaktion wartet dann, bis alle vorbereiteten Transaktionen ausgeglichen wurden (mit Timeout).  
  
4.  Die markierte Transaktion wird vorbereitet, und ein Commit wird ausgeführt.  
  
5.  Das Zurückhalten neuer Vorbereitungen und Commits wird entfernt.  
  
 Das Zurückhalten, das durch markierte Transaktionen generiert wird, die sich über mehrere Datenbanken erstrecken, kann die Leistung des Servers hinsichtlich der Transaktionsverarbeitung beeinträchtigen.  
  
 Es wird davon abgeraten, markierte Transaktionen gleichzeitig auszuführen. Es kommt zwar selten vor, aber es ist möglich, dass der Commit einer verteilten markierten Transaktion einen Deadlock mit anderen verteilten Transaktionen verursacht, für die gleichzeitig ein Commit ausgeführt wird. Wenn dies passiert, wird die Markierungstransaktion als Deadlockopfer gewählt, und ein Rollback wird ausgeführt. In diesem Fall kann die Anwendung versuchen, die markierte Transaktion erneut auszuführen. Wenn mehrere markierte Transaktionen versuchen, gleichzeitig einen Commit auszuführen, steigt die Wahrscheinlichkeit eines Deadlocks.  
  
## <a name="recovering-to-a-marked-transaction"></a>Wiederherstellen bis zu einer markierten Transaktion  
 Informationen zum Wiederherstellen einer Datenbank, die markierte Transaktionen enthält, bis zu einer Markierung oder kurz vor einer bestimmten Markierung finden Sie unter [Wiederherstellen verwandter Datenbanken mit einer markierten Transaktion](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md).  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Vollständige Datenbanksicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Wiederherstellen verwandter Datenbanken mit einer markierten Transaktion](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
  
