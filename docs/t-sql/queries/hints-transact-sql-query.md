---
title: Abfragehinweise (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Query_Hint_TSQL
- Query_TSQL
- Query
- Query Hint
- MAX_GRANT_PERCENT
- MAX_GRANT_PERCENT_TSQL
- MIN_GRANT_PERCENT
- MIN_GRANT_PERCENT_TSQL
- EXTERNALPUSHDOWN
- EXTERNALPUSHDOWN_TSQL
- NOLOCK_TSQL
- MAXDOP_TSQL
- USE_HINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REPORT PLAN query hint
- FORCE ORDER query hint
- HASH JOIN query hint
- query hints [SQL Server]
- OPTIMIZE FOR query hint
- FORCESCAN query hint
- RECOMPILE query hint
- MAXRECURSION query hint
- MERGE JOIN query hint
- HASH GROUP query hint
- KEEP PLAN query hint
- UNION query hint
- FORCESEEK query hint
- ORDER GROUP query hint
- LOOP JOIN query hint
- KEEPFIXED PLAN query hint
- FAST query hint
- MAXDOP query hint
- PARAMETERIZATION query hint
- hints [SQL Server], query
- JOIN query hint
- USE PLAN query hint
- EXPAND VIEWS query hint
- MAX_GRANT_PERCENT query hint
- MIN_GRANT_PERCENT query hint
- EXTERNALPUSHDOWN query hint
- USE HINT query hint
ms.assetid: 66fb1520-dcdf-4aab-9ff1-7de8f79e5b2d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0a3c74aa7b1da86c6d0ac54025d337700019465d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="hints-transact-sql---query"></a>Hinweise (Transact-SQL) – Abfrage
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Abfragehinweise geben an, dass die angezeigten Hinweise in der gesamten Abfrage verwendet werden sollen. Sie wirken sich auf alle Operatoren in der Anweisung aus. Falls UNION in der Hauptabfrage vorkommt, kann nur die letzte Abfrage, die eine UNION-Operation enthält, die OPTION-Klausel aufweisen. Abfragehinweise werden als Teil der [OPTION-Klausel](../../t-sql/queries/option-clause-transact-sql.md) angegeben. Wenn mindestens ein Abfragehinweis dazu führt, dass der Abfrageoptimierer keinen gültigen Plan generiert, wird der Fehler 8622 ausgelöst.  
  
> [!CAUTION]  
>  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer in der Regel den besten Ausführungsplan für eine Abfrage auswählt, wird empfohlen, dass nur erfahrene Entwickler und Datenbankadministratoren Hinweise verwenden, wenn alle anderen Möglichkeiten sich als unbefriedigend erwiesen haben.  
  
 **Gilt für:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
<query_hint > ::=   
{ { HASH | ORDER } GROUP   
  | { CONCAT | HASH | MERGE } UNION   
  | { LOOP | MERGE | HASH } JOIN   
  | EXPAND VIEWS   
  | FAST number_rows   
  | FORCE ORDER   
  | { FORCE | DISABLE } EXTERNALPUSHDOWN  
  | IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
  | KEEP PLAN   
  | KEEPFIXED PLAN  
  | MAX_GRANT_PERCENT = percent  
  | MIN_GRANT_PERCENT = percent  
  | MAXDOP number_of_processors   
  | MAXRECURSION number   
  | NO_PERFORMANCE_SPOOL   
  | OPTIMIZE FOR ( @variable_name { UNKNOWN | = literal_constant } [ , ...n ] )  
  | OPTIMIZE FOR UNKNOWN  
  | PARAMETERIZATION { SIMPLE | FORCED }  
  | RECOMPILE  
  | ROBUST PLAN   
  | USE HINT ( '<hint_name>' [ , ...n ] )
  | USE PLAN N'xml_plan'  | TABLE HINT ( exposed_object_name [ , <table_hint> [ [, ]...n ] ] )  
}  
  
<table_hint> ::=  
[ NOEXPAND ] {   
    INDEX ( index_value [ ,...n ] ) | INDEX = ( index_value )  
  | FORCESEEK [( index_value ( index_column_name [,... ] ) ) ]  
  | FORCESCAN  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT  
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK  
}  
```  
  
## <a name="arguments"></a>Argumente  
 { HASH | ORDER } GROUP  
 Gibt an, dass die in der GROUP BY- oder DISTINCT-Klausel der Abfrage beschriebenen Aggregationen Hash- oder Sortiervorgänge verwenden sollen.  
  
 { MERGE | HASH | CONCAT } UNION  
 Gibt an, dass alle UNION-Vorgänge mithilfe von Merge-, Hash- oder Verkettungsvorgängen für die bei UNION vorkommenden Mengen ausgeführt werden. Wenn mehr als ein UNION-Hinweis angegeben wird, wählt der Abfrageoptimierer unter den angegebenen Hinweisen die Strategie mit dem geringsten Aufwand aus.  
  
 { LOOP | MERGE | HASH } JOIN  
 Gibt an, dass alle Joinvorgänge per LOOP JOIN, MERGE JOIN oder HASH JOIN in der gesamten Abfrage ausgeführt werden. Wenn mehr als ein Joinhinweis angegeben wird, wählt der Optimierer unter den zulässigen Hinweisen die Strategie mit dem geringsten Aufwand aus.  
  
 Wenn in derselben Abfrage auch ein Joinhinweis in der FROM-Klausel für ein bestimmtes Tabellenpaar angegeben ist, hat dieser Joinhinweis Vorrang bei der Verknüpfung der beiden Tabellen; die Abfragehinweise müssen jedoch auch berücksichtigt werden. Deshalb kann der Joinhinweis für das Tabellenpaar nur die Auswahl der zulässigen Joinmethoden für den Abfragehinweis einschränken. Weitere Informationen finden Sie unter [Joinhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-join.md).  
  
 EXPAND VIEWS  
 Gibt an, dass die indizierten Sichten erweitert werden und dass der Abfrageoptimierer keine indizierte Sicht als Ersatz für einen beliebigen Teil der Abfrage auffasst. Eine Sicht wird erweitert, indem der Sichtname im Abfragetext durch die Sichtdefinition ersetzt wird.  
  
 Dieser Abfragehinweis lässt die direkte Verwendung von indizierten Sichten und Indizes für indizierte Sichten im Abfrageplan praktisch nicht zu.  
  
 Die indizierte Ansicht wird nur dann nicht erweitert, wenn im SELECT-Teil der Abfrage direkt auf die Ansicht verwiesen wird und WITH (NOEXPAND) oder WITH (NOEXPAND, INDEX( *index_value* [ **,***...n* ] ) ) angegeben ist. Weitere Informationen zum Abfragehinweis WITH (NOEXPAND) finden Sie unter [FROM](../../t-sql/queries/from-transact-sql.md).  
  
 Der Hinweis wirkt sich nur auf die Sichten im SELECT-Teil von Anweisungen aus, einschließlich der Sichten in den Anweisungen INSERT, UPDATE, MERGE und DELETE.  
  
 FAST *number_rows*  
 Gibt an, dass die Abfrage für den schnellen Abruf der ersten *number_rows* optimiert wird. Dies ist eine nicht negative ganze Zahl. Nachdem die ersten *number_rows* zurückgegeben wurden, wird die Abfrage fortgesetzt und das vollständige Resultset erstellt.  
  
 FORCE ORDER  
 Gibt an, dass die von der Abfragesyntax angegebene Joinreihenfolge während der Abfrageoptimierung beibehalten wird. Die Verwendung von FORCE ORDER hat keine Auswirkung auf das mögliche Rollentauschverhalten des Abfrageoptimierers.  
  
> [!NOTE]  
>  In einer MERGE-Anweisung wird als Standardreihenfolge für Joins zunächst auf die Quelltabelle und dann auf die Zieltabelle zugegriffen, es sei denn, die WHEN SOURCE NOT MATCHED-Klausel wurde angegeben. Wenn Sie FORCE ORDER angeben, wird dieses Standardverhalten beibehalten.  
  
 { FORCE | DISABLE } EXTERNALPUSHDOWN  
 Erzwingen oder Deaktivieren der Weitergabe der Berechnung von qualifizierenden Ausdrücken in Hadoop. Gilt nur für Abfragen mit PolyBase. Wird nicht in den Azure-Speicher weitergegeben.  
  
 KEEP PLAN  
 Zwingt den Abfrageoptimierer, den geschätzten Neukompilierungsschwellenwert für eine Abfrage zu lockern. Der geschätzte Neukompilierungsschwellenwert gibt den Punkt an, bei dem eine Abfrage automatisch erneut kompiliert wird, wenn für eine Tabelle die geschätzte Anzahl von Änderungen für indizierte Spalten durch Ausführen der Anweisungen UPDATE, DELETE, MERGE oder INSERT vorgenommen wurden. Durch Angeben von KEEP PLAN wird sichergestellt, dass eine Abfrage nicht zu häufig erneut kompiliert wird, wenn an einer Tabelle mehrere Updates ausgeführt werden.  
  
 KEEPFIXED PLAN  
 Zwingt den Abfrageoptimierer, die Abfrage aufgrund von Änderungen in den Statistiken nicht erneut zu kompilieren. Durch Angabe von KEEPFIXED PLAN wird sichergestellt, dass eine Abfrage nur dann erneut kompiliert wird, wenn das Schema der zugrunde liegenden Tabellen geändert wird oder für diese Tabellen **sp_recompile** ausgeführt wird.  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Verhindert, dass die Abfrage einen nicht gruppierten speicheroptimierten Columnstore-Index verwendet. Wenn die Abfrage den Abfragehinweis, der die Verwendung des columnstore-Indexes verhindert, und einen Indexhinweis, der die Verwendung eines columnstore-Index angibt, enthält, besteht ein Konflikt zwischen den Hinweisen, und die Abfrage gibt einen Fehler zurück.  
  
 MAX_GRANT_PERCENT = *percent*  
 Die maximale Größe der Arbeitsspeicherzuweisung in Prozent. Die Abfrage überschreitet diese Begrenzung garantiert nicht. Die tatsächliche Begrenzung kann niedriger sein, wenn die Ressourcenkontrolle niedriger als die Begrenzung ist. Gültige Werte liegen in einem Bereich zwischen 0,0 und 100,0.  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 MIN_GRANT_PERCENT = *percent*  
 Die minimale Größe der Arbeitsspeicherzuweisung in PERCENT = % der Standardbegrenzung. Die Abfrage kann MAX (benötigter Speicher, Mindestzuweisung) garantiert abrufen, da zumindest der für das Starten einer Abfrage benötigte Speicher erforderlich ist. Gültige Werte liegen in einem Bereich zwischen 0,0 und 100,0.  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 MAXDOP *number*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Überschreibt die Konfigurationsoption **Max. Grad an Parallelität** von **sp_configure** und die Ressourcenkontrolle für die Abfrage, in der diese Option angegeben wird. Der MAXDOP-Abfragehinweis kann den mit sp_configure konfigurierten Wert überschreiten. Wenn MAXDOP den mit der Ressourcenkontrolle konfigurierten Wert überschreitet, verwendet [!INCLUDE[ssDE](../../includes/ssde-md.md)] den MAXDOP-Wert der Ressourcenkontrolle, wie unter [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md) beschrieben. Alle mit der Konfigurationsoption **Max. Grad an Parallelität** verwendeten semantischen Regeln gelten auch für die Verwendung des MAXDOP-Abfragehinweises. Weitere Informationen finden Sie unter [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
> [!WARNING]  
> Wenn MAXDOP auf 0 (Null) festgelegt wird, wählt der Server den maximalen Grad an Parallelität aus.  
  
 MAXRECURSION *number*  
 Gibt die maximale Anzahl der für diese Abfrage zulässigen Rekursionen an. *number* ist eine nicht negative ganze Zahl zwischen 0 und 32767. Wenn 0 angegeben wird, wird keine Beschränkung angewendet. Wenn diese Option nicht angegeben wird, beträgt das Standardlimit für den Server 100.  
  
 Wenn der angegebene Wert bzw. der Standardwert für MAXRECURSION während der Ausführung der Abfrage erreicht wird, wird die Abfrage beendet und ein Fehler wird zurückgegeben.  
  
 Aufgrund dieses Fehlers wird für alle Änderungen aufgrund der Anweisung ein Rollback ausgeführt. Falls es sich hierbei um eine SELECT-Anweisung handelt, können Teilergebnisse oder keine Ergebnisse zurückgegeben werden. Teilergebnisse schließen möglicherweise nicht alle Zeilen auf Rekursionsebenen ein, die über die angegebene maximale Rekursionsebene hinausgehen.  
  
 Weitere Informationen finden Sie unter [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 NO_PERFORMANCE_SPOOL  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Verhindert, dass ein Spool-Operator zu Abfrageplänen hinzugefügt wird (mit Ausnahme der Pläne, bei denen der Spool-Operator eine gültige Update-Semantik garantieren muss). In einigen Szenarios kann der Spool-Operator die Leistung beeinträchtigen. Der Spool-Operator verwendet beispielsweise „tempdb“. Wenn in den Spool-Vorgängen viele Abfragen gleichzeitig ausgeführt werden, kann es zu einem „tempdb“-Konflikt kommen.  
  
 OPTIMIZE FOR ( *@variable_name* { UNKNOWN | = *literal_constant }* [ **,** ...*n* ] )  
 Weist den Abfrageoptimierer an, einen bestimmten Wert für eine lokale Variable zu verwenden, wenn die Abfrage kompiliert und optimiert wird. Dieser Wert wird nur während der Abfrageoptimierung verwendet, nicht während der Abfrageausführung.  
  
 *@variable_name*  
 Der Name einer lokalen Variablen, die in einer Abfrage verwendet wird und der ein Wert für die Verwendung mit dem OPTIMIZE FOR-Abfragehinweis zugewiesen werden kann.  
  
 *UNKNOWN*  
 Gibt an, dass der Abfrageoptimierer statistische Daten statt des Anfangswerts verwenden soll, um während der Abfrageoptimierung den Wert einer lokalen Variablen zu bestimmen.  
  
 *literal_constant*  
 Ein Literalkonstantenwert, dem *@variable_name* für die Verwendung mit dem OPTIMIZE FOR-Abfragehinweis zugewiesen wird. *literal_constant* wird nur während der Abfrageoptimierung verwendet, nicht als Wert von *@variable_name* während der Abfrageausführung. *literal_constant* kann einen beliebigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp aufweisen, der als Literalkonstante dargestellt werden kann. Der Datentyp von *literal_constant* muss implizit in den Datentyp konvertierbar sein, auf den *@variable_name* in der Abfrage verweist.  
  
 OPTIMIZE FOR kann dem Standard-Parametererkennungsverhalten des Abfrageoptimierers entgegenwirken oder kann beim Erstellen von Planhinweislisten verwendet werden. Weitere Informationen finden Sie unter [Erneutes Kompilieren einer gespeicherten Prozedur](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md).  
  
 OPTIMIZE FOR UNKNOWN  
 Weist den Abfrageoptimierer an, beim Kompilieren und Optimieren der Abfrage für alle lokalen Variablen, einschließlich der Parameter, die mit erzwungener Parametrisierung erstellt werden, statistische Daten statt der Anfangswerte zu verwenden.  
  
 Wenn OPTIMIZE FOR @variable_name = *literal_constant* und OPTIMIZE FOR UNKNOWN in dem gleichen Abfragehinweis verwendet werden, verwendet der Abfrageoptimierer die *literal_constant*, die für einen bestimmten Wert angegeben wurde, und UNKNOWN für die übrigen Variablenwerte. Diese Werte werden nur während der Abfrageoptimierung verwendet, nicht während der Abfrageausführung.  
  
 PARAMETERIZATION { SIMPLE | FORCED }  
 Gibt die Parametrisierungsregeln an, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer bei der Kompilierung auf die Abfrage anwendet.  
  
> [!IMPORTANT]  
> Der PARAMETERIZATION-Abfragehinweis kann nur innerhalb einer Planhinweisliste angegeben werden. Er kann nicht direkt innerhalb einer Abfrage angegeben werden.  
  
 Mit SIMPLE wird der Abfrageoptimierer angewiesen, einfache Parametrisierung auszuführen. Mit FORCED wird der Optimierer angewiesen, erzwungene Parametrisierung auszuführen. Mit dem PARAMETERIZATION-Abfragehinweis wird die aktuelle Einstellung der Option PARAMETERIZATION database SET innerhalb einer Planhinweisliste überschrieben. Weitere Informationen finden Sie unter [Angeben des Abfrageparametrisierungsverhaltens mithilfe von Planhinweislisten](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md).  
  
 RECOMPILE  
 Weist [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] an, den für die Abfrage generierten Abfrageplan nach der Ausführung zu verwerfen. Dadurch wird der Abfrageoptimierer gezwungen, erneut einen Abfrageplan zu kompilieren, wenn dieselbe Abfrage das nächste Mal ausgeführt wird. Ohne die Angabe von RECOMPILE werden Abfragepläne von [!INCLUDE[ssDE](../../includes/ssde-md.md)] zwischengespeichert und wiederverwendet. Beim Kompilieren von Abfrageplänen verwendet der RECOMPILE-Abfragehinweis die aktuellen Werte von lokalen Variablen in der Abfrage und, falls sich die Abfrage innerhalb einer gespeicherten Prozedur befindet, die an Parameter übergebenen aktuellen Werte.  
  
 RECOMPILE ist eine hilfreiche Alternative zum Erstellen einer gespeicherten Prozedur, die die WITH RECOMPILE-Klausel verwendet, wenn nicht die gesamte gespeicherte Prozedur, sondern nur eine Teilmenge davon erneut kompiliert werden muss. Weitere Informationen finden Sie unter [Erneutes Kompilieren einer gespeicherten Prozedur](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md). RECOMPILE ist auch beim Erstellen von Planhinweislisten hilfreich.  
  
 ROBUST PLAN  
 Zwingt den Abfrageoptimierer zu einer Vorgehensweise, bei der der Schwerpunkt auf der maximalen potenziellen Zeilengröße liegt. Dies geht möglicherweise zu Lasten der Leistung. Bei der Verarbeitung der Abfrage müssen möglicherweise Zwischentabellen und Operatoren Zeilen speichern und verarbeiten, die größer sind als alle Eingabezeilen. Die Zeilen können so groß sein, dass der jeweilige Operator in einigen Fällen die Zeile nicht verarbeiten kann. In diesem Fall gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] während der Ausführung der Abfrage einen Fehler aus. Durch das Verwenden von ROBUST PLAN weisen Sie den Abfrageoptimierer an, keine Abfragepläne in Betracht zu ziehen, für die möglicherweise dieses Problem auftritt.  
  
 Ist eine solche Vorgehensweise nicht möglich, gibt der Abfrageoptimierer einen Fehler zurück, statt die Fehlererkennung auf die Abfrageausführung zu verschieben. Die Zeilen können Spalten variabler Länge aufweisen. [!INCLUDE[ssDE](../../includes/ssde-md.md)] läßt die Definition von Zeilen zu, deren maximale potenzielle Größe von [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht mehr verarbeitet werden kann. Trotz der maximalen potenziellen Größe speichert eine Anwendung im Allgemeinen Zeilen, deren tatsächliche Größe innerhalb der Höchstwerte liegen, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] verarbeiten kann. Wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Zeile ermittelt, die zu lang ist, wird ein Ausführungsfehler zurückgegeben.  
 
<a name="use_hint"></a> USE HINT ( **'***hint_name***'** )  
 **Gilt für**: Gilt für[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) und [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
 
 Stellt mindestens einen zusätzlichen Hinweis für den Abfrageprozessor bereit, der von einem Hinweisnamen **innerhalb einfacher Anführungszeichen** angegeben wird. 

 Die folgenden Hinweisnamen werden unterstützt:
 
*  'DISABLE_OPTIMIZED_NESTED_LOOP'  
 Weist den Abfrageprozessor an, bei der Generierung eines Abfrageplans keine Sortiervorgänge (Batch-Sortierung) für optimierte Joins geschachtelter Schleifen zu verwenden. Dies entspricht dem [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2340.
*  'FORCE_LEGACY_CARDINALITY_ESTIMATION'  
 Zwingt den Abfrageoptimierer, das Modell [Kardinalitätsschätzung](../../relational-databases/performance/cardinality-estimation-sql-server.md) von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und Vorgängerversionen zu verwenden. Dies entspricht dem [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 oder der Einstellung LEGACY_CARDINALITY_ESTIMATION=ON für die [datenbankweit gültige Konfiguration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
*  'ENABLE_QUERY_OPTIMIZER_HOTFIXES'  
 Aktiviert Hotfixes für den Abfrageoptimierer (Änderungen wurden in kumulativen Updates und Service Packs von SQL Server veröffentlicht). Dies entspricht dem [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4199 oder der Einstellung QUERY_OPTIMIZER_HOTFIXES=ON für die [Datenbankweit gültige Konfiguration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
*  'DISABLE_PARAMETER_SNIFFING'  
 Weist den Abfrageoptimierer an, bei der Kompilierung einer Abfrage mit mindestens einem Parameter eine durchschnittliche Datenverteilung zu verwenden. Dadurch ist der Abfrageplan unabhängig von dem Parameterwert, der bei der Kompilierung der Abfrage zuerst verwendet wurde. Dies entspricht dem [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4136 oder der Einstellung PARAMETER_SNIFFING=OFF für die [Datenbankweit gültige Konfiguration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
*  'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES'  
 Bewirkt, dass SQL Server bei der Schätzung einen Plan mit minimaler Selektivität verwendet UND Prädikate für Filter zur Berücksichtigung der Korrelation. Dies entspricht dem [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4137, wenn es mit dem Kardinalitätsschätzungsmodell von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und früheren Versionen verwendet wird, und hat ähnliche Auswirkungen, wenn das [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9471 mit dem Kardinalitätsschätzungsmodell von [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] oder einer neueren Version verwendet wird.
*  'DISABLE_OPTIMIZER_ROWGOAL'  
 Bewirkt, dass SQL Server einen Plan generiert, der keine Zeile-Ziel-Korrekturen mit Abfragen verwendet, welche die Schlüsselwörter TOP, OPTION (FAST N), IN oder EXISTS enthalten. Dies entspricht dem [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4138.
*  'ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'  
 Aktiviert automatisch generierte Schnellstatistiken (Histogrammzusatz) für alle führenden Indexspalten, für welche die Kardinalitätsschätzung erforderlich ist. Das für die Kardinalitätsschätzung verwendete Histogramm wird zum Zeitpunkt der Abfragekompilierung angepasst, damit der tatsächliche Höchst- und Mindestwert in dieser Spalte berücksichtigt werden. Dies entspricht dem [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4139. 
*  'ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS'  
 Bewirkt, dass SQL Server unter dem [Kardinalitätsschätzungsmodell](../../relational-databases/performance/cardinality-estimation-sql-server.md) für den Abfrageoptimierer von [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] oder einer neueren Version einen Abfrageplan mithilfe der Simple-Containment-Annahme statt mit der Base-Containment-Annahme generiert. Dies entspricht dem [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9476. 
*  'FORCE_DEFAULT_CARDINALITY_ESTIMATION'  
 Zwingt den Abfrageoptimierer, das [Kardinalitätsschätzungsmodell](../../relational-databases/performance/cardinality-estimation-sql-server.md) zu verwenden, das dem aktuellen Kompatibilitätsgrad der Datenbank entspricht. Verwenden Sie diesen Hinweis, um die Einstellung LEGACY_CARDINALITY_ESTIMATION=ON für die [Datenbankweit gültige Konfiguration](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) zu überschreiben, oder das [Ablaufverfolgungsflag](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481.
 
> [!TIP]
> Bei Hinweisnamen muss die Groß-/Kleinschreibung nicht beachtet werden.
  
  Die Liste aller unterstützten USE HINT-Namen kann über die dynamische Verwaltungsansicht [sys.dm_exec_valid_use_hints ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) abgefragt werden.
> [!IMPORTANT] 
> Einige USE HINT-Hinweise stehen möglicherweise mit Ablaufverfolgungsflags, die auf globaler Ebene oder auf Sitzungsebene aktiviert sind, oder mit Einstellungen für die datenbankweit gültige Konfiguration in Konflikt. In diesem Fall hat der Hinweis auf Abfrageebene (USE HINT) immer Vorrang. Wenn ein USE HINT-Hinweis mit einem anderen Abfragehinweis oder einem auf Abfrageebene aktivierten Ablaufverfolgungsflag (z.B. QUERYTRACEON) in Konflikt steht, generiert SQL Server beim Versuch der Abfrageausführung einen Fehler. 

 USE PLAN N**'***xml_plan***'**  
 Zwingt den Abfrageoptimierer, einen vorhandenen Abfrageplan für eine Abfrage zu verwenden, die mit **'***xml_plan***'** angegeben wird. USE PLAN kann nicht für die Anweisungen INSERT, UPDATE, MERGE oder DELETE angegeben werden.  
  
TABLE HINT **(***exposed_object_name* [ **,** \<table_hint> [ [**,** ]...*n* ] ] **)** Wendet den angegebenen Tabellenhinweis auf die Tabelle oder die Ansicht an, die *exposed_object_name* entspricht. Es wird empfohlen, einen Tabellenhinweis nur im Kontext einer [Planhinweisliste](../../relational-databases/performance/plan-guides.md) als Abfragehinweis zu verwenden.  
  
 *exposed_object_name* kann einer der folgenden Verweise sein:  
  
-   Wenn für die Tabelle oder die Ansicht in der [FROM](../../t-sql/queries/from-transact-sql.md)-Klausel der Abfrage ein Alias verwendet wird, ist *exposed_object_name* der Alias.  
  
-   Wenn kein Alias verwendet wird, entspricht *exposed_object_name* genau der Tabelle oder der Ansicht, auf die in der FROM-Klausel verwiesen wird. Wenn z.B. mit einem zweiteiligen Namen auf die Tabelle oder die Ansicht verwiesen wird, ist *exposed_object_name* der gleiche zweiteilige Name.  
  
 Wenn *exposed_object_name* angegeben wird, ohne dass auch ein Tabellenhinweis angegeben wird, werden alle in der Abfrage als Teil eines Tabellenhinweises für das Objekt festgelegten Indizes ignoriert, und die Indexverwendung wird vom Abfrageoptimierer bestimmt. Sie können diese Vorgehensweise verwenden, um die Auswirkung eines INDEX-Tabellenhinweises zu eliminieren, wenn Sie die ursprüngliche Abfrage nicht ändern können. Siehe Beispiel J.  
  
**\<table_hint> ::=** { [ NOEXPAND ] { INDEX ( *index_value* [ ,...*n* ] ) | INDEX = ( *index_value* ) | FORCESEEK [**(***index_value***(***index_column_name* [**,**... ] **))** ]| FORCESCAN | HOLDLOCK | NOLOCK | NOWAIT | PAGLOCK | READCOMMITTED | READCOMMITTEDLOCK | READPAST | READUNCOMMITTED | REPEATABLEREAD | ROWLOCK | SERIALIZABLE | SNAPSHOT | SPATIAL_WINDOW_MAX_CELLS | TABLOCK | TABLOCKX | UPDLOCK | XLOCK } Ist der Tabellenhinweis, der auf die Tabelle oder die Ansicht angewendet wird, die *exposed_object_name* als Abfragehinweis entspricht. Eine Beschreibung dieser Hinweise finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Andere Tabellenhinweise als INDEX, FORCESCAN und FORCESEEK sind als Abfragehinweise nicht zulässig, es sei denn, die Abfrage enthält bereits eine WITH-Klausel, die einen Tabellenhinweis angibt. Weitere Informationen finden Sie in den Hinweisen.  
  
> [!CAUTION] 
> Bei Angabe von FORCESEEK mit Parametern wird die Anzahl von Plänen, die vom Optimierer berücksichtigt werden können, stärker eingeschränkt als bei Angabe von FORCESEEK ohne Parameter. Dies kann in mehreren Fällen zu dem Fehler führen, dass der Plan nicht generiert werden kann. In zukünftigen Versionen können durch interne Änderungen des Optimierers möglicherweise mehr Pläne berücksichtigt werden.  
  
## <a name="remarks"></a>Remarks  
 Abfragehinweise können nur dann in einer INSERT-Anweisung angegeben werden, wenn eine SELECT-Klausel innerhalb der Anweisung verwendet wird.  
  
 Abfragehinweise können nur in der Abfrage der obersten Ebene angegeben werden, nicht in Unterabfragen. Wenn ein Tabellenhinweis als Abfragehinweis angegeben ist, kann der Hinweis in der Abfrage der obersten Ebene oder in einer Unterabfrage angegeben werden. Der für *exposed_object_name* in der TABLE HINT-Klausel angegebene Wert muss jedoch genau dem verfügbar gemachten Namen in der Abfrage oder Unterabfrage entsprechen.  
  
## <a name="specifying-table-hints-as-query-hints"></a>Angeben von Tabellenhinweisen als Abfragehinweise  
 Es wird empfohlen, den INDEX-, FORCESCAN- oder FORCESEEK-Tabellenhinweis nur im Zusammenhang mit einer [Planhinweisliste](../../relational-databases/performance/plan-guides.md) als Abfragehinweis zu verwenden. Planhinweislisten sind nützlich, wenn Sie die ursprüngliche Abfrage nicht ändern können, beispielsweise bei Anwendungen von Drittanbietern. Der in der Planhinweisliste angegebene Abfragehinweis wird vor dem Kompilieren und Optimieren zur Abfrage hinzugefügt. Verwenden Sie für Ad-hoc-Abfragen die TABLE HINT-Klausel nur dann, wenn Sie Planhinweislisten-Anweisungen testen. Es wird empfohlen, für alle anderen Ad-hoc-Abfragen diese Hinweise nur als Tabellenhinweise anzugeben.  
  
 Wenn die INDEX-, FORCESCAN- und FORCESEEK-Tabellenhinweise als Abfragehinweise angegeben werden, sind sie für die folgenden Objekte gültig:  
  
-   Tabellen  
  
-   Sichten  
  
-   Indizierte Sichten  
  
-   Allgemeine Tabellenausdrücke (Der Hinweis muss in der SELECT-Anweisung angegeben sein, mit deren Resultset der allgemeine Tabellenausdruck aufgefüllt wird.)  
  
-   Dynamische Verwaltungssichten  
  
-   Benannte Unterabfragen  
  
 Die INDEX-, FORCESCAN- und FORCESEEK-Tabellenhinweis können als Abfragehinweise für eine Abfrage angegeben werden, die nicht über vorhandene Tabellenhinweise verfügt, oder sie können verwendet werden, um vorhandene INDEX-, FORCESCAN- oder FORCESEEK-Hinweise in der Abfrage zu ersetzen. Andere Tabellenhinweise als INDEX, FORCESCAN und FORCESEEK sind als Abfragehinweise nicht zulässig, es sei denn, die Abfrage enthält bereits eine WITH-Klausel, die einen Tabellenhinweis angibt. In diesem Fall muss, um die Semantik der Abfrage beizubehalten, mithilfe von TABLE HINT in der OPTION-Klausel auch ein übereinstimmender Hinweis als Abfragehinweis angegeben werden. Wenn die Abfrage beispielsweise den Tabellenhinweis NOLOCK enthält, muss die OPTION-Klausel im **@hints**-Parameter der Planhinweisliste ebenfalls den NOLOCK-Hinweis enthalten. Siehe Beispiel K. Wenn ein anderer Tabellenhinweis als INDEX, FORCESCAN oder FORCESEEK mithilfe von TABLE HINT in der OPTION-Klausel ohne übereinstimmenden Abfragehinweis angegeben wurde (oder umgekehrt), wird der Fehler 8702 ausgelöst (als Hinweis darauf, dass die OPTION-Klausel bewirken kann, dass sich die Semantik der Abfrage ändert), und die Abfrage schlägt fehl.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-merge-join"></a>A. Verwenden von MERGE JOIN  
 Im folgenden Beispiel wird der JOIN-Vorgang in der Abfrage durch einen MERGE JOIN ausgeführt. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>B. Verwenden von OPTIMIZE FOR  
 Im folgenden Beispiel wird der Abfrageoptimierer angewiesen, den Wert `'Seattle'` für die lokale Variable `@city_name` zu verwenden, und statistische Daten zu verwenden, um während der Abfrageoptimierung den Wert der lokalen Variablen `@postal_code` zu bestimmen. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
DECLARE @city_name nvarchar(30);  
DECLARE @postal_code nvarchar(15);  
SET @city_name = 'Ascheim';  
SET @postal_code = 86171;  
SELECT * FROM Person.Address  
WHERE City = @city_name AND PostalCode = @postal_code  
OPTION ( OPTIMIZE FOR (@city_name = 'Seattle', @postal_code UNKNOWN) );  
GO  
```  
  
### <a name="c-using-maxrecursion"></a>C. Verwenden von MAXRECURSION  
 MAXRECURSION kann verwendet werden, um zu verhindern, dass ein fehlerhaft formatierter allgemeiner Tabellenausdruck in eine Endlosschleife gerät. Im folgenden Beispiel wird absichtlich eine Endlosschleife erstellt. Zudem wird der MAXRECURSION-Hinweis verwendet, um die Anzahl der Rekursionsebenen auf zwei zu begrenzen. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```sql  
--Creates an infinite loop  
WITH cte (CustomerID, PersonID, StoreID) AS  
(  
    SELECT CustomerID, PersonID, StoreID  
    FROM Sales.Customer  
    WHERE PersonID IS NOT NULL  
  UNION ALL  
    SELECT cte.CustomerID, cte.PersonID, cte.StoreID  
    FROM cte   
    JOIN  Sales.Customer AS e   
        ON cte.PersonID = e.CustomerID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT CustomerID, PersonID, StoreID  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 Sobald der Fehler im Code behoben wurde, wird MAXRECURSION nicht mehr benötigt.  
  
### <a name="d-using-merge-union"></a>D. Verwenden von MERGE UNION  
 Im folgenden Beispiel wird der MERGE UNION-Abfragehinweis verwendet. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>E. Verwenden von HASH GROUP und FAST  
 Im folgenden Beispiel werden der MERGE UNION- und der FAST-Abfragehinweis verwendet. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>F. Verwenden von MAXDOP  
 Im folgenden Beispiel wird der MAXDOP-Abfragehinweis verwendet. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (MAXDOP 2);    
GO
```  
  
### <a name="g-using-index"></a>G. Verwenden von INDEX  
 In den folgenden Beispielen wird der INDEX-Hinweis verwendet. Im ersten Beispiel wird ein einzelner Index angegeben. Im zweiten Beispiel werden mehrere Indizes für einen einzelnen Tabellenverweis angegeben. Da der INDEX-Hinweis auf eine Tabelle angewendet wird, die einen Alias verwendet, muss in beiden Beispielen in der TABLE HINT-Klausel auch der gleiche Alias wie der verfügbare Objektname angegeben werden. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX (IX_Employee_ManagerID)))';  
