---
title: DBCC SHRINKDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
caps.latest.revision: 62
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7f6e9fa3feea20bfeb82037cb9358370c67aaa0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Reduziert die Größe der Daten- und Protokolldateien in der angegebenen Datenbank.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Database_name* | *Database_id* | 0  
 Der Name oder die ID der Datenbank, die verkleinert werden soll. Wird 0 angegeben, wird die aktuelle Datenbank verwendet.  
  
 *target_percent*  
 Der gewünschte Prozentsatz an freiem Speicherplatz, der in der Datenbankdatei übrig bleiben soll, nachdem die Datenbank verkleinert wurde.  
  
 NOTRUNCATE  
 Komprimiert die Daten in Datendateien durch Verschieben von zugeordneten Seiten vom Ende einer Datei in nicht zugeordnete Seiten am Dateianfang. *Target_percent* ist optional.  
  
 Der freie Speicherplatz am Dateiende wird nicht an das Betriebssystem zurückgegeben, und die physische Größe der Datei bleibt unverändert. Daher scheint die Datenbank bei Angabe von NOTRUNCATE nicht verkleinert zu werden.  
  
 NOTRUNCATE gilt nur für Datendateien. Die Protokolldatei ist nicht betroffen.  
  
 TRUNCATEONLY  
 Gibt den gesamten freien Speicherplatz am Dateiende an das Betriebssystem frei, es werden jedoch keine Seiten innerhalb der Datei verschoben. Die Datendatei wird nur bis zum letzten zugeordneten Block verkleinert. *Target_percent* wird ignoriert, wenn mit TRUNCATEONLY angegeben.  
  
 TRUNCATEONLY wirkt sich auf die Protokolldatei aus. Um nur die Datendatei abzuschneiden, verwenden Sie DBCC SHRINKFILE.  
  
 WITH NO_INFOMSGS  
 Unterdrückt alle Informationsmeldungen mit einem Schweregrad von 0 bis 10.  
  
## <a name="result-sets"></a>Resultsets  
In der folgenden Tabelle werden die Spalten des Resultsets beschrieben:
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**DbId**|Die Datenbank-ID der Datei, die das [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu verkleinern versuchte.|  
|**FileId**|Datei-ID der Datei, die das [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu verkleinern versuchte.|  
|**CurrentSize**|Die Anzahl von 8-KB-Seiten, die die Datei derzeit belegt.|  
|**MinimumSize**|Die Anzahl von 8-KB-Seiten, die die Datei minimal belegen könnte. Dies entspricht der Mindestgröße bzw. der ursprünglich erzeugten Dateigröße.|  
|**UsedPages**|Die Anzahl von 8-KB-Seiten, die derzeit von der Datei verwendet werden.|  
|**EstimatedPages**|Die Anzahl an 8-KB-Seiten, auf die die Datei wahrscheinlich vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] verkleinert werden kann.|  
  
>[!NOTE]
> Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] zeigt keine Zeilen für Dateien an, die nicht verkleinert wurden.  
  
## <a name="remarks"></a>Hinweise  
Zum Verkleinern aller Daten- und Protokolldateien einer bestimmten Datenbank führen Sie den DBCC SHRINKDATABASE-Befehl aus. Führen Sie zum Verkleinern einer einzelnen Daten- oder Protokolldatei zu einem Zeitpunkt für eine bestimmte Datenbank, die [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) Befehl.
  
Führen Sie zum Anzeigen des aktuellen freien (nicht zugeordneten) Speicherplatzes in der Datenbank, [Sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).
  
DBCC SHRINKDATABASE-Vorgänge können an jeder Stelle des Vorgangs beendet werden, wobei der bereits abgeschlossene Anteil erhalten bleibt.
  
Die Datenbank kann nicht unter die Mindestgröße der Datenbank verkleinert werden. Die Mindestgröße ist die Größe, die beim Erstellen der Datei angegeben wurde, bzw. die letzte Größe, die bei einer Dateigrößenänderung, z. B. mit DBCC SHRINKFILE oder ALTER DATABASE, explizit festgelegt wurde. Wenn eine Datenbank z. B. mit einer Größe von 10 MB erstellt und auf 100 MB vergrößert wurde, kann die Datenbank höchstens auf 10 MB verkleinert werden, auch wenn alle Daten in der Datenbank gelöscht wurden.
  
Das Ausführen von DBCC SHRINKDATABASE ohne eine der Optionen NOTRUNCATE oder TRUNCATEONLY entspricht einem DBCC SHRINKDATABASE-Vorgang mit NOTRUNCATE und einem anschließenden DBCC SHRINKDATABASE-Vorgang mit TRUNCATEONLY.
  
