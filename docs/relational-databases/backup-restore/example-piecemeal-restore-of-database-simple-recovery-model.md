---
title: 'Beispiel: Schrittweise Wiederherstellung einer Datenbank (einfaches Wiederherstellungsmodell) | Microsoft-Dokumentation'
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
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
caps.latest.revision: 27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 777bc74e2b51bc2da1d180e72d828673d1fac5f1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="example-piecemeal-restore-of-database-simple-recovery-model"></a>Beispiel: Schrittweise Wiederherstellung einer Datenbank (einfaches Wiederherstellungsmodell)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Mit einer schrittweisen Wiederherstellungssequenz wird eine Datenbank phasenweise auf Dateigruppenebene wiederhergestellt, beginnend mit der primären Dateigruppe und allen sekundären Dateigruppen mit Lese-/Schreibzugriff.  
  
 In diesem Beispiel wird die `adb` -Datenbank nach einem Notfall auf einem neuen Computer wiederhergestellt. Für die Datenbank wird das einfache Wiederherstellungsmodell verwendet. Vor dem Notfall sind alle Dateigruppen online. Die Dateigruppen `A` und `C` weisen Lese-/Schreibzugriff auf, und die Dateigruppe `B` ist schreibgeschützt. Vor der letzten Teilsicherung ist die Dateigruppe `B` schreibgeschützt geworden. Zur letzten Teilsicherung gehören die primäre Dateigruppe und die sekundären Dateigruppen `A` und `C`mit Lese-/Schreibzugriff. Nachdem die Dateigruppe `B` schreibgeschützt geworden ist, wurde eine getrennte Dateisicherung der Dateigruppe `B` ausgeführt.  
  
## <a name="restore-sequences"></a>Wiederherstellen von Sequenzen  
  
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
  
## <a name="additional-examples"></a>Zusätzliche Beispiele  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer Datei mit Lese-/Schreibzugriff &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Onlinewiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
