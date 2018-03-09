---
title: Onlinewiederherstellungen (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- online restores [SQL Server]
- online restores [SQL Server], about online restores
ms.assetid: 7982a687-980a-4eb8-8e9f-6894148e7d8c
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3500b144cc3afb10c5ac12ee76e49dc11953623
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="online-restore-sql-server"></a>Onlinewiederherstellungen [SQL Server]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die Onlinewiederherstellung wird nur von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Enterprise Edition unterstützt. In dieser Edition erfolgen Datei- und Seitenwiederherstellungen sowie schrittweise Wiederherstellungen standardmäßig online. Dieses Thema ist nur für Datenbanken relevant, die mehrere Dateien oder Dateigruppen enthalten (und unter dem einfachen Wiederherstellungsmodell nur für schreibgeschützte Dateigruppen).  
  
 Die Wiederherstellung von Daten, während die Datenbank online ist, wird als *Onlinewiederherstellung*bezeichnet. Eine Datenbank gilt immer als online, wenn die primäre Dateigruppe online ist, selbst wenn eine oder mehrere der sekundären Dateigruppen offline sind. Bei jedem Wiederherstellungsmodell ist es möglich, eine Datei wiederherzustellen, die offline ist, während die Datenbank online ist. Im vollständigen Wiederherstellungsmodell können Sie auch Seiten wiederherstellen, während die Datenbank online ist.  
  
> [!NOTE]  
>  Die Onlinewiederherstellung erfolgt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise automatisch und erfordert keine Benutzeraktion. Wenn Sie keine Onlinewiederherstellung verwenden möchten, können Sie eine Datenbank offline schalten, bevor Sie eine Wiederherstellung starten. Weitere Informationen finden Sie unter [Offlineschalten einer Datenbank oder Datei](#taking_db_or_file_offline)weiter unten in diesem Thema.  
  
 Während einer Onlinedateiwiederherstellung ist jede Datei, die wiederhergestellt wird, sowie deren Dateigruppe offline. Wenn beim Starten einer Onlinewiederherstellung eine dieser Dateien online ist, schaltet die erste Wiederherstellungsanweisung die Dateigruppe der Datei offline. Dagegen ist während einer Onlineseitenwiederherstellung nur die Seite offline.  
  
 Zu jedem Onlinewiederherstellungsszenario gehören die folgenden grundlegenden Schritte:  
  
1.  Stellen Sie die Daten wieder her.  
  
2.  Wiederherstellen des Protokolls mit WITH RECOVERY für die letzte Protokollwiederherstellung. Damit werden die wiederhergestellten Daten online geschaltet.  
  
 Gelegentlich ist für eine Transaktion, für die kein Commit ausgeführt wurde, kein Rollback möglich, weil die für das Rollback erforderlichen Daten während des Starts offline sind. In diesem Fall wird die Transaktion verzögert. Weitere Informationen finden Sie unter [Markierte Transaktionen &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)entfernt werden.  
  
> [!NOTE]  
>  Wenn für die Datenbank aktuell das massenprotokollierte Wiederherstellungsmodell verwendet wird, empfiehlt es sich, zum vollständigen Wiederherstellungsmodell zu wechseln, bevor Sie eine Onlinewiederherstellung starten. Weitere Informationen finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  Wenn die Sicherungen mit mehreren an den Server angeschlossenen Geräten vorgenommen wurden, darf während der Onlinewiederherstellung keines dieser Geräte fehlen.  
  
> [!CAUTION]  
>  Bei der Verwendung von Momentaufnahmesicherungen kann keine **Online Restore**ausgeführt werden. Weitere Informationen zu **Momentaufnahme-Sicherungen**finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
## <a name="log-backups-for-online-restore"></a>Protokollsicherungen für die Onlinewiederherstellung  
 Bei einer Onlinewiederherstellung ist der Wiederherstellungspunkt der Punkt, an dem die wiederhergestellten Daten offline geschaltet oder zum letzten Mal mit einem Schreibschutz versehen wurden. Alle Transaktionsprotokollsicherungen, die zu diesem Wiederherstellungspunkt führen und diesen beinhalten, müssen verfügbar sein. Im Allgemeinen ist nach diesem Punkt eine Protokollsicherung erforderlich, damit der Wiederherstellungspunkt für die Datei abgedeckt ist. Die einzige Ausnahme stellt eine Onlinewiederherstellung schreibgeschützter Daten aus einer Datensicherung dar, die ausgeführt wurde, nachdem die Daten schreibgeschützt wurden. In diesem Fall müssen Sie nicht über eine Protokollsicherung verfügen.  
  
 Im Allgemeinen können Sie Transaktionsprotokollsicherungen ausführen, während die Datenbank online ist, selbst nach dem Start der Wiederherstellungssequenz. Der Ausführungszeitpunkt der letzten Protokollsicherung hängt von den Eigenschaften der wiederhergestellten Datei ab:  
  
-   Für eine schreibgeschützte Onlinedatei können Sie die letzte Protokollsicherung, die für die Wiederherstellung erforderlich ist, vor oder während der ersten Wiederherstellungssequenz ausführen. Für eine schreibgeschützte Dateigruppe müssen möglicherweise keine Protokollsicherungen erstellt werden, wenn eine Datensicherung oder eine differenzielle Sicherung erstellt wurde, nachdem die Dateigruppe schreibgeschützt wurde.  
  
    > [!NOTE]  
    >  Die vorherigen Informationen gelten auch für jede Offlinedatei.  
  
-   Ein besonderer Fall liegt bei einer Datei mit Lese-/Schreibzugriff vor, die beim Ausführen der ersten Wiederherstellungsanweisung online war und die dann durch diese Wiederherstellungsanweisung automatisch offline geschaltet wurde. In diesem Fall müssen Sie eine Protokollsicherung während der ersten *Wiederherstellungssequenz* ausführen (die Sequenz mindestens einer RESTORE-Anweisung, die Daten wiederherstellt und einen Rollforward ausführt). Im Allgemeinen muss diese Protokollsicherung erfolgen, nachdem Sie alle vollständigen Sicherungen wiederherstellen und bevor Sie die Daten wiederherstellen. Wenn für eine bestimmte Dateigruppe jedoch mehrere Dateisicherungen vorliegen, ist der Minimalpunkt der Protokollsicherung der Zeitpunkt, nachdem die Dateigruppe offline geschaltet wurde. Diese Protokollsicherung, die nach dem Wiederherstellen der Daten ausgeführt wird, setzt an dem Punkt an, an dem die Datei offline geschaltet wurde. Die Protokollsicherung nach dem Wiederherstellen der Daten ist erforderlich, da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] die Onlineprotokollierung nicht für eine Onlinewiederherstellung verwenden kann.  
  
    > [!NOTE]  
    >  Die Datei kann auch vor der Wiederherstellungssequenz manuell offline geschaltet werden. Weitere Informationen finden Sie unter "Offlineschalten einer Datenbank oder Datei" weiter unten in diesem Thema.  
  
##  <a name="taking_db_or_file_offline"></a> Offlineschalten einer Datenbank oder Datei  
 Wenn Sie keine Onlinewiederherstellung verwenden möchten, können Sie die Datenbank offline schalten, bevor Sie die Wiederherstellungssequenz starten. Dazu können Sie eine der folgenden Methoden verwenden:  
  
-   Bei jedem Wiederherstellungsmodell können Sie die Datenbank offline schalten, indem Sie die folgende [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) -Anweisung verwenden:  
  
     ALTER DATABASE *database_name* SET OFFLINE  
  
-   Alternativ können Sie beim vollständigen Wiederherstellungsmodell eine Offlinewiederherstellung einer Datei oder Seite erzwingen, indem Sie die folgende [BACKUP LOG](../../t-sql/statements/backup-transact-sql.md) -Anweisung verwenden, um die Datenbank in den Wiederherstellungszustand zu versetzen:  
  
     BACKUP LOG *database_name* WITH NORECOVERY.  
  
 Solange eine Datenbank offline bleibt, sind alle Wiederherstellungsvorgänge Offlinewiederherstellungen.  
  
## <a name="examples"></a>Beispiele  
  
> [!NOTE]  
>  Die Syntax für eine Onlinewiederherstellungssequenz ist dieselbe wie bei einer Offlinewiederherstellungssequenz.  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer Datei mit Lese-/Schreibzugriff &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Wiederherstellen von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)  
  
-   [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
-   [Wiederherstellen einer Datenbank ohne Wiederherstellung von Daten &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
-   [Entfernen von veralteten Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Dateiwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Dateiwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
  
  
