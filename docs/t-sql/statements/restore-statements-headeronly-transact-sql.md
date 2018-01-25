---
title: RESTORE HEADERONLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/07/2016
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
- HEADERONLY
- RESTORE HEADERONLY
- RESTORE_HEADERONLY_TSQL
- HEADERONLY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backup sets [SQL Server], header information
- headers [SQL Server]
- RESTORE HEADERONLY statement
- backup header information [SQL Server]
ms.assetid: 4b88e98c-49c4-4388-ab0e-476cc956977c
caps.latest.revision: "95"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 840793c4bbfee8282676cf90d42d6e7a6c4d6b42
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements---headeronly-transact-sql"></a>RESTORE-Anweisungen - HEADERONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt ein Resultset mit allen Sicherungsheaderinformationen für alle Sicherungssätze auf einem bestimmten Sicherungsmedium in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
> [!NOTE]  
>  Die Beschreibungen der Argumente finden Sie [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RESTORE HEADERONLY   
FROM <backup_device>   
[ WITH   
 {  
--Backup Set Options  
   FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 Beschreibungen der RESTORE HEADERONLY-Argumente finden Sie unter [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>Resultsets  
 Zu jeder Sicherung auf dem jeweiligen Medium sendet der Server eine Zeile mit Headerinformationen, die aus den folgenden Spalten besteht:  
  
> [!NOTE]  
>  RESTORE HEADERONLY liest alle Sicherungssätze auf dem Medium. Beim Verwenden von Bandlaufwerken mit hoher Kapazität kann die Erstellung dieses Resultsets daher eine gewisse Zeit in Anspruch nehmen. Um einen kurzen Blick auf den Medien zu erhalten, ohne das Abrufen von Informationen zu jedem Sicherungssatz RESTORE LABELONLY verwenden, oder geben Sie die Datei **=** *Backup_set_file_number*.  
  
> [!NOTE]  
>  Aufgrund der Natur der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format, es ist möglich für Sicherungssätze anderer Softwareprogramme Speicherplatz auf demselben Medium wie belegen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sicherungssätze. Das von RESTORE HEADERONLY zurückgegebene Resultset schließt eine Zeile für jeden dieser anderen Sicherungssätze ein.  
  
|Spaltenname|Datentyp|Beschreibung für SQL Server-Sicherungssätze|  
|-----------------|---------------|--------------------------------------------|  
|**BackupName**|**nvarchar(128)**|Name des Sicherungssatzes.|  
|**BackupDescription**|**nvarchar(255)**|Beschreibung des Sicherungssatzes.|  
|**BackupType**|**smallint**|Sicherungstyp:<br /><br /> **1** = Datenbank<br /><br /> **2** = Transaktionsprotokoll<br /><br /> **4** = Datei<br /><br /> **5** = Datenbank differenziell<br /><br /> **6** = Datei differenziell<br /><br /> **7** = teilweise<br /><br /> **8** = teilweise differenziell|  
|**ExpirationDate**|**datetime**|Ablaufdatum für den Sicherungssatz.|  
|**Komprimiert**|**BYTE(1)**|Ob der Sicherungssatz mit der softwarebasierten Kompression komprimiert wird.<br /><br /> **0** = Nein<br /><br /> **1** = Ja|  
|**Position**|**smallint**|Position des Sicherungssatzes auf dem Volume (Verwendung mit der Option FILE =).|  
|**DeviceType**|**tinyint**|Zahl, die dem für den Sicherungsvorgang verwendeten Medientyp entspricht.<br /><br /> Datenträger:<br /><br /> **2** = logisch<br /><br /> **102** = physisch<br /><br /> Band:<br /><br /> **5** = logisch<br /><br /> **105** = physisch<br /><br /> Virtuelles Medium:<br /><br /> **7** = logisch<br /><br /> **107** = physisch<br /><br /> Logisches Gerätenamen und Nummern werden **backup_devices**; Weitere Informationen finden Sie unter [backup_devices &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md).|  
|**UserName**|**nvarchar(128)**|Name des Benutzers, der den Sicherungsvorgang ausgeführt hat.|  
|**ServerName**|**nvarchar(128)**|Name des Servers, der den Sicherungssatz geschrieben hat.|  
|**DatabaseName**|**nvarchar(128)**|Name der Datenbank, die gesichert wurde.|  
|**DatabaseVersion**|**int**|Version der Datenbank, von der die Sicherung erstellt wurde.|  
|**DatabaseCreationDate**|**datetime**|Datum und Uhrzeit der Erstellung der Datenbank.|  
|**BackupSize**|**numeric(20,0)**|Größe der Sicherung in Bytes.|  
|**FirstLSN**|**numeric(25,0)**|Protokollfolgenummer des ersten Protokolldatensatzes im Sicherungssatz.|  
|**LastLSN**|**numeric(25,0)**|Protokollfolgenummer des nächsten Protokolldatensatzes nach dem Sicherungssatz.|  
|**CheckpointLSN**|**numeric(25,0)**|Protokollsequenznummer des letzten Prüfpunkts zum Zeitpunkt der Erstellung der Sicherung.|  
|**DatabaseBackupLSN**|**numeric(25,0)**|Protokollsequenznummer der neuesten vollständigen Datenbanksicherung.<br /><br /> **DatabaseBackupLSN** ist der "des Prüfpunkts", das ausgelöst wird, wenn die Sicherung gestartet wird. Dieser LSN stimmt mit **FirstLSN** , wenn die Sicherung erstellt wird, wenn die Datenbank sich im Leerlauf befindet und keine Replikation konfiguriert ist.|  
|**BackupStartDate**|**datetime**|Datum und Uhrzeit des Beginns des Sicherungsvorgangs.|  
|**BackupFinishDate**|**datetime**|Datum und Uhrzeit des Endes des Sicherungsvorgangs.|  
|**SortOrder**|**smallint**|Sortierreihenfolge für den Server. Diese Spalte gilt nur für Datenbanksicherungen. Dieser Parameter wird aus Gründen der Abwärtskompatibilität bereitgestellt.|  
|**CodePage**|**smallint**|Servercodepage; das ist der vom Server verwendete Zeichensatz.|  
|**UnicodeLocaleId**|**int**|Serverseitige Konfigurationsoptionen für die Unicode-Gebietsschema-ID, die für die Sortierung von Unicode-Zeichendaten verwendet wird. Dieser Parameter wird aus Gründen der Abwärtskompatibilität bereitgestellt.|  
|**UnicodeComparisonStyle**|**int**|Serverseitige Konfigurationsoption für die Unicode-Vergleichsart, die zusätzliche Steuerungsmöglichkeiten im Vergleich zur Sortierung von Unicode-Daten bereitstellt. Dieser Parameter wird aus Gründen der Abwärtskompatibilität bereitgestellt.|  
|**CompatibilityLevel**|**tinyint**|Einstellung des Kompatibilitätsgrades der Datenbank, von der aus die Sicherung erstellt wurde.|  
|**SoftwareVendorId**|**int**|ID des Softwareanbieters. Für SQL Server, diese Nummer ist **4608** (oder im Hexadezimalformat **0 x 1200**).|  
|**SoftwareVersionMajor**|**int**|Wichtigste Versionsnummer des Servers, der den Sicherungssatz erstellt hat.|  
|**SoftwareVersionMinor**|**int**|Untergeordnete Versionsnummer des Servers, der den Sicherungssatz erstellt hat.|  
|**SoftwareVersionBuild**|**int**|Buildnummer des Servers, der den Sicherungssatz erstellt hat.|  
|**MachineName**|**nvarchar(128)**|Name des Computers, der den Sicherungsvorgang ausgeführt hat.|  
|**Flags**|**int**|Wenn einzelnen Flagbits festgelegt **1**:<br /><br /> **1** Protokoll = Sicherung enthält massenprotokollierte Vorgänge.<br /><br /> **2** = momentaufnahmesicherung.<br /><br /> **4** = Datenbank war zum Zeitpunkt der Sicherung schreibgeschützt.<br /><br /> **8** = Datenbank wurde in den Einzelbenutzermodus, Zeitpunkt der Sicherung.<br /><br /> **16** = Sicherung enthält sicherungsprüfsummen.<br /><br /> **32** = Datenbank wurde beschädigt, wenn gesichert, aber der Sicherungsvorgang trotz Fehlern fortgesetzt angefordert wurde.<br /><br /> **64** = Sicherung des Protokollfragments.<br /><br /> **128** = Sicherung des Protokollfragments mit unvollständigen Metadaten.<br /><br /> **256** = Sicherung des Protokollfragments mithilfe von WITH NORECOVERY.<br /><br /> **Wichtig:** es wird empfohlen, anstelle von **Flags** verwenden Sie die einzelnen booleschen Spalten (weiter unten aufgeführten **HasBulkLoggedData** und endend mit  **IsCopyOnly**).|  
|**BindingID**|**uniqueidentifier**|Bindungs-ID für die Datenbank. Dies entspricht **sys.database_recovery_status***database_guid**. Wenn eine Datenbank wiederhergestellt wird, wird ein neuer Wert zugewiesen. Siehe auch **FamilyGUID** (siehe unten).|  
|**RecoveryForkID**|**uniqueidentifier**|ID für den letzten Wiederherstellungs-Verzweigungspunkt. Diese Spalte entspricht **Last_recovery_fork_guid** in der [Backupset](../../relational-databases/system-tables/backupset-transact-sql.md) Tabelle.<br /><br /> Bei datensicherungen ist **RecoveryForkID** gleich **FirstRecoveryForkID**.|  
|**Sortierung**|**nvarchar(128)**|Die von der Datenbank verwendete Sortierung.|  
|**FamilyGUID**|**uniqueidentifier**|ID der ursprünglichen Datenbank zum Zeitpunkt der Erstellung. Der Wert bleibt unverändert, wenn die Datenbank wiederhergestellt wird.|  
|**HasBulkLoggedData**|**bit**|**1** = protokollsicherung enthält massenprotokollierte Vorgänge.|  
|**IsSnapshot**|**bit**|**1** = momentaufnahmesicherung.|  
|**IsReadOnly**|**bit**|**1** = Datenbank war zum Zeitpunkt der Sicherung schreibgeschützt.|  
|**IsSingleUser**|**bit**|**1** = Datenbank war Einzelbenutzer-Zeitpunkt der Sicherung.|  
|**HasBackupChecksums**|**bit**|**1** = Sicherung enthält sicherungsprüfsummen.|  
|**IsDamaged**|**bit**|**1** = Datenbank wurde beschädigt, wenn gesichert, aber der Sicherungsvorgang trotz Fehlern fortgesetzt angefordert wurde.|  
|**BeginsLogChain**|**bit**|**1** = Dies ist die erste in einer kontinuierlichen Kette von protokollsicherungen. Eine Protokollkette beginnt mit der ersten Protokollsicherung, die erstellt wurde, nachdem die Datenbank erstellt wurde oder nachdem ein Wechsel vom einfachen zum vollständigen oder massenprotokollierten Wiederherstellungsmodell erfolgt ist.|  
|**HasIncompleteMetaData**|**bit**|**1** = eine Sicherung des Protokollfragments mit unvollständigen Metadaten.<br /><br /> Weitere Informationen zu Sicherungen des Protokollfragments mit unvollständigen Sicherungsmetadaten finden Sie unter [Protokollfragmentsicherungen &#40; SQLServer &#41; ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).|  
|**IsForceOffline**|**bit**|**1** = Sicherung erfolgte mithilfe von NORECOVERY; die Datenbank offline geschaltet wurde von der Sicherung.|  
|**IsCopyOnly**|**bit**|**1** = eine kopiesicherung.<br /><br /> Eine Kopiesicherung wirkt sich nicht auf die Sicherungs- und Wiederherstellungsprozeduren für die Datenbank aus. Weitere Informationen finden Sie unter [Kopiesicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).|  
|**FirstRecoveryForkID**|**uniqueidentifier**|ID für den ersten Wiederherstellungs-Verzweigungspunkt. Diese Spalte entspricht **First_recovery_fork_guid** in der [Backupset](../../relational-databases/system-tables/backupset-transact-sql.md) Tabelle.<br /><br /> Bei datensicherungen ist **FirstRecoveryForkID** gleich **RecoveryForkID**.|  
|**ForkPointLSN**|**numeric(25,0)** NULL|Wenn **FirstRecoveryForkID** stimmt nicht mit **RecoveryForkID**, dies ist die protokollfolgenummer des verzweigungspunkts. Andernfalls ist der Wert NULL.|  
|**RecoveryModel**|**nvarchar(60)**|Wiederherstellungsmodell für die Datenbank. Folgende Werte sind möglich:<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLE|  
|**DifferentialBaseLSN**|**numeric(25,0)** NULL|Für eine einzelne Sicherung auf differenzieller Basis, entspricht der Wert der **FirstLSN** der differenziellen Basis; Änderungen mit LSNs, die größer als oder gleich **DifferentialBaseLSN** im differenziellen Sicherung enthalten sind.<br /><br /> Bei einer differenziellen Sicherung auf der Basis mehrerer Basissicherungen ist der Wert NULL, und die Basis-LSN muss auf Dateiebene bestimmt werden. Weitere Informationen finden Sie unter [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).<br /><br /> Bei nicht differenziellen Sicherungstypen ist der Wert immer NULL.<br /><br /> Weitere Informationen finden Sie unter [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
|**DifferentialBaseGUID**|**uniqueidentifier**|Bei einer differenziellen Sicherung auf der Basis einer Sicherung entspricht dieser Wert dem eindeutigen Bezeichner der differenziellen Basis.<br /><br /> Bei einer differenziellen Sicherung auf der Basis mehrerer Basissicherungen ist der Wert NULL; die Basis für die differenzielle Sicherung muss dateibasiert ermittelt werden.<br /><br /> Bei nicht differenziellen Sicherungstypen ist der Wert NULL.|  
|**BackupTypeDescription**|**nvarchar(60)**|Sicherungstyp in Form einer Zeichenfolge. Folgende Werte sind möglich:<br /><br /> DATABASE<br /><br /> TRANSACTION LOG<br /><br /> FILE OR FILEGROUP<br /><br /> DATABASE DIFFERENTIAL<br /><br /> FILE DIFFERENTIAL PARTIAL<br /><br /> PARTIAL DIFFERENTIAL|  
|**BackupSetGUID**|**uniqueidentifier** NULL|Eindeutige ID des Sicherungssatzes, die zur Identifizierung des Sicherungssatzes auf dem Medium dient.|  
|**CompressedBackupSize**|**bigint**|Bytezahl des Sicherungssatzes. Für nicht komprimierte Sicherungen ist dieser Wert ist identisch mit **BackupSize**.<br /><br /> Um der Komprimierungsrate verwenden **CompressedBackupSize** und **BackupSize**.<br /><br /> Während einer **Msdb** ein Upgrade ausführen, wird dieser Wert festgelegt, mit dem Wert des übereinstimmen der **BackupSize** Spalte.|  
|**containment**|**"tinyint"** not NULL|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Zeigt den Kapselungsstatus der Datenbank an.<br /><br /> 0 = Datenbankkapselung ist deaktiviert<br /><br /> 1 = Datenbank ist in Teilkapselung|  
|**KeyAlgorithm**|**nvarchar(32)**|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) über die aktuelle Version.<br /><br /> Der Verschlüsselungsalgorithmus, der zum Verschlüsseln der Sicherung verwendet wird. NO_Encryption gibt an, dass die Sicherung nicht verschlüsselt wurde. Wenn Sie der richtige Wert nicht bestimmt werden kann sollte der Wert NULL sein.|  
|**EncryptorThumbprint**|**varbinary(20)**|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) über die aktuelle Version.<br /><br /> Der Fingerabdruck der Verschlüsselung, der verwendet werden kann, um das Zertifikat oder den asymmetrischen Schlüssel in der Datenbank zu ermitteln. Wenn die Sicherung nicht verschlüsselt wurde, ist dieser Wert NULL.|  
|**EncryptorType**|**nvarchar(32)**|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (CU1) über die aktuelle Version.<br /><br /> Der verwendete Verschlüsselungstyp: Zertifikat oder Asymmetrischer Schlüssel. Wenn die Sicherung nicht verschlüsselt wurde, ist dieser Wert NULL.|  
  
> [!NOTE]  
>  Wenn für die Sicherungssätze Kennwörter definiert sind, gibt RESTORE HEADERONLY vollständige Informationen nur für den Sicherungssatz zurück, dessen Kennwort mit dem Kennwort übereinstimmt, das mit der Befehlsoption PASSWORD angegeben wird. Außerdem gibt RESTORE HEADERONLY die vollständigen Informationen zu ungeschützten Sicherungssätzen zurück. Die **Sicherungsname** Spalte für die andere kennwortgeschützte Sicherung auf dem Medium setzt auf festgelegt ist "***kennwortgeschützte\*\*\*", und alle anderen Spalten sind NULL.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Ein Client kann RESTORE HEADERONLY zum Abrufen aller Headerinformationen für alle Sicherungen auf einem bestimmten Sicherungsmedium verwenden. Für jede Sicherung auf dem Sicherungsmedium sendet der Server die Headerinformationen als Zeile zurück.  
  
## <a name="security"></a>Sicherheit  
 Bei einem Sicherungsvorgang können optional Kennwörter für einen Mediensatz, einen Sicherungssatz oder für beides angegeben werden. Wurde ein Kennwort für einen Mediensatz oder Sicherungssatz definiert, müssen die richtigen Kennwörter in der RESTORE-Anweisung angegeben werden. Diese Kennwörter zu verhindern, dass nicht autorisierte Wiederherstellungsoptionen und Unbefugtes Anfügen von Sicherungssätzen an Medien mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tools. Mit einem Kennwort kann jedoch das Überschreiben eines Mediums mithilfe der Option FORMAT der BACKUP-Anweisung nicht verhindert werden.  
  
> [!IMPORTANT]  
>  Dieses Kennwort bietet also nur unzureichenden Schutz. Es soll vermeiden, dass autorisierte wie nicht autorisierte Benutzer mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tools fehlerhafte Wiederherstellungen durchführen. Es verhindert jedoch nicht das Lesen der Sicherungsdaten mit anderen Mitteln oder das Ersetzen des Kennworts. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Die bewährte Methode für den Schutz von Sicherungen werden verwahren von Sicherungsbändern an einem sicheren Ort oder Sichern in Datenträgerdateien, die durch ausreichend Zugriffssteuerungslisten (ACLs) geschützt sind. Die ACLs sollten für den Verzeichnisstamm eingerichtet werden, unter dem die Sicherungen erstellt werden.  
  
### <a name="permissions"></a>Berechtigungen  
 Sie benötigen die CREATE DATABASE-Berechtigung, um Informationen zu Sicherungssätzen oder Sicherungsmedien abzurufen. Weitere Informationen finden Sie unter [GRANT (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Informationen im Header der Datenträgerdatei `C:\AdventureWorks-FullBackup.bak` zurückgegeben.  
  
```  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks-FullBackup.bak'   
WITH NOUNLOAD;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [Aktivieren oder Deaktivieren von Sicherungsprüfsummen während der Sicherung oder Wiederherstellung &#40; SQLServer &#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  