GO  
EXEC sp_create_plan_guide   
    @name = N'Guide2',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX(PK_Employee_EmployeeID, IX_Employee_ManagerID)))';  
GO    
```  
  
### <a name="h-using-forceseek"></a>H. Verwenden von FORCESEEK  
 Im folgenden Beispiel wird der FORCESEEK-Tabellenhinweis verwendet. Da der INDEX-Hinweis auf eine Tabelle angewendet wird, die einen zweiteiligen Namen verwendet, muss in der TABLE HINT-Klausel auch der gleiche zweiteilige Name wie der verfügbare Objektname angegeben werden. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide3',   
    @stmt = N'SELECT c.LastName, c.FirstName, HumanResources.Employee.Title  
              FROM HumanResources.Employee  
              JOIN Person.Contact AS c ON HumanResources.Employee.ContactID = c.ContactID  
              WHERE HumanResources.Employee.ManagerID = 3  
              ORDER BY c.LastName, c.FirstName;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT( HumanResources.Employee, FORCESEEK))';  
GO    
```  
  
### <a name="i-using-multiple-table-hints"></a>I. Verwenden von mehreren Tabellenhinweisen  
 Im folgenden Beispiel wird der INDEX-Hinweis auf eine Tabelle angewendet, und der FORCESEEK-Hinweis wird auf eine andere Tabelle angewendet. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide4',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX( IX_Employee_ManagerID))   
                       , TABLE HINT (c, FORCESEEK))';  