Die Datenbank, die verkleinert werden soll, muss sich nicht im Einzelbenutzermodus befinden. Andere Benutzer können während der Verkleinerung darin arbeiten. Das gilt auch für Systemdatenbanken.
  
Während einer Datenbanksicherung können Sie die Datenbank nicht verkleinern. Umgekehrt können Sie eine Datenbank nicht sichern, während ein Verkleinerungsvorgang für die Datenbank ausgeführt wird.
  
## <a name="how-dbcc-shrinkdatabase-works"></a>Funktionsweise von DBCC SHRINKDATABASE  
DBCC SHRINKDATABASE verkleinert Datendateien pro Datei, Protokolldateien jedoch so, als lägen alle Protokolldateien in einem zusammenhängenden Protokollpool vor. Dateien werden immer am Ende verkleinert.
  
Angenommen Sie eine Datenbank namens **Mydb** mit einer Datendatei und zwei Protokolldateien. Die Daten und Protokolldateien sind jeweils 10 MB groß, und die Datendatei enthält 6 MB an Daten.
  
Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] berechnet für jede Datei eine Zielgröße, auf die die Datei verkleinert werden soll. Wenn DBCC SHRINKDATABASE mit *target_percent* angegeben wird, dann berechnet das [!INCLUDE[ssDE](../../includes/ssde-md.md)] als Zielgröße einen prozentualen Anteil von *target_percent* des freien Speicherplatzes der Datei nach der Verkleinerung. Wenn Sie z. B. für die Verkleinerung von **mydb** den Wert 25 für *target_percent* angeben, dann berechnet das [!INCL
  
Angenommen die Datendatei der **Mydb** enthält 7 MB Daten. Angeben einer *Target_percent* von 30 kann diese Datendatei auf einen freien Prozentsatz von 30 verkleinert werden. Allerdings angeben einer *Target_percent* 40 wird nicht verkleinert werden, die Datendatei da die [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht möglich ist, eine Datei auf eine Größe kleiner ist als die Daten aktuell belegt. Sie können auch vorstellen dieses Problems eine andere Möglichkeit: 40 Prozent Erwünschter freier Speicherplatz Plus 70 Prozent volle Datendatei (7 MB von 10 MB) ist mehr als 100 Prozent. Da der gewünschte freie Prozentsatz, der erwünscht ist zuzüglich des Prozentsatzes, der von die Datendatei belegt ist mehr als 100 Prozent (um 10 Prozent), alle *Target_size* größer als 30 die Datendatei nicht verkleinert werden.
  
Für Protokolldateien die [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwendet *Target_percent* zum Berechnen der Zielgröße des gesamten Protokolls; deshalb *Target_percent* ist die Menge des freien Speicherplatzes im Protokoll nach dem Verkleinerungsvorgang. Die Zielgröße für das gesamte Protokoll wird dann in eine Zielgröße für jede Protokolldatei umgewandelt.
  
DBCC SHRINKDATABASE versucht, jede physische Protokolldatei sofort auf ihre Zielgröße zu verkleinern. Wenn sich kein Teil des logischen Protokolls in den virtuellen Protokollen befindet, die außerhalb der Zielgröße der Protokolldatei liegen, wird die Datei erfolgreich abgeschnitten, und DBCC SHRINKDATABASE wird ohne Meldungen beendet. Wenn sich dagegen ein Teil des logischen Protokolls in den virtuellen Protokollen befindet, die außerhalb der Zielgröße liegen, gibt das [!INCLUDE[ssDE](../../includes/ssde-md.md)] so viel Speicherplatz frei wie möglich und gibt dann eine Informationsmeldung aus. Die Meldung beschreibt, welche Aktionen erforderlich sind, um das logische Protokoll aus den virtuellen Protokollen am Ende der Datei zu verschieben. Nachdem diese Aktionen ausgeführt wurden, kann der verbleibende Speicherplatz mit DBCC SHRINKDATABASE freigegeben werden.
  
Da eine Protokolldatei nur auf eine Grenze einer virtuellen Protokolldatei verkleinert werden kann, ist eine Verkleinerung der Protokolldatei auf eine geringere Größe als die einer virtuellen Protokolldatei u. U. nicht möglich, selbst wenn die Protokolldatei nicht verwendet wird. Die Größe der virtuellen Protokolldatei wird dynamisch vom [!INCLUDE[ssDE](../../includes/ssde-md.md)] ausgewählt, wenn Protokolldateien erstellt oder erweitert werden.
  
## <a name="best-practices"></a>Bewährte Methoden  
Berücksichtigen Sie die folgenden Informationen, wenn Sie eine Datenbank verkleinern möchten:
-   Ein Verkleinerungsvorgang ist am effektivsten nach einem Vorgang, durch den umfangreicher nicht verwendeter Speicherplatz bereitgestellt wird, z. B. das Abschneiden oder Löschen einer Tabelle.  
-   Die meisten Datenbanken erfordern verfügbaren freien Speicherplatz für die normalen alltäglichen Vorgänge. Wenn Sie eine Datenbank wiederholt verkleinern und feststellen, dass die Datenbankgröße wieder zunimmt, deutet dies darauf hin, dass der verkleinerte Speicherplatz für regelmäßige Vorgänge benötigt wird. In diesem Fall ist das Verkleinern der Datenbank vergeblich.  
-   Bei einem Verkleinerungsvorgang bleibt der Fragmentierungszustand der Indizes in der Datenbank nicht erhalten. Im Allgemeinen wird die Fragmentierung zu einem gewissen Grad verstärkt. Dies ist ein weiterer Grund, die Datenbank nicht wiederholt zu verkleinern.  
-   Legen Sie die Datenbankoption AUTO_SHRINK nicht auf ON fest, es sei denn, besondere Anforderungen machen dies erforderlich.  
  
## <a name="troubleshooting"></a>Problembehandlung  
 Es ist möglich, dass Verkleinerungsvorgänge durch eine Transaktion blockiert werden, die unter ausgeführt wird eine [Zeile auf zeilenversionsverwaltung basierende Isolationsstufe](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Erfolgt z. B. während eines DBCC SHRINKDATABASE-Vorgangs gleichzeitig ein umfangreicher Löschvorgang, der auf einer auf Zeilenversionsverwaltung basierenden Isolationsstufe ausgeführt wird, wird auf den Abschluss des Löschvorgangs gewartet, bevor die Dateien verkleinert werden. Ist dies der Fall, geben DBCC SHRINKFILE- und DBCC SHRINKDATABASE-Vorgänge in der ersten Stunde alle fünf Minuten, danach jede Stunde eine Informationsmeldung in das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll (5202 für SHRINKDATABASE und 5203 für SHRINKFILE) aus. Das Fehlerprotokoll kann beispielsweise eine Fehlermeldung wie die folgende enthalten:  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Dies bedeutet, dass der Verkleinerungsvorgang durch Momentaufnahmetransaktionen mit Zeitstempeln älter als 109 blockiert ist, was der letzten vom Verkleinerungsvorgang abgeschlossenen Transaktion entspricht. Außerdem zeigt es an, die die **Transaction_sequence_num**, oder **First_snapshot_sequence_num** Spalten in der [Sys. dm_tran_active_snapshot_database_transactions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) -verwaltungssicht Wert 15 enthält. Wenn entweder die **Transaction_sequence_num**, oder **First_snapshot_sequence_num** Spalten in der Sicht enthält eine Zahl kleiner als die letzte Transaktion, die abgeschlossen wird, durch einen Verkleinerungsvorgang (109), die Verkleinern Vorgang wartet, bis zum Abschluss dieser Transaktionen.
  
Um das Problem zu beheben, können Sie eine der folgenden Aufgaben ausführen:
-   Beenden Sie die Transaktion, die den Verkleinerungsvorgang blockiert.  
-   Beenden Sie den Verkleinerungsvorgang. Der bereits abgeschlossene Teil bleibt erhalten.  
-   Führen Sie keine besonderen Aktionen aus, und lassen Sie zu, dass mit dem Verkleinerungsvorgang gewartet wird, bis die blockierende Transaktion abgeschlossen ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>A. Verkleinern einer Datenbank und Angeben des freien Speicherplatzes in Prozent  
 Im folgenden Beispiel wird die Größe der Daten- und Protokolldateien in der `UserDB`-Benutzerdatenbank so verringert, dass die Datenbank 10 Prozent freien Speicherplatz enthält.  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. Abschneiden einer Datenbank  
 Im folgenden Beispiel werden die Daten- und Protokolldateien in der `AdventureWorks`-Beispieldatenbank auf den letzten zugeordneten Block verkleinert.  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>Siehe auch  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[Verkleinern einer Datenbank](../../relational-databases/databases/shrink-a-database.md)
  
  

