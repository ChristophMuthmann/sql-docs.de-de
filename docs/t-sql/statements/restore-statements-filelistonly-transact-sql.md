---
title: RESTORE FILELISTONLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RESTORE FILELISTONLY
- RESTORE_FILELISTONLY_TSQL
- FILELISTONLY
- FILELISTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backups [SQL Server], file lists
- RESTORE FILELISTONLY statement
- listing backed up files
ms.assetid: 0b4b4d11-eb9d-4f3e-9629-6c79cec7a81a
caps.latest.revision: 83
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bdae49bd22b5398d120530db150bc9628e34d92a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="restore-statements---filelistonly-transact-sql"></a>RESTORE-Anweisungen - FILELISTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt ein Resultset mit einer Liste der Datenbank- und Protokolldateien zurück, die im Sicherungssatz in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthalten sind.  
  
> [!NOTE]  
>  Die Beschreibungen der Argumente finden Sie [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RESTORE FILELISTONLY   
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
 Beschreibungen der RESTORE FILELISTONLY-Argumente finden Sie unter [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="result-sets"></a>Resultsets  
 Ein Client kann mit RESTORE FILELISTONLY eine Liste der in einem Sicherungssatz enthaltenen Dateien abrufen. Diese Informationen werden als Resultset zurückgegeben, das eine Zeile für jede Datei enthält.  
  
|Spaltenname|Datentyp|Description|  
|-|-|-|  
|LogicalName|**vom Datentyp nvarchar(128)**|Logischer Name der Datei.|  
|PhysicalName|**nvarchar(260)**|Physischer Name oder Betriebssystemname der Datei.|  
|Typ|**char(1)**|Einer der folgenden Dateitypen:<br /><br /> **L** = Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Protokolldatei<br /><br /> **D**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datendatei<br /><br /> **F** = Volltextkatalog<br /><br /> **S** = FileStream, FileTable oder [!INCLUDE[hek_2](../../includes/hek-2-md.md)] Container|  
|FileGroupName|**vom Datentyp nvarchar(128)**|Name der Dateigruppe, die die Datei enthält.|  
|Größe|**numeric(20,0)**|Aktuelle Größe in Bytes.|  
|MaxSize|**numeric(20,0)**|Maximal zulässige Größe in Bytes.|  
|FileID|**bigint**|Eindeutiger Dateibezeichner in der Datenbank.|  
|CreateLSN|**numeric(25,0)**|Protokollfolgenummer, bei der die Datei erstellt wurde.|  
|DropLSN|**numeric(25,0)** NULL|Die protokollfolgenummer, bei der die Datei gelöscht wurde. Wurde die Datei nicht gelöscht, ist dieser Wert NULL.|  
|UniqueID|**uniqueidentifier**|Global eindeutiger Bezeichner der Datei.|  
|ReadOnlyLSN|**numeric(25,0) NULL**|Protokollfolgenummer, bei der die Dateigruppe mit der Datei von Lesen/Schreiben zu Schreibgeschützt geändert wurde (letzte Änderung).|  
|ReadWriteLSN|**numeric(25,0)** NULL|Protokollfolgenummer, bei der die Dateigruppe mit der Datei von Nur Lesen zu Schreibgeschützt geändert wurde (letzte Änderung).|  
|BackupSizeInBytes|**bigint**|Größe der Sicherung dieser Datei in Bytes.|  
|SourceBlockSize|**int**|Blockgröße des physischen Geräts mit der Datei in Bytes (nicht des Sicherungsmediums).|  
|FileGroupID|**int**|ID der Dateigruppe.|  
|LogGroupGUID|**"uniqueidentifier" NULL**|NULL.|  
|DifferentialBaseLSN|**numeric(25,0)** NULL|Bei differenziellen Sicherungen Änderungen mit protokollfolgenummern größer als oder gleich **DifferentialBaseLSN** im differenziellen Sicherung enthalten sind.<br /><br /> Bei anderen Sicherungstypen ist der Wert NULL.|  
|DifferentialBaseGUID|**uniqueidentifier**|Bei differenziellen Sicherungen der eindeutige Bezeichner der differenziellen Basis.<br /><br /> Bei anderen Sicherungstypen ist der Wert NULL.|  
|IsReadOnly|**bit**|**1** = die Datei ist schreibgeschützt.|  
|IsPresent|**bit**|**1** = die Datei im Sicherungssatz enthalten ist.|  
|TDEThumbprint|**varbinary(32)**|Zeigt den Fingerabdruck des Datenbankverschlüsselungs-Schlüssels an. Der Verschlüsselungsfingerabdruck ist ein SHA-1-Hash des Zertifikats, mit dem der Schlüssel verschlüsselt wurde. Informationen über die datenbankverschlüsselung finden Sie unter [transparente datenverschlüsselung &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).|  
|SnapshotURL|**nvarchar(360)**|Die URL für den Azure-Momentaufnahme der Datenbankdatei, die in der Sicherung FILE_SNAPSHOT enthalten. Gibt NULL zurück, wenn keine Sicherung FILE_SNAPSHOT.|  
  
## <a name="security"></a>Sicherheit  
 Bei einem Sicherungsvorgang können optional Kennwörter für einen Mediensatz, einen Sicherungssatz oder für beides angegeben werden. Wurde ein Kennwort für einen Mediensatz oder Sicherungssatz definiert, müssen die richtigen Kennwörter in der RESTORE-Anweisung angegeben werden. Diese Kennwörter zu verhindern, dass nicht autorisierte Wiederherstellungsoptionen und Unbefugtes Anfügen von Sicherungssätzen an Medien mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tools. Mit einem Kennwort kann jedoch das Überschreiben eines Mediums mithilfe der Option FORMAT der BACKUP-Anweisung nicht verhindert werden.  
  
> [!IMPORTANT]  
>  Dieses Kennwort bietet also nur unzureichenden Schutz. Es soll vermeiden, dass autorisierte wie nicht autorisierte Benutzer mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tools fehlerhafte Wiederherstellungen durchführen. Es verhindert jedoch nicht das Lesen der Sicherungsdaten mit anderen Mitteln oder das Ersetzen des Kennworts. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Eine bewährte Methode für den Schutz von Sicherungen ist das Verwahren von Sicherungsbändern an einem sicheren Ort oder das Sichern in Datenträgerdateien, die durch eine adäquate Zugriffssteuerungsliste (ACL, Access Control List) geschützt sind. Die ACLs sollten für den Verzeichnisstamm eingerichtet werden, unter dem die Sicherungen erstellt werden.  
  
### <a name="permissions"></a>Berechtigungen  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen benötigen Sie die CREATE DATABASE-Berechtigung, um Informationen zu Sicherungssätzen oder Sicherungsmedien abzurufen. Weitere Informationen finden Sie unter [GRANT (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen vom Sicherungsmedium `AdventureWorksBackups` zurückgegeben. Das Beispiel verwendet die `FILE`-Option zum Angeben des zweiten Sicherungssatzes auf dem Gerät.  
  
```  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  

