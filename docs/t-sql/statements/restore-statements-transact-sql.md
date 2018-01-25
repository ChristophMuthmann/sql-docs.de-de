---
title: RESTORE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE DATABASE
- RESTORE_TSQL
- RESTORE_DATABASE_TSQL
- RESTORE
- RESTORE_LOG_TSQL
- RESTORE LOG
dev_langs: TSQL
helpviewer_keywords:
- RESTORE DATABASE, see RESTORE statement
- full backups [SQL Server]
- RECOVERY option
- database snapshots [SQL Server], reverting to
- STOPAT syntax
- differential backups, RESTORE statement
- point in time recovery [SQL Server]
- restoring [SQL Server]
- NORECOVERY option
- online restores [SQL Server], RESTORE statement
- moving databases
- RESTORE statement, syntax
- cross-platform restores
- restoring databases [SQL Server], options
- RESTORE statement
- snapshots [SQL Server database snapshots], reverting to
- reverting database snapshots
- transaction log backups [SQL Server], RESTORE statement
- RESTORE LOG, see RESTORE statement
ms.assetid: 877ecd57-3f2e-4237-890a-08f16e944ef1
caps.latest.revision: "248"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: edafff7cc70224c67ef970ca4c13e47cce113f23
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements-transact-sql"></a>RESTORE-Anweisungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt Sicherungen wieder her, die mit dem BACKUP-Befehl erstellt wurden. Mit diesem Befehl können Sie das folgende Wiederherstellungsszenario durchführen:  
  
-   Wiederherstellen einer ganzen Datenbank aus einer vollständigen Datenbanksicherung (vollständige Wiederherstellung).  
  
-   Wiederherstellen eines Teils einer Datenbank (teilweise Wiederherstellung).  
  
-   Wiederherstellen bestimmter Dateien oder Dateigruppen einer Datenbank (Dateiwiederherstellung).  
  
-   Wiederherstellen bestimmter Seiten einer Datenbank (Seitenwiederherstellung).  
  
-   Wiederherstellen eines Transaktionsprotokolls in einer Datenbank (Transaktionsprotokollwiederherstellung).  
  
