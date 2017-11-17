---
title: DBCC CHECKALLOC (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKALLOC_TSQL
- DBCC CHECKALLOC
- DBCC_CHECKALLOC_TSQL
- CHECKALLOC
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKALLOC statement
- checking database space allocation
- database space allocation [SQL Server]
- consistency [SQL Server], disk space allocations
- space allocation [SQL Server]
- allocation checks
- disk space [SQL Server], allocation consistency checks
- space allocation [SQL Server], checking
ms.assetid: bc1218eb-ffff-44ce-8122-6e4fa7d68a79
caps.latest.revision: 76
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 4cecbb77add5a9afbde3f69bf17ac2bd11bd592b
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="dbcc-checkalloc-transact-sql"></a>DBCC CHECKALLOC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Überprüft die Konsistenz von Strukturen der Speicherplatzzuordnung für eine bestimmte Datenbank.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC CHECKALLOC   
[  
    ( database_name | database_id | 0   
      [ , NOINDEX   
      | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]  
    )  
    [ WITH   
        {   
          [ ALL_ERRORMSGS ]  
          [ , NO_INFOMSGS ]   
          [ , TABLOCK ]   
          [ , ESTIMATEONLY ]   
        }  
    ]  
]  
```  
  
## <a name="arguments"></a>Argumente  
 *Database_name* | *Database_id* | 0   
 Der Name oder die ID der Datenbank, für die Zuordnung und Seite Syntax zu überprüfen.
Erfolgt keine Eingabe, oder wird 0 angegeben, wird die aktuelle Datenbank verwendet.
Datenbanknamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md).

 NOINDEX  
 Gibt an, dass nicht gruppierte Indizes für Benutzertabellen nicht überprüft werden sollen.<br>NOINDEX wird nur aus Gründen der Abwärtskompatibilität beibehalten und hat keine Auswirkungen auf DBCC CHECKALLOC.

 REPAIR_ALLOW_DATA_LOSS \| REPAIR_FAST \| REPAIR_REBUILD  
 Gibt an, dass DBCC CHECKALLOC gefundene Fehler behebt. *Database_name* im Einzelbenutzermodus ausgeführt werden muss.

 REPAIR_ALLOW_DATA_LOSS  
 Versucht, die gefundenen Fehler zu beheben. Diese Reparaturen können zu Datenverlusten führen. REPAIR_ALLOW_DATA_LOSS ist die einzige Option, die die Reparatur von Zuordnungsfehlern ermöglicht.

 REPAIR_FAST  
 Die Syntax wird nur aus Gründen der Abwärtskompatibilität beibehalten. Es werden keine Reparaturaktionen ausgeführt.

 REPAIR_REBUILD  
 Nicht verfügbar.  
 Verwenden Sie die REPAIR-Optionen nur als letzte Möglichkeit. Zum Reparieren von Fehlern empfiehlt sich das Wiederherstellen mithilfe einer Sicherung. Bei Reparaturvorgängen werden keine Einschränkungen berücksichtigt, die möglicherweise in oder zwischen Tabellen vorhanden sind. Wenn die angegebene Tabelle an einer oder mehreren Einschränkungen beteiligt ist, ist es empfehlenswert, nach einem Reparaturvorgang DBCC CHECKCONSTRAINTS auszuführen. Wenn Sie REPAIR verwenden müssen, sollten Sie DBCC CHECKDB ohne Reparaturoption ausführen, um die zu verwendende Reparaturstufe zu ermitteln. Wenn Sie die REPAIR_ALLOW_DATA_LOSS-Ebene verwenden, empfiehlt es sich, die Datenbank vor dem Ausführen von DBCC CHECKDB zu sichern.

 mit  
 Aktiviert anzugebende Optionen.

 ALL_ERRORMSGS  
 Zeigt alle Fehlermeldungen an. Alle Fehlermeldungen werden standardmäßig angezeigt. Das Angeben oder Weglassen dieser Option hat keine Auswirkungen.

 NO_INFOMSGS  
 Unterdrückt alle Informationsmeldungen und die Anzeige des verwendeten Speicherplatzes.

 TABLOCK  
 Bewirkt, dass der DBCC-Befehl eine exklusive Datenbanksperre erhält.

 ESTIMATEONLY  
 Zeigt den geschätzten Speicherplatz in Tempdb, die erforderlich sind, um DBCC CHECKALLOC auszuführen, wenn alle anderen Optionen angegeben werden.
  
## <a name="remarks"></a>Hinweise  
DBCC CHECKALLOC überprüft die Zuordnung aller Seiten in der Datenbank, unabhängig vom Typ der Seite oder des Objekts, zu dem sie gehören. Außerdem überprüft der Befehl die verschiedenen internen Strukturen, mit deren Hilfe diese Seiten und die Beziehungen zwischen ihnen nachverfolgt werden.
Wird NO_INFOMSGS nicht angegeben, sammelt DBCC CHECKALLOC Informationen zur Speicherplatzverwendung für alle Objekte in der Datenbank. Diese Informationen wird zusammen mit Fehlern gedruckt, die gefunden werden.
  
> [!NOTE]  
>DBCC CHECKALLOC-Funktionen [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) und [DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md). Dies bedeutet, dass Sie DBCC CHECKALLOC nicht gesondert von diesen Anweisungen ausführen müssen.   DBCC CHECKALLOC überprüft keine FILESTREAM-Daten. FILESTREAM speichert BLOBs (Binary Large Objects) im Dateisystem.  
  
## <a name="internal-database-snapshot"></a>Interne Datenbankmomentaufnahme  
DBCC CHECKALLOC verwendet eine internen Datenbankmomentaufnahme, um die für die Ausführung dieser Überprüfungen erforderliche Transaktionskonsistenz bereitzustellen. Wenn eine Momentaufnahme nicht erstellt werden kann oder TABLOCK angegeben ist, versucht DBCC CHECKALLOC, eine exklusive Sperre (X) für die Datenbank zu erwerben, um die erforderliche Konsistenz zu erhalten.
  
> [!NOTE]  
> Ausführen von DBCC CHECKALLOC für Tempdb führt keine Überprüfungen durch. Dies liegt daran, dass aus Leistungsgründen keine Datenbankmomentaufnahmen auf tempdb verfügbar sind. Dies bedeutet, dass die erforderliche Transaktionskonsistenz nicht erhalten werden kann. Beenden Sie und starten Sie den MSSQLSERVER-Dienst, um Tempdb Zuordnung Probleme zu beheben. Diese Aktion löscht und die Tempdb-Datenbank neu erstellt.  
  
## <a name="understanding-dbcc-error-messages"></a>Grundlegendes zu DBCC-Fehlermeldungen  
Nach Abschluss des Befehls DBCC CHECKALLOC wird eine Meldung im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll verzeichnet. Wurde der DBCC-Befehl erfolgreich ausgeführt, zeigt die Meldung den erfolgreichen Abschluss und die Ausführungsdauer des Befehls an. Wurde der DBCC-Befehl aufgrund eines Fehlers vor Abschluss der Überprüfung beendet, zeigt die Meldung an, dass der Befehl beendet wurde. Außerdem wird ein Statuswert und die Ausführungsdauer des Befehls angegeben. In der folgenden Tabelle sind die Statuswerte aufgeführt und beschrieben, die in der Meldung enthalten sein können.
  
|Status|Description|  
|---|---|  
|0|Fehlernummer 8930 wurde ausgelöst. Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|  
|1|Fehlernummer 8967 wurde ausgelöst. Ein interner DBCC-Fehler ist aufgetreten.|  
|2|Beim Reparieren einer Datenbank im Notfallmodus ist ein Fehler aufgetreten.|  
|3|Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|  
|4|Eine Assertations- oder Zugriffsverletzung wurde entdeckt.|  
|5|Ein unbekannter Fehler ist aufgetreten, der den DBCC-Befehl beendet hat.|  
  
## <a name="error-reporting"></a>Fehlerberichterstellung  
Eine minidumpdatei (SQLDUMP*nnnn*".txt") wird erstellt, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Protokollverzeichnis, wenn DBCC CHECKALLOC Fehler durch eine Beschädigung erkennt. Falls die Funktionen zur Verwendung der Datensammlung und zur Fehlerberichterstellung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz aktiviert sind, wird die Datei automatisch an [!INCLUDE[msCoName](../../includes/msconame-md.md)] weitergeleitet. Die gesammelten Daten werden zur Verbesserung der Funktionalität von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet.
Die Sicherungsdatei enthält die Ergebnisse des DBCC CHECKALLOC-Befehls sowie eine zusätzliche Diagnoseausgabe. Die Datei verfügt über eingeschränkte, besitzverwaltete Zugriffssteuerungslisten (Discretionary Access Control List, DACL). Zugriff ist auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto und Mitglieder der Sysadmin-Rolle. Die Rolle "Sysadmin" enthält standardmäßig alle Mitglieder der Windows-Gruppe VORDEFINIERT\Administratoren und der lokalen Administratorgruppe sein. Ein Fehler bei der Datensammlung verursacht keinen Fehler des DBCC-Befehls.
  
## <a name="resolving-errors"></a>Auflösen von Fehlern  
Wenn DBCC CHECKALLOC Fehler meldet, ist es empfehlenswert, die Datenbank aus der Datenbanksicherung wiederherzustellen, statt eine Reparatur auszuführen. Ist keine Sicherung vorhanden, können die gemeldeten Fehler durch das Ausführen einer Reparatur behoben werden. Beim Beheben der Fehler ist es jedoch möglicherweise erforderlich, einige Seiten (und somit Daten) zu löschen.
Eine Reparatur kann in einer Benutzertransaktion ausgeführt werden. Dies ermöglicht ein Rollback der Änderungen. Falls für Änderungen ein Rollback ausgeführt wird, enthält die Datenbank immer noch Fehler und muss von einer Datensicherung wiederhergestellt werden. Nach Abschluss der Reparaturen sollten Sie eine Sicherung der Datenbank ausführen.
  
## <a name="result-sets"></a>Resultsets  
In den folgenden Tabellen werden die von DBCC CHECKALLOC zurückgegebenen Informationen beschrieben.
  
|Element|Description|  
|---|---|  
|FirstIAM|Nur interne Verwendung.|  
|Root|Nur interne Verwendung.|  
|Dpages|Anzahl von Datenseiten.|  
|Pages used|Zugeordnete Seiten.|  
|Dedicated extents|Dem Objekt zugeordnete Blöcke.<br /><br /> Wenn Seiten mit gemischter Zuordnung verwendet werden, kann es Seiten geben, die ohne Blöcke zugeordnet sind.|  
  
DBCC CHECKALLOC meldet außerdem eine Zuordnungszusammenfassung für jeden Index und jede Partition in jeder Datei. In dieser Zusammenfassung wird die Verteilung der Daten beschrieben.
  
|Element|Description|  
|---|---|  
|Zugeordnete Seiten|Seiten, die für den Index zugeordnet wurden, und nicht verwendete Seiten in zugeordneten Blöcken.|  
|Verwendete Seiten|Zugeordnete Seiten, die vom Index verwendet werden.|  
|Partitions-ID|Nur interne Verwendung.|  
|Zuordnungseinheits-ID|Nur interne Verwendung.|  
|Daten in Zeilen|Seiten enthalten Index- oder Heapdaten.|  
|LOB-Daten|Seiten enthalten **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Text**, **Ntext**, **Xml**, und **Image** Daten.|  
|Zeilenüberlaufdaten|Seiten enthalten Daten einer Spalte mit variabler Länge, die durch Ausführen eines Pushs außerhalb von Zeilen verschoben wurden.|  
  
DBCC CHECKALLOC gibt das folgende Resultset zurück (die tatsächlichen Werte können davon abweichen), außer wenn ESTIMATEONLY oder NO_INFOMSGS angegeben wird.
  
```sql
DBCC results for 'master'.  
***************************************************************  
Table sysobjects                Object ID 1.  
Index ID 1         FirstIAM (1:11)   Root (1:12)    Dpages 22.  
    Index ID 1. 24 pages used in 5 dedicated extents.  
Index ID 2         FirstIAM (1:1368)   Root (1:1362)    Dpages 10.  
    Index ID 2. 12 pages used in 2 dedicated extents.  
Index ID 3         FirstIAM (1:1392)   Root (1:1408)    Dpages 4.  
    Index ID 3. 6 pages used in 0 dedicated extents.  
Total number of extents is 7.  
***************************************************************  
'...'  
***************************************************************  
Table spt_server_info                Object ID 1938105945.  
Index ID 1         FirstIAM (1:520)   Root (1:508)    Dpages 1.  
    Index ID 1. 3 pages used in 0 dedicated extents.  
Total number of extents is 0.  
***************************************************************  
Processed 52 entries in sysindexes for database ID 1.  
File 1. Number of extents = 210, used pages = 1126, reserved pages = 1280.  
           File 1 (number of mixed extents = 73, mixed pages = 184).  
    Object ID 1, Index ID 0, data extents 5, pages 24, mixed extent pages 9.  
'...'  
    Object ID 1938105945, Index ID 0, data extents 0, pages 3, mixed extent pages 3.  
Total number of extents = 210, used pages = 1126, reserved pages = 1280 in this database.  
       (number of mixed extents = 73, mixed pages = 184) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC results for 'master'.  
***************************************************************  
Table sys.sysrowsetcolumns                Object ID 4.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). FirstIAM (1:98). Root (1:94). Dpages 7.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). 9 pages used in 1 dedicated extents.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). FirstIAM (0:0). Root (0:0). Dpages 0.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). 0 pages used in 0 dedicated extents.  
Total number of extents is 1.  
...  
***************************************************************  
Processed 201 entries in system catalog for database ID 1.  
File 1. Number of extents = 44, used pages = 300, reserved pages = 345.  
           File 1 (number of mixed extents = 29, mixed pages = 225).  
    Object ID 4, index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 5, index ID 1, partition ID 327680, alloc unit ID 327680 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 7, index ID 1, partition ID 458752, alloc unit ID 458752 (type In-row data), data extents 0, pages 5, mixed extent pages 5.  
    Object ID 8, index ID 0, partition ID 524288, alloc unit ID 524288 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 13, index ID 1, partition ID 851968, alloc unit ID 851968 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 15, index ID 1, partition ID 983040, alloc unit ID 983040 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 26, index ID 1, partition ID 281474978414592, alloc unit ID 1703937 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 1, partition ID 281474978480128, alloc unit ID 1769473 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 2, partition ID 562949955190784, alloc unit ID 1769474 (type In-row data), index extents 0, pages 3, mixed extent pages 3.  
...  
    Object ID 1179151246, index ID 1, partition ID 72057594038845440, alloc unit ID 13435136 (type In-row data), data extents 2, pages 18, mixed extent pages 8.  
    Object ID 1179151246, index ID 2, partition ID 72057594038910976, alloc unit ID 13566208 (type In-row data), index extents 1, pages 16, mixed extent pages 8.  
    Object ID 1911677858, index ID 0, partition ID 72057594039631872, alloc unit ID 15073536 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
Total number of extents = 41, used pages = 289, reserved pages = 323 in this database.  
       (number of mixed extents = 27, mixed pages = 211) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Wenn ESTIMATEONLY angegeben wird, gibt DBCC CHECKALLOC das folgende Resultset zurück.
  
```sql
Estimated TEMPDB space needed for CHECKALLOC (KB)   
-------------------------------------------------   
34  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle Sysadmin oder der festen Datenbankrolle "Db_owner".
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird `DBCC CHECKALLOC` für die aktuelle Datenbank und für die `AdventureWorks2012`-Datenbank ausgeführt.
  
```sql  
-- Check the current database.  
DBCC CHECKALLOC;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKALLOC (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  


