---
title: "Beispiel: Onlinewiederherstellung einer Datei mit Lese-/Schreibzugriff (vollst&#228;ndiges Wiederherstellungsmodell) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Vollständiges Wiederherstellungsmodell [SQL Server], RESTORE-Beispiel"
  - "Onlinewiederherstellungen [SQL Server], vollständiges Wiederherstellungsmodell"
  - "Wiederherstellungssequenzen [SQL Server], online"
ms.assetid: 0dbeda81-1464-44ba-9011-914900096368
caps.latest.revision: 33
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 33
---
# Beispiel: Onlinewiederherstellung einer Datei mit Lese-/Schreibzugriff (vollst&#228;ndiges Wiederherstellungsmodell)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Dieses Thema ist nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken mit mehreren Dateien oder Dateigruppen im vollständigen Wiederherstellungsmodell relevant.  
  
 In diesem Beispiel enthält die Datenbank `adb`, für die das vollständige Wiederherstellungsmodell verwendet wird, drei Dateigruppen. Die Dateigruppe `A` weist Lese-/Schreibzugriff auf, die Dateigruppen `B` und `C` sind schreibgeschützt. Zu Beginn sind alle Dateigruppen online.  
  
 Datei `a1` in Dateigruppe `A` ist allem Anschein nach beschädigt, darum beschließt der Datenbankadministrator, die Datei wiederherzustellen; die Datenbank bleibt dabei online.  
  
> [!NOTE]  
>  Bei Verwendung des einfachen Wiederherstellungsmodells ist die Onlinewiederherstellung von Daten mit Lese- und Schreibzugriff nicht zulässig.  
  
## Wiederherstellen von Sequenzen  
  
> [!NOTE]  
>  Die Syntax für eine Onlinewiederherstellungssequenz ist dieselbe wie bei einer Offlinewiederherstellungssequenz.  
  
1.  Onlinewiederherstellung von Datei `a1`.  
  
    ```  
    RESTORE DATABASE adb FILE='a1' FROM backup   
    WITH NORECOVERY;  
    ```  
  
     Datei a1 befindet sich jetzt im Wiederherstellungsstatus, und Dateigruppe A ist offline.  
  
2.  Nach der Wiederherstellung der Datei erstellt der Datenbankadministrator eine neue Protokollsicherung, um sicherzustellen, dass der Status der Datenbank zu dem Zeitpunkt erfasst wird, zu dem die Datei offline geschaltet wurde.  
  
    ```  
    BACKUP LOG adb TO log_backup3;   
    ```  
  
3.  Onlinewiederherstellung von Protokollsicherungen.  
  
     Der Administrator stellt alle seit der wiederhergestellten Dateisicherung erstellten Protokollsicherungen bis zur letzten Protokollsicherung (der in Schritt 2 erstellten Sicherung *log_backup3*) wieder her. Nach dem Wiederherstellen der letzten Protokollsicherung wird die Datenbank wiederhergestellt.  
  
    ```  
    RESTORE LOG adb FROM log_backup1 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup2 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY;  
    RESTORE LOG adb WITH RECOVERY;  
    ```  
  
     Die Datei `a1` ist jetzt online.  
  
## Zusätzliche Beispiele  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## Siehe auch  
 [Onlinewiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  