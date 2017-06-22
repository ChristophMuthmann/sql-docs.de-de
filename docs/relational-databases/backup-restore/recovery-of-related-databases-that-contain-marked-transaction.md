---
title: Wiederherstellen verwandter Datenbanken mit einer markierten Transaktion | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], marks
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- transactions [SQL Server], recovering to a mark
- database recovery [SQL Server]
- marked transactions [SQL Server], restoring
- database restores [SQL Server], point in time
ms.assetid: 77a0d9c0-978a-4891-8b0d-a4256c81c3f8
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8848fbbe73b377a329c8b3af29c8a6a32881f50b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="recovery-of-related--databases-that-contain-marked-transaction"></a>Wiederherstellen verwandter Datenbanken mit einer markierten Transaktion
  Dieses Thema ist nur für Datenbanken relevant, die markierte Transaktionen enthalten und von denen das vollständige oder massenprotokollierte Wiederherstellungsmodell verwendet wird.  
  
 Weitere Informationen zu den Anforderungen für die Wiederherstellung bis zu einem bestimmten Wiederherstellungspunkt finden Sie unter [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird das Einfügen benannter Markierungen in das Transaktionsprotokoll unterstützt, um die Wiederherstellung bis zu einer bestimmten Markierung zu ermöglichen. Protokollmarkierungen sind transaktionsspezifisch und werden nur eingefügt, wenn für die zugehörige Transaktion ein Commit ausgeführt wird. Demzufolge können Sie Markierungen mit bestimmten Daten verknüpfen und die Wiederherstellung bis zu einem bestimmten Punkt vornehmen, der diese Daten ein- oder ausschließt.  
  
 Beachten Sie Folgendes, bevor Sie benannte Markierungen in das Transaktionsprotokoll einfügen:  
  
-   Transaktionsmarkierungen belegen Protokollspeicherplatz und sollten deshalb nur für Transaktionen verwendet werden, die eine wichtige Rolle bei der Wiederherstellungsstrategie für die Datenbank spielen.  
  
-   Nachdem für eine markierte Transaktion ein Commit ausgeführt wurde, wird in die [logmarkhistory](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) -Tabelle in **msdb**eine Zeile eingefügt.  
  
-   Wenn sich eine markierte Transaktion über mehrere Datenbanken auf demselben Datenbankserver oder auf verschiedenen Servern erstreckt, müssen die Markierungen in den Protokollen aller betroffenen Datenbanken aufgezeichnet werden. Weitere Informationen finden Sie unter [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
> [!NOTE]  
>  Informationen zum Markieren von Transaktionen finden Sie unter [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="transact-sql-syntax-for-inserting-named-marks-into-a-transaction-log"></a>Transact-SQL-Syntax für das Einfügen benannter Markierungen in ein Transaktionsprotokoll  
 Verwenden Sie die [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) -Anweisung und die WITH MARK [*description*]-Klausel, um Markierungen in die Transaktionsprotokolle einzufügen. Die Markierung erhält denselben Namen wie die Transaktion. Der optionale *description* -Parameter stellt eine Textbeschreibung der Markierung dar und nicht den Namen der Markierung. Beispielsweise lautet der Name der Transaktion und der Markierung, die in der folgenden `BEGIN TRANSACTION` -Anweisung erstellt werden, jeweils `Tx1`:  
  
```wmimof  
BEGIN TRANSACTION Tx1 WITH MARK 'not the mark name, just a description'    
```  
  
 Mit dem Transaktionsprotokoll werden der Markierungsname (Transaktionsname), die Beschreibung, die Datenbank, der Benutzer, **datetime** -Informationen und die Protokollfolgenummer (LSN, Log Sequence Number) aufgezeichnet. Die **datetime** -Informationen werden zusammen mit dem Markierungsnamen für die eindeutige Identifizierung der Markierung verwendet.  
  
 Informationen zum Einfügen einer Markierung in eine Transaktion, die mehrere Datenbanken umfasst, finden Sie unter [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="transact-sql-syntax-for-recovering-to-a-mark"></a>Transact-SQL-Syntax für das Wiederherstellen bis zu einer Markierung  
 Wenn Sie das Ziel einer markierten Transaktion mithilfe einer[RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md)-Anweisung festlegen, können Sie eine der folgenden Klauseln verwenden, um ein Anhalten bei oder unmittelbar vor der Markierung zu bewirken:  
  
-   Verwenden Sie die WITH STOPATMARK = **'***<mark_name>***'**-Klausel, um anzugeben, dass die markierte Transaktion den Wiederherstellungspunkt darstellt.  
  
     STOPATMARK führt ein Rollforward bis zur Markierung aus und schließt die markierte Transaktion in das Rollforward ein.  
  
-   Verwenden Sie die WITH STOPBEFOREMARK = **'***<mark_name>***'**-Klausel, um anzugeben, dass der Protokolldatensatz unmittelbar vor der Markierung den Wiederherstellungspunkt darstellt.  
  
     STOPBEFOREMARK führt ein Rollforward bis zur Markierung aus und schließt die markierte Transaktion aus dem Rollforward aus.  
  
 Die Optionen STOPATMARK und STOPBEFOREMARK unterstützen beide eine optionale AFTER *datetime* -Klausel. Wenn *datetime* verwendet wird, müssen die Markierungsnamen nicht eindeutig sein.  
  
 Wenn AFTER *datetime* nicht angegeben ist, wird der Rollforward bei der ersten Markierung mit dem angegebenen Namen beendet. Wenn AFTER *datetime* angegeben ist, wird der Rollforward bei der ersten Markierung beendet, die den angegebenen Namen genau um oder nach *datetime*aufweist.  
  
> [!NOTE]  
>  Wie bei jedem Wiederherstellungsvorgang bis zu einem bestimmten Zeitpunkt ist das Wiederherstellen bis zu einer Markierung nicht zulässig in Zeiten, in denen für die Datenbank massenprotokollierte Vorgänge ausgeführt werden.  
  
 **So führen Sie eine Wiederherstellung bis zu einer markierten Transaktion aus**  
  
 [Wiederherstellen einer Datenbank bis zu einer markierten Transaktion &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
### <a name="preparing-the-log-backups"></a>Vorbereiten der Protokollsicherungen  
 Die folgende Sicherungsstrategie für diese verbundenen Datenbanken wäre in diesem Beispiel angemessen:  
  
1.  Verwenden Sie für beide Datenbanken das vollständige Wiederherstellungsmodell.  
  
2.  Erstellen Sie eine vollständige Sicherung jeder einzelnen Datenbank.  
  
     Die Datenbanken können nacheinander oder gleichzeitig gesichert werden.  
  
3.  Markieren Sie vor dem Sichern des Transaktionsprotokolls eine Transaktion, die in allen Datenbanken ausgeführt wird. Informationen zum Erstellen der markierten Transaktionen finden Sie unter [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
4.  Sichern Sie das Transaktionsprotokoll für jede Datenbank.  
  
### <a name="recovering-the-database-to-a-marked-transaction"></a>Wiederherstellen der Datenbank bis zu einer markierten Transaktion  
 **So stellen Sie die Sicherung wieder her**  
  
1.  Erstellen Sie nach Möglichkeit [Sicherungen des Protokollfragments](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) der unbeschädigten Datenbanken.  
  
2.  Stellen Sie die letzte vollständige Datenbanksicherung jeder Datenbank wieder her.  
  
3.  Identifizieren Sie die letzte verfügbare markierte Transaktion in allen Transaktionsprotokollsicherungen. Diese Informationen werden in der **logmarkhistory** -Tabelle in der **msdb** -Datenbank auf dem entsprechenden Server gespeichert.  
  
4.  Identifizieren Sie die Protokollsicherungen für alle verbundenen Datenbanken, die diese Markierung enthalten.  
  
5.  Stellen Sie jede Protokollsicherung bis zur markierten Transaktion wieder her.  
  
6.  Stellen Sie jede Datenbank wieder her.  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Planen und Ausführen von Wiederherstellungssequenzen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
