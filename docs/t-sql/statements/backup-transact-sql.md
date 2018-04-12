---
title: BACKUP (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BACKUP_TSQL
- BACKUP
- BACKUP_DATABASE_TSQL
- BACKUP_LOG_TSQL
- BACKUP LOG
- BACKUP DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], BACKUP statement
- backing up filegroups [SQL Server]
- backup file formats [SQL Server]
- backups [SQL Server]
- database backups [SQL Server], BACKUP statement
- multifamily media sets [SQL Server]
- mirrored media sets [SQL Server]
- backing up files [SQL Server]
- backup sets [SQL Server], BACKUP statement
- backup compression [SQL Server], BACKUP statement
- BACKUP statement
- backups [SQL Server], BACKUP statement
- backup history tables [SQL Server]
- transaction log backups [SQL Server], BACKUP LOG statement
- READ_WRITE_FILEGROUPS option
- BACKUP DATABASE statement
- concurrency [SQL Server], backups
- backing up databases [SQL Server]
- passwords [SQL Server], backups
- security [SQL Server], backups
- media families [SQL Server]
- BACKUP LOG statement
- backing up transaction logs [SQL Server]
- stripe sets [SQL Server]
- cross-platform backups
ms.assetid: 89a4658a-62f1-4289-8982-f072229720a1
caps.latest.revision: 275
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: ad21db12a4d147f8d999c7774a773082cbc6b1b5
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="backup-transact-sql"></a>BACKUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  Sichert eine vollständige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank, um eine Datenbanksicherung zu erstellen, oder eine oder mehrere Dateien oder Dateigruppen, um eine Dateisicherung (BACKUP DATABASE) zu erstellen. Sichert bei Verwendung des vollständigen oder massenprotokollierten Wiederherstellungsmodells auch das Transaktionsprotokoll der Datenbank, um eine Protokollsicherung (BACKUP LOG) zu erstellen. 

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
``` 
Backing Up a Whole Database   
BACKUP DATABASE { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL -- Not supporterd in SQL Database Managed Instance
           | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up Specific Files or Filegroups  
BACKUP DATABASE { database_name | @database_name_var }   
 <file_or_filegroup> [ ,...n ]   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Creating a Partial Backup  
BACKUP DATABASE { database_name | @database_name_var }   
 READ_WRITE_FILEGROUPS [ , <read_only_filegroup> [ ,...n ] ]  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up the Transaction Log (full and bulk-logged recovery models)  
BACKUP LOG -- Not supported in SQL Database Managed Instance
  { database_name | @database_name_var }  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]  
[;]  
  
<backup_device>::=   
 {  
   { logical_device_name | @logical_device_name_var }   
 | {   DISK -- Not supported in SQL Database Managed Instance
     | TAPE -- Not supported in SQL Database Managed Instance
     | URL } =   
     { 'physical_device_name' | @physical_device_name_var | 'NUL' }  
 }   
  
<MIRROR TO clause>::=  
 MIRROR TO <backup_device> [ ,...n ]  
  
<file_or_filegroup>::=  
 {  
   FILE = { logical_file_name | @logical_file_name_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
 }   
  
<read_only_filegroup>::=  
FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
  
<general_WITH_options> [ ,...n ]::=   
--Backup Set Options  
   COPY_ONLY -- Only backup set option supported by SQL Database Managed Instance  
 | { COMPRESSION | NO_COMPRESSION }   
 | DESCRIPTION = { 'text' | @text_variable }   
 | NAME = { backup_set_name | @backup_set_name_var }   
 | CREDENTIAL  
 | ENCRYPTION  
 | FILE_SNAPSHOT  --Not supported in SQL Database Managed Instance
 | { EXPIREDATE = { 'date' | @date_var }   
        | RETAINDAYS = { days | @days_var } }   
  
--Media Set Options  
   { NOINIT | INIT }   
 | { NOSKIP | SKIP }   
 | { NOFORMAT | FORMAT }   
 | MEDIADESCRIPTION = { 'text' | @text_variable }   
 | MEDIANAME = { media_name | @media_name_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
   BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
   { NO_CHECKSUM | CHECKSUM }  
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Compatibility Options  
   RESTART   
  
--Monitoring Options  
   STATS [ = percentage ]   
  
--Tape Options. These are not supported in SQL Database Managed Instance
   { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
--Log-specific Options. These are not supported in SQL Database Managed Instance 
   { NORECOVERY | STANDBY = undo_file_name }  
 | NO_TRUNCATE  
  
--Encryption Options  
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=   
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name   
```  
  
## <a name="arguments"></a>Argumente  

DATABASE  
 Gibt eine vollständige Datenbanksicherung an. Wird eine Liste von Dateien und Dateigruppen angegeben, werden nur diese Dateien und Dateigruppen gesichert. Während einer vollständigen oder differenziellen Datenbanksicherung werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auch die erforderlichen Teile des Transaktionsprotokolls gesichert, um eine konsistente Datenbank zu erzeugen, wenn die Sicherung wiederhergestellt wird.  
  
 Wenn Sie eine von BACKUP DATABASE (eine *Datensicherung*) erstellte Sicherung wiederherstellen, wird die komplette Sicherung wiederhergestellt. Nur Protokollsicherungen können bis zu einem bestimmten Zeitpunkt oder bis zu einer bestimmten Transaktion in der Sicherung wiederhergestellt werden.  
  
> [!NOTE]  
> Für die **Masterdatenbank** kann nur eine vollständige Datenbanksicherung ausgeführt werden.  
  
LOG **Gilt für:** SQL Server

 Gibt an, dass nur das Transaktionsprotokoll gesichert wird. Das Protokoll wird von der letzten erfolgreich ausgeführten Protokollsicherung bis zum aktuellen Ende des Protokolls gesichert. Bevor Sie die erste Protokollsicherung erstellen können, müssen Sie eine vollständige Sicherung erstellen.  
  
 Eine Protokollsicherung können Sie auf eine bestimmte Zeit oder Transaktion in der Sicherung wiederherstellen, indem Sie `WITH STOPAT`, `STOPATMARK` oder `STOPBEFOREMARK` in Ihrer [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md)-Anweisung angeben.  
  
