---
title: "Beispiel: Schrittweise Wiederherstellung einer Datenbank (einfaches Wiederherstellungsmodell) | Microsoft Docs"
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
  - "Schrittweise Wiederherstellung [SQL Server], einfaches Wiederherstellungsmodell"
  - "Wiederherstellungssequenzen [SQL Server], schrittweise"
  - "Einfaches Wiederherstellungsmodell [SQL Server], Beispiele für RESTORE"
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# Beispiel: Schrittweise Wiederherstellung einer Datenbank (einfaches Wiederherstellungsmodell)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Mit einer schrittweisen Wiederherstellungssequenz wird eine Datenbank phasenweise auf Dateigruppenebene wiederhergestellt, beginnend mit der primären Dateigruppe und allen sekundären Dateigruppen mit Lese-/Schreibzugriff.  
  
 In diesem Beispiel wird die `adb`-Datenbank nach einem Notfall auf einem neuen Computer wiederhergestellt. Für die Datenbank wird das einfache Wiederherstellungsmodell verwendet. Vor dem Notfall sind alle Dateigruppen online. Die Dateigruppen `A` und `C` weisen Lese-/Schreibzugriff auf, und die Dateigruppe `B` ist schreibgeschützt. Vor der letzten Teilsicherung ist die Dateigruppe `B` schreibgeschützt geworden. Zur letzten Teilsicherung gehören die primäre Dateigruppe und die sekundären Dateigruppen `A` und `C` mit Lese-/Schreibzugriff.  Nachdem die Dateigruppe `B` schreibgeschützt geworden ist, wurde eine getrennte Dateisicherung der Dateigruppe `B` ausgeführt.  
  
## Wiederherstellen von Sequenzen  
  
1.  Teilwiederherstellung der primären Dateigruppe und der Dateigruppen `A` und `C`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A',FILEGROUP='C'   
       FROM partial_backup   
       WITH PARTIAL, RECOVERY;  
  
    ```  
  
     Die primäre Dateigruppe und die Dateigruppen `A` und `C` sind zu diesem Zeitpunkt online. Bei allen Dateien in der Dateigruppe `B` steht die Wiederherstellung aus, und die Dateigruppe ist offline.  
  
2.  Onlinewiederherstellung der Dateigruppe `B`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY;  
  
    ```  
  
     Alle Dateigruppen sind nun online.  
  
## Zusätzliche Beispiele  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer Datei mit Lese-/Schreibzugriff &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## Siehe auch  
 [Onlinewiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  