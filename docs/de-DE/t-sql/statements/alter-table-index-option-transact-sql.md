---
title: index_option (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- index_option
ms.assetid: 8a14f12d-2fbf-4036-b8b2-8db3354e0eb7
caps.latest.revision: 68
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 40a6e63b89089f0e5ead7c581450cca8077bdccd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-table-indexoption-transact-sql"></a>ALTER TABLE index_option (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Gruppe von Optionen an, die auf einen Index angewendet werden können, der Teil einer mit [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) erstellten Einschränkungsdefinition ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
{   
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | SORT_IN_TEMPDB = { ON | OFF }   
  | ONLINE = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE |ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
<single_partition_rebuild__option> ::=  
{  
    SORT_IN_TEMPDB = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = {NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE } }  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                           ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
## <a name="arguments"></a>Argumente  
 PAD_INDEX **=** { ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Auffüllung von Indizes an. Der Standardwert ist OFF.  
  
 ON  
 Der Prozentsatz des mit FILLFACTOR angegebenen freien Speicherplatzes wird für die Zwischenebenenseiten des Indexes angewendet.  
  
 OFF oder *fillfactor* ist nicht angegeben  
 Die Zwischenebenenseiten werden nahezu vollständig aufgefüllt, wobei jedoch ausreichend freier Speicherplatz verfügbar bleibt, um mindestens eine Zeile in der maximal für diesen Index gültigen Größe aufzunehmen, die sich aus der Schlüsselmenge auf den Zwischenseiten ergibt.  
  
 FILLFACTOR **=***fillfactor*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt einen Prozentwert an, der dem Füllfaktor entspricht. Dieser Faktor legt fest, wie weit die [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -änderung auffüllen soll.  Der angegebene Wert muss ein ganzzahliger Wert zwischen 1 und 100 sein. Die Standardeinstellung ist 0.  
  
> [!NOTE]  
>  Die Füllfaktorwerte 0 und 100 sind in jeglicher Hinsicht identisch.  
  
 IGNORE_DUP_KEY **=** { ON | **OFF** }  
 Gibt die Fehlermeldung an, wenn ein Einfügevorgang versucht, doppelte Schlüsselwerte in einen eindeutigen Index einzufügen. Die IGNORE_DUP_KEY-Option gilt nur für Einfügevorgänge nach dem Erstellen oder Neuerstellen des Index. Beim Ausführen von [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) oder [UPDATE](../../t-sql/queries/update-transact-sql.md) hat die Option keine Auswirkungen. Der Standardwert ist OFF.  
  
 ON  
 Eine Warnmeldung wird ausgegeben, wenn doppelte Schlüsselwerte in einen eindeutigen Index eingefügt werden. Es schlagen nur die Zeilen fehl, die gegen die Eindeutigkeitseinschränkung verstoßen.  
  
 OFF  
 Eine Fehlermeldung wird ausgegeben, wenn doppelte Schlüsselwerte in einen eindeutigen Index eingefügt werden. Für den gesamten INSERT-Vorgang wird ein Rollback ausgeführt.  
  
 IGNORE_DUP_KEY kann für Folgenes nicht auf ON festgelegt werden: für Indizes, die in einer Sicht erstellt wurden, nicht eindeutige Indizes, XML-Indizes, räumliche Indizes und gefilterte Indizes.  
  
 Um IGNORE_DUP_KEY anzuzeigen, verwenden Sie [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 In abwärtskompatibler Syntax ist WITH IGNORE_DUP_KEY gleichwertig mit WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE **=** { ON | **OFF** }  
 Gibt an, ob Statistiken neu berechnet werden. Der Standardwert ist OFF.  
  
 ON  
 Veraltete Indexstatistiken werden nicht automatisch neu berechnet.  
  
 OFF  
 Die automatischen Updates der Statistiken sind aktiviert.  
  
 ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, ob Zeilensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Zeilensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Zeilensperren verwendet werden.  
  
 OFF  
 Zeilensperren werden nicht verwendet.  
  
 ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, ob Seitensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Seitensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Seitensperren verwendet werden.  
  
 OFF  
 Seitensperren werden nicht verwendet.  
  
 SORT_IN_TEMPDB **=** { ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, ob Sortierungsergebnisse in **tempdb** gespeichert werden sollen. Der Standardwert ist OFF.  
  
 ON  
 Die Zwischenergebnisse von Sortierungen, mit denen der Index erstellt wird, werden in **tempdb** gespeichert. Dadurch kann sich die zum Erstellen eines Index erforderliche Zeit verringern, wenn sich **tempdb** in anderen Datenträgersätzen befindet als die Benutzerdatenbank. Sie erhöht jedoch den Betrag an Speicherplatz, der während der Indexerstellung verwendet wird.  
  
 OFF  
 Die Zwischenergebnisse der Sortierung werden in derselben Datenbank gespeichert wie der Index.  
  
 ONLINE **=** { ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, ob die zugrunde liegenden Tabellen und zugeordneten Indizes für Abfragen und Datenänderungen während des Indexvorgangs verfügbar sind. Der Standardwert ist OFF. REBUILD kann als ONLINE-Vorgang ausgeführt werden.  
  
> [!NOTE]  
>  Eindeutige nicht gruppierte Indizes können nicht online erstellt werden. Dies schließt Indizes ein, die aufgrund einer UNIQUE- oder PRIMARY KEY-Einschränkung erstellt werden.  
  
 ON  
 Lang andauernde Sperren werden nicht für die Dauer des Indexvorgangs aufrechterhalten. Während der Hauptphase des Indexvorgangs wird nur eine beabsichtigte freigegebene Sperre für die Quelltabelle aufrechterhalten. Dadurch können Abfragen oder Updates für die zugrunde liegende Tabelle und die Indizes fortgesetzt werden. Zu Beginn des Vorgangs wird für sehr kurze Zeit eine freigegebene Sperre (S) für das Quellobjekt aufrechterhalten. Am Ende des Vorgangs wird für die Quelle für kurze Zeit eine freigegebene Sperre (S) aktiviert, wenn ein nicht gruppierter Index erstellt wird. Eine Schemaänderungssperre (SCH-M) wird aktiviert, wenn ein gruppierter Index online erstellt oder gelöscht und wenn ein gruppierter oder nicht gruppierter Index neu erstellt wird. Obwohl die Onlineindexsperren kurze Metadatensperren sind, muss insbesondere die Sch-M-Sperre warten, bis alle blockierenden Transaktionen für diese Tabelle abgeschlossen sind. Während der Wartezeit sperrt die Sch-M-Sperre alle anderen Transaktionen, die an dieser Sperre warten, wenn sie auf die gleiche Tabelle zugreifen. ONLINE kann nicht auf ON festgelegt werden, wenn ein Index auf einer lokalen temporären Tabelle erstellt wird.  
  
> [!NOTE]  
>  Durch Neuerstellung von Onlineindizes können die *low_priority_lock_wait*-Optionen festgelegt werden, die weiter unten in diesem Abschnitt beschrieben werden. *low_priority_lock_wait* verwaltet die Priorität der S- und Sch-M-Sperren während der Onlineneuerstellung des Indexes.  
  
 OFF  
 Die Tabellensperren werden für die Dauer des Indexvorgangs angewendet. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können. Ein Offlineindexvorgang, bei dem ein gruppierter Index erstellt, neu erstellt oder gelöscht bzw. ein nicht gruppierter Index neu erstellt oder gelöscht wird, aktiviert eine Schemaänderungssperre (SCH-M) für die Tabelle. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können. Ein Offlineindexvorgang, bei dem ein nicht gruppierter Index erstellt wird, aktiviert eine freigegebene Sperre (S) für die Tabelle. Dadurch werden Updates der zugrunde liegenden Tabelle verhindert. Lesevorgänge, wie SELECT-Anweisungen, sind jedoch zulässig.  
  
 Weitere Informationen finden Sie unter [Funktionsweise von Onlineindexvorgängen](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
> [!NOTE]  
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 MAXDOP **=***max_degree_of_parallelism*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Überschreibt die Konfigurationsoption **max degree of parallelism** (Max. Grad an Parallelität) für die Dauer des Indexvorgangs. Weitere Informationen finden Sie unter [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
 *max_degree_of_parallelism* kann folgende Werte haben:  
  
 - 1: Unterdrückt das Generieren paralleler Pläne.  
 - \>1: Begrenzt die Höchstzahl von Prozessoren in einem parallelen Indexvorgang auf die angegebene Zahl.  
 - 0 (Standard): Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
 Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Parallele Indexvorgänge sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 DATA_COMPRESSION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Datenkomprimierungsoption für die angegebene Tabelle, die Partitionsnummer oder den Bereich von Partitionen an. Folgende Optionen stehen zur Verfügung:  
  
 NONE  
 Die Tabelle oder die angegebenen Partitionen werden nicht komprimiert. Gilt nur für rowstore-Tabellen und nicht für columnstore-Tabellen.  
  
 ROW  
 Die Tabelle oder die angegebenen Partitionen werden mit Zeilenkomprimierung komprimiert. Gilt nur für rowstore-Tabellen und nicht für columnstore-Tabellen.  
  
 PAGE  
 Die Tabelle oder die angegebenen Partitionen werden mit Seitenkomprimierung komprimiert. Gilt nur für rowstore-Tabellen und nicht für columnstore-Tabellen.  
  
 COLUMNSTORE  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für columnstore-Tabellen. COLUMNSTORE gibt an, dass eine Partition, die mit der COLUMNSTORE_ARCHIVE-Option komprimiert wurde, dekomprimiert werden soll. Nachdem die Daten wiederhergestellt wurden, wird der Index COLUMNSTORE weiterhin mit der columnstore-Komprimierung komprimiert, die für alle columnstore-Tabellen verwendet wird.  
  
 COLUMNSTORE_ARCHIVE  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für columnstore-Tabellen. Dies sind Tabellen, die mit einem gruppierten columnstore-Index gespeichert wurden. Durch COLUMNSTORE_ARCHIVE wird die angegebene Partition weiter auf eine geringere Größe komprimiert. Dies empfiehlt sich bei der Archivierung und in Situationen, in denen es auf eine geringere Speicherbelegung und nicht auf den zusätzlichen Zeitaufwand für das Speichern und Abrufen ankommt.  
  
 Weitere Informationen zur Datenkomprimierung finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
ON PARTITIONS **(** { \<partition_number_expression> | \<range> } [ **,**...*n* ] **)** **Applies to**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] through [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Partitionen an, für die die DATA_COMPRESSION-Einstellung gilt. Wenn die Tabelle nicht partitioniert ist, erzeugt das ON PARTITIONS-Argument einen Fehler. Wenn die ON PARTITIONS-Klausel nicht angegeben ist, gilt die DATA_COMPRESSION-Option für alle Partitionen einer partitionierten Tabelle.  
  
\<partition_number_expression> kann auf die folgenden Weisen angegeben werden:  
  
-   Geben Sie die Nummer einer Partition an, beispielsweise: ON PARTITIONS (2).  
-   Geben Sie die Partitionsnummern mehrerer einzelner Partitionen durch Trennzeichen getrennt an, beispielsweise: ON PARTITIONS (1, 5).  
-   Geben Sie sowohl Bereiche als auch einzelne Partitionen an, beispielsweise: ON PARTITIONS (2, 4, 6 TO 8).  
  
\<range> kann als Partitionsnummern angegeben werden, die durch das Wort TO voneinander getrennt werden, beispielsweise: ON PARTITIONS (6 TO 8).  
  
 Wenn Sie für verschiedene Partitionen unterschiedliche Datenkomprimierungstypen festlegen möchten, geben Sie die Option DATA_COMPRESSION mehrmals an, beispielsweise:  
  
```sql  
--For rowstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
  
--For columnstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = COLUMNSTORE ON PARTITIONS (1, 3, 5),   
DATA_COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (2, 4, 6 TO 8)  
)  
```  
  
**\<single_partition_rebuild__option>**  
 In den meisten Fällen werden bei der Neuerstellung eines Index alle Partitionen eines partitionierten Index ebenfalls neu erstellt. Die folgenden Optionen erstellen nicht alle Partitionen neu, wenn sie auf eine einzelne Partition angewendet werden.  
  
-   SORT_IN_TEMPDB  
-   MAXDOP  
-   DATA_COMPRESSION  
  
**low_priority_lock_wait**  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 **SWITCH** oder eine Neuerstellung eines Onlineindexes wird abgeschlossen, sobald es keine blockierenden Vorgänge für diese Tabelle gibt. *WAIT_AT_LOW_PRIORITY* gibt an, dass der Vorgang wartet, wenn **SWITCH** oder die Neuerstellung des Onlineindexes nicht sofort abgeschlossen werden kann. Der Vorgang hält Sperren mit niedriger Priorität an und lässt die Fortsetzung anderer Vorgänge zu, die Sperren enthalten, die mit der DDL-Anweisung in Konflikt stehen. Die Option **WAIT AT LOW PRIORITY** wegzulassen, entspricht `WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`.  
  
MAX_DURATION = *time* [**MINUTES** ]  
 Die Wartezeit (ein ganzzahliger Wert, in Minuten angegeben), die von **SWITCH** oder der Onlineneuerstellung des Indexes gesperrt wird, die abgerufen werden muss, wartet beim Ausführen des DDL-Befehls. SWITCH oder die Online-Neuerstellung des Index versucht sofort, den Vorgang abzuschließen. Wenn der Vorgang während des **MAX_DURATION**-Zeitraums blockiert wird, wird eine der **ABORT_AFTER_WAIT**-Aktionen ausgeführt. Der **MAX_DURATION**-Zeitraum wird immer in Minuten angegeben. Das Wort **MINUTES** kann weggelassen werden.  
  
ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERS** } ]  
 Keine  
 Setzt **SWITCH** oder die Neuerstellung des Onlineindexes fort, ohne die Sperrenpriorität zu ändern (mit der normalen Priorität).  
  
SELF  
 Beendet **SWITCH** oder den DDL-Vorgang zur Neuerstellung des Onlineindexes, der gerade ausgeführt wird, ohne weitere Aktionen durchzuführen.  
  
BLOCKERS  
 Bricht alle Benutzertransaktionen ab, die derzeit **SWITCH** oder den DDL-Vorgang zur Neuerstellung des Onlineindexes blockieren, sodass der Vorgang fortgesetzt werden kann.  
 BLOCKERS erfordert die **ALTER ANY CONNECTION**-Berechtigung.  
  
## <a name="remarks"></a>Remarks  
 Eine vollständige Beschreibung der Indexoptionen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)   
 [computed_column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-computed-column-definition-transact-sql.md)   
 [table_constraint (Transact-SQL)](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  
  
 
