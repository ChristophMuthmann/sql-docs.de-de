---
title: 'Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen (einfaches Wiederherstellungsmodell) | Microsoft-Dokumentation'
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
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: d7ad026c-5355-4308-9560-0dc843940d4f
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39b07366c8f2dfd9ccd5322e172b4df5829084ff
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model"></a>Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen (einfaches Wiederherstellungsmodell)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieses Thema ist nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken relevant, für die ein einfaches Wiederherstellungsmodell mit einer schreibgeschützten Dateigruppe verwendet wird.  
  
 Mit einer schrittweisen Wiederherstellungssequenz wird eine Datenbank phasenweise auf Dateigruppenebene wiederhergestellt, beginnend mit der primären Dateigruppe und allen sekundären Dateigruppen mit Lese-/Schreibzugriff.  
  
 In diesem Beispiel sind in der Datenbank `adb`, für die das einfache Wiederherstellungsmodell verwendet wird, drei Dateigruppen enthalten. Die Dateigruppe `A` weist Lese-/Schreibzugriff auf, die Dateigruppen `B` und `C` sind schreibgeschützt. Zu Beginn sind alle Dateigruppen online.  
  
 Die primäre Dateigruppe und die Dateigruppe `B` der `adb` -Datenbank scheinen beschädigt zu sein. Der Datenbankadministrator beschließt, sie mithilfe einer schrittweisen Wiederherstellungssequenz wiederherzustellen. Beim einfachen Wiederherstellungsmodell müssen alle Dateigruppen mit Lese-/Schreibzugriff von derselben Teilsicherung wiederhergestellt werden. Obwohl die Dateigruppe `A` intakt ist, muss sie mit der primären Dateigruppe wiederhergestellt werden, um sicherzustellen, dass beide konsistent sind (die Datenbank wird bis zu dem Zeitpunkt wiederhergestellt, der zum Ende der letzten Teilsicherung definiert wurde). Die Dateigruppe `C` ist intakt, muss jedoch wiederhergestellt werden, damit sie online geschaltet werden kann. Die Dateigruppe `B`ist zwar beschädigt, es sind darin jedoch keine so wichtigen Daten wie in Dateigruppe `C`enthalten. Deshalb wird die Dateigruppe `B` zuletzt wiederhergestellt.  
  
## <a name="restore-sequences"></a>Wiederherstellen von Sequenzen  
  
> [!NOTE]  
>  Die Syntax für eine Onlinewiederherstellungssequenz ist dieselbe wie bei einer Offlinewiederherstellungssequenz.  
  
1.  Teilwiederherstellung der primären Dateigruppe und der Dateigruppe `A` von einer Teilsicherung.  
  
    ```  
    RESTORE DATABASE adb READ_WRITE_FILEGROUPS FROM partial_backup   
    WITH PARTIAL, RECOVERY  
    ```  
  
     Die primäre Dateigruppe und die Dateigruppe `A` sind zu diesem Zeitpunkt online. Für Dateien in den Dateigruppen `B` und `C` steht die Wiederherstellung aus, und die Dateigruppen sind offline.  
  
2.  Onlinewiederherstellung der Dateigruppe `C`.  
  
     Dateigruppe `C` ist konsistent, weil die Teilsicherung, die weiter oben wiederhergestellt wurde, nach dem Kennzeichnen der Dateigruppe `C` als schreibgeschützt erstellt wurde, obwohl für die Datenbank ein früherer Status wiederhergestellt wurde. Der Datenbankadministrator stellt die Dateigruppe `C`wieder her, ohne die Sicherung wiederherzustellen, um sie online zu schalten.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' WITH RECOVERY  
    ```  
  
     Die primäre Dateigruppe und die Dateigruppen `A` und `C` sind zu diesem Zeitpunkt online. Für die Dateien in der Dateigruppe B steht weiterhin die Wiederherstellung aus, wobei die Dateigruppe offline ist.  
  
3.  Onlinewiederherstellung der Dateigruppe `B.`  
  
     Dateien in der Dateigruppe `B` müssen wiederhergestellt werden. Der Datenbankadministrator stellt die Sicherung von Dateigruppe `B` wieder her, die erstellt wurde, nachdem die Dateigruppe `B` als schreibgeschützt gekennzeichnet und bevor die Teilsicherung erstellt wurde.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup   
    WITH RECOVERY  
    ```  
  
     Alle Dateigruppen sind nun online.  
  
## <a name="additional-examples"></a>Zusätzliche Beispiele  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
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
  
  
