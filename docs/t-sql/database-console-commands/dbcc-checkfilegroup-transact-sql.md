---
title: DBCC CHECKFILEGROUP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKFILEGROUP_TSQL
- DBCC_CHECKFILEGROUP_TSQL
- DBCC CHECKFILEGROUP
- CHECKFILEGROUP
dev_langs: TSQL
helpviewer_keywords:
- DBCC CHECKFILEGROUP statement
- database objects [SQL Server], checking
- allocation checks
- integrity [SQL Server], database objects
- filegroups [SQL Server], consistency checks
- table integrity checks [SQL Server]
- checking database objects
ms.assetid: 8c70bf34-7570-4eb6-877a-e35064a1380a
caps.latest.revision: "60"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3ee32ac764afd0e350fe094eb8e18a24589026e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-checkfilegroup-transact-sql"></a>DBCC CHECKFILEGROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]Hier wird überprüft, ob die Zuordnung und strukturelle Integrität aller Tabellen und indizierten Sichten in der angegebenen Dateigruppe der aktuellen Datenbank.
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
  
DBCC CHECKFILEGROUP   
[  
    [ ( { filegroup_name | filegroup_id | 0 }   
        [ , NOINDEX ]   
  ) ]  
    [ WITH   
        {   
            [ ALL_ERRORMSGS | NO_INFOMSGS ]   
            [ , TABLOCK ]   
            [ , ESTIMATEONLY ]  
            [ , PHYSICAL_ONLY ]    
            [ , MAXDOP  = number_of_processors ]  
        }   
    ]  
]  
```  
  
## <a name="arguments"></a>Argumente  
 *filegroup_name*  
 Der Name der Dateigruppe in der aktuellen Datenbank, für die die Tabellenzuordnung und strukturelle Integrität überprüft werden sollen. Wenn dieses Argument fehlt oder mit 0 angegeben ist, wird standardmäßig die primäre Dateigruppe verwendet. Dateigruppennamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
 *Filegroup_name* eine FILESTREAM-Dateigruppe ist nicht möglich.  
  
 *filegroup_id*  
 Die Dateigruppen-ID in der aktuellen Datenbank, für die die Tabellenzuordnung und strukturelle Integrität überprüft werden sollen.  
  
 NOINDEX  
 Legt fest, dass nicht gruppierte Indizes für Benutzertabellen nicht intensiv überprüft werden. Dadurch wird die Ausführungsdauer insgesamt verkürzt. NOINDEX wirkt sich nicht auf Systemtabellen aus, da DBCC CHECKFILEGROUP immer alle Systemtabellenindizes überprüft.  
  
 ALL_ERRORMSGS  
 Zeigt pro Objekt eine unbegrenzte Fehlerzahl an. Alle Fehlermeldungen werden standardmäßig angezeigt. Das Angeben oder Weglassen dieser Option hat keine Auswirkungen.  
  
 NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
 TABLOCK  
 Bewirkt, dass DBCC CHECKFILEGROUP freigegebene Tabellensperren erhält anstatt auf eine interne Datenbank-Momentaufnahme zurückzugreifen.  
  
 ESTIMATEONLY  
 Zeigt den tempdb-Speicherplatz an, der schätzungsweise erforderlich ist, um DBCC CHECKFILEGROUP mit den anderen angegebenen Optionen auszuführen.  
  
 PHYSICAL_ONLY  
 Beschränkt die Überprüfung auf die Integrität der physischen Struktur der Seite, der Datensatzheader und der physischen Struktur von B-Strukturen. Dieses Argument wurde entworfen, um mit geringem Verwaltungsaufwand eine Überprüfung der physischen Konsistenz der Dateigruppe vorzunehmen. Dabei werden auch zerrissene Seiten und häufige Hardwarefehler erkannt, die die Daten gefährden können. Die vollständige Ausführung von DBCC CHECKFILEGROUP kann erheblich mehr Zeit in Anspruch nehmen als in früheren Versionen. Dieses Verhalten tritt aus folgenden Gründen:  
 -   Die logischen Überprüfungen sind umfassender.  
 -   Einige der zu überprüfenden zugrunde liegenden Strukturen sind komplexer.  
 -   Es wurden viele neue Überprüfungen eingeführt, um die neuen Funktionen einzuschließen.  
 Daher bewirkt das Verwenden der PHYSICAL_ONLY-Option möglicherweise eine viel kürzere Ausführungszeit von DBCC CHECKFILEGROUP für große Dateigruppen. Es wird daher für die häufige Verwendung in Produktionssystemen empfohlen. Dennoch ist eine vollständige Ausführung von DBCC CHECKFILEGROUP in regelmäßigen Abständen empfehlenswert. Die Häufigkeit dieser Ausführungsvorgänge hängt von Faktoren ab, die für einzelne Unternehmen und Produktionsumgebungen spezifisch sind. PHYSICAL_ONLY impliziert stets NO_INFOMSGS und kann nicht mit einer der Reparaturoptionen verwendet werden.  
  
> [!NOTE]  
>  Bei Angabe von PHYSICAL_ONLY überspringt DBCC CHECKFILEGROUP alle Überprüfungen der FILESTREAM-Daten.  
  
 MAXDOP  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 SP2 über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 Überschreibt die **Max. Grad an Parallelität** Konfigurationsoption von **Sp_configure** für die Anweisung. Der MAXDOP kann mit Sp_configure konfigurierten Wert überschreiten. Wenn MAXDOP den mit der Ressourcenkontrolle konfigurierten Wert überschreitet, verwendet das Datenbankmodul die Ressourcenkontrolle MAXDOP-Wert in der ALTER WORKLOAD GROUP (Transact-SQL) beschrieben. Alle semantischen Regeln, die mit der Konfigurationsoption Max. Grad an Parallelität verwendet werden können, stehen beim Verwenden des MAXDOP-Abfragehinweises zur Verfügung. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
> [!CAUTION]  
>  Wenn MAXDOP auf 0 (Null) festgelegt wird, wählt der Server den maximalen Grad an Parallelität aus.  
  
## <a name="remarks"></a>Hinweise  
DBCC CHECKFILEGROUP und DBCC CHECKDB sind ähnliche DBCC-Befehle. Der Hauptunterschied besteht darin, dass DBCC CHECKFILEGROUP auf die einzelne angegebene Dateigruppe und die erforderlichen Tabellen beschränkt ist.
Von DBCC CHECKFILEGROUP werden die folgenden Befehle ausgeführt:
-   [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md) der Dateigruppe.  
-   [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md) für jede Tabelle und indizierte Sicht in der Dateigruppe.  
  
Eine von DBCC CHECKFILEGROUP getrennte Ausführung von DBCC CHECKALLOC oder DBCC CHECKTABLE ist nicht erforderlich.
  
## <a name="internal-database-snapshot"></a>Interne Datenbankmomentaufnahme  
Zur Bereitstellung der Transaktionskonsistenz, die für diese Prüfungen vorliegen muss, verwendet DBCC CHECKFILEGROUP eine interne Datenbankmomentaufnahme. Weitere Informationen finden Sie unter [Anzeigen der Größe der Datei mit geringer Dichte einer Datenbank-Momentaufnahme &#40; Transact-SQL &#41; ](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) und im Abschnitt "DBCC interne Datenbankmomentaufnahme" in [DBCC &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Falls keine Momentaufnahme erstellt werden kann oder die TABLOCK-Option angegeben ist, wendet DBCC CHECKFILEGROUP Sperren an, um die erforderliche Konsistenz zu erlangen. In diesem Fall ist für die Durchführung der Zuordnungsprüfungen eine exklusive Datenbanksperre erforderlich, und für die Durchführung der Tabellenprüfungen sind freigegebene Tabellensperren erforderlich. Durch TABLOCK wird DBCC CHECKFILEGROUP für eine Datenbank bei starker Belastung schneller ausgeführt, jedoch wird während der Ausführung von DBCC CHECKFILEGROUP die in der Datenbank verfügbare Parallelität verringert.
  
> [!NOTE]  
>  Durch das Ausführen von DBCC CHECKFILEGROUP für tempdb werden keine Zuordnungsprüfungen veranlasst, und zur Durchführung von Tabellenprüfungen müssen freigegebene Tabellensperren aktiviert werden. Dies liegt daran, dass aus Leistungsgründen keine Datenbankmomentaufnahmen auf tempdb verfügbar sind. Dies bedeutet, dass die erforderliche Transaktionskonsistenz nicht erhalten werden kann.  
  
## <a name="checking-objects-in-parallel"></a>Paralleles Überprüfen von Objekten  
Standardmäßig führt DBCC CHECKFILEGROUP eine parallele Überprüfung von Objekten durch. Der Grad der Parallelität wird automatisch durch den Abfrageprozessor bestimmt. Der Höchstgrad für die Parallelität wird genauso konfiguriert wie parallele Abfragen. Um die maximale Anzahl an Prozessoren zur Verfügung, für die DBCC-Überprüfungen einzuschränken, verwenden Sie [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md). Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
Die parallele Überprüfung kann mithilfe des Ablaufverfolgungsflags 2528 deaktiviert werden. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
  
## <a name="nonclustered-indexes-on-separate-filegroups"></a>Nicht gruppierte Indizes für separate Dateigruppen  
Wenn einem nicht gruppierten Index in der angegebenen Dateigruppe eine Tabelle in einer anderen Dateigruppe zugeordnet wird, wird der Index nicht überprüft, da die Basistabelle nicht für die Überprüfung verfügbar ist.
Wenn eine Tabelle der angegebenen Dateigruppe einen nicht gruppierten Index in einer anderen Dateigruppe besitzt, wird der nicht gruppierte Index aus folgenden Gründen nicht überprüft:
-   Die Basistabellenstruktur ist unabhängig von der Struktur eines nicht gruppierten Indexes. Nicht gruppierte Indizes müssen zur Überprüfung der Gültigkeit der Basistabelle nicht durchsucht werden.  
-   Mit dem Befehl DBCC CHECKFILEGROUP werden nur Objekte in der angegebenen Dateigruppe überprüft.  
Ein gruppierter Index und eine Tabelle dürfen sich nicht in unterschiedlichen Dateigruppen befinden. Die vorausgegangenen Ausführungen gelten daher nur für nicht gruppierte Indizes.
  
## <a name="partitioned-tables-on-separate-filegroups"></a>Partitionierte Tabellen für separate Dateigruppen  
Wenn eine partitionierte Tabelle für mehrere Dateigruppen vorhanden ist, überprüft DBCC CHECKFILEGROUP die Partitionsrowsets, die für die angegebene Dateigruppe vorhanden sind, und ignoriert die Rowsets in den anderen Dateigruppen. In der Informationsmeldung 2594 werden die nicht überprüften Partitionen angegeben. Nicht gruppierte Indizes, die nicht in der angegebenen Dateigruppe vorhanden sind, werden nicht überprüft.
  
## <a name="understanding-dbcc-error-messages"></a>Grundlegendes zu DBCC-Fehlermeldungen  
Nach Ausführung des DBCC CHECKFILEGROUP-Befehls wird eine Meldung im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll verzeichnet. Wurde der DBCC-Befehl erfolgreich ausgeführt, zeigt die Meldung den erfolgreichen Abschluss und die Ausführungsdauer des Befehls an. Wurde der DBCC-Befehl aufgrund eines Fehlers vor Abschluss der Überprüfung beendet, zeigt die Meldung an, dass der Befehl beendet wurde. Außerdem wird ein Statuswert und die Ausführungsdauer des Befehls angegeben. In der folgenden Tabelle sind die Statuswerte aufgeführt und beschrieben, die in der Meldung enthalten sein können.
  
|Status|Description|  
|-----------|-----------------|  
|0|Fehlernummer 8930 wurde ausgelöst. Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|  
|1|Fehlernummer 8967 wurde ausgelöst. Ein interner DBCC-Fehler ist aufgetreten.|  
|2|Beim Reparieren einer Datenbank im Notfallmodus ist ein Fehler aufgetreten.|  
|3|Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|  
|4|Eine Assertations- oder Zugriffsverletzung wurde entdeckt.|  
|5|Ein unbekannter Fehler ist aufgetreten, der den DBCC-Befehl beendet hat.|  
  
## <a name="error-reporting"></a>Fehlerberichterstellung  
Eine minidumpdatei (SQLDUMP*nnnn*".txt") wird erstellt, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Protokollverzeichnis, wenn DBCC CHECKFILEGROUP einen Fehler durch eine Beschädigung erkennt. Falls die Funktionen zur Verwendung der Datensammlung und zur Fehlerberichterstellung für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz aktiviert sind, wird die Datei automatisch an [!INCLUDE[msCoName](../../includes/msconame-md.md)] weitergeleitet. Die gesammelten Daten werden zur Verbesserung der Funktionalität von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet.
Die Sicherungsdatei enthält die Ergebnisse des DBCC CHECKFILEGROUP-Befehls sowie eine zusätzliche Diagnoseausgabe. Die Datei verfügt über eingeschränkte, besitzverwaltete Zugriffssteuerungslisten (Discretionary Access Control List, DACL). Zugriff ist auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto und Mitglieder der **Sysadmin** Rolle. Wird standardmäßig die **Sysadmin** Rolle enthält, die alle Mitglieder der Windows-Gruppe VORDEFINIERT\Administratoren und der lokalen Administratorgruppe sein. Ein Fehler bei der Datensammlung verursacht keinen Fehler des DBCC-Befehls.
  
## <a name="resolving-errors"></a>Auflösen von Fehlern  
Sollten Fehler von DBCC CHECKFILEGROUP gemeldet werden, wird die Wiederherstellung der Datenbank aus der Datenbanksicherung empfohlen. Beachten Sie, dass für DBCC CHECKFILEGROUP keine Reparaturoptionen angegeben werden können.
Falls keine Sicherung vorhanden ist, lassen sich die gemeldeten Fehler durch Ausführung von DBCC CHECKDB mit einer Reparaturoption beheben. Welche Reparaturoption dabei zu verwenden ist, wird am Ende der Liste mit den gemeldeten Fehlern angegeben. Soll die Fehlerkorrektur mithilfe der Option REPAIR_ALLOW_DATA_LOSS erfolgen, müssen möglicherweise einige Seiten, und damit auch Daten, gelöscht werden.
  
## <a name="result-sets"></a>Resultsets  
DBCC CHECKFILEGROUP gibt folgendes Resultset zurück (die tatsächlichen Werte können davon abweichen):
-   Es sei denn, ESTIMATEONLY oder NO_INFOMSGS wurde angegeben.  
-   Für die aktuelle Datenbank (falls keine Datenbank angegeben wurde), ob Optionen (außer NOINDEX) angegeben wurden oder nicht.  
  
```sql
DBCC results for 'master'.  
DBCC results for 'sys.sysrowsetcolumns'.  
There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.  
DBCC results for 'sys.sysrowsets'.  
There are 97 rows in 1 pages for object 'sys.sysrowsets'.  
DBCC results for 'sysallocunits'.  
There are 195 rows in 3 pages for object 'sysallocunits'.  
  