GO  
```  
  
### <a name="j-using-table-hint-to-override-an-existing-table-hint"></a>J. Verwenden von TABLE HINT zum Überschreiben eines vorhandenen Tabellenhinweises  
 Das folgende Beispiel zeigt, wie der TABLE HINT-Hinweis ohne Angabe eines Hinweises verwendet wird, um das Verhalten des INDEX-Tabellenhinweises zu überschreiben, der in der FROM-Klausel der Abfrage angegeben ist. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide5',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e WITH (INDEX (IX_Employee_ManagerID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e))';  
GO    
```  
  
### <a name="k-specifying-semantics-affecting-table-hints"></a>K. Angeben von Tabellenhinweisen, die die Semantik beeinflussen  
 Das folgende Beispiel enthält in der Abfrage zwei Tabellenhinweise: den NOLOCK-Hinweis, der die Semantik beeinflusst, und den INDEX-Hinweis, der die Semantik nicht beeinflusst. Der NOLOCK-Hinweis wird in der OPTIONS-Klausel der Planhinweisliste angegeben, um die Semantik der Abfrage beizubehalten. Neben dem NOLOCK-Hinweis werden auch der INDEX-Hinweis und der FORCESEEK-Hinweis angegeben, die den die Semantik nicht beeinflussenden INDEX-Hinweis in der Abfrage ersetzen, wenn die Anweisung kompiliert und optimiert wird. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide6',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX(IX_Employee_ManagerID), NOLOCK, FORCESEEK))';  
GO    
```  
  
 Das folgende Beispiel zeigt eine alternative Methode, um die Semantik der Abfrage beizubehalten und zuzulassen, dass der Abfrageoptimierer einen anderen als den im Tabellenhinweis angegebenen Index verwendet. Dies erfolgt durch Angabe des NOLOCK-Hinweises in der OPTIONS-Klausel (da dieser die Semantik beeinflusst) und durch Angabe des TABLE HINT-Schlüsselworts nur mit einem Tabellenverweis und ohne INDEX-Hinweis. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide7',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, NOLOCK))';  
GO  
```  
### <a name="l-using-use-hint"></a>L. Verwenden von USE HINT  
 Im folgenden Beispiel werden der RECOMPILE- und der USE HINT-Abfragehinweis verwendet. Im Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [Ablaufverfolgungsflags](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
