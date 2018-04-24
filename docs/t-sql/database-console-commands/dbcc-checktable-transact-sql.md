---
title: DBCC CHECKTABLE (Transact-SQL) | Microsoft-Dokumentation
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHECKTABLE_TSQL
- DBCC_CHECKTABLE_TSQL
- DBCC CHECKTABLE
- CHECKTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], DBCC CHECKTABLE
- page integrity checks [SQL Server]
- consistency [SQL Server], tables
- consistency [SQL Server], indexed views
- DBCC CHECKTABLE statement
- integrity [SQL Server]
- low overhead checks
- table integrity checks [SQL Server]
ms.assetid: 0d6cb620-eb58-4745-8587-4133a1b16994
caps.latest.revision: 89
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: e93755c4eda0f95cdf62add5594b66f2b5944043
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-checktable-transact-sql"></a>DBCC CHECKTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Überprüft die Integrität aller Seiten und Strukturen, aus denen die Tabelle oder indizierte Sicht besteht.

![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
    
## <a name="syntax"></a>Syntax    
    
```    
DBCC CHECKTABLE     
(    
    table_name | view_name    
    [ , { NOINDEX | index_id }    
     |, { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD }     
    ]     
)    
    [ WITH     
        { ALL_ERRORMSGS ]    
          [ , EXTENDED_LOGICAL_CHECKS ]     
          [ , NO_INFOMSGS ]    
          [ , TABLOCK ]     
          [ , ESTIMATEONLY ]     
          [ , { PHYSICAL_ONLY | DATA_PURITY } ]     
          [ , MAXDOP = number_of_processors ]    
        }    
    ]    
```    
    
## <a name="arguments"></a>Argumente    
 *table_name* | *view_name*  
 Die Tabelle oder indizierte Sicht, für die Integritätsüberprüfungen ausgeführt werden sollen. Tabellen- oder Sichtnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
    
NOINDEX  
 Legt fest, dass nicht gruppierte Indizes für Benutzertabellen nicht intensiv überprüft werden. Dadurch wird die Ausführungsdauer insgesamt verkürzt. NOINDEX hat keine Auswirkungen auf Systemtabellen, da die Integritätsüberprüfungen immer für alle Systemtabellenindizes ausgeführt werden.  
    
 *index_id*  
 Die Index-ID, für die Integritätsüberprüfungen ausgeführt werden sollen. Wird *index_id* angegeben, führt DBCC CHECKTABLE Integritätsüberprüfungen nur für den entsprechenden Index zusammen mit dem Heap oder gruppierten Index aus.  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 Legt fest, dass DBCC CHECKTABLE gefundene Fehler behebt. Zum Verwenden einer Reparaturoption muss sich die Datenbank im Einzelbenutzermodus befinden.  
    
REPAIR_ALLOW_DATA_LOSS  
 Versucht, alle gemeldeten Fehler zu reparieren. Diese Reparaturen können zu Datenverlusten führen.  
    
REPAIR_FAST  
 Die Syntax wird nur aus Gründen der Abwärtskompatibilität beibehalten. Es werden keine Reparaturaktionen ausgeführt.  
    
REPAIR_REBUILD  
 Führt Reparaturen aus, bei denen kein Datenverlust möglich ist. Dazu können schnelle Reparaturen gehören, wie z. B. das Reparieren fehlender Zeilen in nicht gruppierten Indizes, als auch zeitaufwändigere Reparaturen, wie das Neuerstellen von Indizes.  
 Dieses Argument behebt keine Fehler, die FILESTREAM-Daten betreffen.  
    
 > [!NOTE]  
 > Verwenden Sie die REPAIR-Optionen nur als letzte Möglichkeit. Zum Reparieren von Fehlern empfiehlt sich das Wiederherstellen mithilfe einer Sicherung. Bei Reparaturvorgängen werden keine Einschränkungen berücksichtigt, die möglicherweise in oder zwischen Tabellen vorhanden sind. Wenn die angegebene Tabelle an einer oder mehreren Einschränkungen beteiligt ist, ist es empfehlenswert, nach einem Reparaturvorgang `DBCC CHECKCONSTRAINTS` auszuführen.
 > Wenn Sie REPAIR verwenden müssen, sollten Sie `DBCC CHECKTABLE` ohne Reparaturoption ausführen, um die zu verwendende Reparaturstufe zu ermitteln. Wenn Sie die Ebene REPAIR_ALLOW_DATA_LOSS verwenden möchten, empfiehlt es sich, die Datenbank vor dem Ausführen von `DBCC CHECKTABLE` mit dieser Option zu sichern.  
    
ALL_ERRORMSGS  
 Zeigt eine unbegrenzte Anzahl von Fehlern an. Alle Fehlermeldungen werden standardmäßig angezeigt. Das Angeben oder Weglassen dieser Option hat keine Auswirkungen.  
    
EXTENDED_LOGICAL_CHECKS  
 Wenn der Kompatiblitätsgrad 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) oder höher ist, werden logische Konsistenzprüfungen an einer indizierten Sicht, XML-Indizes und räumliche Indizes (sofern vorhanden) ausgeführt.  
 Weitere Informationen finden Sie unter *Ausführen logischer Konsistenzprüfungen an Indizes* im Abschnitt [Hinweise](#remarks) weiter unten in diesem Thema.  
    
NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
    
TABLOCK  
 Bewirkt, dass DBCC CHECKTABLE eine freigegebene Tabellensperre erhält, statt eine interne Datenbankmomentaufnahme zu verwenden. Durch TABLOCK wird DBCC CHECKTABLE für eine Tabelle bei starker Belastung schneller ausgeführt, jedoch wird während der Ausführung von DBCC CHECKTABLE die in der Tabelle verfügbare Parallelität verringert.  
    
ESTIMATEONLY  
 Zeigt den tempdb-Speicherplatz an, der schätzungsweise erforderlich ist, um DBCC CHECKTABLE mit allen anderen angegebenen Optionen auszuführen.  
    
PHYSICAL_ONLY  
 Beschränkt die Überprüfung auf die Integrität der physischen Struktur der Seite, der Datensatzheader und der physischen Struktur von B-Strukturen. Wurde entworfen, um mit geringem Verwaltungsaufwand eine Überprüfung der physischen Konsistenz der Tabelle vorzunehmen. Dabei können auch zerrissene Seiten und häufige Hardwarefehler erkannt werden, die die Daten gefährden können. Die vollständige Ausführung von DBCC CHECKTABLE kann erheblich mehr Zeit in Anspruch nehmen als in früheren Versionen. Dieses Verhalten erfolgt normalerweise aus einem der folgenden Gründe:  
 -   Die logischen Überprüfungen sind umfassender.  
 -   Einige der zu überprüfenden zugrunde liegenden Strukturen sind komplexer.  
 -   Es wurden viele neue Überprüfungen eingeführt, um die neuen Funktionen einzuschließen.  
   
Daher bewirkt das Verwenden der PHYSICAL_ONLY-Option möglicherweise eine viel kürzere Ausführungszeit von DBCC CHECKTABLE für große Tabellen. Es wird daher für die häufige Verwendung in Produktionssystemen empfohlen. Dennoch ist eine vollständige Ausführung von DBCC CHECKTABLE in regelmäßigen Abständen empfehlenswert. Die Häufigkeit dieser Ausführungsvorgänge hängt von Faktoren ab, die für einzelne Unternehmen und Produktionsumgebungen spezifisch sind. PHYSICAL_ONLY impliziert stets NO_INFOMSGS und kann nicht mit einer der Reparaturoptionen verwendet werden.  
    
 > [!NOTE]  
 > Bei Angabe von PHYSICAL_ONLY überspringt DBCC CHECKTABLE alle Prüfungen der FILESTREAM-Daten.  
    
DATA_PURITY  
 Bewirkt, dass DBCC CHECKTABLE die Tabelle auf Spaltenwerte überprüft, die ungültig sind oder außerhalb des zulässigen Bereichs liegen. So können mit DBCC CHECKTABLE z.B. Spalten mit Datums- und Zeitwerten erkannt werden, die außerhalb des zulässigen Bereichs für den **datetime**-Datentyp liegen, oder es werden **decimal**-Spalten oder Spalten mit einem ungefähren numerischen Datentyp erkannt, die ungültige Dezimal- oder Genauigkeitswerte enthalten.  
 Die Überprüfung der Spaltenwertintegrität ist standardmäßig aktiviert. Die Option DATA_PURITY ist nicht erforderlich. Bei Datenbanken, die von früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert wurden, können Sie mit DBCC CHECKTABLE WITH DATA_PURITY Fehler in einer bestimmten Tabelle suchen und beheben, jedoch ist die Spaltenwertprüfung standardmäßig erst dann aktiviert, wenn DBCC CHECKDB WITH DATA_PURITY fehlerfrei für die Datenbank ausgeführt wurde. Danach wird die Spaltenwertintegrität standardmäßig von DBCC CHECKDB und DBCC CHECKTABLE überprüft.  
 Mit dieser Option gemeldete Überprüfungsfehler können nicht mithilfe der DBCC-Reparaturoptionen behoben werden. Informationen zur manuellen Behebung dieser Fehler finden Sie im Knowledge Base-Artikel 923247: [Problembehandlung bei DBCC-Fehler 2570 in SQL Server 2005 und höher](http://support.microsoft.com/kb/923247).  
 Wenn PHYSICAL_ONLY angegeben ist, wird die Spaltenintegrität nicht überprüft.  
    
MAXDOP  
 **Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
 
 Überschreibt die Konfigurationsoption **Max. Grad an Parallelität** von **sp_configure** für die Anweisung. Der MAXDOP kann den mit „sp_configure“ konfigurierten Wert überschreiten. Wenn MAXDOP den mit Resource Governor konfigurierten Wert überschreitet, verwendet die Datenbank-Engine den in „ALTER WORKLOAD GROUP (Transact-SQL)“ beschriebenen MAXDOP-Wert von Resource Governor. Alle semantischen Regeln, die mit der Konfigurationsoption Max. Grad an Parallelität verwendet werden können, stehen beim Verwenden des MAXDOP-Abfragehinweises zur Verfügung. Weitere Informationen finden Sie unter [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
    
 > [!NOTE]  
 > Wenn MAXDOP auf 0 (Null) festgelegt wird, wählt der Server den maximalen Grad an Parallelität aus.  
    
## <a name="remarks"></a>Remarks    
    
> [!NOTE]    
> Verwenden Sie [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md), um DBCC CHECKTABLE für jede Tabelle der Datenbank auszuführen.    
    
DBCC CHECKTABLE überprüft für die angegebene Tabelle Folgendes:
-   Überprüft, ob die Index-, LOB- und Zeilenüberlauf-Datenseiten sowie die Datenseiten in Zeilen richtig verknüpft sind.    
-   Überprüft, ob sich die Indizes in der richtigen Sortierreihenfolge befinden.    
-   Überprüft, ob die Zeiger konsistent sind.    
-   Überprüft, ob die Daten auf jeder Seite sinnvoll sind, einschließlich berechneter Spalten.    
-   Überprüft, ob die Seitenoffsets sinnvoll sind.    
-   Überprüft, ob es für jede Zeile in der Basistabelle eine entsprechende Zeile in jedem nicht gruppierten Index gibt und umgekehrt.    
-   Überprüft, ob sich jede Zeile in einer partitionierten Tabelle oder einem partitionierten Index in der richtigen Partition befindet.    
-   Überprüft die Konsistenz auf Linkebene zwischen dem Dateisystem und der Tabelle, wenn die **varbinary(max)**-Daten mit FILESTREAM im Dateisystem gespeichert werden.    
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>Ausführen logischer Konsistenzprüfungen an Indizes    
Die logische Konsistenzprüfung an Indizes variiert wie folgt je nach dem Kompatibilitätsgrad der Datenbank:
-   Wenn der Kompatibilitätsgrad 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) oder höher ist:    
    -   DBCC CHECKTABLE führt sowohl physische als auch logische Konsistenzprüfungen für eine einzelne Tabelle und alle nicht gruppierten Indizes aus, sofern nicht NOINDEX angegeben wird. Allerdings werden an XML-Indizes, räumlichen Indizes und indizierten Sichten standardmäßig nur physische Konsistenzprüfungen ausgeführt.    
    -   Bei Angabe von WITH EXTENDED_LOGICAL_CHECKS werden logische Konsistenzprüfungen an indizierten Sichten, XML-Indizes und räumlichen Indizes (sofern vorhanden) ausgeführt. Standardmäßig werden physische Konsistenzprüfungen vor den logischen Konsistenzprüfungen ausgeführt. Wenn NOINDEX ebenfalls angegeben wird, werden nur die logischen Prüfungen ausgeführt.    
         Diese logischen Konsistenzprüfungen überprüfen die interne Indextabelle des Indexobjekts anhand der Benutzertabelle, auf die verwiesen wird. Zum Auffinden externer Zeilen wird eine interne Abfrage konstruiert, um eine vollständige Schnittmenge der internen Tabellen und der Benutzertabellen zu bilden. Die Ausführung dieser Abfrage kann sich sehr stark auf die Leistung auswirken, und ihr Status kann nicht verfolgt werden. Daher empfiehlt es sich, WITH EXTENDED_LOGICAL_CHECKS nur dann anzugeben, wenn Sie Indexprobleme vermuten, die nicht mit einer physischen Beschädigung in Zusammenhang stehen, oder wenn die Prüfsummen auf Seitenebene deaktiviert wurden und Sie eine Beschädigung der Hardware auf Spaltenebene vermuten.    
    -   Bei einem gefilterten Index prüft DBCC CHECKDB anhand von Konsistenzprüfungen, ob die Indexeinträge dem Filterprädikat entsprechen.   
      
- Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] werden zusätzliche Überprüfungen von persistierten berechneten Spalten, UDT-Spalten und gefilterten Indizes nicht standardmäßig ausgeführt, um die teuren Auswertungen von Ausdrücken zu vermeiden. Durch diese Änderung wird die Dauer der Ausführung von CHECKDB für Datenbanken, die diese Objekte enthalten, stark reduziert. Jedoch werden die physischen Konsistenzprüfungen dieser Objekte stets abgeschlossen. Nur wenn die Option EXTENDED_LOGICAL_CHECKS angegeben wird, werden die Auswertungen von Ausdrücken zusätzlich zu bereits vorhandenen logischen Überprüfungen (indizierte Sicht, XML-Indizes und Räumlichkeitsindizes) als Teil der Option EXTENDED_LOGICAL_CHECKS durchgeführt.
-  Wenn der Kompatibilitätsgrad 90 ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) oder weniger beträgt, führt DBCC CHECKTABLE sowohl physische als auch logische Konsistenzprüfungen für eine einzelne Tabelle oder indizierte Sicht und für alle nicht gruppierten Indizes und XML-Indizes aus, sofern nicht NOINDEX angegeben wird. Räumliche Indizes werden nicht unterstützt.
    
 **So erfahren Sie den Kompatibilitätsgrad einer Datenbank**    
