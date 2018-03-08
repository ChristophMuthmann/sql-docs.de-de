---
title: Anwenden von Transaktionsprotokollsicherungen (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/13/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b4bc4c88baaccf4bf24c1145df466fefbeb88a29
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="apply-transaction-log-backups-sql-server"></a>Anwenden von Transaktionsprotokollsicherungen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Dieses Thema ist nur für das vollständige und für das massenprotokollierte Wiederherstellungsmodell relevant.  
  
 In diesem Thema wird das Anwenden von Transaktionsprotokollsicherungen als Bestandteil der Wiederherstellung einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank erläutert.  
 
  
##  <a name="Requirements"></a> Anforderungen zum Wiederherstellen von Transaktionsprotokollsicherungen  
 Für das Anwenden einer Transaktionsprotokollsicherung müssen folgende Voraussetzungen erfüllt sein:  
  
-   **Ausreichende Protokollsicherungen für eine Wiederherstellungssequenz:** Es müssen ausreichend Protokolldatensätze gesichert sein, damit eine Wiederherstellungssequenz abgeschlossen werden kann. Die erforderlichen Protokollsicherungen (einschließlich der [Sicherung des Protokollfragments](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) , sofern erforderlich) müssen vor dem Start einer Wiederherstellungssequenz zur Verfügung stehen.  
  
-   **Richtige Wiederherstellungsreihenfolge:**  Als Erstes muss die unmittelbar vorherige vollständige oder differenzielle Datenbanksicherung wiederhergestellt werden. Alle nach dieser vollständigen oder differenziellen Datenbanksicherung erstellten Transaktionsprotokolle müssen dann in chronologischer Reihenfolge wiederhergestellt werden. Wenn eine Transaktionsprotokollsicherung in dieser Protokollkette verloren gegangen oder beschädigt ist, können Sie nur Transaktionsprotokolle vor dem fehlenden wiederherstellen.  
  
-   **Noch nicht wiederhergestellte Datenbank:**  Die Datenbank kann erst wiederhergestellt werden, nachdem das letzte Transaktionsprotokoll angewendet wurde. Wenn Sie die Datenbank nach dem Wiederherstellen einer der Zwischen-Transaktionsprotokollsicherungen (einer Sicherung vor dem Ende der Protokollkette) wiederherstellen, können Sie die Datenbank nicht zu einem späteren Zeitpunkt als diesem wiederherstellen, ohne die gesamte Wiederherstellungssequenz, beginnend mit der vollständigen Datenbanksicherung, neu zu starten.  
  
    > **TIPP:** Eine bewährte Methode besteht darin, alle Protokollsicherungen (RESTORE LOG *Datenbankname* WITH NORECOVERY) wiederherzustellen. Stellen Sie nach dem Wiederherstellen der letzten Protokollsicherung die Datenbank in einem separaten Vorgang (RESTORE DATABASE *Datenbankname* WITH RECOVERY) wieder her.  
  
##  <a name="RecoveryAndTlogs"></a> Wiederherstellungs- und Transaktionsprotokolle  
 Wenn Sie den Wiederherstellungsvorgang abschließen und die Datenbank wiederherstellen, wird während der Wiederherstellung für alle unvollständigen Transaktionen ein Rollback ausgeführt. Dies wird als *Rollbackphase*bezeichnet. Das Rollback ist erforderlich, um die Integrität der Datenbank wiederherzustellen. Nach dem Rollback wird die Datenbank online geschaltet, und es können keine weiteren Transaktionsprotokollsicherungen auf die Datenbank angewendet werden.  
  
 So kann z. B. eine Reihe von Transaktionsprotokollsicherungen eine lang andauernde Transaktion enthalten. Der Start der Transaktion wird in der ersten Transaktionsprotokollsicherung, das Ende der Transaktion jedoch in der zweiten Transaktionsprotokollsicherung aufgezeichnet. Es gibt keinen Datensatz für einen Commit- oder Rollbackvorgang in der ersten Transaktionsprotokollsicherung. Wenn ein Wiederherstellungsvorgang nach dem Anwenden der ersten Transaktionsprotokollsicherung ausgeführt wird, wird die lang andauernde Transaktion als unvollständig behandelt, und für die in der ersten Transaktionsprotokollsicherung aufgezeichneten Datenänderungen dieser Transaktion wird ein Rollback ausgeführt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist das Anwenden einer zweiten Transaktionsprotokollsicherung nach diesem Zeitpunkt nicht zulässig.  
  
> **HINWEIS:** Unter bestimmten Umständen können Sie eine Datei während der Protokollwiederherstellung explizit hinzufügen.  
  
##  <a name="PITrestore"></a> Verwenden von Protokollsicherungen zum Wiederherstellen des Zustands vor dem Fehler  
 Nehmen Sie die folgende Ereignissequenz an.  
  
|Uhrzeit|Ereignis|  
|----------|-----------|  
|8:00 Uhr|Sichern der Datenbank zum Erstellen einer vollständigen Datenbanksicherung.|  
|12:00 Uhr|Sichern des Transaktionsprotokolls.|  
|16:00 Uhr|Sichern des Transaktionsprotokolls.|  
|18:00 Uhr|Sichern der Datenbank zum Erstellen einer vollständigen Datenbanksicherung.|  
|20:00 Uhr|Sichern des Transaktionsprotokolls.|  
|21:45 Uhr|Fehler tritt auf.|  
  
> **HINWEIS:** Eine Erklärung dieser Beispielsequenz von Sicherungen finden Sie unter [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 Zum Wiederherstellen des Datenbankzustands von 21:45 Uhr (Zeitpunkt des Fehlers) kann eines der folgenden Verfahren verwendet werden:  
  
 **Alternative 1: Wiederherstellen der Datenbank mithilfe der letzten vollständigen Datenbanksicherung**  
  
1.  Erstellen Sie eine Sicherung des Protokollfragments des aktuell aktiven Transaktionsprotokolls zum Zeitpunkt des Fehlers.  
  
2.  Stellen Sie nicht die vollständige Datenbanksicherung von 8:00 Uhr von 18:00 Uhr. Stellen Sie stattdessen die neuere vollständige Datenbanksicherung von 18:00 Uhr wieder her, und wenden Sie dann die Transaktionsprotokollsicherung von 20:00 Uhr und die Sicherung des Protokollfragments an.  
  
 **Alternative 2: Wiederherstellen der Datenbank mithilfe einer früheren vollständigen Datenbanksicherung**  
  
> **HINWEIS:** Dieser alternative Vorgang ist nützlich, wenn Sie aufgrund eines Problems die vollständige Datenbanksicherung von 18:00 Uhr von 18:00 Uhr. Dieser Vorgang dauert länger als das Wiederherstellen der vollständigen Datenbanksicherung von 18:00 Uhr.  
  
1.  Erstellen Sie eine Sicherung des Protokollfragments des aktuell aktiven Transaktionsprotokolls zum Zeitpunkt des Fehlers.  
  
2.  Stellen Sie die vollständige Datenbanksicherung von 8:00 Uhr und anschließend alle vier Transaktionsprotokollsicherungen in der chronologischen Reihenfolge wieder her. Dadurch wird ein Rollforward für alle abgeschlossenen Transaktionen bis 21:45 Uhr ausgeführt.  
  
     Diese Alternative verdeutlicht, welche redundante Sicherheit eine zwischen eine Folge vollständiger Datenbanksicherungen geschaltete Kette von Transaktionsprotokollsicherungen bietet.  
  
> **HINWEIS:** In einigen Fällen können Sie auch mit Transaktionsprotokollen eine Datenbank zu einem bestimmten Zeitpunkt wiederherstellen. Informationen finden Sie unter [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)bezeichnet.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So wenden Sie eine Transaktionsprotokollsicherung an**  
  
-   [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
 **So stellen Sie einen Wiederherstellungspunkt wieder her**  
  
-   [Wiederherstellen einer Datenbank bis zum Fehlerzeitpunkt im vollständigen Wiederherstellungsmodell &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Wiederherstellen einer SQL Server-Datenbank zu einem Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [Wiederherstellen verwandter Datenbanken mit einer markierten Transaktion](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [Wiederherstellen zu einer Protokollfolgenummer &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
 **So stellen Sie eine Datenbank wieder her, nachdem Sie Sicherungen mit WITH NORECOVERY wiederhergestellt haben**  
  
-   [Wiederherstellen einer Datenbank ohne Wiederherstellung von Daten &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
