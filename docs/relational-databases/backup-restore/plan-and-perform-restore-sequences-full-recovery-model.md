---
title: Planen und Ausführen von Wiederherstellungssequenzen (vollständiges Wiederherstellungsmodell) | Microsoft-Dokumentation
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
- restore sequences [SQL Server], planning for
- full recovery model [SQL Server], planning restore sequences
ms.assetid: 9cbefaf8-d2b6-41c9-83fc-b3807a841fe2
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79425550a136d26f5b135e4691f9a35efe56f5b4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="plan-and-perform-restore-sequences-full-recovery-model"></a>Planen und Ausführen von Wiederherstellungssequenzen (vollständiges Wiederherstellungsmodell)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird erläutert, wie eine Wiederherstellungssequenz für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank geplant und ausgeführt wird, für die normalerweise das vollständige Wiederherstellungsmodell verwendet wird. Eine *Wiederherstellungssequenz* ist eine Sequenz einer oder mehrerer [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Anweisungen. Normalerweise werden von einer Sequenz der Inhalt der Datenbank, Dateien und/oder Seiten, der bzw. die wiederhergestellt werden sollen, initialisiert (Datenkopierphase), und es wird ein Rollforward für protokollierte Transaktionen (Rollforwardphase) und ein Rollback für Transaktionen ohne Commit (Rollbackphase) ausgeführt.  
  
 In einfachen Fällen sind für eine Wiederherstellungssequenz lediglich eine vollständige Datenbanksicherung, eine differenzielle Datenbanksicherung und mindestens eine Protokollsicherung erforderlich. In diesen Fällen ist das Erstellen einer ordnungsgemäßen Wiederherstellungssequenz einfach. Wenn Sie beispielsweise eine Datenbank auf den Punkt wiederherstellen möchten, bevor der Fehler aufgetreten ist, beginnen Sie damit, das Transaktionsprotokoll (das *Fragment* des Protokolls) zu sichern. Stellen Sie anschließend die letzte vollständige Datenbanksicherung, die zuletzt erstellte differenzielle Sicherung (sofern vorhanden) sowie alle nachfolgenden Protokollsicherungen in der Reihenfolge, in der diese erstellt wurden, wieder her.  
  
 In weniger einfachen Fällen kann das Erstellen einer ordnungsgemäßen Wiederherstellungssequenz ein komplexer Prozess sein. Beispielsweise können für eine Wiederherstellungssequenz mehrere Dateisicherungen oder eine Wiederherstellung von Daten bis zu einem bestimmten Zeitpunkt erforderlich sein. In sehr komplexen Fällen muss möglicherweise ein verzweigter Wiederherstellungspfad durchlaufen werden, der mindestens eine Wiederherstellungsverzweigung umfasst.  
  
> [!NOTE]  
>  Ein *Wiederherstellungspfad* ist die Sequenz von Daten- und Protokollsicherungen, mit denen eine Datenbank auf einen bestimmten Zeitpunkt (dem sogenannten Wiederherstellungspunkt) wiederhergestellt wird. Ein Wiederherstellungspfad besteht aus einer eindeutigen Menge bestimmter Transformationen, auf deren Grundlage die Datenbank über einen bestimmten Zeitraum entwickelt und gleichzeitig die Konsistenz der Datenbank sichergestellt wurde. Ein Wiederherstellungspfad stellt einen Bereich von LSNs dar, der von einem Startpunkt (LSN, GUID) zu einem Endpunkt (LSN, GUID) führt. Der Bereich von LSNs in einem Wiederherstellungspfad kann mindestens eine Wiederherstellungsverzweigung von Anfang bis zum Ende durchsuchen.  
  
## <a name="to-plan-a-restore-sequence"></a>So planen Sie eine Wiederherstellungssequenz  
 Führen Sie die folgenden Schritte aus, bevor Sie eine Wiederherstellungssequenz starten:  
  
1.  Erstellen Sie, wenn möglich, eine Sicherung des Protokollfragments der Datenbank. Weitere Informationen finden Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
2.  Bestimmen Sie den Zielwiederherstellungspunkt.  
  
     Der Zielwiederherstellungspunkt kann ein beliebiger Zeitpunkt bzw. eine beliebige Markierung innerhalb einer Transaktionsprotokollsicherung sein. Weitere Informationen finden Sie unter [Wiederherstellen einer SQL Server-Datenbank auf einen Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md) und [Wiederherstellen von verwandten Datenbanken mithilfe von markierten Transaktionen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
3.  Bestimmen Sie die Art der Wiederherstellung, die Sie ausführen möchten. Weitere Informationen finden Sie unter [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
4.  Bestimmen Sie, welche Sicherungen erforderlich sind, und stellen Sie sicher, dass die erforderlichen Mediensätze und Sicherungsmedien verfügbar sind. Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md) und [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
## <a name="to-perform-a-restore-sequence"></a>So führen Sie eine Wiederherstellungssequenz aus  
 Führen Sie die folgenden Schritte aus, um eine Wiederherstellungssequenz auszuführen:  
  
1.  Stellen Sie mindestens eine Datensicherung (z. B. eine Datenbanksicherung, eine Teilsicherung, eine oder mehrere Dateisicherungen) wieder her, um die Sequenz zu starten.  
  
2.  Stellen Sie optional die letzten differenziellen Sicherungen wieder her, die auf diesen vollständigen Sicherungen basieren.  
  
     Bestimmen Sie für jede vollständige Sicherung, die Sie wiederherstellen möchten, ob diese Sicherung als Basis für differenzielle Sicherungen fungiert. Stellen Sie, wenn möglich, in diesem Fall die letzte differenzielle Sicherung wieder her. Weitere Informationen finden Sie unter [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
3.  Führen Sie für die Datenbank einen Rollforward aus, indem Sie die Protokollsicherungen nacheinander bis zu der Sicherung mit dem Wiederherstellungspunkt wiederherstellen. Ob alle Protokollsicherungen angewendet werden müssen, richtet sich danach, in welcher Protokollsicherung der Wiederherstellungspunkt enthalten ist:  
  
    -   Wenn der Wiederherstellungspunkt der Zeitpunkt des Fehlers ist, müssen Sie alle Protokollsicherungen wiederherstellen, die seit der Wiederherstellung der letzten (vollständigen oder differenziellen) Datensicherung erstellt wurden. Weitere Informationen finden Sie unter [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
    -   Für eine Wiederherstellung bis zu einem bestimmten Zeitpunkt sind möglicherweise nicht die aktuellsten Protokollsicherungen erforderlich. Wenn Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verwenden, stellt der Datenbankwiederherstellungsberater sicher, dass nur Sicherungen ausgewählt werden, die auf den angegebenen Zeitpunkt wiederhergestellt werden müssen. Die Sicherungen machen den empfohlenen Wiederherstellungsplan für Ihre Zeitpunktwiederherstellung aus. Informationen finden Sie unter [Wiederherstellen einer SQL Server-Datenbank auf einen Zeitpunkt &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
## <a name="restarting-a-restore-sequence"></a>Neustarten einer Wiederherstellungssequenz  
 Wenn im Rahmen einer Wiederherstellungssequenz ein Problem auftritt, können Sie die Wiederherstellungssequenz beenden und von Anfang an neu starten. Wenn Sie beispielsweise versehentlich zu viele Protokollsicherungen wiederhergestellt und den gewünschten Wiederherstellungspunkt überschritten haben, müssen Sie die Wiederherstellungssequenz neu starten und bis zu der Protokollsicherung wiederherstellen, die den Zielwiederherstellungspunkt enthält.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Vollständige Datenbankwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Onlinewiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Dateiwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