> [!NOTE]  
>  Nach einer normalen Protokollsicherung sind einige Transaktionsprotokolldatensätze inaktiv, sofern Sie nicht `WITH NO_TRUNCATE` oder `COPY_ONLY` angeben. Das Protokoll wird abgeschnitten, nachdem alle Datensätze innerhalb mindestens einer virtuellen Protokolldatei deaktiviert werden. Wenn das Protokoll nach routinemäßigen Protokollsicherungen nicht abgeschnitten wird, wird das Abschneiden des Protokolls möglicherweise verzögert. Weitere Informationen finden Sie in [Faktoren, die die Protokollkürzung verzögern können](../../relational-databases/logs/the-transaction-log-sql-server.md#FactorsThatDelayTruncation).  
  
 { *database_name* | **@***database_name_var* } ist die Datenbank, aus der das Transaktionsprotokoll, die Teildatenbank oder die vollständige Datenbank gesichert werden. Wird das Argument in Form einer Variablen angegeben (**@***database_name_var*), kann dieser Name entweder als Zeichenfolgenkonstante (**@***database_name_var***=***database name*) oder als Variable eines Zeichenfolgen-Datentyps (mit Ausnahme der Datentypen **ntext** oder **text**) angegeben werden.  
  
> [!NOTE]  
> Eine Sicherung der Spiegeldatenbank in einer Datenbank-Spiegelungspartnerschaft ist nicht möglich.  
  
\<file_or_filegroup> [ **,**...*n* ]  
 Wird nur mit BACKUP DATABASE verwendet, gibt eine Datenbankdatei oder eine Dateigruppe in einer Datenbank an, die in einer Dateisicherung enthalten sein soll, oder gibt eine schreibgeschützte Datei oder Dateigruppe an, die in einer Teilsicherung enthalten sein soll.  
  
 FILE **=** { *logical_file_name* | **@***logical_file_name_var* }  
 Der logische Name einer Datei oder einer Variablen, deren Wert dem logischen Namen einer Datei entspricht, die in der Sicherung enthalten sein soll.  
  
 FILEGROUP **=** { *logical_filegroup_name* | **@***logical_filegroup_name_var* }  
 Der logische Name einer Dateigruppe oder einer Variablen, deren Wert dem logischen Namen einer Dateigruppe entspricht, die in der Sicherung enthalten sein soll. Beim einfachen Wiederherstellungsmodell wird die Dateigruppensicherung nur für eine schreibgeschützte Dateigruppe unterstützt.  
  
> [!NOTE]  
> Verwenden Sie Dateisicherungen dann, wenn eine Datenbanksicherung aufgrund der Datenbankgröße und aufgrund von Leistungsanforderungen nicht möglich ist. Das NUL-Gerät kann zum Testen der Leistung von Sicherungen verwendet werden, sollte aber nicht in Produktionsumgebungen eingesetzt werden.
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere Dateien und Dateigruppen in einer durch Trennzeichen getrennten Liste angegeben werden können. Für die Anzahl gibt es keine Einschränkungen. 
  
 Weitere Informationen finden Sie unter [Vollständige Dateisicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) und [Sichern von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md).  
  
 READ_WRITE_FILEGROUPS [ **,** FILEGROUP = { *logical_filegroup_name* | **@***logical_filegroup_name_var* } [ **,**...*n* ] ]  
 Gibt eine Teilsicherung an. Eine Teilsicherung umfasst alle Dateien mit Lese-/Schreibzugriff in einer Datenbank: die primäre Dateigruppe und alle beliebigen sekundären Dateigruppen mit Lese-/Schreibzugriff sowie auch alle angegebenen schreibgeschützten Dateien oder Dateigruppen.  
  
 READ_WRITE_FILEGROUPS  
 Gibt an, dass alle Dateigruppen mit Lese-/Schreibzugriff in der Teilsicherung gesichert werden sollen. Wenn die Datenbank schreibgeschützt ist, umfasst READ_WRITE_FILEGROUPS nur die primäre Dateigruppe.  
  
> [!IMPORTANT]  
> Durch das explizite Auflisten der Dateigruppen mit Lese-/Schreibzugriff mithilfe von FILEGROUP anstelle von READ_WRITE_FILEGROUPS wird eine Dateisicherung erstellt.  
  
 FILEGROUP = { *logical_filegroup_name* | **@***logical_filegroup_name_var* }  
Der logische Name einer schreibgeschützten Dateigruppe oder einer Variablen, deren Wert dem logischen Namen einer schreibgeschützten Dateigruppe entspricht, die in der Teilsicherung enthalten sein soll. Weitere Informationen finden Sie unter "\<file_or_filegroup>" weiter oben in diesem Thema.
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere schreibgeschützte Dateigruppen in einer durch Trennzeichen getrennten Liste angegeben werden können.  
  
 Weitere Informationen zu Sicherungen des Protokollfragments finden Sie unter [Teilsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
TO \<backup_device> [ **,**...*n* ]Gibt an, dass es sich bei dem zugehörigen Satz von [Sicherungsmedien](../../relational-databases/backup-restore/backup-devices-sql-server.md) entweder um einen nicht gespiegelten Mediensatz handelt oder um den ersten Spiegel innerhalb eines gespiegelten Mediensatzes (für den eine oder mehrere MIRROR TO-Klauseln deklariert sind).  
  
\<backup_device> **Gilt für:** SQL Server Gibt ein logisches oder physisches Sicherungsmedium an, das für den Sicherungsvorgang verwendet werden soll.  
  
 { *logical_device_name* | **@***logical_device_name_var* } **Gilt für:** SQL Server Der logische Name des Sicherungsmediums, auf dem die Datenbank gesichert wird. Der logische Name muss den Regeln für Bezeichner entsprechen. Bei der Angabe als Variable (*logical_device_name_var*) kann der Name des Sicherungsmediums entweder als Zeichenfolgenkonstante (@*logical_device_name_var***=** Name des logischen Sicherungsmediums) oder als Variable eines Zeichenfolgen-Datentyps (mit Ausnahme der Datentypen **ntext** oder **text**) angegeben werden.  
  
 {DISK | TAPE | URL} **=** { **'***physical_device_name***'** | **@***physical_device_name_var* | 'NUL' } **Gilt für:** DISK, TAPE und URL gelten für SQL Server. Nur URL gilt für die verwaltete SQL-Datenbankinstanz Gibt eine Datenträgerdatei oder ein Bandmedium oder einen Microsoft Azure Blob Storage-Dienst an. Das URL-Format wird zum Erstellen von Sicherungen im Windows Azure-Speicherdienst verwendet. Weitere Informationen finden Sie unter [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Ein Tutorial finden Sie unter [Tutorial: SQL Server-Sicherung und -Wiederherstellung im Windows Azure-BLOB-Speicherdienst](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md). 

> [!NOTE] 
> Das Datenträgermedium NUL verwirft alle Informationen, die es empfängt, und sollte nur zu Testzwecken verwendet werden. Es ist nicht zur Verwendung in der Produktion bestimmt.
  
> [!IMPORTANT]  
> Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 bis [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] können Sie nur auf ein einzelnes Gerät sichern, wenn Sie über die URL sichern. Um auf mehreren Geräten eine Sicherung durchzuführen, wenn Sie über die URL sichern, verwenden Sie [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Außerdem müssen Sie Shared Access Signature-Token (SAS) verwenden. Beispiele für die Erstellung einer Shared Access Signature finden Sie unter [SQL Server-Sicherung über URLs](../../relational-databases/backup-restore/sql-server-backup-to-url.md) und [Simplifying creation of SQL Credentials with Shared Access Signature (SAS) tokens on Azure Storage with Powershell](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx) (Vereinfachen der Erstellung von SQL-Anmeldeinformationen mit Shared Access Signature-Token in Azure Storage mit PowerShell).  
  
**URL gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) und die verwaltete SQL-Datenbankinstanz.  
  
 Das Datenträgermedium muss erst dann vorhanden sein, wenn es in einer BACKUP-Anweisung angegeben wird. Wenn das physische Medium vorhanden ist und die Option INIT in der BACKUP-Anweisung nicht angegeben ist, wird die Sicherung an das Medium angefügt.  
 
> [!NOTE] 
> Das NUL-Gerät verwirft alle Eingaben, die an diese Datei gesendet werden, aber die Sicherung kennzeichnet noch immer alle Seiten als gesichert.
  
 Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)aufgezeichnet wurde.  
  
> [!NOTE]  
> Die Option TAPE wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr bereitgestellt. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass in einer durch Trennzeichen getrennten Liste möglicherweise bis zu 64 Sicherungsmedien angegeben werden.  
  
MIRROR TO \<backup_device> [ **,**...*n* ] Gibt einen Satz von bis zu drei sekundären Sicherungsmedien an, die die in der TO-Klausel angegebenen Sicherungsmedien spiegeln. Die MIRROR TO-Klausel muss denselben Typ und dieselbe Anzahl von Sicherungsdateien angeben wie die TO-Klausel. Die maximale Anzahl von MIRROR TO-Klauseln lautet drei.  
  
 Diese Option ist nur in der Enterprise Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar.  
  
> [!NOTE]  
> Für MIRROR TO = DISK legt BACKUP automatisch die geeignete Blockgröße für Datenträgermedien fest. Weitere Informationen zur Blockgröße finden Sie weiter unten in dieser Tabelle unter "BLOCKSIZE".  
  
\<backup_device> Informationen finden Sie unter "\<backup_device>" weiter oben in diesem Abschnitt.
  
 *n*  
 Ein Platzhalter, der anzeigt, dass in einer durch Trennzeichen getrennten Liste möglicherweise bis zu 64 Sicherungsmedien angegeben werden. Die Anzahl von Medien in der MIRROR TO-Klausel muss der Anzahl von Medien in der TO-Klausel entsprechen.  
  
 Weitere Informationen finden Sie unter "Medienfamilien in gespiegelten Mediensätzen" im Abschnitt [Hinweise](#general-remarks) weiter unten in diesem Thema.  
  
 [ *next-mirror-to* ]  
 Ein Platzhalter, der anzeigt, dass eine einzelne BACKUP-Anweisung zusätzlich zu der einzelnen TO-Klausel bis zu drei MIRROR TO-Klauseln enthalten kann.  
  
### <a name="with-options"></a>WITH-Optionen  
 Gibt die Optionen an, die bei einem Sicherungsvorgang verwendet werden sollen.  
  
 CREDENTIAL  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) und die verwaltete SQL-Datenbankinstanz.  
 Wird nur verwendet, wenn eine Sicherung im Windows Azure-BLOB-Speicherdienst erstellt wird.  
  
 FILE_SNAPSHOT **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).

 Wird zum Erstellen einer Azure-Momentaufnahme der Datenbankdateien verwendet, wenn alle SQL Server-Datenbankdateien unter Verwendung des Azure-Blob-Speicherdiensts gespeichert werden. Weitere Informationen finden Sie unter [SQL Server-Datendateien in Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Die Momentaufnahmesicherung erstellt Azure-Momentaufnahmen der Datenbankdateien (Daten- und Protokolldateien) in einem konsistenten Zustand. Ein konsistenter Satz von Azure-Momentaufnahmen bildet zusammen eine Sicherung und wird in der Sicherungsdatei aufgezeichnet. Der einzige Unterschied zwischen `BACKUP DATABASE TO URL WITH FILE_SNAPSHOT` und `BACKUP LOG TO URL WITH FILE_SNAPSHOT` ist, dass der zweite Wert auch das Transaktionsprotokoll abschneidet, während dies beim ersten Wert nicht der Fall ist. Bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Momentaufnahmesicherung ist nur eine Transaktionsprotokollsicherung erforderlich, um eine Datenbank auf den Zeitpunkt der Transaktionsprotokollsicherung wiederherzustellen, nachdem die erste vollständige, von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Einrichtung der Sicherungskette vorausgesetzte Sicherung durchgeführt wurde. Darüber hinaus sind nur zwei Sicherungen des Transaktionsprotokolls erforderlich, um eine Datenbank auf einen Zeitpunkt zwischen den beiden Transaktionsprotokollsicherungen wiederherstellen.  
    
 DIFFERENTIAL  
**Gilt für:** SQL Server Nur mit BACKUP DATABASE verwendet, gibt an, dass sich die Datenbank- oder Dateisicherung nur auf die Teile der Datenbank oder Datei beschränken soll, die seit der letzten vollständigen Sicherung geändert wurden. Eine differenzielle Sicherung benötigt in der Regel weniger Speicherplatz als eine vollständige Sicherung. Verwenden Sie diese Option, damit nicht alle seit der letzten vollständigen Sicherung ausgeführten individuellen Protokollsicherungen angewendet werden müssen.  
  
> [!NOTE]  
> Standardmäßig erstellt `BACKUP DATABASE` eine vollständige Sicherung.  
  
 Weitere Informationen finden Sie unter [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
 ENCRYPTION  
 Wird verwendet, um die Verschlüsselung für eine Sicherung anzugeben. Sie können einen Verschlüsselungsalgorithmus angeben, um die Sicherung zu verschlüsseln, oder `NO_ENCRYPTION` angeben, um die Sicherung nicht zu verschlüsseln. Die Verschlüsselung wird empfohlen, um Sicherungsdateien zu sichern. Die Liste der Algorithmen, die Sie angeben können:  
  
-   `AES_128`  
-   `AES_192`  
-   `AES_256`  
-   `TRIPLE_DES_3KEY`  
-   `NO_ENCRYPTION`    

Wenn Sie sich für die Verschlüsselung entscheiden, müssen Sie auch die Verschlüsselung mithilfe der Verschlüsselungsoptionen angeben:  
  
-   SERVER CERTIFICATE = Encryptor_Name  
-   SERVER ASYMMETRIC KEY = Encryptor_Name  
  
> [!WARNING]  
> Bei Verwendung der Verschlüsselung in Verbindung mit dem `FILE_SNAPSHOT`-Argument wird die Metadatendatei selbst mithilfe des angegebenen Verschlüsselungsalgorithmus verschlüsselt, und das System überprüft, ob [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) für die Datenbank durchgeführt wurde. Für die Daten selbst erfolgt keine zusätzliche Verschlüsselung. Die Sicherung schlägt fehl, wenn die Datenbank nicht verschlüsselt oder die Verschlüsselung nicht abgeschlossen wurde, bevor die Backup-Anweisung ausgegeben wurde.  
  
**Sicherungssatzoptionen**  
  
Diese Optionen werden für den durch diesen Sicherungsvorgang erstellten Sicherungssatz verwendet.  
  
> [!NOTE]  
> Verwenden Sie die Option `FILE = <backup_set_file_number>`, um einen Sicherungssatz für einen Wiederherstellungsvorgang anzugeben. Weitere Informationen zum Angeben eines Sicherungssatzes finden Sie unter "Angeben eines Sicherungssatzes" in [RESTORE-Argumente &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md).
  
 COPY_ONLY **Gilt für:** SQL Server und verwaltete SQL-Datenbankinstanz Gibt an, dass die Sicherung eine *Kopiesicherung* ist, die keine Auswirkungen auf die normale Sicherungssequenz hat. Eine Kopiesicherung wird unabhängig von den regelmäßig geplanten konventionellen Sicherungen erstellt. Eine Kopiesicherung hat keine Auswirkungen auf die allgemeinen Sicherungs- und Wiederherstellungsprozeduren für die Datenbank.  
  
 Kopiesicherungen sollten in Situationen verwendet werden, in denen eine Sicherung für einen besonderen Zweck verwendet wird, z. B. zum Sichern des Protokolls vor einer Onlinedateiwiederherstellung. In der Regel wird eine Kopieprotokollsicherung einmal verwendet und dann gelöscht.  
  
-   Bei Verwendung mit `BACKUP DATABASE`BACKUP DATABASE wird durch die Option `COPY_ONLY` eine vollständige Sicherung erstellt, die nicht als eine differenzielle Basis verwendet werden kann. Das differenzielle Bitmuster wird nicht aktualisiert, und die differenziellen Sicherungen verhalten sich so, als sei die Kopiesicherung nicht vorhanden. Nachfolgende differenzielle Sicherungen verwenden die neueste, konventionelle vollständige Sicherung als Basis.  
  
    > [!IMPORTANT]  
    > Wenn `DIFFERENTIAL` und `COPY_ONLY` zusammen verwendet werden, wird `COPY_ONLY` ignoriert, und eine differenzielle Sicherung wird erstellt.  
  
-   Bei Verwendung mit `BACKUP LOG` wird durch die Option `COPY_ONLY` eine *Kopieprotokollsicherung* erstellt, die das Transaktionsprotokoll nicht abschneidet. Die Kopieprotokollsicherung hat keine Auswirkungen auf die Protokollkette, und andere Protokollsicherungen verhalten sich so, als sei die Kopiesicherung nicht vorhanden.  
  
Weitere Informationen finden Sie unter [Kopiesicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
{ COMPRESSION | NO_COMPRESSION }  
Nur in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] und höheren Versionen verfügbar. Gibt an, ob bei dieser Sicherung die [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md) eingesetzt wird, wodurch die Standardeinstellung auf Serverebene überschrieben wird.  
  
Die Sicherungskomprimierung wird bei der Installation standardmäßig deaktiviert. Diese Standardeinstellung kann jedoch durch Festlegen der Serverkonfigurationsoption [backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) geändert werden. Informationen zum Anzeigen des aktuellen Werts dieser Option finden Sie unter [Anzeigen oder Ändern von Servereigenschaften &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  

Informationen zur Verwendung der Sicherungskomprimierung mit [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)-fähigen Datenbanken finden Sie im Abschnitt [Hinweise](#general-remarks).
  
COMPRESSION  
Aktiviert die Sicherungskomprimierung explizit.  
  
NO_COMPRESSION  
Deaktiviert die Sicherungskomprimierung explizit.  
  
DESCRIPTION **=** { **'***Text***'** | **@***Textvariable* }  
Gibt den freien Text an, der als Beschreibung des Sicherungssatzes verwendet wird. Die Zeichenfolge kann maximal 255 Zeichen haben.  
  
NAME **=** { *backup_set_name* | **@***backup_set_var* }  
Gibt den Namen des Sicherungssatzes an. Namen können maximal 128 Zeichen haben. Wird NAME nicht angegeben, erhält der Sicherungssatz einen leeren Namen.  
  
{ EXPIREDATE **='***date***'** | RETAINDAYS **=** *days* }  
Gibt an, wann der Sicherungssatz für diese Sicherung überschrieben werden kann. Wenn beide Optionen verwendet werden, hat RETAINDAYS Vorrang vor EXPIREDATE.  
  
Wenn keine der Optionen angegeben wird, wird das Ablaufdatum durch die Konfigurationseinstellung **media retention** bestimmt. Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)angezeigt oder konfiguriert wird.   
  
> [!IMPORTANT]  
> Diese Optionen verhindern nur, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Datei überschreibt. Bänder können mit anderen Methoden gelöscht werden, und Dateien auf einem Datenträger können mit entsprechenden Betriebssystembefehlen gelöscht werden. Weitere Informationen zur Prüfung des Ablaufdatums finden Sie unter SKIP und FORMAT in diesem Thema.  
  
EXPIREDATE **=** { **'***date***'** | **@***date_var* } Gibt an, wann der Sicherungssatz abläuft und überschrieben werden kann. Wenn dieses Datum als Variable (@*date_var*) bereitgestellt wird, muss es dem konfigurierten Systemformat **datetime** genügen und als eines der folgenden Elemente angegeben werden:  
  
-   Eine Zeichenfolgekonstante (@*date_var* **=** date)  
-   Eine Variable mit einem Zeichenfolgen-Datentyp (mit Ausnahme der Datentypen **ntext** oder **text**)  
-   Eine **smalldatetime**-Variable  
-   Eine **datetime**-Variable  
  
Zum Beispiel:  
  
-   `'Dec 31, 2020 11:59 PM'`  
-   `'1/1/2021'`  
  
Informationen zum Angeben der **datetime**-Werte finden Sie unter [Datums- und Uhrzeittypen](../../t-sql/data-types/date-and-time-types.md).  
  
> [!NOTE]  
> Zum Ignorieren des Ablaufdatums verwenden Sie die Option `SKIP`.  
  
RETAINDAYS **=** { *days* | **@***days_var* } Gibt die Anzahl von Tagen an, die verstreichen müssen, bevor dieser Sicherungsmediensatz überschrieben werden kann. Bei der Angabe als Variable (**@***days_var*) muss der Wert als ganze Zahl angegeben werden.  
  
**Mediensatzoptionen**  
  
Diese Optionen werden für den Mediensatz insgesamt verwendet.  
  
{ **NOINIT** | INIT }  
 Steuert, ob der Sicherungsvorgang an die vorhandenen Sicherungssätze auf dem Sicherungsmedium angefügt wird oder diese überschreibt. Er wird standardmäßig an den neuesten Sicherungssatz auf dem Medium (NOINIT) angefügt.  
  
> [!NOTE]  
> Informationen zu Interaktionen zwischen { **NOINIT** | INIT } und { **NOSKIP** | SKIP } finden Sie unter [Hinweise](#general-remarks) weiter unten in diesem Thema.  
  
NOINIT  
 Zeigt an, dass der Sicherungssatz an den angegebenen Mediensatz angehängt wird, wobei vorhandene Sicherungssätze erhalten bleiben. Wenn für den Mediensatz ein Medienkennwort definiert ist, muss dieses Kennwort angegeben werden. NOINIT ist die Standardeinstellung.  
  
Weitere Informationen finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md):  
  
INIT  
 Gibt an, dass alle Sicherungssätze überschrieben werden sollen, während der Medienheader erhalten bleibt. Wenn INIT angegeben wird, werden alle bereits auf dem Medium vorhandenen Sicherungssätze überschrieben (wenn die Bedingungen dies zulassen). Standardmäßig prüft BACKUP die folgenden Bedingungen und überschreibt die Sicherungsmedien nicht, wenn eine der Bedingungen erfüllt wird:  
  
-   Einer der Sicherungssätze ist noch nicht abgelaufen. Weitere Informationen finden Sie unter `EXPIREDATE` und `RETAINDAYS`.  
-   Der möglicherweise in der BACKUP-Anweisung angegebene Name des Sicherungssatzes stimmt nicht mit dem Namen auf dem Sicherungsmedium überein. Weitere Informationen finden Sie unter der Option NAME weiter oben in diesem Abschnitt.  
  
Verwenden Sie die Option `SKIP`, um diese Überprüfungen zu überschreiben.  
  
Weitere Informationen finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md):  
  
{ **NOSKIP** | SKIP }  
Steuert, ob ein Sicherungsvorgang das Ablaufdatum und die Ablaufzeit der Sicherungssätze auf dem Medium überprüft, bevor diese überschrieben werden.  
  
> [!NOTE]  
> Informationen zu Interaktionen zwischen { **NOINIT** | INIT } und { **NOSKIP** | SKIP } finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
NOSKIP  
Weist die BACKUP-Anweisung an, das Ablaufdatum aller Sicherungssätze auf den Medien zu prüfen, bevor diese überschrieben werden dürfen. Dies ist das Standardverhalten.  
  
SKIP  
Deaktiviert die Prüfung von Ablaufdatum und Namen der Sicherungssätze. Diese Überprüfung wird normalerweise von der BACKUP-Anweisung ausgeführt, damit ein Überschreiben von Sicherungssätzen verhindert wird. Informationen zu Interaktionen zwischen { INIT | NOINIT } und { NOSKIP | SKIP } finden Sie unter "Hinweise" weiter unten in diesem Thema.  
Zum Anzeigen des Ablaufdatums und der Sicherungssätze fragen Sie die **expiration_date**-Spalte der [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)-Verlaufstabelle ab.  
  
{ **NOFORMAT** | FORMAT }  
Gibt an, dass der Medienheader auf alle Volumes geschrieben werden soll, die für diesen Sicherungsvorgang verwendet werden. Dabei werden vorhandene Medienheader und Sicherungssätze überschrieben.  
  
NOFORMAT  
Gibt an, dass der Sicherungsvorgang die vorhandenen Medienheader und Sicherungssätze auf den Medienvolumes beibehält, die für diesen Vorgang verwendet werden. Dies ist das Standardverhalten.  
  
FORMAT  
Gibt an, dass ein neuer Mediensatz erstellt werden kann. FORMAT bewirkt, dass vom Sicherungsvorgang ein neuer Medienheader auf alle Medienvolumes geschrieben wird, die für den Sicherungsvorgang verwendet werden. Der vorhandene Inhalt des Volumes wird ungültig, da alle vorhandenen Medienheader und Sicherungssätze überschrieben werden.  
  
> [!IMPORTANT]  
> Verwenden Sie `FORMAT` mit Bedacht. Die Formatierung von Volumes eines Mediensatzes führt dazu, dass der gesamte Mediensatz nicht mehr verwendet werden kann. Wird beispielsweise ein einzelnes Band initialisiert, das zu vorhandenen Stripesetmedien gehört, führt dies dazu, dass der gesamte Mediensatz unbrauchbar wird.  
  
Durch die Angabe von FORMAT ist `SKIP` impliziert. `SKIP` muss nicht explizit angegeben werden.  
  
MEDIADESCRIPTION **=** { *text* | **@***text_variable* }  
Gibt die Freiform-Textbeschreibung des Mediensatzes an. Diese kann aus maximal 255 Zeichen bestehen.  
  
MEDIANAME **=** { *media_name* | **@***media_name_variable* }  
Gibt den Mediennamen für den gesamten Sicherungsmediensatz an. Der Medienname darf nicht mehr als 128 Zeichen umfassen. Wird `MEDIANAME` angegeben, muss dieser Name dem vorher angegebenen Mediennamen auf den Sicherungsvolumes entsprechen. Wird er nicht angegeben, oder ist die Option SKIP festgelegt, findet keine Prüfung des Mediennamens statt.  
  
BLOCKSIZE **=** { *blocksize* | **@***blocksize_variable* }  
Legt die physische Blockgröße in Bytes fest. Die unterstützten Größen sind 512, 1024, 2048, 4096, 8192, 16.384, 32.768 und 65.536 (64 KB) Bytes. Der Standardwert ist 65.536 für Bandmedien und andernfalls 512. In der Regel ist diese Option nicht erforderlich, da von BACKUP automatisch eine Blockgröße ausgewählt wird, die für das Medium geeignet ist. Mit der expliziten Angabe einer Blockgröße wird die automatische Wahl der Blockgröße überschrieben.  
  
Geben Sie beim Erstellen einer Sicherung, die Sie auf eine CD-ROM kopieren und von dieser wiederherstellen möchten, BLOCKSIZE=2048 an.  
  
> [!NOTE]  
> Diese Option hat i. d. R. nur dann Auswirkungen auf die Leistung, wenn auf Bandmedien geschrieben wird.  
  
**Datenübertragungsoptionen**  
  
BUFFERCOUNT **=** { *buffercount* | **@***buffercount_variable* }  
Gibt die Gesamtanzahl von E/A-Puffern an, die für den Sicherungsvorgang verwendet werden sollen. Sie können eine beliebige positive ganze Zahl angeben. Eine große Pufferanzahl kann jedoch wegen eines ungeeigneten virtuellen Adressraumes im Prozess Sqlservr.exe zu Fehlern aufgrund von nicht genügend Arbeitsspeicher führen.  
  
Der gesamte von den Puffern belegte Speicherplatz wird durch *buffercount/maxtransfersize* bestimmt.  
  
> [!NOTE]  
> Wichtige Informationen zur Verwendung der `BUFFERCOUNT`-Option finden Sie im Blogeintrag [Falsche BufferCount-Datenübertragungsoption kann OOM-Bedingung auslösen](http://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx).  
  
MAXTRANSFERSIZE **=** { *maxtransfersize* | ***@** maxtransfersize_variable* } Gibt die größte zu verwendende Übertragungseinheit zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und dem Sicherungsmedium in Bytes an. Die möglichen Werte sind Vielfache von 65.536 Bytes (64 KB) bis hin zu 4.194.304 Bytes (4 MB).  

> [!NOTE]  
> Wenn beim Erstellen von Sicherungen mithilfe des SQL Writer-Diensts für die Datenbank [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) konfiguriert ist oder [speicheroptimierte Dateigruppen](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md) enthält, dann sollte `MAXTRANSFERSIZE` zum Zeitpunkt der Wiederherstellung größer als oder gleich der `MAXTRANSFERSIZE` sein, die beim Erstellen der Sicherung verwendet wurde. 

> [!NOTE]  
> Für [Transparente Datenverschlüsselung (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)-fähige Datenbanken mit einer einzelnen Datendatei ist der standardmäßige `MAXTRANSFERSIZE`-Wert 65536 (64 KB). Für nicht mit TDE verschlüsselte Datenbanken ist der `MAXTRANSFERSIZE`-Standardwert 1048576 (1 MB) bei Verwendung der Sicherung auf DISK und 65536 (64 KB) bei Verwendung von VDI oder TAPE.
> Weitere Informationen zur Verwendung der Sicherungskomprimierung mit TDE-verschlüsselten Datenbanken finden Sie im Abschnitt [Hinweise](#general-remarks).
  
**Fehlerverwaltungsoptionen**  
  
Mit diesen Optionen können Sie bestimmen, ob Sicherungsprüfsummen für den Sicherungsvorgang aktiviert werden und ob der Vorgang beim Auftreten eines Fehlers beendet wird.  
  
{ **NO_CHECKSUM** | CHECKSUM }  
 Steuert, ob Sicherungsprüfsummen aktiviert sind.  
  
NO_CHECKSUM  
Das Generieren von Sicherungsprüfsummen (und die Überprüfung von Seitenprüfsummen) wird explizit deaktiviert. Dies ist das Standardverhalten.  
  
CHECKSUM  
Gibt an, dass der Sicherungsvorgang jede Seite auf Prüfsumme und zerrissene Seiten überprüft (wenn aktiviert und verfügbar) und eine Prüfsumme für die gesamte Sicherung generiert.  
  
Die Verwendung von Sicherungsprüfsummen kann sich auf die Arbeitsauslastung und den Durchsatz bei der Sicherung auswirken.  
  
Weitere Informationen finden Sie unter [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }  
Steuert, ob ein Sicherungsvorgang beendet oder fortgesetzt wird, nachdem ein Fehler bei der Seitenprüfsumme aufgetreten ist.  
  
STOP_ON_ERROR  
Von BACKUP wird ein Fehler erzeugt, wenn eine Seitenprüfsumme nicht stimmt. Dies ist das Standardverhalten.  
  
CONTINUE_AFTER_ERROR  
BACKUP wird auch dann fortgesetzt, wenn Fehler auftreten, z. B. ungültige Prüfsummen oder zerrissene Seiten.  
  
Wenn Sie das Protokollfragment mithilfe der Option NO_TRUNCATE nicht sichern können, wenn die Datenbank beschädigt ist, können Sie versuchen, eine [Sicherung des Protokollfragments](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) auszuführen, indem Sie CONTINUE_AFTER_ERROR anstelle von NO_TRUNCATE angeben.  
  
Weitere Informationen finden Sie unter [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
**Kompatibilitätsoptionen**  
  
RESTART  
Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] keine Auswirkungen. Die Option wird von der Version aus Gründen der Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angenommen.  
  
**Überwachungsoptionen**  
  
STATS [ **=** *percentage* ]  
 Zeigt nach jedem abgeschlossenen *Prozentsatz* eine Meldung an und wird als Statusanzeige verwendet. Wird *Prozentsatz* nicht angegeben, zeigt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jedes Mal eine Meldung an, wenn weitere 10 Prozent des Vorgangs abgeschlossen sind.  
  
Mit der Option STATS wird der Prozentsatz gemeldet, der beim Erreichen des Schwellenwertes für das nächste Meldungsintervall abgeschlossen ist. Bei dem angegebenen Prozentsatz handelt es sich um einen ungefähren Wert. Wird beispielsweise STATS=10 festgelegt und sind 40 Prozent des Vorgangs abgeschlossen, dann zeigt die Option u. U. 43 Prozent an. Bei größeren Sicherungssätzen stellt dies kein Problem dar, da sich der Wert für den abgeschlossenen Prozentsatz zwischen abgeschlossenen E/A-Aufrufen nur sehr langsam verändert.  
  
**Bandoptionen**  
**Gilt für:** SQL Server  
Diese Optionen werden nur für Bandmedien verwendet. Diese Optionen werden ignoriert, wenn ein anderes Medium als ein Bandmedium verwendet wird.  
  
{ **REWIND** | NOREWIND }  
REWIND **Gilt für:** SQL Server Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Band freigeben und zurückspulen soll. REWIND ist die Standardeinstellung.  
  
NOREWIND **Gilt für:** SQL Server Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Band nach dem Sicherungsvorgang offen hält. Diese Option trägt zur Leistungsverbesserung bei, wenn mehrere Sicherungsvorgänge auf einem Band ausgeführt werden.  
  
NOREWIND impliziert NOUNLOAD, und diese Optionen sind innerhalb einer BACKUP-Anweisung inkompatibel.  
  
> [!NOTE]  
> Wenn Sie `NOREWIND` verwenden, bleibt die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Besitzer des Bandlaufwerks, bis in einer BACKUP- oder RESTORE-Anweisung, die in demselben Prozess ausgeführt wird, die Option `REWIND` oder `UNLOAD` verwendet wird oder bis die Serverinstanz heruntergefahren wird. Ein Offenhalten des Bandes verhindert, dass andere Prozesse auf das Band zugreifen können. Informationen zum Anzeigen einer Liste offener Bänder und zum Schließen eines offenen Bandes finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
{ **UNLOAD** | NOUNLOAD }    
**Gilt für:** SQL Server 
> [!NOTE]  
> `UNLOAD` und `NOUNLOAD` sind Sitzungseinstellungen, die für die Dauer der Sitzung oder bis zur Angabe der alternativen Einstellung persistent gespeichert wird.  
  
UNLOAD **Gilt für:** SQL Server   
 Gibt an, dass das Band automatisch zurückgespult und ausgeworfen wird, wenn die Sicherung vollständig ausgeführt ist. UNLOAD ist die Standardeinstellung beim Beginn einer Sitzung. 
  
NOUNLOAD **Gilt für:** SQL Server Gibt an, dass das Band nach dem BACKUP-Vorgang im Bandlaufwerk geladen bleibt.  
  
> [!NOTE]  
> Beim Sichern auf einem Bandsicherungsmedium wirkt sich die Option `BLOCKSIZE` auf die Leistung des Sicherungsvorgangs aus. Diese Option hat i. d. R. nur dann Auswirkungen auf die Leistung, wenn auf Bandmedien geschrieben wird.  
  
**Protokollspezifische Optionen**  
**Gilt für:** SQL Server  
Diese Optionen werden nur mit `BACKUP LOG` verwendet.  
  
> [!NOTE]  
> Wenn Sie keine Protokollsicherungen vornehmen möchten, verwenden Sie das einfache Wiederherstellungsmodell. Weitere Informationen finden Sie unter [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
{ NORECOVERY | STANDBY **=** *undo_file_name* }  
  NORECOVERY **Gilt für:** SQL Server   
  Sichert das Protokollfragment und belässt die Datenbank im RESTORING-Status. NORECOVERY ist hilfreich, wenn ein Failover zu einer sekundären Datenbank erfolgt oder wenn das Protokollfragment vor einem RESTORE-Vorgang gesichert wird.  
  
  Zum Ausführen einer Protokollsicherung, bei der die Protokollkürzung ausgelassen wird und die Datenbank automatisch den Status RESTORING erhält, verwenden Sie die Optionen `NO_TRUNCATE` und `NORECOVERY` zusammen.  
  
  STANDBY **=** *standby_file_name* 
**Gilt für:** SQL Server   
  Sichert das Protokollfragment und belässt die Datenbank im schreibgeschützten Modus und im STANDBY-Status. Die STANDBY-Klausel schreibt Standbydaten (wobei ein Rollback durchgeführt wird, aber mit der Option weiterer Wiederherstellungen). Die Verwendung der Option STANDBY ist gleichbedeutend mit BACKUP LOG WITH NORECOVERY gefolgt von RESTORE WITH STANDBY.  
  
  Wenn der Standbymodus verwendet wird, ist eine Standbydatei erforderlich, die mit *standby_file_name* angegeben wird und deren Speicherort im Protokoll der Datenbank gespeichert wird. Ist die angegebene Datei bereits vorhanden, wird sie von [!INCLUDE[ssDE](../../includes/ssde-md.md)] überschrieben. Ist sie noch nicht vorhanden, wird sie von [!INCLUDE[ssDE](../../includes/ssde-md.md)] erstellt. Die Standbydatei wird Teil der Datenbank.  
  
  Diese Datei enthält die Änderungen aus dem Rollback, die rückgängig gemacht werden müssen, wenn zu einem späteren Zeitpunkt RESTORE LOG-Vorgänge angewendet werden sollen. Es muss ausreichend Speicherplatz für die Vergrößerung der Standbydatei vorhanden sein, damit diese Datei alle Seiten aus der Datenbank enthalten kann, die durch das Rollback für die Transaktionen ohne Commit geändert wurden.  
  
NO_TRUNCATE  
**Gilt für:** SQL Server  
Gibt an, dass das Protokoll nicht abgeschnitten wird, und führt dazu, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] versucht, die Sicherung unabhängig vom Status der Datenbank durchzuführen. Daraus folgt, dass eine Sicherung, die mit `NO_TRUNCATE` erstellt wird, u.U. unvollständige Metadaten enthält. Diese Option ermöglicht es, das Protokoll auch dann zu sichern, wenn die Datenbank beschädigt ist.  
  
Die NO_TRUNCATE-Option von BACKUP LOG ist gleichbedeutend mit der Angabe von COPY_ONLY und CONTINUE_AFTER_ERROR.  
  
Ohne die Option `NO_TRUNCATE` muss sich die Datenbank im ONLINE-Status befinden. Wenn die Datenbank im SUSPENDED-Status ist, können Sie möglicherweise durch die Angabe von `NO_TRUNCATE` eine Sicherung erstellen. Wenn sich die Datenbank jedoch im Status OFFLINE oder EMERGENCY befindet, ist die Sicherung auch mit `NO_TRUNCATE` nicht zulässig. Weitere Informationen zu Datenbankstatus finden Sie unter [Datenbankstatus](../../relational-databases/databases/database-states.md).  
  
## <a name="about-working-with-sql-server-backups"></a>Informationen zum Arbeiten mit SQL Server-Sicherungen  
 In diesem Abschnitt werden die folgenden grundlegenden Sicherungskonzepte erläutert:  
  
 [Sicherungstypen](#Backup_Types)  
 [Kürzung des Transaktionsprotokolls](#Tlog_Truncation)  
 [Formatieren von Sicherungsmedien](#Formatting_Media)  
 [Arbeiten mit Sicherungsmedien und Mediensätzen](#Backup_Devices_and_Media_Sets)  
 [Wiederherstellen von SQL Server-Sicherungen](#Restoring_Backups)  
  
> [!NOTE]  
> Eine Einführung in die Sicherung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="Backup_Types"></a> Sicherungstypen  
 Die unterstützten Sicherungstypen sind vom Wiederherstellungsmodell der Datenbank abhängig, und zwar wie folgt:  
  
-   Alle Wiederherstellungsmodelle unterstützen vollständige und differenzielle Sicherungen von Daten.  
  
    |Umfang der Sicherung|Sicherungstypen|  
    |---------------------|------------------|  
    |Gesamte Datenbank|[Datenbanksicherungen](../../relational-databases/backup-restore/full-database-backups-sql-server.md) umfassen die gesamte Datenbank.<br /><br /> Optional kann jede Datenbanksicherung als Basis einer Serie von einer oder mehreren [differenziellen Datenbanksicherungen](../../relational-databases/backup-restore/differential-backups-sql-server.md) dienen.|  
    |Teilweise Datenbanksicherung|[Teilsicherungen](../../relational-databases/backup-restore/partial-backups-sql-server.md) umfassen Dateigruppen mit Lese-/Schreibzugriff und möglicherweise mindestens eine schreibgeschützte Datei oder Dateigruppe.<br /><br /> Optional kann jede Teilsicherung als Basis einer Serie von einer oder mehreren [differenziellen Teilsicherungen](../../relational-databases/backup-restore/differential-backups-sql-server.md) dienen.|  
    |Datei oder Dateigruppe|[Dateisicherungen](../../relational-databases/backup-restore/full-file-backups-sql-server.md) umfassen mindestens eine Datei oder Dateigruppe und sind nur für Datenbanken relevant, in denen mehrere Dateigruppen enthalten sind. Beim einfachen Wiederherstellungsmodell werden Dateisicherungen im Wesentlichen auf schreibgeschützte sekundäre Dateigruppen beschränkt.<br /> Optional kann jede Dateisicherung als Basis einer Serie von einer oder mehreren [differenziellen Dateisicherungen](../../relational-databases/backup-restore/differential-backups-sql-server.md) dienen.|  
  
-   Beim vollständigen oder massenprotokollierten Wiederherstellungsmodell enthalten die herkömmlichen Sicherungen auch sequentielle *Transaktionsprotokollsicherungen* (oder *Protokollsicherungen*), die erforderlich sind. Jede Protokollsicherung umfasst den Teil des Transaktionsprotokolls, der beim Erstellen der Sicherung aktiv war, und enthält alle Protokolldatensätze, die in einer vorherigen Protokollsicherung nicht gesichert wurden.  
  
     Wenn Sie die Gefahr eines Datenverlusts minimieren und den damit verbundenen höheren Verwaltungsaufwand in Kauf nehmen möchten, sollten Sie häufige Protokollsicherungen planen. Wenn Sie zwischen vollständigen Sicherungen differenzielle Sicherungen planen, kann dies die Wiederherstellungszeit verkürzen, da Sie nach dem Wiederherstellen der Daten nur eine geringe Anzahl von Protokollsicherungen wiederherstellen müssen.  
  
     Es empfiehlt sich, Protokollsicherungen auf einem anderen Volume als die Datenbanksicherungen zu speichern.  
  
    > [!NOTE]  
    > Bevor Sie die erste Protokollsicherung erstellen können, müssen Sie eine vollständige Sicherung erstellen.  
  
-   Eine *Kopiesicherung* ist eine besondere vollständige Sicherung oder Protokollsicherung, die von der normalen Sequenz konventioneller Sicherungen unabhängig ist. Verwenden Sie zum Erstellen einer Kopiesicherung die Option COPY_ONLY in der BACKUP-Anweisung. Weitere Informationen finden Sie unter [Kopiesicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
###  <a name="Tlog_Truncation"></a> Kürzung des Transaktionsprotokolls  
 Um das schnelle Auffüllen des Transaktionsprotokolls einer Datenbank zu vermeiden, sind routinemäßige Sicherungen von entscheidender Bedeutung. Die Protokollkürzung erfolgt beim einfachen Wiederherstellungsmodell automatisch, wenn die Datenbank gesichert wurde, und beim vollständigen Wiederherstellungsmodell, wenn das Transaktionsprotokoll gesichert wurde. Manchmal kann der Kürzungsprozess jedoch verzögert werden. Informationen zu Faktoren, die eine Protokollkürzung verzögern können, finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> [!NOTE]  
> Die Optionen `BACKUP LOG WITH NO_LOG` und `WITH TRUNCATE_ONLY` werden nicht mehr unterstützt. Wechseln Sie zum einfachen Wiederherstellungsmodell, wenn Sie zur Wiederherstellung das vollständige oder das massenprotokollierte Wiederherstellungsmodell verwenden und die Protokollsicherungskette aus einer Datenbank entfernen müssen. Weitere Informationen finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
###  <a name="Formatting_Media"></a>Formatieren von Sicherungsmedien  
 Sicherungsmedien werden durch eine BACKUP-Anweisung formatiert, und zwar nur dann, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Die Option `FORMAT` wird angegeben.  
-   Das Medium ist leer.  
-   Mit dem Vorgang wird ein Anschlussband geschrieben.  
  
###  <a name="Backup_Devices_and_Media_Sets"></a>Arbeiten mit Sicherungsmedien und Mediensätzen  
  
#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>Sicherungsmedien in Stripesetmedien  
 Bei einem *Stripeset* handelt es sich um eine Gruppe von Datenträgerdateien, für die die Daten in Blöcke aufgeteilt und in einer festen Reihenfolge verteilt werden. Die Anzahl der in einem Stripeset verwendeten Sicherungsmedien muss gleich bleiben (es sei denn, die Medien werden mit `FORMAT` neu initialisiert).  
  
 Im folgenden Beispiel wird eine Sicherung der [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]-Datenbank in ein neues Stripesetmedium geschrieben, für das drei Datenträgerdateien verwendet werden.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3.bak'  
WITH FORMAT,  
   MEDIANAME = 'AdventureWorksStripedSet0',  
   MEDIADESCRIPTION = 'Striped media set for AdventureWorks2012 database;  
GO  
```  
  
 Nachdem ein Sicherungsmedium als Teil eines Stripesets definiert wurde, kann es nicht für eine Sicherung mit einem einzelnen Medium verwendet werden, es sei denn, FORMAT wird angegeben. Ebenso kann ein Sicherungsmedium, das Sicherungen enthält, die nicht von einem Stripeset stammen, erst dann in einem Stripeset verwendet werden, wenn FORMAT angegeben wird. Verwenden Sie FORMAT, um einen im Stripesetformat vorliegenden Sicherungssatz zu teilen.  
  
 Ist weder MEDIANAME noch MEDIADESCRIPTION angegeben, wenn ein Medienheader geschrieben wird, bleibt das entsprechende Feld im Medienheader leer.  
  
#### <a name="working-with-a-mirrored-media-set"></a>Verwenden eines gespiegelten Mediensatzes  
 In der Regel sind Sicherungen ungespiegelt, und BACKUP-Sicherungen enthalten einfach eine TO-Klausel. Pro Mediensatz sind jedoch insgesamt vier Spiegel möglich. Bei einem gespiegelten Mediensatz schreibt der Sicherungsvorgang in mehrere Gruppen von Sicherungsmedien. Jede Gruppe von Sicherungsmedien umfasst einen einzelnen Spiegel im gespiegelten Mediensatz. Jede Spiegelung muss dieselbe Anzahl und denselben Typ von physischen Sicherungsmedien verwenden, die alle über dieselben Eigenschaften verfügen müssen.  
  
 Zum Sichern eines gespiegelten Mediensatzes müssen alle Spiegel vorhanden sein. Zum Sichern eines gespiegelten Mediensatzes geben Sie die `TO`-Klausel an, um den ersten Spiegel anzugeben, und geben Sie eine `MIRROR TO`-Klausel für jeden zusätzlichen Spiegel an.  
  
 Bei einem gespiegelten Mediensatz muss jede `MIRROR TO`-Klausel dieselbe Anzahl (und denselben Typ) von Medien wie die TO-Klausel aufführen. Im folgenden Beispiel wird in einen gespiegelten Mediensatz geschrieben, der zwei Spiegel enthält und drei Medien pro Spiegel verwendet:  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1a.bak',   
  DISK='Y:\SQLServerBackups\AdventureWorks2a.bak',   
  DISK='Z:\SQLServerBackups\AdventureWorks3a.bak'  
MIRROR TO DISK='X:\SQLServerBackups\AdventureWorks1b.bak',   
  DISK='Y:\SQLServerBackups\AdventureWorks2b.bak',   
  DISK='Z:\SQLServerBackups\AdventureWorks3b.bak';  
GO  
```  
  
> [!IMPORTANT]  
> Dieses Beispiel wurde so entwickelt, dass Sie es auf Ihrem lokalen System testen können. In der Praxis würde das Sichern auf mehreren Medien desselben Laufwerks die Leistung beeinträchtigen und die Redundanz zunichte machen, für die gespiegelte Mediensätze entwickelt wurden.  
  
##### <a name="media-families-in-mirrored-media-sets"></a>Medienfamilien in gespiegelten Mediensätzen  
 Jedes in der `TO`-Klausel einer BACKUP-Sicherung angegebene Sicherungsmedium entspricht einer Medienfamilie. Werden beispielsweise in den `TO`-Klauseln drei Medien aufgelistet, schreibt BACKUP Daten in drei Medienfamilien. In einem gespiegelten Mediensatz muss jeder Spiegel eine Kopie jeder Medienfamilie enthalten. Aus diesem Grund muss die Anzahl der Medien in jedem Spiegel identisch sein.  
  
 Wenn für jeden Spiegel mehrere Medien aufgeführt sind, bestimmt die Reihenfolge der Medien, welche Medienfamilie in ein bestimmtes Medium geschrieben wird. In jeder Medienliste entspricht beispielsweise das zweite Medium der zweiten Medienfamilie. Für die im obigen Beispiel genannten Medien ist die Entsprechung zwischen Medien und Medienfamilien in der folgenden Tabelle dargestellt:  
  
|Spiegel|Medienfamilie 1|Medienfamilie 2|Medienfamilie 3|  
|---------|---------|---------|---------|  
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|  
|1|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|  
  
 Eine Medienfamilie muss immer auf dem gleichen Gerät innerhalb eines bestimmten Spiegels gesichert werden. Daher müssen Sie bei Verwendung eines vorhandenen Mediensatzes jedes Mal die Medien eines Spiegels in derselben Reihenfolge wie beim Erstellen des Mediensatzes aufführen.  
  
 Weitere Informationen über gespiegelte Mediensätze finden Sie unter [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)noch nicht kennen. Weitere Informationen über Mediensätze und Medienfamilien finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
###  <a name="Restoring_Backups"></a>Wiederherstellen von SQL Server-Sicherungen  
 Um eine Datenbank wiederherzustellen und (optional) wieder online zu schalten, oder um eine Datei oder Dateigruppe wiederherzustellen, können Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)-Anweisung oder die [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Restore**-Tasks verwenden. Weitere Informationen finden Sie unter [Übersicht über Wiederherstellungsvorgänge &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
##  <a name="Additional_Considerations"></a>Weitere Überlegungen zu BACKUP-Optionen  
  
###  <a name="Interactions_SKIP_etc"></a>Interaktion von SKIP, NOSKIP, INIT und NOINIT  
 In dieser Tabelle werden die Interaktionen zwischen den Optionen { **NOINIT** | INIT } und { **NOSKIP** | SKIP } beschrieben.  
  
> [!NOTE]  
> Wenn das Bandmedium leer oder die Datenträger-Sicherungsdatei nicht vorhanden ist, wird bei allen nachfolgend aufgeführten Interaktionen ein Medienheader geschrieben und erst danach fortgefahren. Wenn das Medium nicht leer ist und keinen gültigen Medienheader aufweist, wird von diesen Vorgängen die Rückmeldung gegeben, dass dies kein gültiges MTF-Medium ist, und der Sicherungsvorgang wird beendet.  
  
||NOINIT|INIT|  
|------|------------|----------|  
|NOSKIP|Überprüft, wenn das Volume einen gültigen Medienheader enthält, ob der Medienname mit dem angegebenen `MEDIANAME` (sofern vorhanden) übereinstimmt. Wenn dies der Fall ist, wird der Sicherungssatz angefügt, wobei alle vorhandenen Sicherungssätze beibehalten werden.<br /> Enthält das Volume keinen gültigen Medienheader, tritt ein Fehler auf.|Wenn das Volume einen gültigen Medienheader enthält, werden die folgenden Überprüfungen durchgeführt:<br /><ul><li>Wenn `MEDIANAME` angegeben wurde, wird überprüft, ob der angegebene Medienname mit dem Mediennamen im Medienheader übereinstimmt.<sup>1</sup></li><li>Stellt sicher, dass auf dem Medium keine noch nicht abgelaufenen Sicherungssätze vorhanden sind. Wenn solche vorhanden sind, wird die Sicherung beendet.</li></ul><br />Wenn diese Überprüfungen erfolgreich sind, werden alle Sicherungssätze auf dem Medium überschrieben, und nur der Medienheader wird beibehalten.<br /> Wenn das Volume keinen gültigen Medienheader enthält, wird dieser mithilfe der angegebenen Optionen `MEDIANAME` und `MEDIADESCRIPTION` (sofern vorhanden) generiert.|  
|SKIP|Wenn das Volume einen gültigen Medienheader enthält, wird der Sicherungssatz angefügt. Alle vorhandenen Sicherungssätze werden beibehalten.|Wenn das Volume einen gültigen<sup>2</sup> Medienheader enthält, werden alle Sicherungssätze auf dem Medium überschrieben. Nur der Medienheader wird beibehalten.<br /> Wenn das Medium leer ist, wird ein Medienheader mithilfe der Optionen `MEDIANAME` und `MEDIADESCRIPTION` (sofern vorhanden) generiert.|  

<sup>1</sup> Damit der Benutzer einen Sicherungsvorgang ausführen kann, muss er den entsprechenden festen Datenbank- oder Serverrollen angehören.    

<sup>2</sup> Zur Gültigkeit gehören die MTF-Versionsnummer und andere Headerinformationen. Wenn die angegebene Version nicht unterstützt wird oder einen unerwarteten Wert hat, tritt ein Fehler auf.  
  
## <a name="compatibility"></a>Kompatibilität  
  
> [!CAUTION]  
> Sicherungen, die mit aktuelleren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt werden, können in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht wiederhergestellt werden.  
  
Um die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu gewährleisten, unterstützt BACKUP die `RESTART`-Option. RESTART hat jedoch keine Auswirkungen.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Datenbank- oder Protokollsicherungen können an das Ende jedes beliebigen Datenträgers oder Bandmediums angefügt werden. Damit ist es möglich, eine Datenbank und ihre Transaktionsprotokolle an einem einzelnen physischen Speicherort unterzubringen.  
  
Die BACKUP-Anweisung ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
Sicherungsvorgänge über Plattformen hinweg, sogar zwischen unterschiedlichen Prozessortypen, können ausgeführt werden, solange die Sortierung der Datenbank vom Betriebssystem unterstützt wird.  
 
Bei Verwendung der Sicherungskomprimierung mit [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)-fähigen Datenbanken mit einer einzelnen Datendatei wird empfohlen, eine `MAXTRANSFERSIZE` Einstellung  **zu verwenden, die 65536 (64 KB) überschreitet**.   
Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ermöglicht dies einen optimierten Komprimierungsalgorithmus für TDE-verschlüsselte Datenbanken, der eine Seite zuerst entschlüsselt, komprimiert und dann erneut verschlüsselt. Bei Verwendung von `MAXTRANSFERSIZE = 65536` (64 KB), komprimiert die Sicherungskomprimierung mit TDE-verschlüsselten Datenbanken die verschlüsselten Seiten direkt und gibt möglicherweise keine guten Komprimierungsraten aus. Weitere Informationen finden Sie unter [Backup Compression for TDE-enabled Databases (Sicherungskomprimierung für TDE-fähige Datenbanken)](http://blogs.msdn.microsoft.com/sqlcat/2016/06/20/sqlsweet16-episode-1-backup-compression-for-tde-enabled-databases/).

> [!NOTE]  
> Der optimierte Komprimierungsalgorithmus für TDE-verschlüsselte Datenbanken wird automatisch verwendet, wenn:
> * 
>  In diesem Fall wird die Standardeinstellung `MAXTRANSFERSIZE` in 1048576 (1 MB) geändert und nicht auf einen niedrigeren Wert erzwungen.
> * Die Datenbank mehrere Datendateien besitzt. In diesem Fall wird die Standardeinstellung `MAXTRANSFERSIZE` in ein Vielfaches von 65536 (64 KB) und nicht in einen niedrigeren Wert geändert (z.B. `MAXTRANSFERSIZE = 65536`). 
  
Standardmäßig wird bei jedem erfolgreichen Sicherungsvorgang dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll und dem Systemereignisprotokoll ein Eintrag hinzugefügt. Wenn Sie das Protokoll regelmäßig sichern, kann die Anzahl dieser Erfolgsmeldungen schnell ansteigen, d. h., es entstehen sehr große Fehlerprotokolle, die das Suchen nach anderen Meldungen erschweren können. In solchen Fällen können Sie diese Protokolleinträge mithilfe des Ablaufverfolgungsflags 3226 unterdrücken, wenn keines der Skripts von diesen Einträgen abhängig ist. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
## <a name="interoperability"></a>Interoperabilität  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet einen Onlinesicherungsprozess, um das Ausführen einer Datenbanksicherung zu ermöglichen, während die Datenbank weiterhin verwendet wird. Bei einer Sicherung sind die meisten Vorgänge möglich, so sind z. B. die Anweisungen INSERT, UPDATE oder DELETE bei einem Sicherungsvorgang zulässig.  
  
 Folgende Vorgänge können nicht ausgeführt werden, während eine Datenbank oder ein Transaktionsprotokoll gesichert werden:  
  
-   Dateiverwaltungsvorgänge, wie z.B. die `ALTER DATABASE`-Anweisung mit der Option `ADD FILE` oder `REMOVE FILE`.  
  
-   Vorgänge zum Verkleinern der Datenbank oder von Dateien. Dazu gehören auch Vorgänge zum automatischen Verkleinern.  
  
Wenn sich ein Sicherungsvorgang mit einem Dateiverwaltungs- oder Verkleinerungsvorgang überschneidet, tritt ein Konflikt auf. Unabhängig davon, welcher am Konflikt beteiligte Vorgang zuerst begonnen hat, wartet der zweite Vorgang auf das Timeout der Sperre, die vom ersten Vorgang angewendet wurde (der Timeoutzeitraum wird durch eine Timeouteinstellung für die Sitzung gesteuert). Wenn die Sperre während des Timeoutzeitraums aufgehoben wird, wird der zweite Vorgang fortgesetzt. Wenn das Timeout für die Sperre eintritt, erzeugt der zweite Vorgang einen Fehler.  

## <a name="limitations-for-sql-database-managed-instance"></a>Einschränkungen bei verwalteten SQL-Datenbank-Instanzen
Verwaltete SQL-Datenbank-Instanzen können eine Datenbank mit bis zu 32 Streifen speichern. Dies ist ausreichend für Datenbanken bis zu 4 TB, wenn die Sicherungskomprimierung verwendet wird.

Die max. Streifengröße bei der Speicherung beträgt 195 GB (maximale Blob-Größe). Erhöhen Sie die Streifenanzahl im Backup-Befehl, um die einzelne Streifengröße zu reduzieren und innerhalb dieser Einschränkungen zu bleiben.

> [!NOTE]
> Um diese Einschränkung lokal umgehen zu können, führen Sie eine Sicherung auf `DISK` und nicht auf `URL` durch, laden Sie die Sicherungsdatei in den Blob, und führen Sie anschließend eine Wiederherstellung durch. Die Wiederherstellung unterstützt größere Dateien, da ein anderer Blobtyp verwendet wird.

 
## <a name="metadata"></a>Metadaten  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind folgende Tabellen mit Sicherungsverläufen enthalten, in denen Sicherungsaktivitäten nachverfolgt werden:  
  
-   [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)  
-   [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
-   [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
-   [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
-   [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
Wird eine Wiederherstellung durchgeführt, wenn der Sicherungssatz noch nicht in der **msdb**-Datenbank erfasst ist, werden möglicherweise die Tabellen mit Sicherungsverläufen verändert.  
  
## <a name="security"></a>Security  
 Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] werden die Optionen `PASSWORD` und `MEDIAPASSWORD` nicht mehr für die Erstellung von Sicherungen verwendet. Es ist weiterhin möglich, mit Kennwörtern erstellte Sicherungen wiederherzustellen.  
  
### <a name="permissions"></a>Berechtigungen  
 Mitglieder der festen Serverrolle **sysadmin** und der festen Datenbankrollen **db_owner** und **db_backupoperator** verfügen standardmäßig über BACKUP DATABASE- und BACKUP LOG-Berechtigungen.  
  
 Besitz- und Berechtigungsprobleme im Zusammenhang mit der physischen Datei des Sicherungsmediums können den Sicherungsvorgang beeinträchtigen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss über Lese- und Schreibberechtigungen für das Medium verfügen. Das Konto, unter dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird, muss Schreibberechtigungen haben. Allerdings prüft die gespeicherte Prozedur [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), die den Systemtabellen einen Eintrag für ein Sicherungsmedium hinzufügt, nicht die Dateizugriffsberechtigungen. Solche Probleme mit der physischen Datei des Sicherungsmediums treten möglicherweise erst auf, wenn auf die physische Ressource zugegriffen wird, um einen Sicherungs- oder Wiederherstellungsvorgang auszuführen.  
  
##  <a name="examples"></a> Beispiele  
 Dieser Abschnitt enthält die folgenden Beispiele:  
  
-   A. [Sichern einer vollständigen Datenbank](#backing_up_db)  
-   B. [Sichern der Datenbank und des Protokolls](#backing_up_db_and_log)  
-   C. [Erstellen einer vollständigen Dateisicherung der sekundären Dateigruppen](#full_
-   file_backup)  
-   D. [Erstellen einer differenziellen Dateisicherung der sekundären Dateigruppen](#differential_file_backup)  
-   E. [Erstellen eines gespiegelten Mediensatzes für eine Medienfamilie und Sichern auf einen gespiegelten Mediensatz für eine Medienfamilie](#create_single_family_mirrored_media_set)  
-   F. [Erstellen eines gespiegelten Mediensatzes für mehrere Medienfamilien und Sichern auf einen gespiegelten Mediensatz für mehrere Medienfamilien](#create_multifamily_mirrored_media_set)  
-   G. [Sichern auf einen vorhandenen gespiegelten Mediensatz](#existing_mirrored_media_set)  
-   H. [Erstellen einer komprimierten Sicherung in einem neuen Mediensatz](#creating_compressed_backup_new_media_set)  
-   I. [Sichern in den Microsoft Azure BLOB-Speicherdienst](#url)  
  
> [!NOTE]  
> In den Themen über die Vorgehensweisen bei der Sicherung sind weitere Beispiele aufgeführt. Weitere Informationen finden Sie unter [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="backing_up_db"></a> A. Sichern einer vollständigen Datenbank  
 Im folgenden Beispiel wird die [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]-Datenbank in einer Datenträgerdatei gesichert.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH FORMAT;  
GO  
```  
  
###  <a name="backing_up_db_and_log"></a> B. Sichern der Datenbank und des Protokolls  
 Im folgenden Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank gesichert, in der standardmäßig das einfache Wiederherstellungsmodell verwendet wird. Zum Unterstützen der Protokollsicherungen wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank für die Verwendung des vollständigen Wiederherstellungsmodells geändert.  
  
 Im Beispiel wird [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) verwendet, um ein logisches [Sicherungsmedium](../../relational-databases/backup-restore/backup-devices-sql-server.md) zum Sichern von Daten zu erstellen, `AdvWorksData`, und ein anderes logisches Sicherungsmedium zum Sichern des Protokolls, `AdvWorksLog`, wird erstellt.  
  
 Im Beispiel wird eine vollständige Datenbanksicherung in `AdvWorksData` erstellt, und nach einer Updateaktivität wird das Protokoll in `AdvWorksLog` gesichert.  
  
```sql  
-- To permit log backups, before the full database backup, modify the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
   SET RECOVERY FULL;  
GO  
-- Create AdvWorksData and AdvWorksLog logical backup devices.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'Z:\SQLServerBackups\AdvWorksData.bak';  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksLog',   
'X:\SQLServerBackups\AdvWorksLog.bak';  
GO  
  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012 TO AdvWorksData;  
GO  
-- Back up the AdventureWorks2012 log.  
BACKUP LOG AdventureWorks2012  
   TO AdvWorksLog;  
GO  
```  
  
> [!NOTE]  
>  Für eine Produktionsdatenbank sollte das Protokoll regelmäßig gesichert werden. Protokollsicherungen sollten möglichst häufig ausgeführt werden, damit ein ausreichender Schutz vor Datenverlusten besteht.  
  
###  <a name="full_file_backup"></a> C. Erstellen einer vollständigen Dateisicherung der sekundären Dateigruppen  
 Im folgenden Beispiel wird eine vollständige Dateisicherung von jeder Datei der beiden sekundären Dateigruppen erstellt.  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck';  
GO  
```  
  
###  <a name="differential_file_backup"></a> D. Erstellen einer differenziellen Dateisicherung der sekundären Dateigruppen  
 Im folgenden Beispiel wird eine differenzielle Dateisicherung von jeder Datei der beiden sekundären Dateigruppen erstellt.  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
###  <a name="create_single_family_mirrored_media_set"></a> E. Erstellen eines gespiegelten Mediensatzes für eine Medienfamilie und Sichern auf einen gespiegelten Mediensatz für eine Medienfamilie  
 Im folgenden Beispiel wird ein gespiegelter Mediensatz erstellt, der eine einzelne Medienfamilie und vier Spiegel umfasst. Auf diese wird die [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]-Datenbank gesichert.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0'  
MIRROR TO TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2'  
MIRROR TO TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet0';  
```  
  
###  <a name="create_multifamily_mirrored_media_set"></a> F. Erstellen eines gespiegelten Mediensatzes für mehrere Medienfamilien und Sichern auf einen gespiegelten Mediensatz für mehrere Medienfamilien  
 Im folgenden Beispiel wird ein gespiegelter Mediensatz erstellt, in dem jeder Spiegel zwei Medienfamilien enthält. Im Beispiel wird dann die [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]-Datenbank auf beide Spiegel gesichert.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
###  <a name="existing_mirrored_media_set"></a> G. Sichern auf einen vorhandenen gespiegelten Mediensatz  
 Im folgenden Beispiel wird ein Sicherungssatz an den Mediensatz angefügt, der im vorherigen Beispiel erstellt wurde.  
  
```sql  
BACKUP LOG AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH   
   NOINIT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
> [!NOTE]  
>  Die Standardeinstellung NOINIT wird hier zur Verdeutlichung gezeigt.  
  
###  <a name="creating_compressed_backup_new_media_set"></a> H. Erstellen einer komprimierter Sicherung in einem neuen Mediensatz  
 Im folgenden Beispiel wird das Medium formatiert, wobei ein neuer Mediensatz angelegt wird, und eine vollständige, komprimierte Sicherung der [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]-Datenbank wird erstellt.  
  
```sql  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   COMPRESSION;  
```  

###  <a name="url"></a> I. Sichern in den Microsoft Azure BLOB-Speicherdienst 
In dem Beispiel wird eine vollständige Sicherung der `Sales`-Datenbank in den Microsoft Azure BLOB-Speicherdienst ausgeführt.  Der Speicherkontoname lautet `mystorageaccount`.  Der Container heißt `myfirstcontainer`.  Eine gespeicherte Zugriffsrichtlinie wurde mit Lese-, Schreib-, Lösch- und Auflistungsrechten erstellt.  Die Anmeldeinformation [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` wurde mit einer Shared Access Signature (SAS) erstellt, die der gespeicherten Zugriffsrichtlinie zugeordnet ist.  Informationen zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sicherung im Windows Azure-BLOB-Speicherdienst finden Sie unter [SQL Server-Sicherung und -Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) und [SQL Server-Sicherung über URLs](../../relational-databases/backup-restore/sql-server-backup-to-url.md).

```sql  
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Schrittweise Wiederherstellung von Datenbanken mit speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)  
  
  
