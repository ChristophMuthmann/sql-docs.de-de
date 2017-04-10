---
title: "Protokollfragmentsicherungen (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "08/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sichern [SQL Server], Protokollfragment"
  - "Transaktionsprotokollsicherungen [SQL Server], Sicherungen des Protokollfragments"
  - "NO_TRUNCATE-Klausel"
  - "Sicherungen [SQL Server], Protokollsicherungen"
  - "Sicherungen des Protokollfragments"
  - "Sicherungen [SQL Server], Sicherungen des Protokollfragments"
ms.assetid: 313ddaf6-ec54-4a81-a104-7ffa9533ca58
caps.latest.revision: 55
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 55
---
# Protokollfragmentsicherungen (SQL Server)
  Dieses Thema ist nur Sicherungen und Wiederherstellungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken relevant, die das vollständige oder das massenprotokollierte Wiederherstellungsmodell verwenden.  
  
 Eine *Sicherung des Protokollfragments* zeichnet Protokolldatensätze auf, die bisher noch nicht gesichert wurden (das *Protokollfragment*), um Datenverlust zu vermeiden und die Protokollkette intakt zu halten. Bevor Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank auf den letzten Zeitpunkt wiederherstellen können, müssen Sie das Transaktionsprotokollfragment sichern. Die Sicherung des Protokollfragments ist die letzte relevante Sicherung im Wiederherstellungsplan für die Datenbank.  
  
> **HINWEIS:** Nicht für alle Wiederherstellungsszenarien ist eine Sicherung des Protokollfragments erforderlich. Sie benötigen keine Sicherung des Protokollfragments, wenn der Wiederherstellungspunkt in einer früheren Protokollsicherung enthalten ist. Eine Sicherung des Protokollfragments ist auch dann nicht erforderlich, wenn Sie eine Datenbank verschieben oder ersetzen (überschreiben) und sie nicht für einen Zeitpunkt nach der letzten Sicherung wiederherstellen müssen.  
  
   ##  <a name="TailLogScenarios"></a> Szenarien, die eine Sicherung des Protokollfragments erfordern  
 In den folgenden Szenarien wird empfohlen, eine Sicherung des Protokollfragments auszuführen:  
  
-   Wenn die Datenbank online ist und Sie einen Wiederherstellungsvorgang für die Datenbank ausführen möchten, beginnen Sie mit der Sicherung des Protokollfragments: Verwenden Sie zur Vermeidung eines Fehlers bei einer Onlinedatenbank die … Die Option WITH NORECOVERY der [BACKUP](../../t-sql/statements/backup-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung.  
  
-   Wenn eine Datenbank offline ist und nicht gestartet werden kann, Sie aber die Datenbank wiederherstellen möchten, sichern Sie zunächst das Protokollfragment. Da während dieser Zeit keine Transaktionen auftreten können, kann WITH NORECOVERY optional verwendet werden.  
  
-   Falls eine Datenbank beschädigt ist, nehmen Sie eine Sicherung eines Protokollfragments mithilfe der WITH CONTINUE_AFTER_ERROR-Option der BACKUP-Anweisung vor.  
  
     Die Sicherung des Protokollfragments bei einer beschädigten Datenbank verläuft nur dann erfolgreich, wenn die Protokolldateien unbeschädigt sind, die Datenbank sich in einem Zustand befindet, in dem Protokollfragmentsicherungen unterstützt werden und die Datenbank keine massenprotokollierten Änderungen enthält. Wenn keine Protokollfragmentsicherung erstellt werden kann, gehen alle nach der letzten Protokollsicherung ausgeführten Transaktionen verloren.  
  
 In der folgenden Tabelle werden die BACKUP NORECOVERY- und CONTINUE_AFTER_ERROR-Optionen zusammengefasst.  
  
|BACKUP LOG-Option|Kommentare|  
|-----------------------|--------------|  
|NORECOVERY|Verwenden Sie NORECOVERY immer dann, wenn Sie vorhaben, einen Wiederherstellungsvorgang in der Datenbank fortzusetzen. Mit NORECOVERY wird die Datenbank in den Wiederherstellungszustand versetzt. Damit wird sichergestellt, dass sich die Datenbank nach der Sicherung des Protokollfragments nicht ändert. Das Protokoll wird abgeschnitten, es sei denn, die NO_TRUNCATE-Option oder COPY_ONLY-Option ist ebenfalls angegeben.<br /><br /> **\*\* Wichtig \*\*** Verwenden Sie NO_TRUNCATE nur, wenn die Datenbank beschädigt ist.|  
|CONTINUE_AFTER_ERROR|Verwenden Sie CONTINUE_AFTER_ERROR nur dann, wenn Sie das Fragment einer beschädigten Datenbank sichern.<br /><br /> Wenn Sie das Protokollfragment in einer beschädigten Datenbank sichern, sind einige der Metadaten, die normalerweise in Protokollsicherungen erfasst werden, eventuell nicht verfügbar. Weitere Informationen finden Sie in diesem Thema unter [Sicherungen des Protokollfragments mit unvollständigen Sicherungsmetadaten](#IncompleteMetadata).|  
  
##  <a name="IncompleteMetadata"></a> Sicherungen des Protokollfragments mit unvollständigen Sicherungsmetadaten  
 Eine Protokollfragmentsicherung erfasst das Protokollfragment selbst dann, wenn die Datenbank offline geschaltet oder beschädigt ist oder wenn Datendateien fehlen. Dies kann zu unvollständigen Metadaten aus den Wiederherstellungsinformationsbefehlen und aus **msdb** führen. In diesem Fall sind jedoch nur die Metadaten unvollständig; das erfasste Protokoll ist vollständig und kann verwendet werden.  
  
 Enthält eine Sicherung des Protokollfragments unvollständige Metadaten, wird der Eintrag **has_incomplete_metadata** in der [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)-Tabelle auf **1** festgelegt. Auch in der Ausgabe von [RESTORE HEADERONLY](../Topic/RESTORE%20HEADERONLY%20\(Transact-SQL\).md) ist **HasIncompleteMetadata** auf **1** festgelegt.  
  
 Wenn die Metadaten in einer Sicherung des Protokollfragments unvollständig sind, fehlt in der [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)-Tabelle ein Großteil der Informationen zu den Dateigruppen zum Zeitpunkt der Sicherung des Protokollfragments. Die meisten Spalten der **backupfilegroup**-Tabelle sind dann NULL, und nur die folgenden Spalten sind dann sinnvoll:  
  
-   **backup_set_id**  
  
-   **filegroup_id**  
  
-   **Typ**  
  
-   **type_desc**  
  
-   **is_readonly**  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 Informationen zum Erstellen einer Sicherung der Protokolldatei finden Sie unter [Sichern des Transaktionsprotokolls bei beschädigter Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
 Informationen zum Wiederherstellen einer Transaktionsprotokollsicherung finden Sie unter [Wiederherstellen einer Transaktionsprotokollsicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
    
## Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Kopiesicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  