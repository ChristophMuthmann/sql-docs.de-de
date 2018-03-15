---
title: "ALTER DATABASE-Optionen für Dateien und Dateigruppen (Transact-SQL) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/07/2017
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
- ADD FILE
- ADD_FILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting files
- removing files
- deleting filegroups
- file modifications [SQL Server]
- databases [SQL Server], size
- relocating files
- databases [SQL Server], modifying
- file additions [SQL Server], ALTER DATABASE
- file moving [SQL Server]
- default filegroups
- ALTER DATABASE statement, files and filegroups
- initializing files [SQL Server]
- database files [SQL Server]
- moving files
- filegroups [SQL Server], deleting
- adding filegroups
- adding files
- database filegroups [SQL Server]
- adding log files
- modifying files
- filegroups [SQL Server], adding
- file initialization [SQL Server]
- files [SQL Server], deleting
- files [SQL Server], adding
- databases [SQL Server], moving
ms.assetid: 1f635762-f7aa-4241-9b7a-b51b22292b07
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 826b8a5abb14ee677f89f1c77956215ec72f90c6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>ALTER DATABASE-Optionen für Dateien und Dateigruppen (Transact-SQL) 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die zu der Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gehörenden Dateien und Dateigruppen. Fügt einer Datenbank Dateien und Dateigruppen hinzu oder entfernt sie, ändert die Attribute einer Datenbank oder ihrer Dateien und Dateigruppen. Informationen zu anderen ALTER DATABASE-Optionen finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER DATABASE database_name   
{  
    <add_or_modify_files>  
  | <add_or_modify_filegroups>  
}  
[;]  
  
<add_or_modify_files>::=  
{  
    ADD FILE <filespec> [ ,...n ]   
        [ TO FILEGROUP { filegroup_name } ]  
  | ADD LOG FILE <filespec> [ ,...n ]   
  | REMOVE FILE logical_file_name   
  | MODIFY FILE <filespec>  
}  
  
<filespec>::=   
(  
    NAME = logical_file_name    
    [ , NEWNAME = new_logical_name ]   
    [ , FILENAME = {'os_file_name' | 'filestream_path' | 'memory_optimized_data_path' } ]   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]   
    [ , OFFLINE ]  
)   
  
<add_or_modify_filegroups>::=  
{  
    | ADD FILEGROUP filegroup_name   
        [ CONTAINS FILESTREAM | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    | REMOVE FILEGROUP filegroup_name   
    | MODIFY FILEGROUP filegroup_name  
        { <filegroup_updatability_option>  
        | DEFAULT  
        | NAME = new_filegroup_name   
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }  
        }  
}  
<filegroup_updatability_option>::=  
{  
    { READONLY | READWRITE }   
    | { READ_ONLY | READ_WRITE }  
}  
  
