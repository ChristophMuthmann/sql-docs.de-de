---
title: BACKUP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 3654be2e02163cd8069a95eb5e82d4649cec1ab5
ms.contentlocale: de-de
ms.lasthandoff: 09/14/2017

---
# <a name="backup-transact-sql"></a>BACKUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sichert eine vollständige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank, um eine datenbanksicherung oder eine oder mehrere Dateien oder Dateigruppen der Datenbank um eine dateisicherung (BACKUP DATABASE) zu erstellen. Sichert bei Verwendung des vollständigen oder massenprotokollierten Wiederherstellungsmodells auch das Transaktionsprotokoll der Datenbank, um eine Protokollsicherung (BACKUP LOG) zu erstellen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
``` 
Backing Up a Whole Database   
BACKUP DATABASE { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
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
BACKUP LOG { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]  
[;]  
  
<backup_device>::=   
 {  
   { logical_device_name | @logical_device_name_var }   
 | { DISK | TAPE | URL} =   
     { 'physical_device_name' | @physical_device_name_var }  
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
   COPY_ONLY   
 | { COMPRESSION | NO_COMPRESSION }   
 | DESCRIPTION = { 'text' | @text_variable }   
 | NAME = { backup_set_name | @backup_set_name_var }   
 | CREDENTIAL  
 | ENCRYPTION  
 | FILE_SNAPSHOT  
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
  
--Tape Options  
   { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
--Log-specific Options  
   { NORECOVERY | STANDBY = undo_file_name }  
 | NO_TRUNCATE  
  
--Encryption Options  
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=   
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name   
```  
  
## <a name="arguments"></a>Argumente  
 DATABASE  
 Gibt eine vollständige Datenbanksicherung an. Wird eine Liste von Dateien und Dateigruppen angegeben, werden nur diese Dateien und Dateigruppen gesichert. Während einer vollständigen oder differenziellen Datenbanksicherung werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auch die erforderlichen Teile des Transaktionsprotokolls gesichert, um eine konsistente Datenbank zu erzeugen, wenn die Sicherung wiederhergestellt wird.  
  
 Wenn Sie eine Sicherung erstellt wurde, indem Sie BACKUP DATABASE restore (eine *datensicherung*), wird die gesamte Sicherung wiederhergestellt. Nur Protokollsicherungen können bis zu einem bestimmten Zeitpunkt oder bis zu einer bestimmten Transaktion in der Sicherung wiederhergestellt werden.  
  
> [!NOTE]  
>  Nur eine vollständige Sicherung ausgeführt werden kann, auf die **master** Datenbank.  
  
 LOG  
 Gibt an, dass nur das Transaktionsprotokoll gesichert wird. Das Protokoll wird von der letzten erfolgreich ausgeführten Protokollsicherung bis zum aktuellen Ende des Protokolls gesichert. Bevor Sie die erste Protokollsicherung erstellen können, müssen Sie eine vollständige Sicherung erstellen.  
  
 Sie können eine Sicherung des Protokolls auf eine bestimmte Zeit oder Transaktion in der Sicherung wiederherstellen, durch Angabe von WITH STOPAT, STOPATMARK oder STOPBEFOREMARK in Ihre [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md) Anweisung.  
  
> [!NOTE]  
>  Eine Medienfamilie muss immer auf demselben Medium innerhalb eines bestimmten Spiegels gesichert werden. Das Protokoll wird abgeschnitten, nachdem alle Datensätze innerhalb mindestens einer virtuellen Protokolldatei deaktiviert werden. Wenn das Protokoll nach routinemäßigen Protokollsicherungen nicht abgeschnitten wird, wird das Abschneiden des Protokolls möglicherweise verzögert. Weitere Informationen finden Sie weiter oben unter  
  
 { *Database_name* | **@**Database_name_var *}   
 Die Datenbank, für die ein Transaktionsprotokoll, eine Teildatenbank oder die vollständige Datenbank gesichert wird. Wenn als Variable (**@***Database_name_var*), kann dieser Name entweder als Zeichenfolgenkonstante ( **@**   *Database_name_var***=***Datenbankname*) oder als Variable eines Zeichenfolgen-Datentyp, mit Ausnahme der **Ntext** oder **Text** -Datentypen.  
  
> [!NOTE]  
>  Eine Sicherung der Spiegeldatenbank in einer Datenbank-Spiegelungspartnerschaft ist nicht möglich.  
  
\<File_or_filegroup > [ **,**... *n* ]  
 Wird nur mit BACKUP DATABASE verwendet, gibt eine Datenbankdatei oder eine Dateigruppe in einer Datenbank an, die in einer Dateisicherung enthalten sein soll, oder gibt eine schreibgeschützte Datei oder Dateigruppe an, die in einer Teilsicherung enthalten sein soll.  
  
 Datei  **=**  { *Logical_file_name*| **@***Logical_file_name_var* }  
 Der logische Name einer Datei oder einer Variablen, deren Wert dem logischen Namen einer Datei entspricht, die in der Sicherung enthalten sein soll.  
  
 DATEIGRUPPE  **=**  { *logischer_dateigruppenname*| **@***Logical_filegroup_name_var* }  
 Der logische Name einer Dateigruppe oder einer Variablen, deren Wert dem logischen Namen einer Dateigruppe entspricht, die in der Sicherung enthalten sein soll. Beim einfachen Wiederherstellungsmodell wird die Dateigruppensicherung nur für eine schreibgeschützte Dateigruppe unterstützt.  
  
