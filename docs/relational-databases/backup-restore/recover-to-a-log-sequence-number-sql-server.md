---
title: Wiederherstellen zu einer Protokollfolgenummer (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql-non-specified
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
- log sequence numbers [SQL Server]
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- LSNs
- database recovery [SQL Server]
- database restores [SQL Server], point in time
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb43b2630d4eebe0c101f616e7da71908c031ac7
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>Wiederherstellen zu einer Protokollfolgenummer (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Dieses Thema ist nur für Datenbanken relevant, die das vollständige oder das massenprotokollierte Wiederherstellungsmodell verwenden.  
  
 Sie können eine Protokollfolgenummer (Log Sequence Number, LSN) zum Definieren des Wiederherstellungspunkts für einen Wiederherstellungsvorgang verwenden. Hierbei handelt es sich jedoch um eine auf Anbieter von Tools zugeschnittene Funktion, die nur in speziellen Fällen nutzbringend anzuwenden ist.  
  
##  <a name="LSNs"></a> Übersicht der Protokollfolgenummern  
 Mit LSNs wird intern während einer RESTORE-Sequenz der Zeitpunkt nachverfolgt, bis zu dem Daten wiederhergestellt wurden. Wenn eine Sicherung wiederhergestellt wird, werden die Daten bis zu der LSN wiederhergestellt, die dem Zeitpunkt entspricht, an dem die Sicherung erstellt wurde. Durch differenzielle Sicherungen und Protokollsicherungen wird ein späterer Status der Datenbank wiederhergestellt, was wiederum einer höheren LSN entspricht.  
  
 Jeder Datensatz im Transaktionsprotokoll wird eindeutig durch eine Protokollfolgenummer (Log Sequence Number, LSN) identifiziert. LSNs halten sich an eine bestimmte Reihenfolge. Wenn LSN2 größer als LSN1 ist, erfolgte die durch den Protokolldatensatz von LSN2 beschriebene Änderung nach der durch den Protokolldatensatz von LSN1 beschriebenen Änderung.  
  
 Die LSN eines Protokolldatensatzes, bei dem ein wichtiges Ereignis aufgetreten ist, kann zum Erstellen richtiger Wiederherstellungssequenzen hilfreich sein. Da LSNs eine bestimmte Reihenfolge aufweisen, kann verglichen werden, ob sie gleich oder ungleich sind (d.h. **\<**, **>**, **=**, **\<=**, **>=**). Solche Vergleiche sind beim Erstellen von Wiederherstellungssequenzen hilfreich.  
  
> [!NOTE]  
>  LSNs sind Werte vom Datentyp **numeric**(25,0). Arithmetische Operationen (z. B. Addition oder Subtraktion) sind ohne Bedeutung und dürfen für LSNs nicht verwendet.  
  
  
## <a name="viewing-lsns-used-by-backup-and-restore"></a>Anzeigen von LSNs, die von der Sicherung und Wiederherstellung verwendet werden  
 Die LSN eines Protokolldatensatzes, bei dem ein bestimmtes Sicherungs- und Wiederherstellungsereignis aufgetreten ist, kann mithilfe der folgenden Methoden angezeigt werden:  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md); [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
-   [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
> [!NOTE]  
>  LSNs werden auch in manchen Meldungstexten angezeigt.  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>Transact-SQL-Syntax für die Wiederherstellung bis zu einer LSN  
 Mithilfe einer [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Anweisung können Sie an oder direkt vor der LSN stoppen, wie im Folgenden gezeigt:  
  
-   Verwenden Sie die WITH STOPATMARK **='**lsn:*<LSN-Nummer>***'**-Klausel, wobei lsn:*\<LSN-Nummer>* eine Zeichenfolge darstellt, die angibt, dass der Protokolldatensatz mit der angegebenen LSN der Wiederherstellungspunkt ist.  
  
     Von STOPATMARK wird ein Rollforward zur LSN ausgeführt und dieser Protokolldatensatz im Rollforward eingeschlossen.  
  
-   Verwenden Sie die WITH STOPBEFOREMARK **='**lsn:*<LSN-Nummer>****'-Klausel, wobei lsn:*\<LSN-Nummer>* eine Zeichenfolge darstellt, die angibt, dass der Protokolldatensatz direkt vor dem Protokolldatensatz mit der angegebenen LSN der Wiederherstellungspunkt ist.  
  
     Von STOPBEFOREMARK wird ein Rollforward bis zur LSN ausgeführt und dieser Protokolldatensatz aus dem Rollforward ausgeschlossen.  
  
 Typischerweise wird eine bestimmte Transaktion zum Einschließen oder Ausschließen ausgewählt. Praktisch handelt es sich bei dem angegebenen Protokolldatensatz um einen Transaktionscommitdatensatz, wobei diese Angabe nicht zwingend erforderlich ist.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird davon ausgegangen, dass die `AdventureWorks` -Datenbank so geändert wurde, dass das vollständige Wiederherstellungsmodell verwendet wird.  
  
```  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Wiederherstellen einer Datenbank bis zum Fehlerzeitpunkt im vollständigen Wiederherstellungsmodell &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Wiederherstellen einer Datenbank bis zu einer markierten Transaktion &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