```  
  
## <a name="arguments"></a>Argumente  
**\<add_or_modify_files>::=**
  
 Gibt die Datei an, die hinzugefügt, entfernt oder geändert werden soll.  
  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll.  
  
 ADD FILE  
 Fügt einer Datenbank eine Datei hinzu.  
  
 TO FILEGROUP { *filegroup_name* }  
 Gibt die Dateigruppe an, der die angegebene Datei hinzugefügt werden soll. Verwenden Sie die [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)-Katalogsicht, um die aktuellen Dateigruppen und die aktuelle Standarddateigruppe anzuzeigen.  
  
 ADD LOG FILE  
 Fügt eine Protokolldatei hinzu, die der angegebenen Datenbank hinzufügt werden soll.  
  
 REMOVE FILE *logical_file_name*  
 Entfernt die logische Dateibeschreibung aus einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und löscht die physische Datei. Die Datei kann nur entfernt werden, wenn sie leer ist.  
  
 *logical_file_name*  
 Der logische Dateiname, der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Verweis auf die Datei verwendet wird.  
  
> [!WARNING]  
> Sie können zwar eine Datenbankdatei entfernen, der FILE_SNAPSHOT-Sicherungen zugeordnet ist, jedoch werden keine zugeordneten Momentaufnahmen gelöscht, um zu vermeiden, dass die Sicherungen, die auf die Datenbankdatei verweisen, ungültig gemacht wird. Die Datei wird zwar abgeschnitten, aber nicht physisch gelöscht, damit die FILE_SNAPSHOT-Sicherungen vollständig erhalten bleiben. Weitere Informationen finden Sie unter [SQL Server Backup and Restore with Windows Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 MODIFY FILE  
 Gibt die Datei an, die geändert werden soll. Es kann jeweils nur eine \<filespec>-Eigenschaft geändert werden. NAME muss zur Identifikation der Datei, die geändert werden soll, stets in \<filespec> angegeben sein. Wenn SIZE angegeben ist, muss die neue Größe die aktuelle Dateigröße übersteigen.  
  
 Geben Sie in der `NAME`-Klausel den logischen Namen der Datei an, die umbenannt werden soll, und geben Sie in der `NEWNAME`-Klausel den neuen logischen Namen für die Datei an, um den logischen Namen einer Daten- oder Protokolldatei zu ändern. Zum Beispiel:  
  
```  
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )   
```  
  
 Geben Sie den aktuellen logischen Dateinamen in der `NAME`-Klausel an, und geben Sie den neuen Pfad und den Betriebssystem-Dateinamen in der `FILENAME`-Klausel an, um eine Datendatei oder Protokolldatei an einen neuen Speicherort zu verschieben. Zum Beispiel:  
  
```  
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )  
```  
  
 Wenn Sie einen Volltextkatalog verschieben, geben Sie nur den neuen Pfad in der FILENAME-Klausel an. Geben Sie nicht den Betriebssystem-Dateinamen an.  
  
 Weitere Informationen finden Sie unter [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md).  
  
 Bei einer FILESTREAM-Dateigruppe kann NAME online geändert werden. FILENAME kann online geändert werden; die Änderung wird jedoch erst wirksam, nachdem der Container physisch verschoben und der Server heruntergefahren und dann neu gestartet wurde.  
  
 Sie können eine FILESTREAM-Datei auf OFFLINE festlegen. Ist eine FILESTREAM-Datei offline, wird ihre übergeordnete Dateigruppe intern als offline markiert; daher schlägt jeder Zugriff auf FILESTREAM-Daten in der Dateigruppe fehl.  
  
> [!NOTE]  
>  \<add_or_modify_files>-Optionen sind in einer eigenständigen Datenbank nicht verfügbar.
  
 **\<filespec>::=**  
  
 Steuert die Dateieigenschaften.  
  
 NAME *logical_file_name*  
 Gibt den logischen Namen der Datei an.  
  
 *logical_file_name*  
 Der logische Dateiname, der in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Verweis auf die Datei verwendet wird.  
  
 NEWNAME *new_logical_file_name*  
 Gibt einen neuen logischen Namen für die Datei an.  
  
 *new_logical_file_name*  
 Der Name, der den vorhandenen logischen Dateinamen ersetzen soll. Der Name muss in der Datenbank eindeutig sein und den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Der Name kann eine Zeichen- oder Unicodekonstante, ein regulärer Bezeichner oder ein Begrenzungsbezeichner sein.  
  
 FILENAME { **'***os_file_name***'** | **'***filestream_path***'** | **'***memory_optimized_data_path***'**}  
 Gibt einen Betriebssystem-Dateinamen (physischer Dateiname) an.  
  
 ' *os_file_name* '  
 Bei einer Standarddateigruppe (ROWS) ist dies der Pfad und der Dateiname, die vom Betriebssystem beim Erstellen der Datei verwendet werden. Die Datei muss sich auf dem Server befinden, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist. Der angegebene Pfad muss vorhanden sein, bevor die ALTER DATABASE-Anweisung ausgeführt wird.  
  
 Die Parameter SIZE, MAXSIZE und FILEGROWTH können nicht festgelegt werden, wenn für die Datei ein UNC-Pfad angegeben ist.  
  
> [!NOTE]  
> Systemdatenbanken dürfen nicht in Verzeichnissen von UNC-Freigaben enthalten sein.  
  
 Datendateien sollten nicht in komprimierten Dateisystemen abgelegt werden, es sei denn, die Dateien sind schreibgeschützte sekundäre Dateien, oder die Datenbank ist schreibgeschützt. Protokolldateien sollten niemals in komprimierten Dateisystemen abgelegt werden.  
  
 Wenn sich die Datei auf einer Rawpartition befindet, darf *os_file_name* nur den Laufwerkbuchstaben einer vorhandenen Rawpartition angeben. Auf jeder Rawpartition kann nur eine Datei abgelegt werden.  
  
 **'** *filestream_path* **'**  
 Für eine FILESTREAM-Dateigruppe verweist FILENAME auf einen Pfad, wo FILESTREAM-Daten gespeichert werden. Der Pfad muss bis zum letzten Ordner vorhanden sein, und der letzte Ordner darf nicht vorhanden sein. Wenn Sie z. B. den Pfad C:\MyFiles\MyFilestreamData angeben, muss C:\MyFiles vor der Ausführung von ALTER DATABASE vorhanden sein, der Ordner MyFilestreamData muss jedoch noch nicht existieren.  
  
 Die Eigenschaften SIZE und FILEGROWTH gelten nicht für eine FILESTREAM-Dateigruppe.  
  
 **'** *memory_optimized_data_path* **'**  
 Bei einer speicheroptimierten Dateigruppe verweist FILENAME auf einen Pfad, unter dem speicheroptimierte Daten gespeichert werden. Der Pfad muss bis zum letzten Ordner vorhanden sein, und der letzte Ordner darf nicht vorhanden sein. Wenn Sie z. B. den Pfad C:\MyFiles\MyData angeben, muss C:\MyFiles vor der Ausführung von ALTER DATABASE vorhanden sein, der Ordner MyData muss jedoch noch nicht vorhanden sein.  
  
 Die Dateigruppe und die Datei (`<filespec>`) müssen in derselben Anweisung erstellt werden.  
  
 Die Eigenschaften SIZE, MAXSIZE und FILEGROWTH gelten nicht für eine speicheroptimierte Dateigruppe.  
  
 SIZE *size*  
 Gibt die Dateigröße an. SIZE gilt nicht für FILESTREAM-Dateigruppen.  
  
 *size*  
 Die Größe der Datei.  
  
 In Verbindung mit ADD FILE ist *size* die Anfangsgröße für die Datei. In Verbindung mit MODIFY FILE ist *size* die neue Größe für die Datei und muss größer als die aktuelle Dateigröße sein.  
  
 Wenn *size* für die primäre Datei nicht angegeben wird, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Größe der primären Datei in der**model**-Datenbank. Wenn eine sekundäre Datendatei oder Protokolldatei angegeben wird, für die *size* jedoch nicht angegeben ist, legt [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Größe der Datei auf 1 MB fest.  
  
 Die Suffixe KB, MB, GB und TB können verwendet werden, um Kilobyte, Megabyte, Gigabyte oder Terabyte als Einheit anzugeben. Die Standardeinheit ist MB. Geben Sie eine ganze Zahl (also ohne Dezimalstellen) an. Um einen Bruchteil eines Megabyte anzugeben, konvertieren Sie den Wert in Kilobyte, indem Sie die Zahl mit 1024 multiplizieren. Geben Sie z. B. 1536 KB statt 1,5 MB (1,5 x 1024 = 1536) an.  
  
 MAXSIZE { *max_size*| UNLIMITED }  
 Gibt die maximale Größe an, auf die die Datei vergrößert werden kann.  
  
 *max_size*  
 Die maximale Dateigröße. Die Suffixe KB, MB, GB und TB können verwendet werden, um Kilobyte, Megabyte, Gigabyte oder Terabyte als Einheit anzugeben. Die Standardeinheit ist MB. Geben Sie eine ganze Zahl (also ohne Dezimalstellen) an. Wenn *max_file_size* nicht angegeben ist, kann die Datei so lange größer werden, bis der Speicherplatz auf dem Datenträger erschöpft ist.  
  
 UNLIMITED  
 Gibt an, dass die Größe der Datei so lange zunehmen kann, bis auf dem Datenträger kein Speicherplatz mehr verfügbar ist. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gilt für eine Protokolldatei, für die keine Größenbeschränkung festgelegt ist, eine Maximalgröße von 2 TB und für eine Datendatei eine Maximalgröße von 16 TB. Wenn diese Option für einen FILESTREAM-Container angegeben wird, gilt keine Maximalgröße. Die Dateigröße erhöht sich so lange, bis der Datenträger voll ist.  
  
 FILEGROWTH *growth_increment*  
 Gibt das automatische Dateivergrößerungs-Inkrement an. Die FILEGROWTH-Einstellung für eine Datei darf die MAXSIZE-Einstellung nicht überschreiten. FILEGROWTH gilt nicht für FILESTREAM-Dateigruppen.  
  
 *growth_increment*  
 Die Menge an Speicherplatz, die der Datei hinzugefügt wird, wenn neuer Speicherplatz erforderlich wird.  
  
 Der Wert kann in MB, KB, GB, TB oder Prozent (%) angegeben werden. Bei Zahlen ohne Angabe von MB, KB oder % wird standardmäßig MB verwendet. Wenn der Wert in Prozent angegeben wird, ist die growth_increment-Größe der angegebene Prozentsatz der Dateigröße zum Zeitpunkt der Vergrößerung. Die angegebene Größe wird auf den nächsten durch 64 KB teilbaren Wert gerundet.  
  
 Der Wert 0 gibt an, dass die automatische Vergrößerung deaktiviert und kein zusätzlicher Speicherplatz zugelassen ist.  
  
 Wenn FILEGROWTH nicht angegeben ist, lauten die Standardwerte wie folgt:  
  
|Versionsoptionen|Standardwerte|  
|-------------|--------------------|  
|Seit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Daten: 64 MB, Protokolldateien: 64 MB|  
|Seit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Daten: 1 MB, Protokolldateien: 10 %|  
|Vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Daten: 10 %, Protokolldateien: 10 %|  
  
 OFFLINE  
 Legt die Datei auf offline fest und sperrt den Zugriff auf alle Objekte in der Dateigruppe.  
  
> [!CAUTION]  
>  Diese Option sollte nur verwendet werden, wenn die Datei beschädigt ist und wiederhergestellt werden kann. Eine Datei, für die OFFLINE festgelegt ist, kann nur wieder online geschaltet werden, indem sie aus der Sicherung wiederhergestellt wird. Weitere Informationen zum Wiederherstellen einer einzelnen Datei finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
> [!NOTE]  
> \<filespec>-Optionen sind in einer eigenständigen Datenbank nicht verfügbar.  
  
 **\<add_or_modify_filegroups>::=**  
  
 Hinzufügen, Ändern oder Entfernen einer Dateigruppe aus der Datenbank.  
  
 ADD FILEGROUP *filegroup_name*  
 Fügt der Datenbank eine Dateigruppe hinzu.  
  
 CONTAINS FILESTREAM  
 Gibt an, dass die Dateigruppe FILESTREAM-BLOBs (Binary Large Objects) im Dateisystem speichert.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
 Gibt an, dass die Dateigruppe arbeitsspeicheroptimierte Daten im Dateisystem speichert. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Nur eine MEMORY_OPTIMIZED_DATA-Dateigruppe ist pro Datenbank zulässig. Zum Erstellen von speicheroptimierten Tabellen kann die Dateigruppe nicht leer sein. Mindestens eine Datei muss angegeben werden. *filegroup_name* verweist auf einen Pfad. Der Pfad muss bis zum letzten Ordner vorhanden sein, und der letzte Ordner darf nicht vorhanden sein.  
  
 Im folgenden Beispiel wird eine Dateigruppe erstellt, die einer Datenbank namens xtp_db hinzugefügt wird. Außerdem wird eine Datei der Dateigruppe hinzugefügt. Die Dateigruppe speichert memory_optimized-Daten.  
  
```sql  
ALTER DATABASE xtp_db ADD FILEGROUP xtp_fg CONTAINS MEMORY_OPTIMIZED_DATA;  
GO  
ALTER DATABASE xtp_db ADD FILE (NAME='xtp_mod', FILENAME='d:\data\xtp_mod') TO FILEGROUP xtp_fg;  
```  
  
 REMOVE FILEGROUP *filegroup_name*  
 Entfernt eine Dateigruppe aus der Datenbank. Die Dateigruppe kann nur entfernt werden, wenn sie leer ist. Entfernen Sie zuerst alle Dateien aus der Dateigruppe. Weitere Informationen finden Sie im Abschnitt „REMOVE FILE *logical_file_name*“ in diesem Artikel.  
  
> [!NOTE]  
> Wenn vom FILESTREAM-Garbage Collector nicht alle Dateien aus einem FILESTREAM-Container entfernt wurden, wird beim Ausführen von ALTER DATABASE REMOVE FILE zum Entfernen eines FILESTREAM-Containers ein Fehler erzeugt. Weitere Informationen finden Sie unter "Entfernen eines FILESTREAM-Containers" im Abschnitt "Hinweise" weiter unten in diesem Thema.  
  
MODIFY FILEGROUP *filegroup_name* { \<filegroup_updatability_option> | DEFAULT | NAME **=***new_filegroup_name* } Ändert die Dateigruppe durch Festlegen des Status auf READ_ONLY oder READ_WRITE, Festlegen der Dateigruppe als Standarddateigruppe für die Datenbank oder Ändern des Dateigruppennamens.  
  
 \<filegroup_updatability_option>  
 Legt die read-only- oder read/write-Eigenschaft für die Dateigruppe fest.  
  
 DEFAULT  
 Ändert die Standarddatenbank-Dateigruppe in *filegroup_name*. Es können nicht mehrere Dateigruppen in der Datenbank gleichzeitig als Standarddateigruppe verwendet werden. Weitere Informationen finden Sie unter [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 NAME = *new_filegroup_name*  
 Ändert den Namen der Dateigruppe in *new_filegroup_name*.  
  
 AUTOGROW_SINGLE_FILE  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
 Wenn sich eine Datei in der Dateigruppe dem Schwellenwert für die automatische Vergrößerung nähert, wird nur diese Datei vergrößert. Dies ist die Standardeinstellung.  
  
 AUTOGROW_ALL_FILES  

**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
 Wenn sich eine Datei in der Dateigruppe dem Schwellenwert für die automatische Vergrößerung nähert, werden alle Dateien in der Dateigruppe vergrößert.  
  
 **\<filegroup_updatability_option>::=**  
  
 Legt die read-only- oder read/write-Eigenschaft für die Dateigruppe fest.  
  
 READ_ONLY | READONLY  
 Gibt an, dass die Dateigruppe schreibgeschützt ist. Updates von Objekten in der Dateigruppe sind nicht zulässig. Die primäre Dateigruppe kann nicht schreibgeschützt werden. Sie müssen über exklusiven Zugriff auf die Datenbank verfügen, um diesen Status zu ändern. Weitere Informationen finden Sie unter der SINGLE_USER-Klausel.  
  
 Da in einer schreibgeschützten Datenbank keine Datenänderungen vorgenommen werden dürfen, gilt Folgendes:  
  
-   Die automatische Wiederherstellung wird beim Systemstart ausgelassen.  
-   Das Verkleinern der Datenbank ist nicht möglich.  
-   In schreibgeschützten Datenbanken werden keine Daten gesperrt. Dies kann zu einer schnelleren Ausführung von Abfragen führen.  
  
> [!NOTE]  
>  Das Schlüsselwort READONLY wird in zukünftigen Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr bereitgestellt. Vermeiden Sie die Verwendung von READONLY bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen READONLY aktuell verwendet wird. Verwenden Sie stattdessen READ_ONLY.  
  
 READ_WRITE | READWRITE  
 Gibt an, dass die Gruppe den Status READ_WRITE hat. Updates sind für die Objekte in der Dateigruppe möglich. Sie müssen über exklusiven Zugriff auf die Datenbank verfügen, um diesen Status zu ändern. Weitere Informationen finden Sie unter der SINGLE_USER-Klausel.  
  
> [!NOTE]  
>  Das Schlüsselwort `READWRITE` wird in zukünftigen Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr bereitgestellt. Vermeiden Sie die Verwendung von `READWRITE` bei neuen Entwicklungsarbeiten, und planen Sie die Änderung von Anwendungen, in denen derzeit `READWRITE` verwendet wird, sodass diese stattdessen `READ_WRITE` verwenden.  
  
 Der Status dieser Optionen kann mithilfe der Spalte **is_read_only** in der **sys.databases**-Katalogsicht oder der **Updateability**-Eigenschaft der `DATABASEPROPERTYEX`-Funktion ermittelt werden.  
  
## <a name="remarks"></a>Remarks  
 Verwenden Sie [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md), um die Größe einer Datenbank zu reduzieren.  
  
Sie können keine Dateien hinzufügen oder entfernen, während eine `BACKUP`-Anweisung ausgeführt wird.  
  
Für jede Datenbank können maximal 32.767 Dateien und 32.767 Dateigruppen angegeben werden.  
  
Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder einer höheren Version wird der Status einer Datenbankdatei (z.B. online oder offline) unabhängig vom Status der Datenbank verwaltet. Weitere Informationen finden Sie im Abschnitt [Dateistatus](../../relational-databases/databases/file-states.md). 
-  Der Status der Dateien in einer Dateigruppe bestimmt die Verfügbarkeit der gesamten Dateigruppe. Damit eine Dateigruppe verfügbar ist, müssen alle Dateien in der Dateigruppe online sein. 
-  Ist eine Dateigruppe offline, verursacht jeder Versuch, über eine SQL-Anweisung auf die Dateigruppe zuzugreifen, einen Fehler. Wenn Sie Abfragepläne für `SELECT`-Anweisungen erstellen, vermeidet der Abfrageoptimierer nicht gruppierte Indizes und indizierte Sichten, die sich in Offlinedateigruppen befinden. Dadurch wird ein erfolgreiches Ausführen der Anweisungen ermöglicht. Enthält die Offlinedateigruppe jedoch den Heap oder gruppierten Index der Zieltabelle, schlagen die `SELECT`-Anweisungen fehl. Auch alle `INSERT`-, `UPDATE`- oder `DELETE`-Anweisungen, die eine Tabelle mit einem Index in einer Offlinedateigruppe ändern, schlagen fehl.  
  
## <a name="moving-files"></a>Verschieben von Dateien  
Sie können System- oder benutzerdefinierte Daten und Protokolldateien verschieben, indem Sie in FILENAME den neuen Speicherort angeben. Dies kann in den folgenden Szenarien nützlich sein:  
  
-   Bei der Wiederherstellung nach Fehlern. Beispiel: Die Datenbank befindet sich im verdächtigen Modus oder wurde aufgrund eines Hardwarefehlers heruntergefahren.  
-   Bei geplanter Verschiebung.  
-   Verschiebung aufgrund planmäßiger Datenträgerwartung.  
  
Weitere Informationen finden Sie unter [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md).  
  
## <a name="initializing-files"></a>Initialisieren von Dateien  
Standardmäßig werden Daten- und Protokolldateien durch Ausfüllen der Dateien mit Nullen initialisiert, wenn Sie eine der folgenden Operationen ausführen:  
  
-   Erstellen einer Datenbank   
-   Hinzufügen von Dateien zu einer bestehenden Datenbank.   
-   Erhöhen der Größe einer vorhandenen Datei.   
-   Wiederherstellen einer Datenbank oder Dateigruppe   
  
Datendateien können sofort initialisiert werden. Dies ermöglicht ein schnelles Ausführen der entsprechenden Dateioperationen. Weitere Informationen finden Sie unter [Datenbankdatei-Initialisierung](../../relational-databases/databases/database-instant-file-initialization.md). 
  
## <a name="removing-a-filestream-container"></a>Entfernen eines FILESTREAM-Containers  
 Auch wenn der FILESTREAM-Container möglicherweise durch Ausführen von DBCC SHRINKFILE geleert wurde, kann es auch Gründen der Systemwartung erforderlich sein, Verweise auf die gelöschten Dateien beizubehalten. [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) führt den FILESTREAM-Garbage Collector aus, um diese Dateien zum richtigen Zeitpunkt zu entfernen. Wenn vom FILESTREAM-Garbage Collector nicht alle Dateien aus einem FILESTREAM-Container entfernt wurden, wird beim Ausführen von ALTER DATABASE REMOVE FILE zum Entfernen eines FILESTREAM-Containers ein Fehler zurückgegeben. Um einen FILESTREAM-Container zu entfernen, wird empfohlen, den folgenden Prozess auszuführen.  
  
1.  Führen Sie [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) mit der EMPTYFILE-Option aus, um die aktiven Inhalte dieses Containers in andere Container zu verschieben.  
  
2.  Stellen Sie sicher, dass Protokollsicherungen im FULL- oder BULK_LOGGED-Wiederherstellungsmodell erfolgt sind.  
  
3.  Stellen Sie sicher, dass der Replikationsprotokollleser-Auftrag ausgeführt wurde, sofern erforderlich.  
  
4.  Führen Sie [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) aus, um das Löschen nicht mehr benötigter Dateien aus diesem Container durch den Garbage Collector zu erzwingen.  
  
5.  Führen Sie ALTER DATABASE mit der REMOVE FILE-Option aus, um diesen Container zu entfernen.  
  
6.  Wiederholen Sie die Schritte 2 bis 4, um die Garbage Collection abzuschließen.  
  
7.  Verwenden von ALTER-Datenbank...REMOVE FILE, um diesen Container zu entfernen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-adding-a-file-to-a-database"></a>A. Hinzufügen einer Datei zu einer Datenbank  
 Im folgenden Beispiel wird der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank eine 5-MB-Datendatei hinzugefügt.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD FILE   
(  
    NAME = Test1dat2,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat2.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
);  
GO  
  
```  
  
### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. Hinzufügen einer Dateigruppe mit zwei Dateien zu einer Datenbank  
 Im folgenden Beispiel wird die Dateigruppe `Test1FG1` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank erstellt, und der Dateigruppe werden zwei 5-MB-Dateien hinzugefügt.  
  
```sql  
USE master  
GO  
ALTER DATABASE AdventureWorks2012  
ADD FILEGROUP Test1FG1;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD FILE   
(  
    NAME = test1dat3,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat3.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
),  
(  
    NAME = test1dat4,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat4.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
)  
TO FILEGROUP Test1FG1;  
GO  
  
```  
  
### <a name="c-adding-two-log-files-to-a-database"></a>C. Hinzufügen von zwei Protokolldateien zu einer Datenbank  
 Im folgenden Beispiel werden der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zwei 5-MB-Protokolldateien hinzugefügt.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD LOG FILE   
(  
    NAME = test1log2,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\test2log.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
),  
(  
    NAME = test1log3,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\DATA\test3log.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
);  
GO  
  
```  
  
### <a name="d-removing-a-file-from-a-database"></a>D. Entfernen einer Datei aus einer Datenbank  
 Im folgenden Beispiel wird eine der in Beispiel B hinzugefügten Dateien entfernt.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4;  
GO  
```  
  
