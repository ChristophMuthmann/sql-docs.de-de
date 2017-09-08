---
title: ALTER DATABASE-Datei und Dateigruppe-Optionen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 61
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fdd1f2aaab4e4aeeced6eb069255adba5b333abf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>ALTER DATABASE (Transact-SQL) Optionen Datei und Dateigruppe 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die zu der Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gehörenden Dateien und Dateigruppen. Fügt hinzu oder entfernt Dateien und Dateigruppen aus einer Datenbank, und ändert die Attribute einer Datenbank oder Dateien und Dateigruppen. Weitere ALTER DATABASE-Optionen finden Sie unter [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
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
**\<Add_or_modify_files >:: =**
  
 Gibt die Datei an, die hinzugefügt, entfernt oder geändert werden soll.  
  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll.  
  
 ADD FILE  
 Fügt einer Datenbank eine Datei hinzu.  
  
 DATEIGRUPPE { *Filegroup_name* }  
 Gibt die Dateigruppe an, der die angegebene Datei hinzugefügt werden soll. Verwenden Sie zum Anzeigen der aktuellen Dateigruppen und die Dateigruppe der aktuelle Standard ist die ["Sys.FileGroups"](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) -Katalogsicht angezeigt.  
  
 ADD LOG FILE  
 Fügt eine Protokolldatei hinzu, die der angegebenen Datenbank hinzufügt werden soll.  
  
 REMOVE FILE *Logical_file_name*  
 Entfernt die logische Dateibeschreibung aus einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und löscht die physische Datei. Die Datei kann nur entfernt werden, wenn sie leer ist.  
  
 *logical_file_name*  
 Der logische Dateiname, der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Verweis auf die Datei verwendet wird.  
  
> [!WARNING]  
>  Entfernen einer Datenbankdatei, die FILE_SNAPSHOT Sicherungen erfolgreich ausgeführt werden, aber alle zugehörigen Momentaufnahmen werden nicht entfernt werden, um zu vermeiden, dass die Sicherungen auf die Datenbankdatei verweist. Die Datei wird abgeschnitten, jedoch nicht physisch gelöscht, um die Sicherungen FILE_SNAPSHOT intakt zu halten. Weitere Informationen finden Sie unter [SQL Server Backup and Restore with Windows Azure Blob Storage Service](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 MODIFY FILE  
 Gibt die Datei an, die geändert werden soll. Nur ein \<Filespec >-Eigenschaft kann zu einem Zeitpunkt geändert werden. Der NAME muss immer angegeben werden, der \<Filespec > zum Identifizieren der Datei, die geändert werden. Wenn SIZE angegeben ist, muss die neue Größe die aktuelle Dateigröße übersteigen.  
  
 Geben Sie in der `NAME`-Klausel den logischen Namen der Datei an, die umbenannt werden soll, und geben Sie in der `NEWNAME`-Klausel den neuen logischen Namen für die Datei an, um den logischen Namen einer Daten- oder Protokolldatei zu ändern. Beispiel:  
  
```  
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )   
```  
  
 Geben Sie den aktuellen logischen Dateinamen in der `NAME`-Klausel an, und geben Sie den neuen Pfad und den Betriebssystem-Dateinamen in der `FILENAME`-Klausel an, um eine Datendatei oder Protokolldatei an einen neuen Speicherort zu verschieben. Beispiel:  
  
```  
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )  
```  
  
 Wenn Sie einen Volltextkatalog verschieben, geben Sie nur den neuen Pfad in der FILENAME-Klausel an. Geben Sie nicht den Betriebssystem-Dateinamen an.  
  
 Weitere Informationen finden Sie unter [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md).  
  
 Bei einer FILESTREAM-Dateigruppe kann NAME online geändert werden. FILENAME kann online geändert werden; die Änderung wird jedoch erst wirksam, nachdem der Container physisch verschoben und der Server heruntergefahren und dann neu gestartet wurde.  
  
 Sie können eine FILESTREAM-Datei auf OFFLINE festlegen. Ist eine FILESTREAM-Datei offline, wird ihre übergeordnete Dateigruppe intern als offline markiert; daher schlägt jeder Zugriff auf FILESTREAM-Daten in der Dateigruppe fehl.  
  
> [!NOTE]  
>  \<Add_or_modify_files > Optionen sind nicht in einer enthaltenen Datenbank verfügbar.
  
 **\<Filespec >:: =**  
  
 Steuert die Dateieigenschaften.  
  
 Namen *Logical_file_name*  
 Gibt den logischen Namen der Datei an.  
  
 *logical_file_name*  
 Der logische Dateiname, der in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Verweis auf die Datei verwendet wird.  
  
 NEWNAME *New_logical_file_name*  
 Gibt einen neuen logischen Namen für die Datei an.  
  
 *new_logical_file_name*  
 Der Name, der den vorhandenen logischen Dateinamen ersetzen soll. Der Name muss innerhalb der Datenbank eindeutig sein und den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Der Name kann eine Zeichen- oder Unicodekonstante, ein regulärer Bezeichner oder ein Begrenzungsbezeichner sein.  
  
 FILENAME { **"***logische***"** | **"***Filestream_path* **"** | **"***Memory_optimized_data_path***"**}  
 Gibt einen Betriebssystem-Dateinamen (physischer Dateiname) an.  
  
 " *logische* "  
 Bei einer Standarddateigruppe (ROWS) ist dies der Pfad und der Dateiname, die vom Betriebssystem beim Erstellen der Datei verwendet werden. Die Datei muss befinden, auf dem Server, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist. Der angegebene Pfad muss vorhanden sein, bevor die ALTER DATABASE-Anweisung ausgeführt wird.  
  
 Die Parameter SIZE, MAXSIZE und FILEGROWTH können nicht festgelegt werden, wenn für die Datei ein UNC-Pfad angegeben ist.  
  
> [!NOTE]  
>  Systemdatenbanken dürfen nicht in Verzeichnissen von UNC-Freigaben enthalten sein.  
  
 Datendateien sollten nicht in komprimierten Dateisystemen abgelegt werden, es sei denn, die Dateien sind schreibgeschützte sekundäre Dateien, oder die Datenbank ist schreibgeschützt. Protokolldateien sollten niemals in komprimierten Dateisystemen abgelegt werden.  
  
 Wenn die Datei auf einer Rawpartition befindet *logische* müssen nur den Laufwerkbuchstaben einer vorhandenen Rawpartition angeben. Auf jeder Rawpartition kann nur eine Datei abgelegt werden.  
  
 **"** *Filestream_path* **"**  
 Für eine FILESTREAM-Dateigruppe verweist FILENAME auf einen Pfad, wo FILESTREAM-Daten gespeichert werden. Der Pfad muss bis zum letzten Ordner vorhanden sein, und der letzte Ordner darf nicht vorhanden sein. Wenn Sie z. B. den Pfad C:\MyFiles\MyFilestreamData angeben, muss C:\MyFiles vor der Ausführung von ALTER DATABASE vorhanden sein, der Ordner MyFilestreamData muss jedoch noch nicht existieren.  
  
 Die Eigenschaften SIZE und FILEGROWTH gelten nicht für eine FILESTREAM-Dateigruppe.  
  
 **"** *Memory_optimized_data_path* **"**  
 Bei einer speicheroptimierten Dateigruppe verweist FILENAME auf einen Pfad, unter dem speicheroptimierte Daten gespeichert werden. Der Pfad muss bis zum letzten Ordner vorhanden sein, und der letzte Ordner darf nicht vorhanden sein. Wenn Sie z. B. den Pfad C:\MyFiles\MyData angeben, muss C:\MyFiles vor der Ausführung von ALTER DATABASE vorhanden sein, der Ordner MyData muss jedoch noch nicht vorhanden sein.  
  
 Die Dateigruppe und die Datei (`<filespec>`) müssen in derselben Anweisung erstellt werden.  
  
 Die Eigenschaften SIZE, MAXSIZE und FILEGROWTH gelten nicht für eine speicheroptimierte Dateigruppe.  
  
 Größe *Größe*  
 Gibt die Dateigröße an. SIZE gilt nicht für FILESTREAM-Dateigruppen.  
  
 *Größe*  
 Ist die Größe der Datei.  
  
 Bei Angabe der ADD FILE *Größe* ist die Anfangsgröße für die Datei. Verbindung mit MODIFY FILE *Größe* ist die neue Größe für die Datei, und muss größer als die aktuelle Dateigröße sein.  
  
 Wenn *Größe* nicht angegeben wird, für die primäre Datei der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die Größe der primären Datei in die **Modell** Datenbank. Wenn eine sekundäre Datendatei oder Protokolldatei angegeben wird, aber *Größe* ist nicht angegeben, für die Datei die [!INCLUDE[ssDE](../../includes/ssde-md.md)] macht die Datei 1 MB.  
  
 Die Suffixe KB, MB, GB und TB können verwendet werden, um Kilobyte, Megabyte, Gigabyte oder Terabyte als Einheit anzugeben. Die Standardeinheit ist MB. Geben Sie eine ganze Zahl (also ohne Dezimalstellen) an. Um einen Bruchteil eines Megabyte anzugeben, konvertieren Sie den Wert in Kilobyte, indem Sie die Zahl mit 1024 multiplizieren. Geben Sie z. B. 1536 KB statt 1,5 MB (1,5 x 1024 = 1536) an.  
  
 MAXSIZE { *Max_size*| UNBEGRENZTE}  
 Gibt die maximale Dateigröße, die auf der die Datei vergrößert werden kann.  
  
 *max_size*  
 Die maximale Dateigröße. Die Suffixe KB, MB, GB und TB können verwendet werden, um Kilobyte, Megabyte, Gigabyte oder Terabyte als Einheit anzugeben. Die Standardeinheit ist MB. Geben Sie eine ganze Zahl (also ohne Dezimalstellen) an. Wenn *Max_size* nicht angegeben ist, wird die Dateigröße erhöht, bis der Datenträger voll ist.  
  
 UNLIMITED  
 Gibt an, dass die Größe der Datei so lange zunehmen kann, bis auf dem Datenträger kein Speicherplatz mehr verfügbar ist. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gilt für eine Protokolldatei, für die keine Größenbeschränkung festgelegt ist, eine Maximalgröße von 2 TB und für eine Datendatei eine Maximalgröße von 16 TB. Wenn diese Option für einen FILESTREAM-Container angegeben wird, gilt keine Maximalgröße. Die Dateigröße erhöht sich so lange, bis der Datenträger voll ist.  
  
 FILEGROWTH *Growth_increment*  
 Gibt das automatische Dateivergrößerungs-Inkrement an. Die FILEGROWTH-Einstellung für eine Datei darf die MAXSIZE-Einstellung nicht überschreiten. FILEGROWTH gilt nicht für FILESTREAM-Dateigruppen.  
  
 *growth_increment*  
 Die Menge an Speicherplatz, die der Datei hinzugefügt wird, wenn neuer Speicherplatz erforderlich wird.  
  
 Der Wert kann in MB, KB, GB, TB oder Prozent (%) angegeben werden. Bei Zahlen ohne Angabe von MB, KB oder % wird standardmäßig MB verwendet. Wenn der Wert in Prozent angegeben wird, ist die growth_increment-Größe der angegebene Prozentsatz der Dateigröße zum Zeitpunkt der Vergrößerung. Die angegebene Größe wird auf den nächsten durch 64 KB teilbaren Wert gerundet.  
  
 Der Wert 0 gibt an, dass die automatische Vergrößerung deaktiviert und kein zusätzlicher Speicherplatz zugelassen ist.  
  
 Ist FILEGROWTH nicht angegeben ist, sind die Standardwerte:  
  
|Version|Standardwerte|  
|-------------|--------------------|  
|Anfang[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Data 64 MB. Protokolldateien 64 MB.|  
|Anfang[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Data 1 MB. Protokolldateien Sie 10 %.|  
|Vor dem[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Daten 10 %. Protokolldateien Sie 10 %.|  
  
 OFFLINE  
 Legt die Datei auf offline fest und sperrt den Zugriff auf alle Objekte in der Dateigruppe.  
  
> [!CAUTION]  
>  Diese Option sollte nur verwendet werden, wenn die Datei beschädigt ist und wiederhergestellt werden kann. Eine Datei, für die OFFLINE festgelegt ist, kann nur wieder online geschaltet werden, indem sie aus der Sicherung wiederhergestellt wird. Weitere Informationen zum Wiederherstellen einer einzelnen Datei finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
> [!NOTE]  
>  \<Filespec > Optionen sind nicht in einer enthaltenen Datenbank verfügbar.  
  
 **\<Add_or_modify_filegroups >:: =**  
  
 Hinzufügen, Ändern oder Entfernen einer Dateigruppe aus der Datenbank.  
  
 ADD FILEGROUP *Filegroup_name*  
 Fügt der Datenbank eine Dateigruppe hinzu.  
  
 CONTAINS FILESTREAM  
 Gibt an, dass die Dateigruppe FILESTREAM-BLOBs (Binary Large Objects) im Dateisystem speichert.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt an, dass die Dateigruppe Speicheroptimierte Daten im Dateisystem speichert. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Nur eine MEMORY_OPTIMIZED_DATA-Dateigruppe ist pro Datenbank zulässig. Zum Erstellen von speicheroptimierten Tabellen kann die Dateigruppe nicht leer sein. Mindestens eine Datei muss angegeben werden. *Filegroup_name* bezieht sich auf einem Pfad. Der Pfad muss bis zum letzten Ordner vorhanden sein, und der letzte Ordner darf nicht vorhanden sein.  
  
 Im folgenden Beispiel wird eine Dateigruppe erstellt, die einer Datenbank namens xtp_db hinzugefügt wird. Außerdem wird eine Datei der Dateigruppe hinzugefügt. Die Dateigruppe speichert memory_optimized-Daten.  
  
```  
ALTER DATABASE xtp_db ADD FILEGROUP xtp_fg CONTAINS MEMORY_OPTIMIZED_DATA;  
GO  
ALTER DATABASE xtp_db ADD FILE (NAME='xtp_mod', FILENAME='d:\data\xtp_mod') TO FILEGROUP xtp_fg;  
```  
  
 Entfernen Sie DATEIGRUPPE *Filegroup_name*  
 Entfernt eine Dateigruppe aus der Datenbank. Die Dateigruppe kann nur entfernt werden, wenn sie leer ist. Entfernen Sie zuerst alle Dateien aus der Dateigruppe. Weitere Informationen finden Sie unter "REMOVE FILE *Logical_file_name*," weiter oben in diesem Thema.  
  
> [!NOTE]  
>  Wenn vom FILESTREAM-Garbage Collector nicht alle Dateien aus einem FILESTREAM-Container entfernt wurden, wird beim Ausführen von ALTER DATABASE REMOVE FILE zum Entfernen eines FILESTREAM-Containers ein Fehler erzeugt. Weitere Informationen finden Sie unter "Entfernen eines FILESTREAM-Containers" im Abschnitt "Hinweise" weiter unten in diesem Thema.  
  
MODIFY FILEGROUP *Filegroup_name* { \<Filegroup_updatability_option > | DEFAULT | Namen  **=**  *New_filegroup_name* } ändert die Dateigruppe durch Festlegen des Status auf READ_ONLY oder READ_WRITE, Festlegen der Dateigruppe die Standarddateigruppe für die Datenbank, oder ändern den Namen der Dateigruppe.  
  
 \<Filegroup_updatability_option >  
 Legt die read-only- oder read/write-Eigenschaft für die Dateigruppe fest.  
  
 DEFAULT  
 Ändert die Standarddatenbank-Dateigruppe in *Filegroup_name*. Nur in der Datenbank eine Dateigruppe als Standarddateigruppe verwendet werden kann. Weitere Informationen finden Sie unter [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 NAME = *New_filegroup_name*  
 Ändert den Namen der Dateigruppe, die *New_filegroup_name*.  
  
 OPTION AUTOGROW_SINGLE_FILE  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Wenn eine Datei in die Dateigruppe den Schwellenwert für die automatische Vergrößerung entspricht, wird nur diese Datei vergrößert. Dies ist die Standardeinstellung.  
  
 AUTOGROW_ALL_FILES  

**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Wenn eine Datei in die Dateigruppe den Schwellenwert für die automatische Vergrößerung entspricht, werden alle Dateien in der Dateigruppe.  
  
 **\<Filegroup_updatability_option >:: =**  
  
 Legt die read-only- oder read/write-Eigenschaft für die Dateigruppe fest.  
  
 READ_ONLY | READONLY  
 Gibt an, dass die Dateigruppe schreibgeschützt ist. Updates von Objekten in der Dateigruppe sind nicht zulässig. Die primäre Dateigruppe kann nicht schreibgeschützt werden. Sie müssen über exklusiven Zugriff auf die Datenbank verfügen, um diesen Status zu ändern. Weitere Informationen finden Sie unter der SINGLE_USER-Klausel.  
  
 Da in einer schreibgeschützten Datenbank keine Datenänderungen vorgenommen werden dürfen, gilt Folgendes:  
  
-   Die automatische Wiederherstellung wird beim Systemstart ausgelassen.  
  
-   Das Verkleinern der Datenbank ist nicht möglich.  
  
-   In schreibgeschützten Datenbanken werden keine Daten gesperrt. Dies kann zu einer schnelleren Ausführung von Abfragen führen.  
  
> [!NOTE]  
>  Das Schlüsselwort READONLY wird in einer zukünftigen Version von entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vermeiden Sie die Verwendung von READONLY bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen READONLY aktuell verwendet wird. Verwenden Sie stattdessen READ_ONLY.  
  
 READ_WRITE | READWRITE  
 Gibt an, dass die Gruppe den Status READ_WRITE hat. Updates sind für die Objekte in der Dateigruppe möglich. Sie müssen über exklusiven Zugriff auf die Datenbank verfügen, um diesen Status zu ändern. Weitere Informationen finden Sie unter der SINGLE_USER-Klausel.  
  
> [!NOTE]  
>  Das Schlüsselwort READWRITE wird in einer zukünftigen Version von entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vermeiden Sie die Verwendung von READWRITE bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen READWRITE aktuell verwendet wird. Verwenden Sie stattdessen READ_WRITE.  
  
 Der Status dieser Optionen kann ermittelt werden die **Is_read_only** Spalte in der **sys.databases** Katalogsicht oder die **Updateability** Eigenschaft von der DATABASEPROPERTYEX-Funktion.  
  
## <a name="remarks"></a>Hinweise  
 Um die Größe einer Datenbank zu reduzieren, verwenden Sie [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
 Sie können keine Dateien hinzufügen oder entfernen, während eine BACKUP-Anweisung ausgeführt wird.  
  
 Für jede Datenbank können maximal 32.767 Dateien und 32.767 Dateigruppen angegeben werden.  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder einer höheren Version wird der Status einer Datenbankdatei (z. B. online oder offline) unabhängig vom Status der Datenbank verwaltet. Weitere Informationen finden Sie unter [Dateistatus](../../relational-databases/databases/file-states.md). Der Status der Dateien in einer Dateigruppe bestimmt die Verfügbarkeit der gesamten Dateigruppe. Damit eine Dateigruppe verfügbar ist, müssen alle Dateien in der Dateigruppe online sein. Ist eine Dateigruppe offline, verursacht jeder Versuch, über eine SQL-Anweisung auf die Dateigruppe zuzugreifen, einen Fehler. Wenn Sie Abfragepläne für SELECT-Anweisungen erstellen, vermeidet der Abfrageoptimierer nicht gruppierte Indizes und indizierte Sichten, die sich in Offlinedateigruppen befinden. Dadurch wird ein erfolgreiches Ausführen der Anweisungen ermöglicht. Enthält die Offlinedateigruppe jedoch den Heap oder gruppierten Index der Zieltabelle, schlagen die SELECT-Anweisungen fehl. Auch alle INSERT-, UPDATE- oder DELETE-Anweisungen, die eine Tabelle mit einem Index in einer Offlinedateigruppe ändern, schlagen fehl.  
  
## <a name="moving-files"></a>Verschieben von Dateien  
 Sie können System- oder benutzerdefinierte Daten und Protokolldateien verschieben, indem Sie in FILENAME den neuen Speicherort angeben. Dies kann in den folgenden Szenarien nützlich sein:  
  
-   Bei der Wiederherstellung nach Fehlern. Beispiel: Die Datenbank befindet sich im verdächtigen Modus oder wurde wegen eines Hardwarefehlers heruntergefahren.  
  
-   Zur geplanten Verschiebung  
  
-   Verschiebung aufgrund planmäßiger datenträgerwartung  
  
 Weitere Informationen finden Sie unter [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md).  
  
## <a name="initializing-files"></a>Initialisieren von Dateien  
 Standardmäßig werden Daten- und Protokolldateien durch Ausfüllen der Dateien mit Nullen initialisiert, wenn Sie eine der folgenden Operationen ausführen:  
  
-   Erstellen Sie eine Datenbank  
  
-   Hinzufügen von Dateien zu einer vorhandenen Datenbank  
  
-   Vergrößerung einer vorhandenen Datei  
  
-   Wiederherstellen einer Datenbank oder Dateigruppe  
  
 Datendateien können sofort initialisiert werden. Dies ermöglicht ein schnelles Ausführen der entsprechenden Dateioperationen.  
  
## <a name="removing-a-filestream-container"></a>Entfernen eines FILESTREAM-Containers  
 Auch wenn der FILESTREAM-Container möglicherweise durch Ausführen von DBCC SHRINKFILE geleert wurde, kann es auch Gründen der Systemwartung erforderlich sein, Verweise auf die gelöschten Dateien beizubehalten. [Sp_filestream_force_garbage_collection &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) führt den FILESTREAM-Garbage Collector, um diese Dateien zu entfernen, wenn sie dazu sicher ist. Es sei denn, die FILESTREAM-Garbage Collector alle Dateien aus einem FILESTREAM-Container entfernt, wird die Operation ALTER DATABASEREMOVE FILE zum Entfernen eines FILESTREAM-Containers fehl, und gibt einen Fehler zurück. Um einen FILESTREAM-Container zu entfernen, wird empfohlen, den folgenden Prozess auszuführen.  
  
1.  Führen Sie [DBCC SHRINKFILE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) mit der EMPTYFILE-Option, um die aktiven Inhalte dieses Containers in andere Container zu verschieben.  
  
2.  Stellen Sie sicher, dass Protokollsicherungen im FULL- oder BULK_LOGGED-Wiederherstellungsmodell erfolgt sind.  
  
3.  Stellen Sie sicher, dass der Replikationsprotokollleser-Auftrag ausgeführt wurde, sofern erforderlich.  
  
4.  Führen Sie [Sp_filestream_force_garbage_collection &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) zum Erzwingen der Garbage Collector alle Dateien löscht, die in diesem Container nicht mehr benötigt werden.  
  
5.  Führen Sie ALTER DATABASE mit der REMOVE FILE-Option aus, um diesen Container zu entfernen.  
  
6.  Wiederholen Sie die Schritte 2 bis 4, um die Garbage Collection abzuschließen.  
  
7.  Verwenden von ALTER-Datenbank...REMOVE FILE, um diesen Container zu entfernen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-adding-a-file-to-a-database"></a>A. Hinzufügen einer Datei zu einer Datenbank  
 Im folgenden Beispiel wird der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank eine 5-MB-Datendatei hinzugefügt.  
  
```  
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
  
```  
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
  
```  
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
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4;  
GO  
  
```  
  
### <a name="e-modifying-a-file"></a>E. Ändern einer Datei  
Im folgenden Beispiel wird die Größe einer der in Beispiel B hinzugefügten Dateien reduziert.  
 Die ALTER DATABASE MODIFY FILE-Befehl kann nur eine Dateigröße, vergrößern, wenn Sie die Dateigröße kleiner vornehmen müssen, Sie DBCC SHRINKFILE verwenden müssen.  
  
```  
USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO  
```

In diesem Beispiel wird die Größe einer Datendatei auf 100 MB verkleinert, und legt dann die Größe dieser Betrag. 

```
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
>  Sie müssen die Datei physisch in das neue Verzeichnis verschieben, bevor Sie dieses Beispiel ausführen. Halten Sie anschließend die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, und starten Sie diese neu, oder schalten Sie die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank OFFLINE und wieder ONLINE, um die Änderung zu implementieren.  
  
```  
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
  
1.  Bestimmen Sie die logischen Dateinamen, der die `tempdb` Datenbank und ihren aktuellen Speicherort auf dem Datenträger.  
  
    ```  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    GO  
    ```  
  
2.  Ändern Sie den Speicherort der einzelnen Dateien mithilfe von `ALTER DATABASE`.  
  
    ```  
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
  
    ```  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    ```  
  
5.  Löschen Sie die Dateien tempdb.mdf und templog.ldf von deren ursprünglichen Speicherorten.  
  
### <a name="h-making-a-filegroup-the-default"></a>H. Festlegen einer Dateigruppe als Standarddateigruppe  
 Im folgenden Beispiel wird die `Test1FG1` Dateigruppe in Beispiel B die Standarddateigruppe erstellt. Die Standarddateigruppe wird dann auf die `PRIMARY`-Dateigruppe zurückgesetzt. `PRIMARY` muss durch eckige Klammern oder Anführungszeichen begrenzt werden.  
  
```  
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
  
```  
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
        
### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>J. Ändern Sie Dateigruppe, sodass, wenn eine Datei in die Dateigruppe den Schwellenwert für die automatische Vergrößerung erfüllt, alle Dateien in der Dateigruppe vergrößert
 Im folgenden Beispiel wird die erforderliche `ALTER DATABASE` Anweisungen zum Ändern von Dateigruppen mit Lese-/ Schreibzugriff mit der `AUTOGROW_ALL_FILES` Einstellung.  
  
```  
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
  
## <a name="see-also"></a>Siehe auch  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [Sys. data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sys. master_files &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Binary Large Object &#40;Blob&#41; Daten &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)  
  
  