[Anzeigen oder Ändern des Kompatibilitätsgrads einer Datenbank](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>Interne Datenbankmomentaufnahme    
DBCC CHECKTABLE verwendet eine interne Datenbankmomentaufnahme, um die für die Ausführung dieser Überprüfungen erforderliche Transaktionskonsistenz bereitzustellen. Weitere Informationen finden Sie unter [Anzeigen der Größe der Datei mit geringer Dichte einer Datenbankmomentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) und im Abschnitt „Verwenden einer internen Datenbankmomentaufnahme mit DBCC“ unter [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Wenn eine Momentaufnahme nicht erstellt werden kann oder TABLOCK angegeben ist, erwirbt DBCC CHECKTABLE eine freigegebene Tabellensperre, um die erforderliche Konsistenz zu erhalten.
    
> [!NOTE]    
> Wird DBCC CHECKTABLE für tempdb ausgeführt, muss eine freigegebene Tabellensperre erworben werden. Dies liegt daran, dass aus Leistungsgründen keine Datenbankmomentaufnahmen auf tempdb verfügbar sind. Dies bedeutet, dass die erforderliche Transaktionskonsistenz nicht erhalten werden kann.    
    
## <a name="checking-and-repairing-filestream-data"></a>Überprüfen und Reparieren von FILESTREAM-Daten    
Wenn FILESTREAM für eine Datenbank und eine Tabelle aktiviert ist, können Sie **varbinary(max)**-BLOBs (Binary Large Objects) optional im Dateisystem speichern. Wenn Sie DBCC CHECKTABLE für eine Tabelle verwenden, die BLOBs im Dateisystem speichert, überprüft DBCC die Konsistenz auf Linkebene zwischen dem Dateisystem und der Datenbank.
Wenn eine Tabelle beispielsweise eine **varbinary(max)**-Spalte mit dem FILESTREAM-Attribut enthält, überprüft DBCC CHECKTABLE, ob zwischen den Dateisystemverzeichnissen und -dateien und den Tabellenzeilen, Spalten und Spaltenwerten eine 1:1-Zuordnung besteht. DBCC CHECKTABLE kann Beschädigungen reparieren, wenn Sie die REPAIR_ALLOW_DATA_LOSS-Option angeben. Zum Reparieren einer FILESTREAM-Beschädigung löscht DBCC alle Tabellenzeilen, für die Dateisystemdaten fehlen, sowie alle Verzeichnisse und Dateien, die keiner Tabellenzeile, keiner Spalte oder keinem Spaltenwert zugeordnet sind.
    
## <a name="checking-objects-in-parallel"></a>Paralleles Überprüfen von Objekten    
Standardmäßig führt DBCC CHECKTABLE eine parallele Überprüfung von Objekten durch. Der Grad der Parallelität wird automatisch durch den Abfrageprozessor bestimmt. Der maximale Grad der Parallelität wird auf dieselbe Weise konfiguriert wie der maximale Grad bei parallelen Abfragen. Verwenden Sie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md), um die maximale Anzahl von Prozessoren zu beschränken, die für DBCC-Überprüfungen verfügbar sind. Weitere Informationen finden Sie unter [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
Die parallele Überprüfung kann mithilfe des Ablaufverfolgungsflags 2528 deaktiviert werden. Weitere Informationen finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
    
> [!NOTE]    
> Während eines DBCC CHECKTABLE-Vorgangs müssen die Bytes, die in einer Spalte eines benutzerdefinierten Typs gespeichert sind, dessen Sortierreihenfolge eine Bytereihenfolge ist, gleich der berechneten Serialisierung des UDT-Werts (User-Defined Type, benutzerdefinierter Typ) sein. Falls dies nicht zutrifft, meldet die DBCC CHECKTABLE-Routine einen Konsistenzfehler.    
    
## <a name="understanding-dbcc-error-messages"></a>Grundlegendes zu DBCC-Fehlermeldungen    
Nach Beendigung des Befehls DBCC CHECKTABLE wird eine Meldung in das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll geschrieben. Wurde der DBCC-Befehl erfolgreich ausgeführt, zeigt die Meldung den erfolgreichen Abschluss und die Ausführungsdauer des Befehls an. Wurde der DBCC-Befehl aufgrund eines Fehlers vor Abschluss der Überprüfung beendet, zeigt die Meldung an, dass der Befehl beendet wurde. Außerdem wird ein Statuswert und die Ausführungsdauer des Befehls angegeben. In der folgenden Tabelle sind die Statuswerte aufgeführt und beschrieben, die in der Meldung enthalten sein können.
    
|Status|Description|    
|-----------|-----------------|    
|0|Fehlernummer 8930 wurde ausgelöst. Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|    
|1|Fehlernummer 8967 wurde ausgelöst. Ein interner DBCC-Fehler ist aufgetreten.|    
|2|Beim Reparieren einer Datenbank im Notfallmodus ist ein Fehler aufgetreten.|    
|3|Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|    
|4|Eine Assertations- oder Zugriffsverletzung wurde entdeckt.|    
|5|Ein unbekannter Fehler ist aufgetreten, der den DBCC-Befehl beendet hat.|    
    
## <a name="error-reporting"></a>Fehlerberichterstellung    
Eine Minidumpdatei (`SQLDUMP*nnnn*.txt`) wird jedes Mal im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-LOG-Verzeichnis erstellt, wenn DBCC CHECKTABLE einen Fehler durch eine Beschädigung erkennt. Falls die Features zur Datensammlung zur *Verwendung von Features* und zur *Fehlerberichterstellung* für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz aktiviert sind, wird die Datei automatisch an [!INCLUDE[msCoName](../../includes/msconame-md.md)] weitergeleitet. Die gesammelten Daten werden zur Verbesserung der Funktionalität von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet.
Die Sicherungsdatei enthält die Ergebnisse des DBCC CHECKTABLE-Befehls sowie eine zusätzliche Diagnoseausgabe. Die Datei verfügt über eingeschränkte, besitzverwaltete Zugriffssteuerungslisten (Discretionary Access Control List, DACL). Der Zugriff ist auf das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto und Mitglieder der Systemadministratorrolle beschränkt. Die Systemadministratorrolle enthält standardmäßig alle Mitglieder der Windows-Gruppe VORDEFINIERT\Administratoren und der Gruppe lokaler Administratoren. Ein Fehler bei der Datensammlung verursacht keinen Fehler des DBCC-Befehls.
    
## <a name="resolving-errors"></a>Auflösen von Fehlern    
 Wenn DBCC CHECKTABLE Fehler meldet, ist es empfehlenswert, die Datenbank aus der Datenbanksicherung wiederherzustellen, statt REPAIR mit einer der REPAIR-Optionen auszuführen. Ist keine Sicherung vorhanden, können durch das Ausführen von REPAIR die gemeldeten Fehler behoben werden. Die zu verwendende REPAIR-Option wird am Ende der Liste der gemeldeten Fehler angegeben. Beim Beheben der Fehler mithilfe der REPAIR_ALLOW_DATA_LOSS-Option ist es jedoch möglicherweise erforderlich, einige Seiten (und somit Daten) zu löschen.    
Die Reparatur kann im Rahmen einer Benutzertransaktion ausgeführt werden, damit der Benutzer für die vorgenommenen Änderungen ggf. ein Rollback ausführen kann. Falls für Reparaturen ein Rollback ausgeführt wird, enthält die Datenbank immer noch Fehler und muss von einer Sicherung wiederhergestellt werden. Sichern Sie die Datenbank nach dem Abschluss aller Reparaturen.
    
## <a name="result-sets"></a>Resultsets    
DBCC CHECKTABLE gibt das folgende Resultset zurück. Das gleiche Resultset wird zurückgegeben, wenn Sie nur den Tabellennamen oder eine der Optionen angeben.
    
```
DBCC results for 'HumanResources.Employee'.    
There are 288 rows in 13 pages for object 'Employee'.    
DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```    
    
DBCC CHECKTABLE gibt das folgende Resultset zurück, wenn die ESTIMATEONLY-Option angegeben wurde:
    
```
Estimated TEMPDB space needed for CHECKTABLES (KB)     
--------------------------------------------------     
21    
(1 row(s) affected)    
DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```    
    
## <a name="permissions"></a>Berechtigungen    
Sie müssen der Besitzer der Tabelle sein oder ein Mitglied der festen Serverrolle „sysadmin“ bzw. der festen Datenbankrollen „db_owner“ oder „db_ddladmin“.    
    
## <a name="examples"></a>Beispiele    
    
### <a name="a-checking-a-specific-table"></a>A. Überprüfen einer bestimmten Tabelle    
Im folgenden Beispiel wird die Datenseitenintegrität der `HumanResources.Employee`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank überprüft.
    
```sql    
DBCC CHECKTABLE ('HumanResources.Employee');    
GO    
```    
    
### <a name="b-performing-a-low-overhead-check-of-the-table"></a>B. Ausführen einer Überprüfung der Tabelle mit geringem Verwaltungsaufwand    
 Im folgenden Beispiel wird eine Überprüfung der `Employee`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank mit geringem Verwaltungsaufwand ausgeführt.    
    
```sql    
DBCC CHECKTABLE ('HumanResources.Employee') WITH PHYSICAL_ONLY;    
GO    
```    
    
### <a name="c-checking-a-specific-index"></a>C. Überprüfen eines bestimmten Indexes    
 Im folgenden Beispiel wird ein bestimmter Index überprüft, der durch Zugreifen auf `sys.indexes` ermittelt wird.    
    
```sql    
DECLARE @indid int;    
SET @indid = (SELECT index_id     
              FROM sys.indexes    
              WHERE object_id = OBJECT_ID('Production.Product')    
                    AND name = 'AK_Product_Name');    
DBCC CHECKTABLE ('Production.Product',@indid);    
```    
    
## <a name="see-also"></a>Weitere Informationen finden Sie unter    
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)     
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)    
    
  