### <a name="e-modifying-a-file"></a>E. Ändern einer Datei  
Im folgenden Beispiel wird die Größe einer der in Beispiel B hinzugefügten Dateien reduziert.  
 Über den Befehl ALTER DATABASE mit MODIFY FILE kann nur die Dateigröße erhöht werden. Wenn Sie die Dateigröße hingegen verringern möchten, müssen Sie DBCC SHRINKFILE verwenden.  
  
```sql  
USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO  
```

Dieses Beispiel verringert die Größe einer Datendatei auf 100 MB und gibt diese Menge anschließend als Größe an. 

```sql
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO
```
 
  
### <a name="f-moving-a-file-to-a-new-location"></a>F. Verschieben einer Datei an einen neuen Speicherort  
 Im folgenden Beispiel wird die in Beispiel A erstellte Datei `Test1dat2` in ein neues Verzeichnis verschoben.  
  
> [!NOTE]  
> Sie müssen die Datei physisch in das neue Verzeichnis verschieben, bevor Sie dieses Beispiel ausführen. Halten Sie anschließend die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, und starten Sie diese neu, oder schalten Sie die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank OFFLINE und wieder ONLINE, um die Änderung zu implementieren.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
MODIFY FILE  
(  
    NAME = Test1dat2,  
    FILENAME = N'c:\t1dat2.ndf'  
);  
GO  
```  
  
### <a name="g-moving-tempdb-to-a-new-location"></a>G. Verschieben von tempdb an einen neuen Speicherort  
 Im folgenden Beispiel wird `tempdb` vom aktuellen Speicherort auf dem Datenträger an einen anderen Speicherort verschoben. Da `tempdb` jedes Mal beim Starten des MSSQLSERVER-Diensts neu erstellt wird, müssen Sie die Daten- und Protokolldateien nicht physisch verschieben. Die Dateien werden erstellt, sobald der Dienst in Schritt 3 neu gestartet wird. Bis der Dienst neu gestartet wird, arbeitet `tempdb` an dem bisherigen Speicherort weiter.  
  
1.  Ermitteln Sie die logischen Dateinamen der `tempdb`-Datenbank und ihren aktuellen Speicherort auf dem Datenträger.  
  
    ```sql  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    GO  
    ```  
  
2.  Ändern Sie den Speicherort der einzelnen Dateien mithilfe von `ALTER DATABASE`.  
  
    ```sql  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE  tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'E:\SQLData\templog.ldf');  
    GO  
    ```  
  
3.  Beenden Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und starten Sie sie erneut.  
  
4.  Überprüfen Sie die Dateiänderung.  
  
    ```sql  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    ```  
  
5.  Löschen Sie die Dateien tempdb.mdf und templog.ldf von deren ursprünglichen Speicherorten.  
  
### <a name="h-making-a-filegroup-the-default"></a>H. Festlegen einer Dateigruppe als Standarddateigruppe  
 Im folgenden Beispiel wird die in Beispiel B erstellte `Test1FG1`-Dateigruppe als Standarddateigruppe festgelegt. Die Standarddateigruppe wird dann auf die `PRIMARY`-Dateigruppe zurückgesetzt. `PRIMARY` muss durch eckige Klammern oder Anführungszeichen begrenzt werden.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
MODIFY FILEGROUP Test1FG1 DEFAULT;  
GO  
ALTER DATABASE AdventureWorks2012   
MODIFY FILEGROUP [PRIMARY] DEFAULT;  
GO  
```  
  
