---
title: 'Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen (Vollständiges Wiederherstellungsmodell) | Microsoft-Dokumentation'
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
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: bced4b54-e819-472b-b784-c72e14e72a0b
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 37851ddc426e78b1c6a760edb7f9c1fca7e86a1c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-full-recovery-model"></a>Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen (Vollständiges Wiederherstellungsmodell)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieses Thema ist nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken mit mehreren Dateien oder Dateigruppen im vollständigen Wiederherstellungsmodell relevant.  
  
 Mit einer schrittweisen Wiederherstellungssequenz wird eine Datenbank phasenweise auf Dateigruppenebene wiederhergestellt, beginnend mit der primären Dateigruppe und allen sekundären Dateigruppen mit Lese-/Schreibzugriff.  
  
 In diesem Beispiel enthält die Datenbank `adb`, für die das vollständige Wiederherstellungsmodell verwendet wird, drei Dateigruppen. Die Dateigruppe `A` weist Lese-/Schreibzugriff auf, die Dateigruppen `B` und `C` sind schreibgeschützt. Zu Beginn sind alle Dateigruppen online.  
  
 Die primäre Dateigruppe und die Dateigruppe `B` der `adb` -Datenbank scheinen beschädigt zu sein. Die primäre Dateigruppe ist ziemlich klein und kann schnell wiederhergestellt werden. Der Datenbankadministrator beschließt, sie mithilfe einer schrittweisen Wiederherstellungssequenz wiederherzustellen. Zunächst werden die primäre Dateigruppe und die nachfolgenden Transaktionsprotokolle wiederhergestellt.  
  
 In den intakten Dateigruppen `A` und `C` sind wichtige Daten enthalten. Deshalb werden sie anschließend wiederhergestellt, um sie so schnell wie möglich online zu schalten. Schließlich wird die beschädigte sekundäre Dateigruppe `B`wiederhergestellt.  
  
## <a name="restore-sequences"></a>Wiederherstellungssequenzen  
  
> [!NOTE]  
>  Die Syntax für eine Onlinewiederherstellungssequenz ist dieselbe wie bei einer Offlinewiederherstellungssequenz.  
  
1.  Erstellen Sie eine Sicherung des Protokollfragments der `adb`-Datenbank. Dieser Schritt ist entscheidend dafür, dass die intakten Dateigruppen `A` und `C` mit dem Wiederherstellungspunkt der Datenbank übereinstimmen.  
  
    ```  
    BACKUP LOG adb TO tailLogBackup WITH NORECOVERY  
    ```  
  
2.  Teilweise Wiederherstellung der primären Dateigruppe.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup   
    WITH PARTIAL, NORECOVERY  
    RESTORE LOG adb FROM backup1 WITH NORECOVERY  
    RESTORE LOG adb FROM backup2 WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     Die primäre Dateigruppe ist zu diesem Zeitpunkt online. Für Dateien in den Dateigruppen `A`, `B`und `C` steht die Wiederherstellung aus, und die Dateigruppen sind offline.  
  
3.  Onlinewiederherstellung der Dateigruppen `A` und `C`.  
  
     Da die Daten unbeschädigt sind, müssen diese Dateigruppen nicht anhand einer Sicherung wiederhergestellt werden. Sie müssen jedoch wiederhergestellt werden, damit sie online geschaltet werden können.  
  
     Der Datenbankadministrator stellt `A` und `C` sofort wieder her.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A', FILEGROUP='C' WITH RECOVERY  
    ```  
  
     Die primäre Dateigruppe und die Dateigruppen `A` und `C` sind zu diesem Zeitpunkt online. Für die Dateien in der Dateigruppe `B` steht weiterhin die Wiederherstellung aus; die Dateigruppe ist offline.  
  
4.  Onlinewiederherstellung der Dateigruppe `B`.  
  
     Die Dateien in der Dateigruppe `B` werden zu einem beliebigen späteren Zeitpunkt wiederhergestellt.  
  
    > [!NOTE]  
    >  Die Sicherung von Dateigruppe `B` wurde erstellt, nachdem die Dateigruppe als schreibgeschützt gekennzeichnet wurde. Deshalb muss für diese Dateien kein Rollforward ausgeführt werden.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY  
    ```  
  
     Alle Dateigruppen sind nun online.  
  
## <a name="additional-examples"></a>Zusätzliche Beispiele  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer Datei mit Lese-/Schreibzugriff &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Beispiel: Onlinewiederherstellung einer schreibgeschützten Datei &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Onlinewiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