> [!NOTE]  
>  Verwenden Sie Dateisicherungen dann, wenn eine Datenbanksicherung aufgrund der Datenbankgröße und aufgrund von Leistungsanforderungen nicht möglich ist.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere Dateien und Dateigruppen in einer durch Trennzeichen getrennten Liste angegeben werden können. Für die Anzahl gibt es keine Einschränkungen. 
  
 Weitere Informationen finden Sie unter: [vollständige Dateisicherungen &#40; SQLServer &#41; ](../../relational-databases/backup-restore/full-file-backups-sql-server.md) und [sichern Sie Dateien und Dateigruppen &#40; SQLServer &#41; ](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md).  
  
 READ_WRITE_FILEGROUPS [ **,** FILEGROUP = { *logischer_dateigruppenname*| **@***Logical_filegroup_name_var* } [ **,**... *n* ] ]  
 Gibt eine Teilsicherung an. Eine Teilsicherung umfasst alle Dateien mit Lese-/Schreibzugriff in einer Datenbank: die primäre Dateigruppe und alle beliebigen sekundären Dateigruppen mit Lese-/Schreibzugriff sowie auch alle angegebenen schreibgeschützten Dateien oder Dateigruppen.  
  
 READ_WRITE_FILEGROUPS  
 Gibt an, dass alle Dateigruppen mit Lese-/Schreibzugriff in der Teilsicherung gesichert werden sollen. Wenn die Datenbank schreibgeschützt ist, umfasst READ_WRITE_FILEGROUPS nur die primäre Dateigruppe.  
  
> [!IMPORTANT]  
>  Durch das explizite Auflisten der Dateigruppen mit Lese-/Schreibzugriff mithilfe von FILEGROUP anstelle von READ_WRITE_FILEGROUPS wird eine Dateisicherung erstellt.  
  
 FILEGROUP = { *logischer_dateigruppenname*| **@***Logical_filegroup_name_var* }  
Der logische Name einer schreibgeschützten Dateigruppe oder einer Variablen, deren Wert dem logischen Namen einer schreibgeschützten Dateigruppe entspricht, die in der Teilsicherung enthalten sein soll. Weitere Informationen finden Sie unter "\<File_or_filegroup >," weiter oben in diesem Thema.
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere schreibgeschützte Dateigruppen in einer durch Trennzeichen getrennten Liste angegeben werden können.  
  
 Weitere Informationen zu teilsicherungen finden Sie unter [Teilsicherungen &#40; SQLServer &#41; ](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
UM \<Backup_device > [ **,**...  *n*  ] Gibt an, die dem zugehörigen von Satz [Sicherungsmedien](../../relational-databases/backup-restore/backup-devices-sql-server.md) wird ein ungespiegeltes Medium festlegen oder den ersten Spiegel innerhalb eines gespiegelten Mediensatzes (für welche eine oder mehrere MIRROR TO Klauseln deklariert werden).  
  
\<Backup_device > Gibt ein logisches oder physisches Sicherungsmedium für den Sicherungsvorgang verwendet.  
  
 { *Logical_device_name* | **@***Logical_device_name_var* }  
 Der logische Name des Sicherungsmediums, auf dem die Datenbank gesichert wird. Der logische Name muss den Regeln für Bezeichner entsprechen. Wenn als Variable (@*Logical_device_name_var*), Name des Sicherungsmediums kann entweder als Zeichenfolgenkonstante (@*Logical_device_name_var*  **=**  logischen Sicherungsmediums) oder als Variable eines alle Zeichenfolgen-Datentyp mit Ausnahme der **Ntext** oder **Text** -Datentypen.  
  
 {DISK | BAND | URL}  **=**  { **"***Physical_device_name***"**  |   **@**  *Physical_device_name_var* }  
 Gibt eine Datenträgerdatei oder ein Bandmedium oder einen Windows Azure-BLOB-Speicherdienst an. Das URL-Format wird zum Erstellen von Sicherungen im Windows Azure-Speicherdienst verwendet. Weitere Informationen und Beispiele finden Sie unter [SQL Server-Sicherung und-Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Ein Lernprogramm finden Sie unter [Lernprogramm: SQL Server-Sicherung und-Wiederherstellung im Windows Azure Blob Storage Service](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md).  
  
> [!IMPORTANT]  
>  Mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 bis [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], Sie können nur auf einem einzelnen Gerät sichern, wenn die URL sichern. Um auf mehrere Geräte sichern, wenn zur URL sichern, verwenden Sie [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und Sie Shared Access Signature (SAS)-Token verwenden müssen. Beispiele zum Erstellen einer Shared Access Signature finden Sie in [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md) und [vereinfacht die Erstellung von SQL-Anmeldeinformationen mit Shared Access Signature (SAS)-Token in Azure Storage mit Powershell](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx).  
  
**URL betrifft**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 Das Datenträgermedium muss erst dann vorhanden sein, wenn es in einer BACKUP-Anweisung angegeben wird. Wenn das physische Medium vorhanden ist und die Option INIT in der BACKUP-Anweisung nicht angegeben ist, wird die Sicherung an das Medium angefügt.  
  
 Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)aufgezeichnet wurde.  
  
> [!NOTE]  
>  Die Option TAPE wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr bereitgestellt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass in einer durch Trennzeichen getrennten Liste möglicherweise bis zu 64 Sicherungsmedien angegeben werden.  
  
MIRROR TO \<Backup_device > [ **,**...  *n*  ] Gibt einen Satz von bis zu drei sekundären Sicherungsmedien, jedes der Spiegel den Sicherungsmedien in der TO-Klausel angegeben. Die MIRROR TO-Klausel muss denselben Typ und Anzahl der Sicherungsmedien wie die TO-Klausel angeben. Die maximale Anzahl von MIRROR TO-Klauseln lautet drei.  
  
 Diese Option ist nur in der Enterprise Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar.  
  
> [!NOTE]  
>  Für MIRROR TO = DISK legt BACKUP automatisch die geeignete Blockgröße für Datenträgermedien fest. Weitere Informationen zur Blockgröße finden Sie weiter unten in dieser Tabelle unter "BLOCKSIZE".  
  
\<Backup_device > finden Sie unter "\<Backup_device >," weiter oben in diesem Abschnitt.
  
 *n*  
 Ein Platzhalter, der anzeigt, dass in einer durch Trennzeichen getrennten Liste möglicherweise bis zu 64 Sicherungsmedien angegeben werden. Die Anzahl von Medien in der MIRROR TO-Klausel muss der Anzahl von Medien in der TO-Klausel entsprechen.  
  
 Weitere Informationen finden Sie unter "Medienfamilien in gespiegelten Mediensätzen" im Abschnitt "Hinweise" weiter unten in diesem Thema.  
  
 [ *weiter Mirror to* ]  
 Ein Platzhalter, der anzeigt, dass eine einzelne BACKUP-Anweisung zusätzlich zu der einzelnen TO-Klausel bis zu drei MIRROR TO-Klauseln enthalten kann.  
  
### <a name="with-options"></a>WITH-Optionen  
 Gibt die Optionen an, die bei einem Sicherungsvorgang verwendet werden sollen.  
  
 CREDENTIAL  
 Wird nur verwendet, wenn eine Sicherung im Windows Azure-BLOB-Speicherdienst erstellt wird.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 FILE_SNAPSHOT  
 Erstellen Sie eine Azure-Momentaufnahme der Datenbankdateien aus, wenn alle SQL Server-Datenbankdateien gespeichert sind, mit dem Azure-Blob-Speicherdienst verwendet. Weitere Informationen finden Sie unter [SQL Server-Datendateien in Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Dateimomentaufnahme-Sicherung erstellt Azure-Momentaufnahmen der Datenbankdateien (Daten- und Protokolldateien-Dateien) in einem konsistenten Zustand. Ein konsistenter Satz von Azure-Momentaufnahmen, bilden zusammen eine Sicherung und werden in der Sicherungsdatei aufgezeichnet. Der einzige Unterschied zwischen **BACKUP DATABASE, URL WITH FILE_SNAPSHOT** und **BACKUP LOG, URL WITH FILE_SNAPSHOT** ist, dass der zweite Wert wird auch das Transaktionsprotokoll abgeschnitten während der erste Wert nicht der Fall ist. Mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Momentaufnahme Sicherungen, nach der ersten vollständigen Sicherung, die erforderlich ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die sicherungskette herstellen, nur eine einzelnen transaktionsprotokollsicherung zum Wiederherstellen einer Datenbank zu dem Punkt in der Zeitpunkt der Sicherung des Transaktionsprotokolls erforderlich ist. Darüber hinaus sind nur zwei Sicherungen des Transaktionsprotokolls erforderlich, um eine Datenbank bis zu einem bestimmten Zeitpunkt zwischen dem Zeitpunkt von zwei transaktionsprotokollsicherungen wiederherstellen.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 DIFFERENTIAL  
 Gibt bei der Verwendung nur mit BACKUP DATABASE an, dass sich die Datenbank- oder Dateisicherung nur auf die Teile der Datenbank oder Datei beschränken soll, die seit der letzten vollständigen Sicherung geändert wurden. Eine differenzielle Sicherung benötigt in der Regel weniger Speicherplatz als eine vollständige Sicherung. Verwenden Sie diese Option, damit nicht alle seit der letzten vollständigen Sicherung ausgeführten individuellen Protokollsicherungen angewendet werden müssen.  
  
> [!NOTE]  
>  BACKUP DATABASE erstellt standardmäßig eine vollständige Sicherung.  
  
 Weitere Informationen finden Sie unter [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
 ENCRYPTION  
 Wird verwendet, um die Verschlüsselung für eine Sicherung anzugeben. Sie können einen Verschlüsselungsalgorithmus angeben, um die Sicherung zu verschlüsseln, oder NO_ENCRYPION angeben, um die Sicherung nicht zu verschlüsseln. Die Verschlüsselung wird empfohlen, um Sicherungsdateien zu sichern. Die Liste der Algorithmen, die Sie angeben können:  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 Wenn Sie sich für die Verschlüsselung entscheiden, müssen Sie auch die Verschlüsselung mithilfe der Verschlüsselungsoptionen angeben:  
  
-   SERVER CERTIFICATE = Encryptor_Name  
  
-   SERVER ASYMMETRIC KEY = Encryptor_Name  
  
    > [!WARNING]  
    >  Bei der Verschlüsselung in Verbindung mit dem FILE_SNAPSHOT-Argument verwendet wird, die Metadatendatei selbst wird mithilfe des angegebenen Verschlüsselungsalgorithmus verschlüsselt, und das System stellt sicher, dass TDE für die Datenbank abgeschlossen wurde. Keine zusätzliche Verschlüsselung erfolgt für die Daten selbst. Die Sicherung schlägt fehl, wenn die Datenbank nicht verschlüsselt wurde oder die backup-Anweisung wurde ausgegeben, wenn die Verschlüsselung nicht vor abgeschlossen wurde.  
  
**Sicherungssatzoptionen**  
  
Diese Optionen werden für den durch diesen Sicherungsvorgang erstellten Sicherungssatz verwendet.  
  
> [!NOTE]  
>  Um einen Sicherungssatz für einen Wiederherstellungsvorgang anzugeben, verwenden Sie die Datei  **=**   *\<Backup_set_file_number >* Option. Weitere Informationen zum Angeben eines Sicherungssatzes finden Sie unter "Angeben eines Sicherungssatzes" in [RESTORE-Argumente &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).
  
 COPY_ONLY  
 Gibt an, dass die Sicherung ist ein *kopiesicherung*, wirkt sich nicht die normale Sequenz von Sicherungen. Eine Kopiesicherung wird unabhängig von den regelmäßig geplanten konventionellen Sicherungen erstellt. Eine Kopiesicherung hat keine Auswirkungen auf die allgemeinen Sicherungs- und Wiederherstellungsprozeduren für die Datenbank.  
  
 Kopiesicherungen sollten in Situationen verwendet werden, in denen eine Sicherung für einen besonderen Zweck verwendet wird, z. B. zum Sichern des Protokolls vor einer Onlinedateiwiederherstellung. In der Regel wird eine Kopieprotokollsicherung einmal verwendet und dann gelöscht.  
  
-   Bei Verwendung mit BACKUP DATABASE wird durch die Option COPY_ONLY eine vollständige Sicherung erstellt, die nicht als eine differenzielle Basis verwendet werden kann. Das differenzielle Bitmuster wird nicht aktualisiert, und die differenziellen Sicherungen verhalten sich so, als sei die Kopiesicherung nicht vorhanden. Nachfolgende differenzielle Sicherungen verwenden die neueste, konventionelle vollständige Sicherung als Basis.  
  
    > [!IMPORTANT]  
    >  Wenn DIFFERENTIAL und COPY_ONLY zusammen verwendet werden, wird COPY_ONLY ignoriert, und eine differenzielle Sicherung wird erstellt.  
  
-   Bei Verwendung mit BACKUP LOG wird die COPY_ONLY-Option erstellt eine *kopiesicherungen protokollsicherung*, die das Transaktionsprotokoll nicht abschneidet. Die Kopieprotokollsicherung hat keine Auswirkungen auf die Protokollkette, und andere Protokollsicherungen verhalten sich so, als sei die Kopiesicherung nicht vorhanden.  
  
Weitere Informationen finden Sie unter [Kopiesicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
{ COMPRESSION | NO_COMPRESSION }  
In [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] und höheren Versionen gibt nur an, ob [sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md) für diese Sicherung, überschreiben die Standardeinstellung auf Serverebene ausgeführt wird.  
  
Die Sicherungskomprimierung wird bei der Installation standardmäßig deaktiviert. Diese Standardeinstellung kann jedoch geändert werden durch Festlegen der [Komprimierungsstandard für Sicherung](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) Serverkonfigurationsoption. Informationen zum Anzeigen des aktuellen Wert dieser Option finden Sie unter [anzeigen oder Ändern von Servereigenschaften &#40; SQLServer &#41; ](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  
  
COMPRESSION  
Aktiviert die Sicherungskomprimierung explizit.  
  
NO_COMPRESSION  
Deaktiviert die Sicherungskomprimierung explizit.  
  
DESCRIPTION **=** { **'***text***'** | **@***text_variable* }  
Gibt den freien Text an, der als Beschreibung des Sicherungssatzes verwendet wird. Die Zeichenfolge kann maximal 255 Zeichen haben.  
  
Namen  **=**  { *Backup_set_name*| **@***Backup_set_var* }  
Gibt den Namen des Sicherungssatzes an. Namen können maximal 128 Zeichen haben. Wird NAME nicht angegeben, erhält der Sicherungssatz einen leeren Namen.  
  
{EXPIREDATE **= "***Datum***"**| RETAINDAYS  **=**  *Tage* }  
Gibt an, wann der Sicherungssatz für diese Sicherung überschrieben werden kann. Wenn beide Optionen verwendet werden, hat RETAINDAYS Vorrang vor EXPIREDATE.  
  
Wenn keine der Optionen angegeben wird, richtet sich das Ablaufdatum durch die **Mediaretention** -Konfigurationseinstellung. Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)angezeigt oder konfiguriert wird.  
  
> [!IMPORTANT]  
>  Diese Optionen verhindern nur, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Datei überschreibt. Bänder können mit anderen Methoden gelöscht werden, und Dateien auf einem Datenträger können mit entsprechenden Betriebssystembefehlen gelöscht werden. Weitere Informationen zur Prüfung des Ablaufdatums finden Sie unter SKIP und FORMAT in diesem Thema.  
  
EXPIREDATE  **=**  { **"***Datum***"** |   **@**  *Date_var* }  
 Gibt an, wann der Sicherungssatz abläuft und überschrieben werden kann. Wenn als Variable (@*Date_var*), dieses Datum muss das konfigurierte System folgen **"DateTime"** formatieren und als eines der folgenden angegeben werden:  
  
-   Eine Zeichenfolgenkonstante (@*Date_var*  **=**  Datum)  
-   Eine Variable eines Zeichenfolgen-Datentyps (mit Ausnahme der **Ntext** oder **Text** Datentypen)  
-   Ein **Smalldatetime**  
-   Ein **"DateTime"** Variable  
  
Beispiel:  
  
-   `'Dec 31, 2020 11:59 PM'`  
-   `'1/1/2021'`  
  
Informationen zum Angeben der **"DateTime"** -Werte finden Sie in [Datums- und Uhrzeittypen](../../t-sql/data-types/date-and-time-types.md).  
  
> [!NOTE]  
>  Zum Ignorieren des Ablaufdatums verwenden Sie die Option SKIP.  
  
RETAINDAYS  **=**  { *Tage*| **@***Days_var* }  
 Gibt die Anzahl von Tagen an, die verstreichen müssen, bevor dieser Sicherungsmediensatz überschrieben werden kann. Wenn als Variable (**@***Days_var*), muss Sie als ganze Zahl angegeben werden.  
  
**Mediensatzoptionen**  
  
Diese Optionen werden für den Mediensatz insgesamt verwendet.  
  
{ **NOINIT** | INIT}  
 Steuert, ob der Sicherungsvorgang an die vorhandenen Sicherungssätze auf dem Sicherungsmedium angefügt wird oder diese überschreibt. Er wird standardmäßig an den neuesten Sicherungssatz auf dem Medium (NOINIT) angefügt.  
  
> [!NOTE]  
>  Informationen zu Interaktionen zwischen { **NOINIT** | INIT} und { **NOSKIP** | SKIP}, finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
NOINIT  
 Zeigt an, dass der Sicherungssatz an den angegebenen Mediensatz angehängt wird, wobei vorhandene Sicherungssätze erhalten bleiben. Wenn für den Mediensatz ein Medienkennwort definiert ist, muss dieses Kennwort angegeben werden. NOINIT ist die Standardeinstellung.  
  
Weitere Informationen finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md):  
  
INIT  
 Gibt an, dass alle Sicherungssätze überschrieben werden sollen, während der Medienheader erhalten bleibt. Wenn INIT angegeben wird, werden alle bereits auf dem Medium vorhandenen Sicherungssätze überschrieben (wenn die Bedingungen dies zulassen). Standardmäßig prüft BACKUP die folgenden Bedingungen und überschreibt die Sicherungsmedien nicht, wenn eine der Bedingungen erfüllt wird:  
  
-   Einer der Sicherungssätze ist noch nicht abgelaufen. Weitere Informationen finden Sie unter den Optionen EXPIREDATE und RETAINDAYS.  
-   Der möglicherweise in der BACKUP-Anweisung angegebene Name des Sicherungssatzes stimmt nicht mit dem Namen auf dem Sicherungsmedium überein. Weitere Informationen finden Sie unter der Option NAME weiter oben in diesem Abschnitt.  
  
Verwenden Sie die Option SKIP, um diese Überprüfungen zu überschreiben.  
  
Weitere Informationen finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md):  
  
{ **NOSKIP** | SKIP}  
Steuert, ob ein Sicherungsvorgang das Ablaufdatum und die Ablaufzeit der Sicherungssätze auf dem Medium überprüft, bevor diese überschrieben werden.  
  
> [!NOTE]  
>  Informationen zu Interaktionen zwischen { **NOINIT** | INIT} und { **NOSKIP** | SKIP}, finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
NOSKIP  
Weist die BACKUP-Anweisung an, das Ablaufdatum aller Sicherungssätze auf den Medien zu prüfen, bevor diese überschrieben werden dürfen. Dies ist das Standardverhalten.  
  
SKIP  
Deaktiviert die Prüfung von Ablaufdatum und Namen der Sicherungssätze. Diese Überprüfung wird normalerweise von der BACKUP-Anweisung ausgeführt, damit ein Überschreiben von Sicherungssätzen verhindert wird. Informationen zu Interaktionen zwischen { INIT | NOINIT } und { NOSKIP | SKIP } finden Sie unter "Hinweise" weiter unten in diesem Thema.  
Um das Ablaufdatum der Sicherungssätze anzuzeigen, Fragen Sie die **Expiration_date** Spalte die [Backupset](../../relational-databases/system-tables/backupset-transact-sql.md) Verlaufstabelle.  
  
{ **"NOFORMAT"** | DAS FORMAT}  
Gibt an, dass der Medienheader auf alle Volumes geschrieben werden soll, die für diesen Sicherungsvorgang verwendet werden. Dabei werden vorhandene Medienheader und Sicherungssätze überschrieben.  
  
NOFORMAT  
Gibt an, dass der Sicherungsvorgang die vorhandenen Medienheader und Sicherungssätze auf den Medienvolumes beibehält, die für diesen Vorgang verwendet werden. Dies ist das Standardverhalten.  
  
FORMAT  
Gibt an, dass ein neuer Mediensatz erstellt werden kann. FORMAT bewirkt, dass vom Sicherungsvorgang ein neuer Medienheader auf alle Medienvolumes geschrieben wird, die für den Sicherungsvorgang verwendet werden. Der vorhandene Inhalt des Volumes wird ungültig, da alle vorhandenen Medienheader und Sicherungssätze überschrieben werden.  
  
> [!IMPORTANT]  
>  Verwenden Sie FORMAT mit Vorsicht. Die Formatierung von Volumes eines Mediensatzes führt dazu, dass der gesamte Mediensatz nicht mehr verwendet werden kann. Wird beispielsweise ein einzelnes Band initialisiert, das zu vorhandenen Stripesetmedien gehört, führt dies dazu, dass der gesamte Mediensatz unbrauchbar wird.  
  
Durch die Angabe von FORMAT ist SKIP impliziert. SKIP muss nicht explizit angegeben werden.  
  
MEDIADESCRIPTION  **=**  { *Text* | **@***Text_variable* }  
Gibt die Freiform-Textbeschreibung des Mediensatzes an. Diese kann aus maximal 255 Zeichen bestehen.  
  
MEDIANAME  **=**  { *Media_name* | **@***Media_name_variable* }  
Gibt den Mediennamen für den gesamten Sicherungsmediensatz an. Der Medienname darf nicht mehr als 128 Zeichen umfassen. Wird MEDIANAME angegeben, muss dieser Name dem vorher angegebenen Mediennamen auf den Sicherungsvolumes entsprechen. Wird er nicht angegeben, oder ist die Option SKIP festgelegt, findet keine Prüfung des Mediennamens statt.  
  
BLOCKSIZE  **=**  { *Blocksize* | **@***Blocksize_variable* }  
Legt die physische Blockgröße in Bytes fest. Die unterstützten Größen sind 512, 1024, 2048, 4096, 8192, 16.384, 32.768 und 65.536 (64 KB) Bytes. Der Standardwert ist 65.536 für Bandmedien und andernfalls 512. In der Regel ist diese Option nicht erforderlich, da von BACKUP automatisch eine Blockgröße ausgewählt wird, die für das Medium geeignet ist. Mit der expliziten Angabe einer Blockgröße wird die automatische Wahl der Blockgröße überschrieben.  
  
Geben Sie beim Erstellen einer Sicherung, die Sie auf eine CD-ROM kopieren und von dieser wiederherstellen möchten, BLOCKSIZE=2048 an.  
  
> [!NOTE]  
>  Diese Option hat i. d. R. nur dann Auswirkungen auf die Leistung, wenn auf Bandmedien geschrieben wird.  
  
**Datenübertragungsoptionen**  
  
"BUFFERCOUNT"  **=**  { *"BUFFERCOUNT"* | **@***Buffercount_variable* }  
Gibt die Gesamtanzahl von E/A-Puffern an, die für den Sicherungsvorgang verwendet werden sollen. Sie können eine beliebige positive ganze Zahl angeben. Eine große Pufferanzahl kann jedoch wegen eines ungeeigneten virtuellen Adressraumes im Prozess Sqlservr.exe zu Fehlern aufgrund von nicht genügend Arbeitsspeicher führen.  
  
Der von den Puffern belegte Gesamtspeicherplatz richtet sich nach: *"BUFFERCOUNT"***\****"MAXTRANSFERSIZE"*.  
  
> [!NOTE]  
>  Wichtige Informationen zur Verwendung der BUFFERCOUNT-Option finden Sie unter der [falsche "BUFFERCOUNT" Data Transfer-Option kann dazu führen, dass OOM-Bedingung](http://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx) Blog.  
  
"MAXTRANSFERSIZE"  **=**  { *"MAXTRANSFERSIZE"* | **@***Maxtransfersize_variable* }  
 Gibt die größte zu verwendende Übertragungseinheit zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und dem Sicherungsmedium in Bytes an. Die möglichen Werte sind Vielfache von 65.536 Bytes (64 KB) bis hin zu 4.194.304 Bytes (4 MB).  
> [!NOTE]  
>  Beim Erstellen von Sicherungen mithilfe der SQL Writer-Dienst, wenn die Datenbank FILESTREAM konfiguriert wurde, oder In-Memory-OLTP-Dateigruppen, enthält die `MAXTRANSFERSIZE` zum Zeitpunkt der Wiederherstellung muss größer als oder gleich der `MAXTRANSFERSIZE` wurde verwendet, wenn die Sicherung erstellt wurde. 
  
**Fehlerverwaltungsoptionen**  
  
Diese Optionen können Sie bestimmen, ob sicherungsprüfsummen für den Sicherungsvorgang aktiviert werden, und gibt an, ob der Vorgang bei Auftreten eines Fehlers beendet wird.  
  
{ **NO_CHECKSUM** | CHECKSUM}  
 Steuert, ob Sicherungsprüfsummen aktiviert sind.  
  
NO_CHECKSUM  
Das Generieren von Sicherungsprüfsummen (und die Überprüfung von Seitenprüfsummen) wird explizit deaktiviert. Dies ist das Standardverhalten.  
  
CHECKSUM  
Gibt an, dass der Sicherungsvorgang jede Seite auf Prüfsumme und zerrissene Seiten überprüft, wenn aktiviert und verfügbar, und generiert eine Prüfsumme für die gesamte Sicherung.  
  
Die Verwendung von Sicherungsprüfsummen kann sich auf die Arbeitsauslastung und den Durchsatz bei der Sicherung auswirken.  
  
Weitere Informationen finden Sie unter [mögliche Medienfehler während der Sicherung und Wiederherstellung &#40; SQLServer &#41; ](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR}  
Steuert, ob ein Sicherungsvorgang beendet oder fortgesetzt wird, nachdem ein Fehler bei der Seitenprüfsumme aufgetreten ist.  
  
STOP_ON_ERROR  
Von BACKUP wird ein Fehler erzeugt, wenn eine Seitenprüfsumme nicht stimmt. Dies ist das Standardverhalten.  
  
CONTINUE_AFTER_ERROR  
BACKUP wird auch dann fortgesetzt, wenn Fehler auftreten, z. B. ungültige Prüfsummen oder zerrissene Seiten.  
  
Wenn Sie nicht zum Sichern des Protokollfragments die NO_TRUNCATE mithilfe option, wenn die Datenbank beschädigt ist, können Sie versuchen eine [Sicherung des Protokollfragments](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) durch CONTINUE_AFTER_ERROR anstelle von NO_TRUNCATE angeben.  
  
Weitere Informationen finden Sie unter [mögliche Medienfehler während der Sicherung und Wiederherstellung &#40; SQLServer &#41; ](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
**Kompatibilitätsoptionen**  
  
RESTART  
Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] keine Auswirkungen. Die Option wird von der Version aus Gründen der Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angenommen.  
  
**Optionen für die Überwachung**  
  
STATS [  **=**  *Prozentsatz* ]  
 Zeigt eine Meldung, die jedes Mal, wenn eine andere *Prozentsatz* abgeschlossen ist, und wird als Statusanzeige verwendet. Wenn *Prozentsatz* weggelassen wird, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird eine Meldung angezeigt, nach jeweils 10 Prozent abgeschlossen ist.  
  
Mit der Option STATS wird der Prozentsatz gemeldet, der beim Erreichen des Schwellenwertes für das nächste Meldungsintervall abgeschlossen ist. Bei dem angegebenen Prozentsatz handelt es sich um einen ungefähren Wert. Wird beispielsweise STATS=10 festgelegt und sind 40 Prozent des Vorgangs abgeschlossen, dann zeigt die Option u. U. 43 Prozent an. Bei größeren Sicherungssätzen stellt dies kein Problem dar, da sich der Wert für den abgeschlossenen Prozentsatz zwischen abgeschlossenen E/A-Aufrufen nur sehr langsam verändert.  
  
**Bandoptionen**  
  
Diese Optionen werden nur für Bandmedien verwendet. Diese Optionen werden ignoriert, wenn ein anderes Medium als ein Bandmedium verwendet wird.  
  
{ **REWIND** | NOREWIND }  
REWIND  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Band freigibt und zurückspult. REWIND ist die Standardeinstellung.  
  
NOREWIND  
Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Band nach dem Sicherungsvorgang offen hält. Diese Option trägt zur Leistungsverbesserung bei, wenn mehrere Sicherungsvorgänge auf einem Band ausgeführt werden.  
  
NOREWIND impliziert NOUNLOAD, und diese Optionen sind innerhalb einer BACKUP-Anweisung inkompatibel.  
  
> [!NOTE]  
>  Wenn Sie NOREWIND verwenden, bleibt die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Besitzer des Bandlaufwerks, bis in einer BACKUP- oder RESTORE-Anweisung, die in demselben Prozess ausgeführt wird, die Option REWIND oder UNLOAD verwendet wird oder bis die Serverinstanz heruntergefahren wird. Ein Offenhalten des Bandes verhindert, dass andere Prozesse auf das Band zugreifen können. Informationen dazu, wie eine Liste offener Bänder anzeigen und Schließen eines offenen Bandes finden Sie unter [Sicherungsmedien &#40; SQLServer &#41; ](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
{ **ENTLADEN** | "NOUNLOAD"}  
> [!NOTE]  
>  UNLOAD/NOUNLOAD ist eine Sitzungseinstellung, die für die Dauer der Sitzung oder bis zur Angabe der alternativen Einstellung persistent gespeichert wird.  
  
UNLOAD  
 Gibt an, dass das Band automatisch zurückgespult und ausgeworfen wird, wenn die Sicherung vollständig ausgeführt ist. UNLOAD ist die Standardeinstellung beim Beginn einer Sitzung. 
  
NOUNLOAD  
 Gibt an, dass nach der BACKUP-Vorgang im Bandlaufwerk auf dem Bandlaufwerk geladen bleibt.  
  
> [!NOTE]  
>  Beim Sichern auf einem Bandsicherungsmedium wirkt sich die Option BLOCKSIZE auf die Leistung des Sicherungsvorgangs aus. Diese Option hat i. d. R. nur dann Auswirkungen auf die Leistung, wenn auf Bandmedien geschrieben wird.  
  
**Protokollspezifische Optionen**  
  
Diese Optionen werden nur mit BACKUP LOG verwendet.  
  
> [!NOTE]  
>  Wenn Sie keine Protokollsicherungen vornehmen möchten, verwenden Sie das einfache Wiederherstellungsmodell. Weitere Informationen finden Sie unter [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
{NORECOVERY | STANDBY  **=**  *Undo_file_name* }  
  NORECOVERY  
  Sichert das Protokollfragment und belässt die Datenbank im RESTORING-Status. NORECOVERY ist hilfreich, wenn ein Failover zu einer sekundären Datenbank erfolgt oder wenn das Protokollfragment vor einem RESTORE-Vorgang gesichert wird.  
  
  Zum Ausführen einer Protokollsicherung, bei der die Protokollkürzung ausgelassen wird und die Datenbank automatisch den Status RESTORING erhält, verwenden Sie die Optionen NO_TRUNCATE und NORECOVERY zusammen.  
  
  STANDBY  **=**  *Standby_file_name*  
  Sichert das Protokollfragment und belässt die Datenbank im schreibgeschützten Modus und im STANDBY-Status. Die STANDBY-Klausel schreibt Standbydaten (wobei ein Rollback durchgeführt wird, aber mit der Option weiterer Wiederherstellungen). Die Verwendung der Option STANDBY ist gleichbedeutend mit BACKUP LOG WITH NORECOVERY gefolgt von RESTORE WITH STANDBY.  
  
  Verwenden von standby-Modus erfordert eine standbydatei gespeichert, die gemäß *Standby_file_name*, deren Speicherort im Protokoll der Datenbank gespeichert ist. Ist die angegebene Datei bereits vorhanden, wird sie von [!INCLUDE[ssDE](../../includes/ssde-md.md)] überschrieben. Ist sie noch nicht vorhanden, wird sie von [!INCLUDE[ssDE](../../includes/ssde-md.md)] erstellt. Die Standbydatei wird Teil der Datenbank.  
  
  Diese Datei enthält die Änderungen aus dem Rollback, die rückgängig gemacht werden müssen, wenn zu einem späteren Zeitpunkt RESTORE LOG-Vorgänge angewendet werden sollen. Es muss ausreichend Speicherplatz für die Vergrößerung der Standbydatei vorhanden sein, damit diese Datei alle Seiten aus der Datenbank enthalten kann, die durch das Rollback für die Transaktionen ohne Commit geändert wurden.  
  
NO_TRUNCATE  
Gibt an, dass das Protokoll nicht abgeschnitten wird, und bewirkt, dass die [!INCLUDE[ssDE](../../includes/ssde-md.md)] versucht die Sicherung unabhängig vom Status der Datenbank. Daraus folgt, dass eine Sicherung, die mit NO_TRUNCATE erstellt wird, u. U. unvollständige Metadaten enthält. Diese Option ermöglicht es, das Protokoll auch dann zu sichern, wenn die Datenbank beschädigt ist.  
  
Die NO_TRUNCATE-Option von BACKUP LOG ist gleichbedeutend mit der Angabe von COPY_ONLY und CONTINUE_AFTER_ERROR.  
  
Ohne die Option NO_TRUNCATE muss sich die Datenbank im ONLINE-Status befinden. Wenn die Datenbank im SUSPENDED-Status ist, können Sie möglicherweise durch die Angabe von NO_TRUNCATE eine Sicherung erstellen. Wenn sich die Datenbank jedoch im Status OFFLINE oder EMERGENCY befindet, ist die Sicherung auch mit NO_TRUNCATE nicht zulässig. Informationen zum Status von Datenbanken finden Sie unter [Datenbankstatus](../../relational-databases/databases/database-states.md).  
  
## <a name="about-working-with-sql-server-backups"></a>Informationen zum Arbeiten mit SQL Server-Sicherungen  
 In diesem Abschnitt werden die folgenden grundlegenden Sicherungskonzepte erläutert:  
  
 [Sicherungstypen](#Backup_Types)  
 [Kürzungen von Transaktionsprotokollen](#Tlog_Truncation)  
 [Formatieren von Sicherungsmedien](#Formatting_Media)  
 [Arbeiten mit Sicherungsmedien und Mediensätzen](#Backup_Devices_and_Media_Sets)  
 [Wiederherstellen von SQL Server-Sicherungen](#Restoring_Backups)  
  
> [!NOTE]  
>  Eine Einführung in die Sicherung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [Übersicht über Sicherungen &#40; SQLServer &#41; ](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="Backup_Types"></a>Sicherungstypen  
 Die unterstützten Sicherungstypen sind vom Wiederherstellungsmodell der Datenbank abhängig, und zwar wie folgt:  
  
-   Alle Wiederherstellungsmodelle unterstützen vollständige und differenzielle Sicherungen von Daten.  
  
    |Umfang der Sicherung|Sicherungstypen|  
    |---------------------|------------------|  
    |Gesamte Datenbank|[Datenbanksicherungen](../../relational-databases/backup-restore/full-database-backups-sql-server.md) umfassen die gesamte Datenbank.<br /><br /> Optional kann jede datenbanksicherung als Basis einer Reihe von einem oder mehreren dienen [differenzielle datenbanksicherungen](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
    |Teilweise Datenbanksicherung|[Teilsicherungen](../../relational-databases/backup-restore/partial-backups-sql-server.md) Abdeckung zu lesen, Dateigruppen / / Schreibzugriff und möglicherweise eine oder mehrere schreibgeschützte Dateien oder Dateigruppen.<br /><br /> Optional kann jede teilsicherung als Basis einer Reihe von einem oder mehreren dienen [differenzielle teilsicherungen](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
    |Datei oder Dateigruppe|[Dateisicherungen](../../relational-databases/backup-restore/full-file-backups-sql-server.md) abdecken einer oder mehrere Dateien oder Dateigruppen und nur für Datenbanken mit mehreren Dateigruppen relevant sind. Beim einfachen Wiederherstellungsmodell werden Dateisicherungen im Wesentlichen auf schreibgeschützte sekundäre Dateigruppen beschränkt.<br /> Optional kann jede dateisicherung als Basis einer Reihe von einem oder mehreren dienen [differenzielle dateisicherungen](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
  
-   Unter dem vollständigen Wiederherstellungsmodell oder beim massenprotokollierten Wiederherstellungsmodell, konventionelle Sicherungen auch enthalten die *transaktionsprotokollsicherungen* (oder *protokollsicherungen*), die erforderlich sind. Jede protokollsicherung umfasst den Teil des Transaktionsprotokolls, die beim Erstellen die Sicherung aktiv war, und enthält alle Protokolldatensätze, die nicht in einer vorherigen protokollsicherung gesichert.  
  
     Wenn Sie die Gefahr eines Datenverlusts minimieren und den damit verbundenen höheren Verwaltungsaufwand in Kauf nehmen möchten, sollten Sie häufige Protokollsicherungen planen. Wenn Sie zwischen vollständigen Sicherungen differenzielle Sicherungen planen, kann dies die Wiederherstellungszeit verkürzen, da Sie nach dem Wiederherstellen der Daten nur eine geringe Anzahl von Protokollsicherungen wiederherstellen müssen.  
  
     Es empfiehlt sich, Protokollsicherungen auf einem anderen Volume als die Datenbanksicherungen zu speichern.  
  
    > [!NOTE]  
    >  Bevor Sie die erste Protokollsicherung erstellen können, müssen Sie eine vollständige Sicherung erstellen.  
  
-   Ein *kopiesicherung* ist eine zweckgebundene vollständige oder protokollsicherung, die von der normalen Sequenz konventioneller Sicherungen unabhängig ist. Verwenden Sie zum Erstellen einer Kopiesicherung die Option COPY_ONLY in der BACKUP-Anweisung. Weitere Informationen finden Sie unter [Kopiesicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
###  <a name="Tlog_Truncation"></a>Kürzungen von Transaktionsprotokollen  
 Um das schnelle Auffüllen des Transaktionsprotokolls einer Datenbank zu vermeiden, sind routinemäßige Sicherungen von entscheidender Bedeutung. Die Protokollkürzung erfolgt beim einfachen Wiederherstellungsmodell automatisch, wenn die Datenbank gesichert wurde, und beim vollständigen Wiederherstellungsmodell, wenn das Transaktionsprotokoll gesichert wurde. Manchmal kann der Kürzungsprozess jedoch verzögert werden. Informationen zu Faktoren, die eine Protokollkürzung verzögern können, finden Sie unter [Das Transaktionsprotokoll &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> [!NOTE]  
>  Die Optionen BACKUP LOG WITH NO_LOG und WITH-TRUNCATE_ONLY werden nicht mehr unterstützt. Wechseln Sie zum einfachen Wiederherstellungsmodell, wenn Sie zur Wiederherstellung das vollständige oder das massenprotokollierte Wiederherstellungsmodell verwenden und die Protokollsicherungskette aus einer Datenbank entfernen müssen. Weitere Informationen finden Sie unter [Anzeigen oder Ändern des Wiederherstellungsmodells einer Datenbank &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
###  <a name="Formatting_Media"></a>Formatieren von Sicherungsmedien  
 Sicherungsmedien werden durch eine BACKUP-Anweisung formatiert, und zwar nur dann, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Die Option FORMAT ist angegeben.  
-   Das Medium ist leer.  
-   Mit dem Vorgang wird ein Anschlussband geschrieben.  
  
###  <a name="Backup_Devices_and_Media_Sets"></a>Arbeiten mit Sicherungsmedien und Mediensätzen  
  
#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>Sicherungsmedien in Stripesetmedien  
 Ein *Stripeset* ist ein Satz von Dateien auf Datenträgern für die Daten in Blöcke aufgeteilt und in einer festen Reihenfolge verteilt. Die Anzahl der in einem Stripeset verwendeten Sicherungsmedien muss gleich bleiben (es sei denn, die Medien werden mit FORMAT neu initialisiert).  
  
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
  
 Wenn weder MEDIANAME noch MEDIADESCRIPTION angegeben wird, wenn ein Medienheader geschrieben wird, ist für das leere Element Feld im Medienheader leer.  
  
#### <a name="working-with-a-mirrored-media-set"></a>Verwenden eines gespiegelten Mediensatzes  
 In der Regel sind Sicherungen ungespiegelt, und BACKUP-Sicherungen enthalten einfach eine TO-Klausel. Pro Mediensatz sind jedoch insgesamt vier Spiegel möglich. Bei einem gespiegelten Mediensatz schreibt der Sicherungsvorgang in mehrere Gruppen von Sicherungsmedien. Jede Gruppe von Sicherungsmedien umfasst einen einzelnen Spiegel im gespiegelten Mediensatz. Jede Spiegelung muss dieselbe Anzahl und denselben Typ von physischen Sicherungsmedien verwenden, die alle über dieselben Eigenschaften verfügen müssen.  
  
 Zum Sichern eines gespiegelten Mediensatzes müssen alle Spiegel vorhanden sein. Zum Sichern eines gespiegelten Mediensatzes geben Sie die TO-Klausel an, um den ersten Spiegel anzugeben, und geben Sie eine MIRROR TO-Klausel für jeden zusätzlichen Spiegel an.  
  
 Bei einem gespiegelten Mediensatz muss jede MIRROR TO-Klausel dieselbe Anzahl (und denselben Typ) von Medien wie die TO-Klausel aufführen. Im folgenden Beispiel wird in einen gespiegelten Mediensatz geschrieben, der zwei Spiegel enthält und drei Medien pro Spiegel verwendet:  
  
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
>  Dieses Beispiel wurde so entwickelt, dass Sie es auf Ihrem lokalen System testen können. In der Praxis würde das Sichern auf mehreren Medien desselben Laufwerks die Leistung beeinträchtigen und die Redundanz zunichte machen, für die gespiegelte Mediensätze entwickelt wurden.  
  
##### <a name="media-families-in-mirrored-media-sets"></a>Medienfamilien in gespiegelten Mediensätzen  
 Jedes in der TO-Klausel einer BACKUP-Sicherung angegebene Sicherungsmedium entspricht einer Medienfamilie. Werden beispielsweise in den TO-Klauseln drei Medien aufgelistet, schreibt BACKUP Daten in drei Medienfamilien. In einem gespiegelten Mediensatz muss jeder Spiegel eine Kopie jeder Medienfamilie enthalten. Aus diesem Grund muss die Anzahl der Medien in jedem Spiegel identisch sein.  
  
 Wenn für jeden Spiegel mehrere Medien aufgeführt sind, bestimmt die Reihenfolge der Medien, welche Medienfamilie in ein bestimmtes Medium geschrieben wird. In jeder Medienliste entspricht beispielsweise das zweite Medium der zweiten Medienfamilie. Für die im obigen Beispiel genannten Medien ist die Entsprechung zwischen Medien und Medienfamilien in der folgenden Tabelle dargestellt:  
  
|Spiegel|Medienfamilie 1|Medienfamilie 2|Medienfamilie 3|  
|------------|--------------------|--------------------|--------------------|  
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|  
|1|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|  
  
 Eine Medienfamilie muss immer auf dem gleichen Gerät innerhalb eines bestimmten Spiegels gesichert werden. Daher müssen Sie bei Verwendung eines vorhandenen Mediensatzes jedes Mal die Medien eines Spiegels in derselben Reihenfolge wie beim Erstellen des Mediensatzes aufführen.  
  
 Weitere Informationen über gespiegelte Mediensätze finden Sie unter [Gespiegelte Sicherungsmediensätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)noch nicht kennen. Weitere Informationen zu Mediensätzen und Medienfamilien im Allgemeinen finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40; SQLServer &#41; ](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
###  <a name="Restoring_Backups"></a>Wiederherstellen von SQL Server-Sicherungen  
 Zum Wiederherstellen einer Datenbank aus, und klicken Sie optional die Wiederherstellung online zu schalten oder einer Datei oder Dateigruppe wiederherstellen, verwenden Sie entweder die [!INCLUDE[tsql](../../includes/tsql-md.md)] [wiederherstellen](../../t-sql/statements/restore-statements-transact-sql.md) Anweisung oder der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **wiederherstellen** Aufgaben. Weitere Informationen finden Sie unter [wiederherstellen und Übersicht über Wiederherstellungsvorgänge &#40; SQLServer &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
##  <a name="Additional_Considerations"></a>Weitere Überlegungen zu BACKUP-Optionen  
  
###  <a name="Interactions_SKIP_etc"></a>Interaktion von SKIP, NOSKIP, INIT und NOINIT  
 In dieser Tabelle sind die Wechselwirkungen zwischen den { **NOINIT** | INIT} und { **NOSKIP** | SKIP}-Optionen.  
  
> [!NOTE]  
>  Wenn das Bandmedium leer oder die Datenträger-Sicherungsdatei nicht vorhanden ist, wird bei allen nachfolgend aufgeführten Interaktionen ein Medienheader geschrieben und erst danach fortgefahren. Wenn das Medium nicht leer ist und keinen gültigen Medienheader aufweist, wird von diesen Vorgängen die Rückmeldung gegeben, dass dies kein gültiges MTF-Medium ist, und der Sicherungsvorgang wird beendet.  
  
||NOINIT|INIT|  
|------|------------|----------|  
|NOSKIP|Überprüft, wenn das Volume einen gültigen Medienheader enthält, ob der Medienname mit dem angegebenen MEDIANAME (sofern vorhanden) übereinstimmt. Wenn dies der Fall ist, wird der Sicherungssatz angefügt, wobei alle vorhandenen Sicherungssätze beibehalten werden.<br /> Enthält das Volume keinen gültigen Medienheader, tritt ein Fehler auf.|Wenn das Volume einen gültigen Medienheader enthält, werden die folgenden Überprüfungen durchgeführt:<br /> – Wenn MEDIANAME angegeben wurde, überprüft, ob der angegebene Medienname des Medienheaders Medien name.* * übereinstimmt<br /> – Stellt sicher, dass keine abgelaufenen Sicherungssätze bereits auf dem Medium vorhanden sind. Wenn solche vorhanden sind, wird die Sicherung beendet.<br /> Wenn diese Überprüfungen erfolgreich sind, werden alle Sicherungssätze auf dem Medium überschrieben, und nur der Medienheader wird beibehalten.<br /> Wenn das Volume keinen gültigen Medienheader enthält, wird dieser mithilfe der angegebenen Optionen MEDIANAME und MEDIADESCRIPTION (sofern vorhanden) generiert.|  
|SKIP|Wenn das Volume einen gültigen Medienheader enthält, wird der Sicherungssatz angefügt. Alle vorhandenen Sicherungssätze werden beibehalten.|Wenn das Volume einen gültigen enthält * Medienheader wird, werden alle Sicherungssätze auf dem Medium, das nur den Medienheader beibehalten überschrieben.<br /> Wenn das Medium leer ist, wird ein Medienheader mithilfe der Optionen MEDIANAME und MEDIADESCRIPTION (sofern vorhanden) generiert.|  
  
 * Gültigkeit gehören die MTF-Versionsnummer und andere Headerinformationen. Wenn die angegebene Version nicht unterstützt wird oder einen unerwarteten Wert hat, tritt ein Fehler auf.  
  
 ** Der Benutzer muss der entsprechenden festen Datenbank- oder Serverrollen, einen Sicherungsvorgang auszuführen angehören.  
  
## <a name="compatibility"></a>Kompatibilität  
  
> [!CAUTION]  
>  Sicherungen, die mit aktuelleren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt werden, können in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht wiederhergestellt werden.  
  
 Um die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu gewährleisten, unterstützt BACKUP die RESTART-Option. RESTART hat jedoch keine Auswirkungen.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Datenbank- oder Protokollsicherungen können an das Ende jedes beliebigen Datenträgers oder Bandmediums angefügt werden. Damit ist es möglich, eine Datenbank und ihre Transaktionsprotokolle an einem einzelnen physischen Speicherort unterzubringen.  
  
 Die BACKUP-Anweisung ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
 Sicherungsvorgänge über Plattformen hinweg, sogar zwischen unterschiedlichen Prozessortypen, können ausgeführt werden, solange die Sortierung der Datenbank vom Betriebssystem unterstützt wird.  
  
> [!NOTE]  
>  Standardmäßig wird bei jedem erfolgreichen Sicherungsvorgang dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll und dem Systemereignisprotokoll ein Eintrag hinzugefügt. Wenn Sie das Protokoll regelmäßig sichern, kann die Anzahl dieser Erfolgsmeldungen schnell ansteigen, d. h., es entstehen sehr große Fehlerprotokolle, die das Suchen nach anderen Meldungen erschweren können. In solchen Fällen können Sie diese Protokolleinträge mithilfe des Ablaufverfolgungsflags 3226 unterdrücken, wenn keines der Skripts von diesen Einträgen abhängig ist. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
## <a name="interoperability"></a>Interoperabilität  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet einen Onlinesicherungsprozess, um das Ausführen einer Datenbanksicherung zu ermöglichen, während die Datenbank weiterhin verwendet wird. Bei einer Sicherung sind die meisten Vorgänge möglich, so sind z. B. die Anweisungen INSERT, UPDATE oder DELETE bei einem Sicherungsvorgang zulässig.  
  
 Vorgänge, die während einer Datenbank nicht ausgeführt werden können oder ein Transaktionsprotokoll gesichert enthalten:  
  
-   Vorgänge, die die Dateiverwaltung betreffen, wie z. B. die ALTER DATABASE-Anweisung mit der Option ADD FILE oder REMOVE FILE.  
  
-   Vorgänge zum Verkleinern der Datenbank oder von Dateien. Dazu gehören auch Vorgänge zum automatischen Verkleinern.  
  
Wenn sich ein Sicherungsvorgang mit einem Dateiverwaltungs- oder Verkleinerungsvorgang überschneidet, tritt ein Konflikt auf. Unabhängig davon, welcher am Konflikt beteiligte Vorgang zuerst begonnen hat, wartet der zweite Vorgang auf das Timeout der Sperre, die vom ersten Vorgang angewendet wurde (der Timeoutzeitraum wird durch eine Timeouteinstellung für die Sitzung gesteuert). Wenn die Sperre während des Timeoutzeitraums aufgehoben wird, wird der zweite Vorgang fortgesetzt. Wenn das Timeout für die Sperre eintritt, erzeugt der zweite Vorgang einen Fehler.  
  
## <a name="metadata"></a>Metadaten  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind folgende Tabellen mit Sicherungsverläufen enthalten, in denen Sicherungsaktivitäten nachverfolgt werden:  
  
-   [Backupfile &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)  
-   [Backupfilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
-   [Backupmediafamily &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
-   [Backupmediaset &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
-   [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
Wenn eine Wiederherstellung ausgeführt wird, wenn der Sicherungssatz nicht bereits in aufgezeichnet wurde die **Msdb** Datenbank, auf den Sicherungsverlauf Tabellen möglicherweise geändert werden.  
  
## <a name="security"></a>Sicherheit  
 Beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], **Kennwort** und **MEDIAPASSWORD** -Optionen nicht mehr zum Erstellen von Sicherungen. Es ist weiterhin möglich, mit Kennwörtern erstellte Sicherungen wiederherzustellen.  
  
### <a name="permissions"></a>Berechtigungen  
 Mitglieder der festen Serverrolle **sysadmin** und der festen Datenbankrollen **db_owner** und **db_backupoperator** verfügen standardmäßig über BACKUP DATABASE- und BACKUP LOG-Berechtigungen.  
  
 Besitz- und Berechtigungsprobleme im Zusammenhang mit der physischen Datei des Sicherungsmediums können den Sicherungsvorgang beeinträchtigen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss über Lese- und Schreibberechtigungen für das Medium verfügen. Das Konto, unter dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird, muss Schreibberechtigungen haben. Allerdings prüft die gespeicherte Prozedur [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), die den Systemtabellen einen Eintrag für ein Sicherungsmedium hinzufügt, nicht die Dateizugriffsberechtigungen. Solche Probleme mit der physischen Datei des Sicherungsmediums treten möglicherweise erst auf, wenn auf die physische Ressource zugegriffen wird, um einen Sicherungs- oder Wiederherstellungsvorgang auszuführen.  
  
##  <a name="examples"></a> Beispiele  
 Dieser Abschnitt enthält die folgenden Beispiele:  
  
-   A. [Sichern einer vollständigen Datenbank](#backing_up_db)  
-   B. [Sichern der Datenbank und des Protokolls](#backing_up_db_and_log)  
-   C. [Erstellen einer vollständigen dateisicherung der sekundären Dateigruppen](#full_file_backup)  
-   D. [Erstellen einer differenziellen dateisicherung der sekundären Dateigruppen](#differential_file_backup)  
-   E. [Erstellen und Sichern eines gespiegelten Medien festgelegt.](#create_single_family_mirrored_media_set)  
-   F. [Erstellen und Sichern auf einen gespiegelten festlegen](#create_multifamily_mirrored_media_set)  
-   G [Sichern auf einen vorhandenen gespiegelten Mediensatz](#existing_mirrored_media_set)  
-   H. [Erstellen einer komprimierter Sicherung in einem neuen Mediensatz](#creating_compressed_backup_new_media_set)  
-   I.  [Sichern im Microsoft Azure Blob Storage service](#url)  
  
> [!NOTE]  
>  In den Themen über die Vorgehensweisen bei der Sicherung sind weitere Beispiele aufgeführt. Weitere Informationen finden Sie unter [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="backing_up_db"></a> A. Sichern einer vollständigen Datenbank  
 Im folgende Beispiel sichert die [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] Datenbank in eine Datei.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH FORMAT;  
GO  
```  
  
###  <a name="backing_up_db_and_log"></a> B. Sichern der Datenbank und des Protokolls  
 Im folgenden Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank gesichert, in der standardmäßig das einfache Wiederherstellungsmodell verwendet wird. Zum Unterstützen der Protokollsicherungen wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank für die Verwendung des vollständigen Wiederherstellungsmodells geändert.  
  
 Als Nächstes im Beispiel wird [Sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) zum Erstellen einer logischen [Sicherungsmedium](../../relational-databases/backup-restore/backup-devices-sql-server.md) datensicherung, `AdvWorksData`, und erstellt ein anderes logisches Sicherungsmedium für das Sichern des Protokolls `AdvWorksLog`.  
  
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
  
###  <a name="existing_mirrored_media_set"></a>G. Sichern auf einen vorhandenen gespiegelten Mediensatz  
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
  
###  <a name="creating_compressed_backup_new_media_set"></a>H. Erstellen einer komprimierter Sicherung in einem neuen Mediensatz  
 Im folgenden Beispiel wird das Medium formatiert, wobei ein neuer Mediensatz angelegt wird, und eine vollständige, komprimierte Sicherung der [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]-Datenbank wird erstellt.  
  
```sql  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   COMPRESSION;  
```  

###  <a name="url"></a>ICH. Sichern in den Microsoft Azure BLOB-Speicherdienst 
Im Beispiel wird eine vollständige Sicherung der `Sales` an den Microsoft Azure Blob-Speicherdienst.  Der Speicherkontoname lautet `mystorageaccount`.  Der Container heißt `myfirstcontainer`.  Eine gespeicherte Zugriffsrichtlinie wurde mit Lese-, Schreib-, Lösch- und Auflistungsrechten erstellt.  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldeinformationen `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, erstellt wurde, mithilfe einer SAS, die der gespeicherten Zugriffsrichtlinie zugeordnet ist.  Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie im Windows Azure-Blob-Speicherdienst gesichert [SQL Server-Sicherung und-Wiederherstellung mit dem Microsoft Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) und [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).

```sql  
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```

  
## <a name="see-also"></a>Siehe auch  
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC SQLPERF &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Sp_helpfile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [Sp_helpfilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Schrittweise Wiederherstellung von Datenbanken mit speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)  
  
  