### <a name="i-adding-a-filegroup-using-alter-database"></a>I. Hinzufügen einer Dateigruppe mit ALTER DATABASE  
 Im folgenden Beispiel wird eine `FILEGROUP`, die die `FILESTREAM`-Klausel enthält, der `FileStreamPhotoDB`-Datenbank hinzugefügt.  
  
```sql  
--Create and add a FILEGROUP that CONTAINS the FILESTREAM clause to  
--the FileStreamPhotoDB database.  
ALTER DATABASE FileStreamPhotoDB  
ADD FILEGROUP TodaysPhotoShoot  
CONTAINS FILESTREAM;  
GO  
  
--Add a file for storing database photos to FILEGROUP   
ALTER DATABASE FileStreamPhotoDB  
ADD FILE  
(  
    NAME= 'PhotoShoot1',  
    FILENAME = 'C:\Users\Administrator\Pictures\TodaysPhotoShoot.ndf'  
)  
TO FILEGROUP TodaysPhotoShoot;  
GO  
```      
        
### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>J. Ändern der Dateigruppe, sodass alle Dateien in der Dateigruppe vergrößert werden, wenn sich eine Datei in der Dateigruppe dem Schwellenwert für die automatische Vergrößerung nähert
 Im folgenden Beispiel werden die erforderlichen `ALTER DATABASE`-Anweisungen generiert, um Dateien mit Lese-/Schreibzugriff mit der `AUTOGROW_ALL_FILES`-Einstellung zu ändern.  
  
```sql  
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements  
--so that all read-write filegroups grow at the same time.  
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

    SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
    INSERT INTO #tmpfgs
    EXEC (@query)

    UPDATE #tmpdbs
    SET isdone = 1
    WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
    WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
    BEGIN
        SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

        SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

        PRINT @query

        UPDATE #tmpfgs
        SET isdone = 1
        WHERE [dbid] = @dbid AND fgname = @fgname
    END
END; 
GO  
```      
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Binary Large Object &#40;Blob&#41; Daten &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)  
 [Datenbankdatei-Initialisierung](../../relational-databases/databases/database-instant-file-initialization.md)    
  
  
