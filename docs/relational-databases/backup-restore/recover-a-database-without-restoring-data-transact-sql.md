---
title: Wiederherstellen einer Datenbank ohne Wiederherstellung von Daten (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restoring [SQL Server], recovery-only
- recovery-only scenario [SQL Server]
- restoring databases [SQL Server], recovery-only
- recovery [SQL Server], recovery-only
- database recovery [SQL Server]
- database restores [SQL Server], recovery-only
- recovery [SQL Server], without restoring data
ms.assetid: 7e8fa620-315d-4e10-a718-23fa5171c09e
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 06806d82a8075b0aa25bd66028eefee1a83ec2f9
ms.lasthandoff: 04/11/2017

---
# <a name="recover-a-database-without-restoring-data-transact-sql"></a>Wiederherstellen einer Datenbank ohne Wiederherstellung von Daten (Transact-SQL)
  Normalerweise werden alle Daten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank wiederhergestellt, bevor die Datenbank wiederhergestellt wird. Ein Wiederherstellungsvorgang kann jedoch eine Datenbank wiederherstellen, ohne dabei eine Sicherung wiederherzustellen, z. B. beim Wiederherstellen einer schreibgeschützten Datei, die mit der Datenbank konsistent ist. Dies wird als *reine Wiederherstellung*bezeichnet. Wenn Offlinedaten bereits mit der Datenbank konsistent sind und nur zur Verfügung gestellt werden müssen, stellt die reine Wiederherstellung die Datenbank wieder her und schaltet die Daten online.  
  
 Eine reine Wiederherstellung kann für eine ganze Datenbank oder Dateien bzw. Dateigruppen ausgeführt werden.  
  
## <a name="recovery-only-database-restore"></a>Reine Datenbankwiederherstellung  
 Eine reine Datenbankwiederherstellung kann in den folgenden Situationen hilfreich sein:  
  
-   Sie haben die Datenbank beim Speichern der letzten Sicherung in einer Wiederherstellungssequenz nicht wiederhergestellt und möchten jetzt die Datenbank wiederherstellen, um diese online zu schalten.  
  
-   Die Datenbank befindet sich im Standbymodus, und Sie möchten, dass die Datenbank aktualisierbar ist, ohne dass eine weitere Protokollsicherung angewendet werden muss.  
  
 Die [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) -Syntax für eine reine Datenbankwiederherstellung lautet wie folgt:  
  
 RESTORE DATABASE *database_name* WITH RECOVERY  
  
> [!NOTE]  
>  Die FROM **=**\<*backup_device>*-Klausel wird für reine Wiederherstellungsvorgänge nicht verwendet, da keine Sicherung erforderlich ist.  
  
 **Beispiel**  
  
 Im folgenden Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank ohne die zugehörigen Daten wiederhergestellt.  
  
```  
-- Restore database using WITH RECOVERY.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY  
```  
  
## <a name="recovery-only-file-restore"></a>Reine Dateiwiederherstellung  
 Eine reine Dateiwiederherstellung kann in der folgenden Situation hilfreich sein:  
  
 Eine Datenbank wird schrittweise wiederhergestellt. Nach Abschluss der Wiederherstellung der primären Dateigruppe sind eine oder mehrere der nicht wiederhergestellten Dateien mit dem neuen Datenbankstatus konsistent, weil sie vielleicht einige Zeit schreibgeschützt waren. Diese Dateien müssen lediglich wiederhergestellt werden. Das Kopieren von Daten ist nicht erforderlich.  
  
 Bei einem reinen Wiederherstellungsvorgang werden die Daten in der Offlinedateigruppe wieder online geschaltet; es erfolgt keine Datenkopierphase, kein Wiederholen (Rollforwardphase) oder Rückgängig machen (Rollbackphase). Informationen zu den Wiederherstellungsphasen finden Sie unter [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
 Die [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)-Syntax für eine reine Dateiwiederherstellung lautet:  
  
 RESTORE DATABASE *database_name* { FILE **=***logical_file_name* | FILEGROUP **=***logical_filegroup_name* }[ **,**...*n* ] WITH RECOVERY  
  
 **Beispiel**  
  
 Im folgenden Beispiel wird eine reine Dateiwiederherstellung der Dateien in einer sekundären Dateigruppe ( `SalesGroup2`) in der `Sales` -Datenbank veranschaulicht. Die primäre Dateigruppe wurde bereits zu Beginn der schrittweisen Wiederherstellung gespeichert, und `SalesGroup2` ist konsistent mit der wiederhergestellten primären Dateigruppe. Es ist nur eine einzige Anweisung erforderlich, um die Dateigruppe wiederherzustellen und online zu schalten.  
  
```  
RESTORE DATABASE Sales FILEGROUP=SalesGroup2 WITH RECOVERY;  
```  
  
## <a name="examples-of-completing-a-piecemeal-restore-scenario-with-a-recovery-only-restore"></a>Beispiele zum Abschließen von schrittweisen Wiederherstellungsszenarien mit einer reinen Wiederherstellung  
 **Einfaches Wiederherstellungsmodell**  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
 **Vollständiges Wiederherstellungsmodell**  
  
-   [Beispiel: Schrittweise Wiederherstellung einer Datenbank &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Beispiel: Schrittweise Wiederherstellung nur bestimmter Dateigruppen &#40;Vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
## <a name="see-also"></a>Siehe auch  
 [Onlinewiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Dateiwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Dateiwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