There are 2340 rows in 16 pages for object 'spt_values'.  
DBCC results for 'MSreplication_options'.  
There are 2 rows in 1 pages for object 'MSreplication_options'.  
CHECKFILEGROUP found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Wurde NO_INFOMSGS angegeben, gibt DBCC CHECKFILEGROUP Folgendes zurück:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
 Wurde ESTIMATEONLY angegeben, gibt DBCC CHECKFILEGROUP Folgendes zurück (die tatsächlichen Werte können davon abweichen):  

```sql
Estimated TEMPDB space needed for CHECKALLOC (KB)
-------------------------------------------------   
15  
  
(1 row(s) affected)  
  
Estimated TEMPDB space needed for CHECKTABLES (KB)   
--------------------------------------------------   
207  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner** .
  
## <a name="examples"></a>Beispiele  
### <a name="a-checking-the-primary-filegroup-in-the-a-database"></a>A. Überprüfen der Dateigruppe PRIMARY in der Datenbank  
Das folgende Beispiel überprüft die primäre Dateigruppe der aktuellen Datenbank.
  
```sql  
  
DBCC CHECKFILEGROUP;  
GO  
```  
  
### <a name="b-checking-the-adventureworks-primary-filegroup-without-nonclustered-indexes"></a>B. Überprüfen der PRIMARY-Dateigruppe von AdventureWorks ohne nicht gruppierte Indizes  
Das folgende Beispiel überprüft die `AdventureWorks2012` Datenbank primary-Dateigruppe (ohne nicht gruppierte Indizes) durch die ID der primären Dateigruppe angeben, und geben `NOINDEX`.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKFILEGROUP (1, NOINDEX);  
GO  
```  
  
### <a name="c-checking-the-primary-filegroup-with-options"></a>C. Überprüfen der PRIMARY-Dateigruppe mit Optionen  
Im folgenden Beispiel wird die primäre Dateigruppe der `master`-Datenbank überprüft. Dabei wird die Option `ESTIMATEONLY` angegeben.
  
```sql  
USE master;  
GO  
DBCC CHECKFILEGROUP (1)  
WITH ESTIMATEONLY;  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Filegroup_id &#40; Transact-SQL &#41;](../../t-sql/functions/filegroup-id-transact-sql.md)  
[Sp_helpfile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)  
[Sp_helpfilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)  
[Sys.sysfilegroups &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysfilegroups-transact-sql.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKALLOC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)
  
  