-   Wiederherstellen einer Datenbank auf den Zeitpunkt, der über eine Datenbankmomentaufnahme erfasst wurde.  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Wiederherstellungsszenarien, finden Sie unter [wiederherstellen und Übersicht über Wiederherstellungsvorgänge &#40; SQLServer &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  Weitere Informationen zu Beschreibungen der Argumente, finden Sie unter [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).   Berücksichtigen Sie beim Wiederherstellen einer Datenbank aus einer anderen Instanz die Informationen unter [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).
  
> **Hinweis:** Weitere Informationen zum Wiederherstellen aus dem Windows Azure-Blob-Speicherdienst finden Sie unter [SQL Server-Sicherung und-Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
--To Restore an Entire Database from a Full database backup (a Complete Restore):  
RESTORE DATABASE { database_name | @database_name_var }   
 [ FROM <backup_device> [ ,...n ] ]  
 [ WITH   
   {  
    [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
   | ,  <general_WITH_options> [ ,...n ]  
   | , <replication_WITH_option>  
   | , <change_data_capture_WITH_option>  
   | , <FILESTREAM_WITH_option>  
   | , <service_broker_WITH options>   
   | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
   } [ ,...n ]  
 ]  
[;]  
  
--To perform the first step of the initial restore sequence  
-- of a piecemeal restore:  
RESTORE DATABASE { database_name | @database_name_var }   
   <files_or_filegroups> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
      PARTIAL, NORECOVERY   
      [  , <general_WITH_options> [ ,...n ]   
       | , \<point_in_time_WITH_options—RESTORE_DATABASE>   
      ] [ ,...n ]   
[;]  
  
--To Restore Specific Files or Filegroups:   
RESTORE DATABASE { database_name | @database_name_var }   
   <file_or_filegroup> [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
   {  
      [ RECOVERY | NORECOVERY ]  
      [ , <general_WITH_options> [ ,...n ] ]  
   } [ ,...n ]   
[;]  
  
--To Restore Specific Pages:   
RESTORE DATABASE { database_name | @database_name_var }   
   PAGE = 'file:page [ ,...n ]'   
 [ , <file_or_filegroups> ] [ ,...n ]  
 [ FROM <backup_device> [ ,...n ] ]   
   WITH   
       NORECOVERY     
      [ , <general_WITH_options> [ ,...n ] ]  
[;]  
  
--To Restore a Transaction Log:  
RESTORE LOG { database_name | @database_name_var }   
 [ <file_or_filegroup_or_pages> [ ,...n ] ]  
 [ FROM <backup_device> [ ,...n ] ]   
 [ WITH   
   {  
     [ RECOVERY | NORECOVERY | STANDBY =   
        {standby_file_name | @standby_file_name_var }   
       ]  
    | ,  <general_WITH_options> [ ,...n ]  
    | , <replication_WITH_option>  
    | , \<point_in_time_WITH_options—RESTORE_LOG>   
   } [ ,...n ]  
 ]   
[;]  
  
--To Revert a Database to a Database Snapshot:     
RESTORE DATABASE { database_name | @database_name_var }   
FROM DATABASE_SNAPSHOT = database_snapshot_name   
  
<backup_device>::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
 | { DISK | TAPE | URL } = { 'physical_backup_device_name' |  
      @physical_backup_device_name_var }   
}   
Note: URL is the format used to specify the location and the file name for the Windows Azure Blob. Although Windows Azure storage is a service, the implementation is similar to disk and tape to allow for a consistent and seemless restore experince for all the three devices.  
<files_or_filegroups>::=   
{   
   FILE = { logical_file_name_in_backup | @logical_file_name_in_backup_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }   
 | READ_WRITE_FILEGROUPS  
}   
  
<general_WITH_options> [ ,...n ]::=   
--Restore Operation Options  
   MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
 | REPLACE   
 | RESTART   
 | RESTRICTED_USER  | CREDENTIAL  
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
 | BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }   
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
<replication_WITH_option>::=  
 | KEEP_REPLICATION   
  
<change_data_capture_WITH_option>::=  
 | KEEP_CDC  
  
<FILESTREAM_WITH_option>::=  
 | FILESTREAM ( DIRECTORY_NAME = directory_name )  
  
<service_broker_WITH_options>::=   
 | ENABLE_BROKER   
 | ERROR_BROKER_CONVERSATIONS   
 | NEW_BROKER  
  
\<point_in_time_WITH_options—RESTORE_DATABASE>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = 'lsn:lsn_number'  
                 [ AFTER 'datetime']   
   }   
  
\<point_in_time_WITH_options—RESTORE_LOG>::=   
 | {  
   STOPAT = { 'datetime'| @datetime_var }   
 | STOPATMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
 | STOPBEFOREMARK = { 'mark_name' | 'lsn:lsn_number' }  
                 [ AFTER 'datetime']   
   }  
  
```  
  
## <a name="arguments"></a>Argumente  
 Beschreibungen der Argumente finden Sie [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="about-restore-scenarios"></a>Info zu Wiederherstellungsszenarien  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt eine Vielzahl von Wiederherstellungsszenarien:  
  
-   Vollständige Datenbankwiederherstellung  
  
     Stellt die gesamte Datenbank wieder her. Dabei wird mit einer vollständigen Datenbanksicherung begonnen, darauf folgt gegebenenfalls eine differenzielle Datenbanksicherung (sowie Protokollsicherungen). Weitere Informationen finden Sie unter [Vollständige Datenbankwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md) oder [Vollständige Datenbankwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md).  
  
-   Dateiwiederherstellung  
  
     Stellt eine Datei oder Dateigruppe in einer Datenbank mit mehreren Dateigruppen wieder her. Beachten Sie, dass die Datei im Rahmen des Modells der einfachen Wiederherstellung zu einer schreibgeschützten Dateigruppe gehören muss. Nach einer vollständigen Dateiwiederherstellung kann eine differenzielle Dateisicherung wiederhergestellt werden. Weitere Informationen finden Sie unter [Dateiwiederherstellungen &#40; Vollständiges Wiederherstellungsmodell &#41; ](../../relational-databases/backup-restore/file-restores-full-recovery-model.md) und [Datei Dateiwiederherstellungen &#40; Einfaches Wiederherstellungsmodell &#41; ](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md).  
  
-   Seitenwiederherstellung  
  
     Stellt einzelne Seiten wieder her. Die Seitenwiederherstellung ist nur bei den Modellen der vollständigen und der massenprotokollierten Wiederherstellung verfügbar. Weitere Informationen finden Sie unter [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md).  
  
-   Schrittweise Wiederherstellung  
  
     Stellt die Datenbank schrittweise wieder her, wobei mit der primären Dateigruppe und einer oder mehreren sekundären Dateigruppen begonnen wird. Eine schrittweise Wiederherstellung beginnt mit RESTORE DATABASE, wobei die Option PARTIAL verwendet wird und eine oder mehrere sekundäre Dateigruppen für die Wiederherstellung angegeben werden. Weitere Informationen finden Sie unter [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).  
  
-   Nur Wiederherstellung  
  
     Stellt Daten wieder her, die bereits konsistent mit der Datenbank sind und nur zur Verfügung gestellt werden müssen. Weitere Informationen finden Sie unter [Wiederherstellen einer Datenbank ohne Wiederherstellung von Daten &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
-   Wiederherstellung des Transaktionsprotokolls  
  
     Beim Modell der vollen oder massenprotokollierten Wiederherstellung ist die Wiederherstellung von Protokollsicherungen erforderlich, um den gewünschten Wiederherstellungspunkt zu erreichen. Weitere Informationen zum Wiederherstellen von protokollsicherungen finden Sie unter [Anwenden von Transaktionsprotokollsicherungen &#40; SQLServer &#41; ](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
-   Vorbereiten einer verfügbarkeitsdatenbank für eine Always On-verfügbarkeitsgruppe  
  
     Weitere Informationen finden Sie unter [Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
-   Vorbereiten einer Spiegeldatenbank für die Datenbankspiegelung  
  
     Weitere Informationen finden Sie unter [Vorbereiten einer Spiegeldatenbank auf die Spiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Onlinewiederherstellung  
  
    > **Hinweis:** onlinewiederherstellung ist nur in Enterprise-Edition von zulässig [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Wenn die Onlinewiederherstellung unterstützt wird und die Datenbank online ist, sind Datei- und Seitenwiederherstellungen automatisch Onlinewiederherstellungen. Dies gilt auch für Wiederherstellungen einer sekundären Dateigruppe nach der Anfangsphase einer schrittweisen Wiederherstellung.  
  
    > **Hinweis:** onlinewiederherstellungen können [verzögerte Transaktionen](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
     Weitere Informationen finden Sie unter [Onlinewiederherstellung &#40; SQLServer &#41; ](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
## <a name="additional-considerations-about-restore-options"></a>Weitere Überlegungen zu RESTORE-Optionen  
  
### <a name="discontinued-restore-keywords"></a>Nicht mehr unterstützte RESTORE-Schlüsselwörter  
 Die folgenden Schlüsselwörter werden in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] nicht mehr unterstützt:  
  
|Nicht mehr unterstütztes Schlüsselwort|Ersetzt durch...|Beispiel für Ersetzungsschlüsselwort|  
|--------------------------|------------------|------------------------------------|  
|LOAD|RESTORE|`RESTORE DATABASE`|  
|TRANSACTION|LOG|`RESTORE LOG`|  
|DBO_ONLY|RESTRICTED_USER|`RESTORE DATABASE ... WITH RESTRICTED_USER`|  
  
### <a name="restore-log"></a>RESTORE LOG  
 RESTORE LOG kann eine Dateiliste einschließen, um das Erstellen von Dateien bei einem Rollforward zu ermöglichen. Diese wird verwendet, wenn die Protokollsicherung Protokolleinträge enthält, die erstellt wurden, als der Datenbank eine Datei hinzugefügt wurde.  
  
> **Hinweis:** für eine Datenbank das vollständige oder massenprotokollierte Wiederherstellungsmodell verwenden, in den meisten Fällen müssen Sie sichern die Protokollfragment vor dem Wiederherstellen der Datenbank. Wenn eine Datenbank ohne vorherige Sicherung des Protokollfragments wiederhergestellt wird, tritt ein Fehler auf. Dies gilt nicht, wenn die RESTORE DATABASE-Anweisung die WITH REPLACE- oder die WITH STOPAT-Klausel enthält, in der eine Zeit oder Transaktion nach dem Ende der Datensicherung angegeben sein muss. Weitere Informationen zu Sicherungen des Protokollfragments finden Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
### <a name="comparison-of-recovery-and-norecovery"></a>Vergleich zwischen RECOVERY und NORECOVERY  
 Ein Rollback wird von der RESTORE-Anweisung über die Optionen [ RECOVERY | NORECOVERY ] gesteuert:  
  
-   NORECOVERY gibt an, dass kein Rollback erfolgt. Damit kann das Rollforward die nächste Anweisung in der Sequenz fortsetzen.  
  
     In diesem Fall können über die Wiederherstellungssequenz andere Sicherungen wiederhergestellt werden, und für diese kann ein Rollforward ausgeführt werden.  
  
-   RECOVERY (die Standardeinstellung) gibt an, dass das Rollback erst dann ausgeführt werden kann, wenn das Rollforward für die aktuelle Sicherung abgeschlossen ist.  
  
     Wiederherstellen der Datenbank erfordert, dass die gesamte Satz von Daten, die wiederhergestellt wird (die *rollforwardgruppe*) mit der Datenbank konsistent ist. Wenn das Rollforward für die Rollforwardgruppe nicht weit genug ausgeführt wurde, um die Konsistenz mit der Datenbank herzustellen, und wenn RECOVERY angegeben ist, dann gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus.  
  
## <a name="compatibility-support"></a>Kompatibilitätsunterstützung  
 Sicherungen von **master**, **Modell** und **Msdb** , die mit einer früheren Version erstellt wurden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann nicht wiederhergestellt werden, indem [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> **Hinweis:** keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sicherung wiederhergestellt werden, um eine frühere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als die Version auf dem die Sicherung erstellt wurde.  
  
 Jede Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet im Vergleich zu früheren Versionen jedoch einen anderen Standardpfad. Daher muss zum Wiederherstellen einer Datenbank, die am Standardort für Sicherungen in früheren Versionen erstellt wurde, die MOVE-Option verwendet werden. Informationen zum neuen Standardpfad finden Sie unter [Dateispeicherorte für Standard- und benannte Instanzen von SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Nachdem Sie eine Datenbank einer früheren Version in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wiederhergestellt haben, wird die Datenbank automatisch aktualisiert. In der Regel ist die Datenbank sofort verfügbar. Wenn eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbank aber Volltextindizes aufweist, werden diese beim Upgrade entweder importiert, zurückgesetzt oder neu erstellt, je nach der Einstellung der Servereigenschaft  **upgrade_option** . Wenn die Upgradeoption auf „Importieren“ (**upgrade_option** = 2) oder „Neu erstellen“ (**upgrade_option** = 0) festgelegt ist, sind die Volltextindizes während des Upgrades nicht verfügbar. Je nach Menge der indizierten Daten kann der Importvorgang mehrere Stunden dauern; die Neuerstellung sogar bis zu zehnmal länger. Wenn die Upgradeoption auf Importieren festgelegt ist und kein Volltextkatalog verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt. Um die Einstellung der Servereigenschaft **upgrade_option** zu ändern, verwenden Sie [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
 Wird eine Datenbank zum ersten Mal an eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angefügt oder wiederhergestellt, ist noch keine Kopie des Datenbank-Hauptschlüssels (verschlüsselt vom Diensthauptschlüssel) auf dem Server gespeichert. Der Datenbank-Hauptschlüssel (Database Master Key, DMK) muss mithilfe der Anweisung **OPEN MASTER KEY** entschlüsselt werden. Nachdem der Datenbank-Hauptschlüssel entschlüsselt wurde, können Sie für die Zukunft die automatische Entschlüsselung aktivieren, indem Sie die Anweisung **ALTER MASTER KEY REGENERATE** verwenden. Auf diese Weise können Sie eine Kopie des mit dem Diensthauptschlüssel (Service Master Key, SMK) verschlüsselten Datenbank-Hauptschlüssels für den Server bereitstellen. Wenn eine Datenbank von einer früheren Version aktualisiert wurde, sollte der DMK neu generiert werden, damit er den neueren AES-Algorithmus verwendet. Weitere Informationen zum Neugenerieren des DMK finden Sie unter [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). Die zum Neugenerieren des DMK zum Upgrade auf AES erforderliche Zeit hängt von der Anzahl der Objekte ab, die durch den DMK geschützt werden. Der DMK muss nur einmal auf AES aktualisiert und neu generiert werden. Dies hat keine Auswirkungen auf zukünftige Neugenerierungen im Rahmen einer Schlüsselrotationsstrategie.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Wenn bei einer Offlinewiederherstellung die angegebene Datenbank verwendet wird, zwingt RESTORE die Benutzer nach einer kurzen Verzögerung zum Beenden der Datenbankverwendung. Bei der Onlinewiederherstellung einer nicht primären Dateigruppe kann die Datenbank weiter verwendet werden, es sei denn, die zu wiederherstellende Dateigruppe wird offline geschaltet. Alle in der angegebenen Datenbank vorhandenen Daten werden durch die wiederhergestellten Daten ersetzt.  
  
 Weitere Informationen zur datenbankwiederherstellung finden Sie unter [wiederherstellen und Übersicht über Wiederherstellungsvorgänge &#40; SQLServer &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
 Wiederherstellungsvorgänge über Plattformen hinweg, sogar zwischen unterschiedlichen Prozessortypen, können ausgeführt werden, solange die Sortierung der Datenbank vom Betriebssystem unterstützt wird.  
  
 RESTORE kann nach einem Fehler neu gestartet werden. Außerdem können Sie RESTORE anweisen, den Vorgang auch bei Fehlern fortzusetzen und so viele Daten wie möglich wiederherzustellen (siehe die Option CONTINUE_AFTER_ERROR).  
  
 RESTORE ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
 Wiederherstellen einer beschädigten **master** Datenbank ist eine spezielle Vorgehensweise ausgeführt. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
 Durch das Wiederherstellen einer Datenbank wird der Plancache für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht. Durch das Löschen des Plancaches wird eine Neukompilierung aller nachfolgenden Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. Für jeden gelöschten Cachespeicher im Plancache enthält das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll folgende Informationsmeldung: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat für den %s-Cachespeicher (Bestandteil des Plancache) %d Leerungen des Cachespeichers gefunden, die von Datenbankwartungs- oder Neukonfigurierungsvorgängen ausgelöst wurden". Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.  
  
 Um eine Verfügbarkeitsdatenbank wiederherzustellen, stellen Sie zuerst die Datenbank mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wieder her, und fügen Sie dann die Datenbank der Verfügbarkeitsgruppe hinzu.  
  
## <a name="interoperability"></a>Interoperabilität  
  
### <a name="database-settings-and-restoring"></a>Datenbankeinstellungen und -wiederherstellung  
 Bei einer Wiederherstellung werden die meisten Datenbankoptionen, die mit ALTER DATABASE festgelegt werden können, auf die Werte zurückgesetzt, die am Ende der Sicherung gültig waren.  
  
 Durch die Verwendung der Option WITH RESTRICTED_USER wird dieses Verhalten jedoch für die Einstellung der Benutzerzugriffsoption überschrieben. Diese Einstellung wird immer im Anschluss an eine RESTORE-Anweisung festgelegt, die die Option WITH RESTRICTED_USER einschließt.  
  
### <a name="restoring-an-encrypted-database"></a>Wiederherstellen einer verschlüsselten Datenbank  
 Um eine verschlüsselte Datenbank wiederherstellen zu können, muss das Zertifikat oder der asymmetrische Schlüssel verfügbar sein, das oder der zum Verschlüsseln der Datenbank verwendet wurde. Ohne das Zertifikat oder den asymmetrischen Schlüssel kann die Datenbank nicht wiederhergestellt werden. Darum muss das Zertifikat, das zur Verschlüsselung des Verschlüsselungsschlüssels für die Datenbank verwendet wurde, so lange beibehalten werden, wie die Sicherung benötigt wird. Weitere Informationen finden Sie unter [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
### <a name="restoring-a-database-enabled-for-vardecimal-storage"></a>Wiederherstellen einer für vardecimal-Speicher aktivierten Datenbank  
 Sicherung und Wiederherstellung funktionieren ordnungsgemäß mit der **Vardecimal** Speicherformat. Weitere Informationen zu **Vardecimal** Speicherformat, finden Sie unter [Sp_db_vardecimal_storage_format &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md).  
  
### <a name="restore-full-text-data"></a>Wiederherstellen von Volltextdaten  
 Bei einer vollständigen Wiederherstellung werden Volltextdaten zusammen mit anderen Datenbankdaten wiederhergestellt. Beim Verwenden der normalen Syntax `RESTORE DATABASE database_name FROM backup_device` erfolgt die Wiederherstellung der Volltextdateien bei der Wiederherstellung der Datenbankdateien.  
  
 Die RESTORE-Anweisung kann auch für folgende Wiederherstellungen verwendet werden: Wiederherstellungen auf alternativen Speicherorten, differenzielle Wiederherstellungen, Datei- und Dateigruppenwiederherstellungen sowie differenzielle Datei- und Dateigruppenwiederherstellungen von Volltextdaten. Darüber hinaus können mit RESTORE Volltextdateien ohne oder mit Datenbankdaten wiederhergestellt werden.  
  
> **Hinweis:** -Volltextkataloge aus importierten [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] werden immer noch als Datenbankdateien behandelt. Für diese findet weiterhin die [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Prozedur zur Sicherung von Volltextkatalogen Anwendung. Das Anhalten und Fortsetzen des Sicherungsvorgangs ist jedoch nicht mehr erforderlich. Weitere Informationen finden Sie unter [sichern und Wiederherstellen von Volltextkatalogen](http://go.microsoft.com/fwlink/?LinkId=107381).  
  
## <a name="metadata"></a>Metadaten  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält Tabellen mit Sicherungs- und Wiederherstellungsverlauf, in denen die Sicherungs- und Wiederherstellungsaktivität für jede Serverinstanz nachverfolgt wird. Beim Ausführen einer Wiederherstellung werden auch die Tabellen mit Sicherungsverläufen geändert. Informationen zu diesen Tabellen finden Sie unter [Sicherungsverlauf und Headerinformationen &#40; SQLServer &#41; ](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md).  
  
##  <a name="REPLACEoption"></a>Ersetzen Sie die Option Auswirkungen  
 REPLACE sollte nur selten verwendet werden und nur nach sorgfältiger Überlegung. Die Wiederherstellung verhindert normalerweise, dass eine Datenbank versehentlich durch eine andere Datenbank überschrieben wird. Wenn die in einer RESTORE-Anweisung angegebene Datenbank bereits auf dem aktuellen Server vorhanden ist und sich die angegebene GUID der Datenbankfamilie von der im Sicherungssatz aufgezeichneten GUID der Datenbankfamilie unterscheidet, wird die Datenbank nicht wiederhergestellt. Dies ist ein wichtiges Sicherheitselement.  
  
 Die Option REPLACE überschreibt verschiedene wichtige Sicherheitsprüfungen, die die Wiederherstellung normalerweise ausführt. Folgende Prüfungen werden überschrieben:  
  
-   Wiederherstellung über eine vorhandene Datenbank mit einer von einer anderen Datenbank erstellten Sicherung.  
  
     Mit der Option REPLACE ermöglicht die Wiederherstellung das Überschreiben einer vorhandenen Datenbank mit einer beliebigen im Sicherungssatz enthaltenen Datenbank, selbst wenn der angegebene Datenbankname sich von dem im Sicherungssatz aufgezeichneten Datenbanknamen unterscheidet. Dies kann zur Folge haben, dass eine Datenbank versehentlich durch eine andere Datenbank überschrieben wird.  
  
-   Wiederherstellung über eine Datenbank mithilfe des vollständigen oder massenprotokollierten Wiederherstellungsmodells, wobei keine Sicherung des Protokollfragments erstellt wurde und die Option STOPAT nicht verwendet wird.  
  
     Mit der Option REPLACE können Sie Arbeit verlieren, für die ein Commit ausgeführt wurde, da das zuletzt geschriebene Protokoll nicht gesichert wurde.  
  
-   Überschreiben von vorhandenen Dateien.  
  
     Beispielsweise könnten irrtümlicherweise Dateien des falschen Typs (z. B. XLS-Dateien) oder Dateien, die von einer anderen Datenbank verwendet werden, die zurzeit nicht online ist, überschrieben werden. Willkürliche Datenverluste sind möglich, wenn vorhandene Dateien überschrieben werden, auch wenn die wiederhergestellte Datenbank vollständig ist.  
  
## <a name="redoing-a-restore"></a>Wiederholen einer Wiederherstellung  
 Eine Wiederherstellung kann nicht rückgängig gemacht werden. Sie können jedoch die Auswirkungen des Datenkopiervorgangs und des Rollforwards negieren, indem Sie noch einmal beginnen und pro Datei vorgehen. Um noch einmal zu starten, stellen Sie die gewünschte Datei wieder her und führen dann erneut das Rollforward aus. Wenn Sie beispielsweise versehentlich zu viele Protokollsicherungen wiederhergestellt haben und über den beabsichtigten Endpunkt hinausgegangen sind, müssen Sie die Sequenz neu starten.  
  
 Eine Wiederherstellungssequenz kann abgebrochen und neu gestartet werden, indem der gesamte Inhalt der betroffenen Dateien wiederhergestellt wird.  
  
## <a name="reverting-a-database-to-a-database-snapshot"></a>Wiederherstellen einer Datenbank aus einer Datenbank-Momentaufnahme  
 Ein *Datenbank-Wiederherstellungsvorgang* (angegeben mithilfe der Option DATABASE_SNAPSHOT) nimmt eine vollständige Quelldatenbank wieder Zeit vom Zeitpunkt des Datenbank-Momentaufnahme wiederherstellen, d. h. die Quelldatenbank mit Daten von dem Zeitpunkt überschrieben Zeitpunkt in der angegebenen Datenbank-Momentaufnahme beibehalten. Derzeit darf nur die Momentaufnahme vorhanden sein, aus der Sie die Datenbank wiederherstellen. Bei diesem Wiederherstellungsvorgang wird das Protokoll neu erstellt (deshalb können Sie für eine wiederhergestellte Datenbank später kein Rollforward bis zum Punkt des Benutzerfehlers durchführen).  
  
 Der Datenverlust beschränkt sich auf Updates der Datenbank, die nach der Erstellung der Momentaufnahme vorgenommen wurden. Die Metadaten einer wiederhergestellten Datenbank sind dieselben wie die Metadaten zum Zeitpunkt der Momentaufnahmeerstellung. Durch das Wiederherstellen einer Momentaufnahme werden jedoch alle Volltextkataloge gelöscht.  
  
 Die Wiederherstellung von einer Datenbankmomentaufnahme ist nicht für die Medienwiederherstellung vorgesehen. Im Gegensatz zu einem normalen Sicherungssatz ist die Datenbankmomentaufnahme eine unvollständige Kopie der Datenbankdateien. Wenn die Datenbank oder die Datenbankmomentaufnahme beschädigt ist, ist die Wiederherstellung von einer Momentaufnahme vermutlich unmöglich. Darüber hinaus auch nach Möglichkeit eine Wiederherstellung ist im Falle einer Beschädigung es unwahrscheinlich, dass das Problem zu beheben.  
  
### <a name="restrictions-on-reverting"></a>Einschränkungen zur Wiederherstellung  
 Die Wiederherstellung wird unter folgenden Bedingungen nicht unterstützt:  
  
-   Die Quelldatenbank enthält schreibgeschützte oder komprimierte Dateigruppen.  
  
-   Mindestens eine Datei ist offline, die beim Erstellen der Momentaufnahme online war.  
  
-   Derzeit ist mehr als eine Momentaufnahme der Datenbank vorhanden.  
  
 Weitere Informationen finden Sie unter [Wiederherstellen einer Datenbank zu einer Datenbank-Momentaufnahme](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md).  
  
## <a name="security"></a>Sicherheit  
 Bei einem Sicherungsvorgang können optional Kennwörter für einen Mediensatz, einen Sicherungssatz oder für beides angegeben werden. Wurde ein Kennwort für einen Mediensatz oder Sicherungssatz definiert, müssen die richtigen Kennwörter in der RESTORE-Anweisung angegeben werden. Über diese Kennwörter werden nicht autorisierte Wiederherstellungsoptionen und unbefugtes Anfügen von Sicherungssätzen an Medien mithilfe der Tools von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verhindert. Kennwortgeschützte Medien können nicht mit der Option FORMAT der BACKUP-Anweisung überschrieben werden.  
  
> [!IMPORTANT]  
>  Dieses Kennwort bietet also nur unzureichenden Schutz. Es soll vermeiden, dass autorisierte wie nicht autorisierte Benutzer mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tools fehlerhafte Wiederherstellungen durchführen. Es verhindert jedoch nicht das Lesen der Sicherungsdaten mit anderen Mitteln oder das Ersetzen des Kennworts. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Die bewährte Methode für den Schutz von Sicherungen werden verwahren von Sicherungsbändern an einem sicheren Ort oder Sichern in Datenträgerdateien, die durch ausreichend Zugriffssteuerungslisten (ACLs) geschützt sind. Die ACLs sollten für den Verzeichnisstamm eingerichtet werden, unter dem die Sicherungen erstellt werden.  
>   
>  Informationen zu SQL Server-Sicherung und-Wiederherstellung mit Windows Azure-Blob-Speicher finden Sie unter [SQL Server-Sicherung und-Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="permissions"></a>Berechtigungen  
 Ist die wiederherzustellende Datenbank nicht vorhanden, muss der Benutzer über CREATE DATABASE-Berechtigungen verfügen, um RESTORE ausführen zu können. Ist die Datenbank vorhanden, werden RESTORE-Berechtigungen standardmäßig den Mitgliedern der festen Serverrollen **sysadmin** und **dbcreator** sowie dem Besitzer (**dbo**) der Datenbank erteilt (für die Option FROM DATABASE_SNAPSHOT ist die Datenbank immer vorhanden).  
  
 RESTORE-Berechtigungen werden Rollen erteilt, in denen Mitgliedsinformationen immer für den Server verfügbar sind. Da die Mitgliedschaft in einer festen Datenbankrolle nur geprüft werden kann, wenn die Datenbank unbeschädigt ist und auf sie zugegriffen werden kann, was beim Ausführen von RESTORE nicht immer der Fall ist, verfügen Mitglieder der festen Datenbankrolle **db_owner** nicht über RESTORE-Berechtigungen.  
  
##  <a name="examples"></a> Beispiele  
 Bei allen Beispielen wird davon ausgegangen, dass eine vollständige Datenbanksicherung ausgeführt wurde.  
  
 Die Beispiele zu RESTORE schließen Folgendes ein:  
  
-   A. [Wiederherstellen einer vollständigen Datenbank](#restoring_full_db)  
  
-   B. [Vollständige und differenzielle datenbanksicherungen wiederherstellen](#restoring_full_n_differential_db_backups)  
  
-   C. [Wiederherstellen einer Datenbank mit der RESTART-syntax](#restoring_db_using_RESTART)  
  
-   D. [Wiederherstellen einer Datenbank und Verschieben von Dateien](#restoring_db_n_move_files)  
  
-   E. [Kopieren einer Datenbank mithilfe der Sicherung und Wiederherstellung](#copying_db_using_bnr)  
  
-   F. [Wiederherstellen eines bestimmten Zeitpunkts mithilfe von STOPAT](#restoring_to_pit_using_STOPAT)  
  
-   G. [Wiederherstellen eines Transaktionsprotokolls bis zu einer Markierung](#restoring_transaction_log_to_mark)  
  
-   H. [Wiederherstellen mit der TAPE-syntax](#restoring_using_TAPE)  
  
-   I. [Wiederherstellen mit der File- und FILEGROUP-syntax](#restoring_using_FILE_n_FG)  
  
-   J. [Wiederherstellen aus einer Datenbankmomentaufnahme](#reverting_from_db_snapshot)  
  
-   K. [Wiederherstellen aus dem Microsoft Azure Blob-Speicherdienst](#Azure_Blob)  
  
> **Hinweis:** zusätzliche Beispiele finden Sie die Restore-Themen, die aufgelisteten [wiederherstellen und Übersicht über Wiederherstellungsvorgänge &#40; SQLServer &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
###  <a name="restoring_full_db"></a> A. Wiederherstellen einer vollständigen Datenbank  
 Im folgenden Beispiel wird eine vollständige Datenbanksicherung vom logischen Sicherungsmedium `AdventureWorksBackups` wiederhergestellt. Ein Beispiel zum Erstellen dieses Mediums finden Sie unter [Sicherungsmedien](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorks2012Backups;  
```  
  
> **Hinweis:** für eine Datenbank mit der vollständigen oder massenprotokollierten Wiederherstellungsmodell [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert in den meisten Fällen, die Sie das Protokollfragment sichern, bevor die Datenbank wiederhergestellt. Weitere Informationen finden Sie unter [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="restoring_full_n_differential_db_backups"></a> B. Wiederherstellung von vollständigen und von differenziellen Datenbanksicherungen  
 Im folgenden Beispiel wird eine vollständige Datenbanksicherung und anschließend eine differenzielle Sicherung vom `Z:\SQLServerBackups\AdventureWorks2012.bak`-Sicherungsmedium wiederhergestellt, das beide Sicherungen enthält. Die vollständige Datenbanksicherung, die wiederhergestellt werden soll, ist der sechste Sicherungssatz auf dem Medium (`FILE = 6`). Die differenzielle Sicherung ist der neunte Sicherungssatz auf dem Medium (`FILE = 9`). Sobald die differenzielle Sicherung wiederhergestellt wird, wird die Datenbank wiederhergestellt.  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 6  
      NORECOVERY;  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak'  
   WITH FILE = 9  
      RECOVERY;  
```  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="restoring_db_using_RESTART"></a> C. Wiederherstellen einer Datenbank mit der RESTART-Syntax  
 Im folgenden Beispiel wird die Option `RESTART` zum Neustart eines `RESTORE`-Vorgangs verwendet, der durch einen Stromausfall des Servers unterbrochen wurde.  
  
```  
-- This database RESTORE halted prematurely due to power failure.  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups;  
-- Here is the RESTORE RESTART operation.  
RESTORE DATABASE AdventureWorks2012   
   FROM AdventureWorksBackups WITH RESTART;  
```  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="restoring_db_n_move_files"></a> D. Wiederherstellen einer Datenbank und Verschieben von Dateien  
 Im folgenden Beispiel wird eine vollständige Datenbank und ein Transaktionsprotokoll wiederhergestellt. Anschließend wird die wiederhergestellte Datenbank in das Verzeichnis `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data` verschoben.  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH NORECOVERY,   
      MOVE 'AdventureWorks2012_Data' TO   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.mdf',   
      MOVE 'AdventureWorks2012_Log'   
TO 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\NewAdvWorks.ldf';  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH RECOVERY;  
```  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="copying_db_using_bnr"></a> E. Kopieren einer Datenbank mithilfe von BACKUP und RESTORE  
 Im folgenden Beispiel werden die Anweisungen `BACKUP` und `RESTORE` verwendet, um eine Kopie der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank zu erstellen. Die `MOVE`-Anweisung bewirkt, dass die Daten- und die Protokolldatei an den angegebenen Speicherorten wiederhergestellt werden. Die `RESTORE FILELISTONLY`-Anweisung wird verwendet, um die Anzahl und die Namen der Dateien der Datenbank zu bestimmen, die wiederhergestellt werden. Die neue Kopie der Datenbank erhält den Namen `TestDB`. Weitere Informationen finden Sie unter [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups ;  
  
RESTORE FILELISTONLY   
   FROM AdventureWorksBackups ;  
  
RESTORE DATABASE TestDB   
   FROM AdventureWorksBackups   
   WITH MOVE 'AdventureWorks2012_Data' TO 'C:\MySQLServer\testdb.mdf',  
   MOVE 'AdventureWorks2012_Log' TO 'C:\MySQLServer\testdb.ldf';  
GO  
```  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="restoring_to_pit_using_STOPAT"></a> F. Wiederherstellen eines bestimmten Zeitpunkts mithilfe von STOPAT  
 Im folgenden Beispiel wird eine Datenbank in den am `12:00 AM` um `April 15, 2020` bestehenden Status wiederhergestellt und ein Wiederherstellungsvorgang gezeigt, der mehrere Protokollsicherungen umfasst. Auf dem Sicherungsmedium ( `AdventureWorksBackups`) ist die wiederherzustellende vollständige Datenbanksicherung der dritte Sicherungssatz (`FILE = 3`), die erste Protokollsicherung ist der vierte Sicherungssatz (`FILE = 4`), und die zweite Protokollsicherung ist der fünfte Sicherungssatz (`FILE = 5`).  
  
```  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks2012 WITH RECOVERY;  
  
```  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="restoring_transaction_log_to_mark"></a> G. Wiederherstellen eines Transaktionsprotokolls bis zu einer Markierung  
 Im folgenden Beispiel wird das Transaktionsprotokoll bis zur Markierung in der markierten Transaktion mit dem Namen `ListPriceUpdate`wiederhergestellt.  
  
```  
USE AdventureWorks2012  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master;  
GO  
  
RESTORE DATABASE AdventureWorks2012  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'UPDATE Product list prices';  
```  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="restoring_using_TAPE"></a> H. Wiederherstellen mit der TAPE-Syntax  
 Im folgenden Beispiel wird eine vollständige Datenbanksicherung von einem `TAPE`-Sicherungsmedium wiederhergestellt.  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM TAPE = '\\.\tape0';  
```  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="restoring_using_FILE_n_FG"></a> I. Wiederherstellen mithilfe der FILE- und FILEGROUP-Syntax  
 Im folgenden Beispiel wird eine Datenbank mit dem Namen `MyDatabase` wiederhergestellt, die über zwei Dateien, eine sekundäre Dateigruppe und ein Transaktionsprotokoll verfügt. Für die Datenbank wird das vollständige Wiederherstellungsmodell verwendet.  
  
 Die Datenbanksicherung ist der neunte Sicherungssatz im Mediensatz auf einem logischen Sicherungsmedium mit dem Namen `MyDatabaseBackups`. Anschließend werden drei Protokollsicherungen, die sich in den nächsten drei Sicherungssätzen (`10`, `11` und `12`) im Medium `MyDatabaseBackups` befinden, mit `WITH NORECOVERY` wiederhergestellt. Nach dem Wiederherstellen der letzten Protokollsicherung wird die Datenbank wiederhergestellt.  
  
> **Hinweis:** Wiederherstellung als separater Schritt reduziert die Möglichkeit, dass Sie zu früh ausgeführt wird, bevor Sie das gesamte Protokoll Sicherungen wiederhergestellt wurde.  
  
 Beachten Sie, dass in der `RESTORE DATABASE`-Anweisung zwei Typen von `FILE`-Optionen vorhanden sind. Mit den `FILE`-Optionen vor dem Namen des Sicherungsmediums werden die logischen Dateinamen der Datenbankdateien angegeben, die aus dem Sicherungssatz wiederhergestellt werden sollen, beispielsweise `FILE = 'MyDatabase_data_1'`. Dieser Sicherungssatz ist nicht die erste Datenbanksicherung im Mediensatz. Daher wird seine Position im Mediensatz mit der Option `FILE` in der `WITH`-Klausel angegeben: `FILE=9`.  
  
```  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'new_customers'  
   FROM MyDatabaseBackups  
   WITH   
      FILE = 9,  
      NORECOVERY;  
GO  
-- Restore the log backups.  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 10,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 11,   
      NORECOVERY;  
GO  
RESTORE LOG MyDatabase  
   FROM MyDatabaseBackups  
   WITH FILE = 12,   
      NORECOVERY;  
GO  
--Recover the database:  
RESTORE DATABASE MyDatabase WITH RECOVERY;  
GO  
```  
  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="reverting_from_db_snapshot"></a> J. Wiederherstellen aus einer Datenbank-Momentaufnahme  
 Im folgenden Beispiel wird eine Datenbank aus einer Datenbank-Momentaufnahme wiederhergestellt. In diesem Beispiel wird davon ausgegangen, dass derzeit in der Datenbank nur eine Momentaufnahme vorhanden ist. Ein Beispiel zum Erstellen dieser Datenbankmomentaufnahme finden Sie unter [Erstellen einer Datenbankmomentaufnahme &#40; Transact-SQL &#41; ](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md).  
  
> **Hinweis:** Reverting zu einer Momentaufnahme löscht alle Volltextkataloge.  
  
```  
USE master;    
RESTORE DATABASE AdventureWorks2012 FROM DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
 Weitere Informationen finden Sie unter [Wiederherstellen einer Datenbank zu einer Datenbank-Momentaufnahme](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md).  

 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
###  <a name="Azure_Blob"></a> K. Wiederherstellen aus dem Microsoft Azure Blob-Speicherdienst  
Die folgenden drei Beispiele umfassen die Verwendung des Microsoft Azure Storage-Diensts.  Der Speicherkontoname lautet `mystorageaccount`.  Der Container für Datendateien heißt `myfirstcontainer`.  Der Container für Sicherungsdateien heißt `mysecondcontainer`.  Eine gespeicherte Zugriffsrichtlinie wurde mit Lese-, Schreib-, löschen und Liste Rechte für jeden Container erstellt wurde.  SQL Server-Anmeldeinformationen erstellt wurden, mithilfe der Shared Access Signatures, die die gespeicherte Zugriffsrichtlinien zugeordnet sind.  Informationen zu SQL Server-Sicherung und-Wiederherstellung mit dem Microsoft Azure Blob-Speicher finden Sie unter [SQL Server-Sicherung und-Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  

**K1.  Stellen Sie eine vollständige datenbanksicherung wieder her, aus dem Microsoft Azure-Speicherdienst**  
Eine vollständige datenbanksicherung finden Sie unter `mysecondcontainer`, der `Sales` wird wiederhergestellt werden, um `myfirstcontainer`.  `Sales`derzeit vorhanden nicht auf dem Server. 
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```

**K2. Wiederherstellen einer vollständigen datenbanksicherung aus dem Microsoft Azure-Speicherdienst in den lokalen Speicher**  
Eine vollständige datenbanksicherung controllerarbeitsverzeichnis `mysecondcontainer`, der `Sales` wird in den lokalen Speicher wiederhergestellt werden.  `Sales`derzeit vorhanden nicht auf dem Server.
```
RESTORE DATABASE Sales
  FROM URL = 'https://mystorageaccount.blob.core.windows.net/mysecondcontainer/Sales.bak'   
  WITH  MOVE 'Sales_Data1' to 'H:\DATA\Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'O:\LOG\Sales_log.ldf', 
  STATS = 10;
```
  
**K3. Wiederherstellen einer vollständigen datenbanksicherung aus dem lokalen Speicher an den Microsoft Azure Storage-Dienst**  
```
RESTORE DATABASE Sales
  FROM DISK = 'E:\BAK\Sales.bak'
  WITH  MOVE 'Sales_Data1' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_Data1.mdf', 
  MOVE 'Sales_log' to 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_log.ldf', 
  STATS = 10;
```  
  

  
 [&#91; Der Anfang des Beispiele &#93;](#examples)  
  
## <a name="much-more-information"></a>Viele weitere Informationen.  
 - [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md) 
- [Sichern und Wiederherstellen von Systemdatenbanken (SQLServer)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md) 
 - [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
 - [Sichern und Wiederherstellen von Volltextkatalogen und Indizes](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 - [Sichern und Wiederherstellen von replizierten Datenbanken](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 - [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 - [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 - [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 - [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 - [RESTORE FILELISTONLY (Transact-SQL)](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
 - [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
 - [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
