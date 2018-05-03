---
title: DBCC SHRINKFILE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SHRINKFILE
- DBCC_SHRINKFILE_TSQL
- DBCC SHRINKFILE
- SHRINKFILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- TRUNCATEONLY option
- shrinking files
- NOTRUNCATE option
- shrinking databases
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
- DBCC SHRINKFILE statement
ms.assetid: e02b2318-bee9-4d84-a61f-2fddcf268c9f
caps.latest.revision: 87
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5225b9c6da68489845921f6351e86eb36a02358a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-shrinkfile-transact-sql"></a>DBCC SHRINKFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Reduziert die Größe der angegebenen Daten- oder Protokolldatei für die aktuelle Datenbank oder leert eine Datei, indem die Daten aus der angegebenen Datei in andere Dateien in derselben Dateigruppe verschoben werden, sodass die Datei aus der Datenbank entfernt werden kann. Sie können eine Datei auf eine Größe reduzieren, die kleiner ist als die bei der Erstellung angegebene Größe. Dadurch wird die Mindestdateigröße auf den neuen Wert zurückgesetzt.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
  
DBCC SHRINKFILE   
(  
    { file_name | file_id }   
    { [ , EMPTYFILE ]   
    | [ [ , target_size ] [ , { NOTRUNCATE | TRUNCATEONLY } ] ]  
    }  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
*file_name*  
Der logische Name der Datei, die verkleinert werden soll.
  
*file_id*  
Die Datei-ID der Datei, die verkleinert werden soll. Verwenden Sie zum Ermitteln einer Datei-ID die [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)-Systemfunktion, oder fragen Sie die [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)-Katalogsicht in der aktuellen Datenbank ab.
  
*target_size*  
Die Größe für die Datei in MB (als ganze Zahl). Wenn nichts angegeben wird, wird die Größe von DBCC SHRINKFILE auf die standardmäßige Dateigröße reduziert. Die Standardgröße ist die Größe, die beim Erstellen der Datei angegeben wurde.
  
> [!NOTE]  
>  Sie können die Standardgröße einer leeren Datei mit DBCC SHRINKFILE *target_size* verringern. Wenn Sie z. B. eine 5 MB große Datei erstellen und die Dateigröße dann auf 3 MB herabsetzen, während die Datei noch leer ist, wird die Standarddateigröße auf 3 MB festgelegt. Dies gilt nur für leere Dateien, die nie Daten enthalten haben.  
  
Diese Option wird in FILESTREAM-Dateigruppencontainern nicht unterstützt.  
Wenn *target_size* angegeben wird, versucht DBCC SHRINKFILE, die Datei auf die gewünschte Größe zu verkleinern. Bereits verwendete Seiten in dem Teil der Datei, der freigegeben werden soll, werden auf freien Speicherplatz in dem Teil der Datei verschoben, der beibehalten werden soll. Ist z.B. eine Datendatei mit einer Größe von 10 MB vorhanden, wird durch einen DBCC SHRINKFILE-Vorgang mit einem *target_size*-Wert von 8 veranlasst, dass alle verwendeten Seiten, die sich in den letzten 2 MB der Datei befinden, in nicht zugeordnete Seiten der ersten 8 MB dieser Datei verschoben werden. DBCC SHRINKFILE verkleinert die Datei nur so weit, dass der erforderliche Speicherplatz für die Daten unangetastet bleibt. Werden beispielsweise 7 MB einer 10 MB großen Datendatei verwendet, verkleinert eine DBCC SHRINKFILE-Anweisung mit einem *target_size*-Wert von 6 die Datei lediglich auf 7 MB statt auf 6 MB.
  
EMPTYFILE  
Verlagert alle Daten aus der angegebenen Datei in andere Dateien in **derselben Dateigruppe**. EMPTYFILE migriert die Daten also aus der angegebenen Datei zu anderen Dateien in derselben Dateigruppe. EMPTYFILE stellt sicher, dass der Datei keine neuen Daten hinzugefügt werden. Die Datei kann mithilfe der [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)-Anweisung entfernt werden.
Die Datei kann aus FILESTREAM-Dateigruppencontainern erst dann mit ALTER DATABASE entfernt werden, nachdem der FILESTREAM-Garbage Collector ausgeführt und alle nicht benötigten Dateigruppen-Containerdateien gelöscht wurden, die von EMPTYFILE in einen anderen Container kopiert wurden. Weitere Informationen finden Sie unter [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md).
  
> [!NOTE]  
>  Informationen zum Entfernen eines FILESTREAM-Containers finden Sie im entsprechenden Abschnitt [ALTER DATABASE-Optionen für Dateien und Dateigruppen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
NOTRUNCATE  
Verschiebt zugeordnete Seiten vom Ende einer Datendatei in nicht zugeordnete Seiten am Dateianfang, und zwar mit oder ohne Angabe von *target_percent*. Der freie Speicherplatz am Dateiende wird nicht an das Betriebssystem zurückgegeben, und die physische Größe der Datei bleibt unverändert. Daher scheint die Datei bei Angabe von NOTRUNCATE nicht verkleinert zu werden.
NOTRUNCATE gilt nur für Datendateien. Die Protokolldateien sind nicht betroffen.   Diese Option wird in FILESTREAM-Dateigruppencontainern nicht unterstützt.
  
TRUNCATEONLY  
Gibt den gesamten freien Speicherplatz am Dateiende an das Betriebssystem frei, es werden jedoch keine Seiten innerhalb der Datei verschoben. Die Datendatei wird nur bis zum letzten zugeordneten Block verkleinert.
Der Parameter *target_size* wird ignoriert, wenn er mit TRUNCATEONLY angegeben wird.  
Die Option TRUNCATEONLY verschiebt Informationen nicht in das Protokoll, entfernt jedoch inaktive VLFs am Ende der Protokolldatei. Diese Option wird in FILESTREAM-Dateigruppencontainern nicht unterstützt.
  
WITH NO_INFOMSGS  
Alle Informationsmeldungen werden unterdrückt.
  
## <a name="result-sets"></a>Resultsets  
In der folgenden Tabelle werden die Spalten des Resultsets beschrieben:
  
|Spaltenname|Description|  
|---|---|
|**DbId**|Die Datenbank-ID der Datei, die das [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu verkleinern versuchte.|  
|**FileId**|Die Datei-ID der Datei, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu verkleinern versuchte.|  
|**CurrentSize**|Die Anzahl von 8-KB-Seiten, die die Datei derzeit belegt.|  
|**MinimumSize**|Die Anzahl von 8-KB-Seiten, die die Datei minimal belegen könnte. Dies entspricht der Mindestgröße bzw. der ursprünglich erzeugten Dateigröße.|  
|**UsedPages**|Die Anzahl von 8-KB-Seiten, die derzeit von der Datei verwendet werden.|  
|**EstimatedPages**|Die Anzahl an 8-KB-Seiten, auf die die Datei wahrscheinlich vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] verkleinert werden kann.|  
  
## <a name="remarks"></a>Remarks  
DBCC SHRINKFILE gilt für die Dateien der aktuellen Datenbank. Weitere Informationen zum Ändern der aktuellen Datenbank finden Sie unter [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md).
  
DBCC SHRINKFILE-Vorgänge können an jeder Stelle des Prozesses beendet werden, wobei der abgeschlossene Anteil erhalten bleibt. Wenn der EMPTYFILE-Parameter in einer Datei verwendet und der Vorgang unterbrochen wird, wird die Datei nicht markiert, um das Hinzufügen weiterer Daten zu verhindern.
  
Wenn ein DBCC SHRINKFILE-Vorgang fehlschlägt, wird ein Fehler ausgelöst.
  
 Die Datenbank, die verkleinert werden soll, muss sich nicht im Einzelbenutzermodus befinden. Andere Benutzer können während der Verkleinerung der Datei an der Datenbank arbeiten. Um die Systemdatenbanken zu verkleinern, muss auch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht im Einzelbenutzermodus ausgeführt werden.  
  
## <a name="shrinking-a-log-file"></a>Verkleinern einer Protokolldatei  
Bei Protokolldateien wird *target_size* von [!INCLUDE[ssDE](../../includes/ssde-md.md)] dazu verwendet, die Zielgröße der gesamten Protokolldatei zu berechnen, sodass *target_size* die Größe des freien Speicherplatzes in der Protokolldatei nach dem Verkleinern angibt. Die Zielgröße des gesamten Protokolls wird dann in die Zielgröße für jede Protokolldatei umgewandelt. DBCC SHRINKFILE versucht, jede physische Protokolldatei sofort auf ihre Zielgröße zu verkleinern. Wenn sich dagegen ein Teil des logischen Protokolls in den virtuellen Protokollen befindet, die außerhalb der Zielgröße liegen, gibt das [!INCLUDE[ssDE](../../includes/ssde-md.md)] so viel Speicherplatz frei wie möglich und gibt dann eine Informationsmeldung aus. Die Meldung beschreibt, welche Aktionen erforderlich sind, um das logische Protokoll aus den virtuellen Protokollen am Ende der Datei zu verschieben. Nachdem diese Aktionen ausgeführt wurden, kann der verbleibende Speicherplatz mit DBCC SHRINKFILE freigegeben werden.
  
Da eine Protokolldatei nur auf eine Grenze einer virtuellen Protokolldatei verkleinert werden kann, ist eine Verkleinerung der Protokolldatei auf eine geringere Größe als die einer virtuellen Protokolldatei u. U. nicht möglich, selbst wenn die Protokolldatei nicht verwendet wird. Die Größe der virtuellen Protokolldatei wird dynamisch vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] ausgewählt, wenn Protokolldateien erstellt oder erweitert werden.
  
## <a name="best-practices"></a>Bewährte Methoden  
Berücksichtigen Sie die folgenden Informationen, wenn Sie eine Datei verkleinern möchten:
-   Ein Verkleinerungsvorgang ist am effektivsten nach einem Vorgang, durch den umfangreicher nicht verwendeter Speicherplatz bereitgestellt wird, z. B. das Abschneiden oder Löschen einer Tabelle.  
-   Die meisten Datenbanken erfordern verfügbaren freien Speicherplatz für die normalen alltäglichen Vorgänge. Wenn Sie eine Datenbank wiederholt verkleinern und feststellen, dass die Datenbankgröße wieder zunimmt, deutet dies darauf hin, dass der verkleinerte Speicherplatz für regelmäßige Vorgänge benötigt wird. In diesem Fall ist das Verkleinern der Datenbank vergeblich.  
-   Bei einem Verkleinerungsvorgang bleibt der Fragmentierungszustand der Indizes in der Datenbank nicht erhalten. Im Allgemeinen wird die Fragmentierung zu einem gewissen Grad verstärkt. Dies ist ein weiterer Grund, die Datenbank nicht wiederholt zu verkleinern.  
-   Verkleinern Sie mehrere Dateien in der gleichen Datenbank sequenziell statt gleichzeitig. Konflikte bei Systemtabellen können aufgrund der Blockierung Verzögerungen verursachen.  
  
## <a name="troubleshooting"></a>Problembehandlung  
In diesem Abschnitt wird beschrieben, wie Probleme, die beim Ausführen des DBCC SHRINKFILE-Befehls auftreten können, diagnostiziert und behoben werden.
  
### <a name="the-file-does-not-shrink"></a>Die Datei wird nicht verkleinert  
Wenn beim Verkleinerungsvorgang kein Fehler auftritt, die Dateigröße jedoch unverändert scheint, überprüfen Sie, ob die Datei über ausreichend freien zu entfernenden Speicherplatz verfügt. Führen Sie dazu eine der folgenden Aktionen aus:
- Führen Sie die folgende Abfrage aus.  
  
```sql
SELECT name ,size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 AS AvailableSpaceInMB
FROM sys.database_files;
```

-   Führen Sie den Befehl [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md) aus, um den vom Transaktionsprotokoll verwendeten Speicherplatz zurückzugeben.  
Falls nicht ausreichend Speicherplatz verfügbar ist, kann die Dateigröße durch den Verkleinerungsvorgang nicht weiter reduziert werden.
  
In der Regel ist es die Protokolldatei, die scheinbar nicht verkleinert wurde. Gewöhnlich liegt es daran, dass die Protokolldatei nicht abgeschnitten wurde. Sie können das Protokoll abschneiden, indem Sie das Wiederherstellungsmodell der Datenbank auf SIMPLE festlegen oder indem Sie das Protokoll sichern und dann den DBCC SHRINKFILE-Vorgang erneut ausführen.
  
### <a name="the-shrink-operation-is-blocked"></a>Der Verkleinerungsvorgang ist blockiert  
Es kann vorkommen, dass Verkleinerungsvorgänge durch eine Transaktion blockiert werden, die auf einer auf [Zeilenversionsverwaltung basierenden Isolationsstufe](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md) ausgeführt wird. Erfolgt z. B. während eines DBCC SHRINKDATABASE-Vorgangs gleichzeitig ein umfangreicher Löschvorgang, der auf einer auf Zeilenversionsverwaltung basierenden Isolationsstufe ausgeführt wird, wird auf den Abschluss des Löschvorgangs gewartet, bevor die Dateien verkleinert werden. Ist dies der Fall, geben DBCC SHRINKFILE- und DBCC SHRINKDATABASE-Vorgänge in der ersten Stunde alle fünf Minuten, danach jede Stunde eine Informationsmeldung in das SQL Server-Fehlerprotokoll (5202 für SHRINKDATABASE und 5203 für SHRINKFILE) aus. Wenn das Fehlerprotokoll beispielsweise folgende Fehlermeldung enthält, tritt folgender Fehler auf:
  
```sql
DBCC SHRINKFILE for file ID 1 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Dies bedeutet, dass der Verkleinerungsvorgang durch Momentaufnahmetransaktionen mit Zeitstempeln älter als 109 blockiert ist, was der letzten vom Verkleinerungsvorgang abgeschlossenen Transaktion entspricht. Außerdem zeigt es an, dass die **transaction_sequence_num**-Spalte oder die **first_snapshot_sequence_num**-Spalte in der dynamischen Verwaltungssicht [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) einen Wert von 15 enthält. Wenn die Spalte **transaction_sequence_num** oder **first_snapshot_sequence_num** in der Sicht eine Zahl enthält, die kleiner als die letzte durch einen Verkleinerungsvorgang abgeschlossene Transaktion ist (109), wird mit dem Verkleinerungsvorgang bis zum Abschluss dieser Transaktionen gewartet.
  
Führen Sie eine der folgenden Aufgaben aus, um das Problem zu beheben:
-   Beenden Sie die Transaktion, die den Verkleinerungsvorgang blockiert.
-   Beenden Sie den Verkleinerungsvorgang. Wenn der Verkleinerungsvorgang beendet wird, bleibt der bereits abgeschlossene Teil erhalten.  
-   Führen Sie keine besonderen Aktionen aus, und lassen Sie zu, dass mit dem Verkleinerungsvorgang gewartet wird, bis die blockierende Transaktion abgeschlossen ist.  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-shrinking-a-data-file-to-a-specified-target-size"></a>A. Verkleinern einer Datendatei auf eine angegebene Zielgröße  
Im folgenden Beispiel wird die Größe der Datendatei `DataFile1` in der `UserDB`-Benutzerdatenbank auf 7 MB verkleinert.
  
```sql  
USE UserDB;  
GO  
DBCC SHRINKFILE (DataFile1, 7);  
GO  
```  
  
### <a name="b-shrinking-a-log-file-to-a-specified-target-size"></a>B. Verkleinern einer Protokolldatei auf eine angegebene Zielgröße  
Im folgenden Beispiel wird die Protokolldatei in der `AdventureWorks`-Datenbank auf 1 MB verkleinert. Damit die Datei mit dem DBCC SHRINKFILE-Befehl verkleinert werden kann, wird die Datei zunächst abgeschnitten, indem das Wiederherstellungsmodell für die Datenbank auf SIMPLE festgelegt wird.
  
```sql  
USE AdventureWorks2012;  
GO  
-- Truncate the log by changing the database recovery model to SIMPLE.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY SIMPLE;  
GO  
-- Shrink the truncated log file to 1 MB.  
DBCC SHRINKFILE (AdventureWorks2012_Log, 1);  
GO  
-- Reset the database recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-truncating-a-data-file"></a>C. Abschneiden einer Datendatei  
Im folgenden Beispiel wird die primäre Datendatei in der `AdventureWorks`-Datenbank abgeschnitten. Die `sys.database_files`-Katalogsicht wird abgefragt, um den `file_id`-Wert für die Datendatei zu erhalten.
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name  
FROM sys.database_files;  
GO  
DBCC SHRINKFILE (1, TRUNCATEONLY);  
```  
  
### <a name="d-emptying-a-file"></a>D. Leeren einer Datei  
Das folgende Beispiel veranschaulicht das Verfahren zum Leeren einer Datei, sodass sie aus der Datenbank entfernt werden kann. Für die Zwecke dieses Beispiels wird zunächst eine Datendatei erstellt, und es wird angenommen, dass die Datei Daten enthält.
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create a data file and assume it contains data.  
ALTER DATABASE AdventureWorks2012   
ADD FILE (  
    NAME = Test1data,  
    FILENAME = 'C:\t1data.ndf',  
    SIZE = 5MB  
    );  
GO  
-- Empty the data file.  
DBCC SHRINKFILE (Test1data, EMPTYFILE);  
GO  
-- Remove the data file from the database.  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE Test1data;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
[FILE_ID &#40;Transact-SQL&#41;](../../t-sql/functions/file-id-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[Verkleinern einer Datei](../../relational-databases/databases/shrink-a-file.md)
  
  
