---
title: "Beispiel: Onlinewiederherstellung einer schreibgesch&#252;tzten Datei (einfaches Wiederherstellungsmodell) | Microsoft Docs"
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
  - "Wiederherstellungssequenzen [SQL Server], online"
  - "Onlinewiederherstellungen [SQL Server], einfaches Wiederherstellungsmodell"
  - "Einfaches Wiederherstellungsmodell [SQL Server], Beispiele für RESTORE"
ms.assetid: 0c691fc6-9865-46a7-b055-8097424492d6
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# Beispiel: Onlinewiederherstellung einer schreibgesch&#252;tzten Datei (einfaches Wiederherstellungsmodell)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Dieses Thema ist nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken relevant, für die ein einfaches Wiederherstellungsmodell mit einer schreibgeschützten Dateigruppe verwendet wird. Bei einem einfachen Wiederherstellungsmodell kann eine schreibgeschützte Datei online wiederhergestellt werden, wenn eine Dateisicherung vorhanden ist, die erstellt wurde, nachdem der Schreibschutz letztmalig festgelegt wurde.  
  
 In diesem Beispiel sind in der Datenbank `adb` drei Dateigruppen enthalten. Die Dateigruppe `A` weist Lese-/Schreibzugriff auf, die Dateigruppen `B` und `C` sind schreibgeschützt. Zu Beginn sind alle Dateigruppen online. Eine schreibgeschützte Datei in Dateigruppe `B`, `b1`, muss wiederhergestellt werden. Der Datenbankadministrator kann sie mithilfe einer Sicherung wiederherstellen, die erstellt wurde, nachdem der Schreibschutz für die Datei festgelegt wurde. Für die Dauer der Wiederherstellung ist die Dateigruppe `B` offline, der Rest der Datenbank bleibt jedoch online.  
  
## Wiederherstellungssequenz  
  
> [!NOTE]  
>  Die Syntax für eine Onlinewiederherstellungssequenz ist dieselbe wie bei einer Offlinewiederherstellungssequenz.  
  
 Zum Wiederherstellen der Datei befolgt der Datenbankadministrator die folgende Wiederherstellungssequenz:  
  
```  
RESTORE DATABASE adb FILE='b1' FROM filegroup_B_backup   
WITH RECOVERY  
```  
  
 Die Datei ist zurzeit online.  
  
## Zusätzliche Beispiele  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer Datei mit Lese-/Schreibzugriff &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## Siehe auch  
 [Onlinewiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Dateiwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  