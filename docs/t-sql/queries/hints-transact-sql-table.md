---
title: Tabellenhinweise (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TABLE_HINT_TSQL
- Table Hint
dev_langs:
- TSQL
helpviewer_keywords:
- SERIALIZABLE table hint
- UPDLOCK table hint
- HOLDLOCK table hint
- TABLOCKX table hint
- READUNCOMMITTED table hint
- hints [SQL Server], tables
- READCOMMITTEDLOCK table hint
- FORCESCAN table hint
- ROWLOCK table hint
- XLOCK table hint
- NOLOCK table hint
- READPAST table hint
- NOWAIT table hint
- FORCESEEK table hint
- table hints [SQL Server]
- TABLOCK table hint
- REPEATABLEREAD table hint
- READ COMMITTED table hint
- NOEXPAND table hint
- PAGLOCK table hint
ms.assetid: 8bf1316f-c0ef-49d0-90a7-3946bc8e7a89
caps.latest.revision: 174
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 036b2c26536aaa1257bfbb41075d570149b04e54
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="hints-transact-sql---table"></a>Hinweise (Transact-SQL): Tabelle
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Tabellenhinweise überschreiben das Standardverhalten des Abfrageoptimierers für die Dauer der DML-Anweisung (Data Manipulation Language, Datenbearbeitungssprache) durch Angabe einer Sperrmethode, eines Index oder mehrerer Indizes, eines Abfrageverarbeitungsvorgangs, beispielsweise einen Tabellenscan oder eine Indexsuche, oder anderer Optionen. Tabellenhinweise werden in der FROM-Klausel der DML-Anweisung angegeben und wirken sich nur auf die Tabelle oder Sicht aus, auf die in der betreffenden Klausel verwiesen wird.  
  
> [!CAUTION]  
>  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer in der Regel den optimalen Ausführungsplan für eine Abfrage auswählt, wird empfohlen, dass erfahrene Entwickler und Datenbankadministratoren Hinweise nur dann verwenden, wenn alle anderen Möglichkeiten sich als unzureichend erwiesen haben.  
  
 **Gilt für:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WITH  ( <table_hint> [ [, ]...n ] )  
  
<table_hint> ::=   
[ NOEXPAND ] {   
    INDEX  ( index_value [ ,...n ] )   
  | INDEX =  ( index_value )      
  | FORCESEEK [( index_value ( index_column_name  [ ,... ] ) ) ]  
  | FORCESCAN  
  | FORCESEEK  
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
  
<table_hint_limited> ::=  
{  
    KEEPIDENTITY   
  | KEEPDEFAULTS   
  | HOLDLOCK   
  | IGNORE_CONSTRAINTS   
  | IGNORE_TRIGGERS   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
```  
  
## <a name="arguments"></a>Argumente  
 WITH **(** \<<table_hint>**)** [ [**,** ]...*n* ]  
 Bis auf einige Ausnahmen werden Tabellenhinweise nur dann in der FROM-Klausel unterstützt, wenn die Hinweise mit dem WITH-Schlüsselwort angegeben werden. Tabellenhinweise müssen zudem mit Klammern angegeben werden.  
  
> [!IMPORTANT]  
>  Das WITH-Schlüsselwort wegzulassen ist eine veraltete Funktion: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Die folgenden Tabellentipps sind mit und ohne WITH-Schlüsselwort zulässig: NOLOCK, READUNCOMMITTED, UPDLOCK, REPEATABLEREAD, SERIALIZABLE, READCOMMITTED, TABLOCK, TABLOCKX, PAGLOCK, ROWLOCK, NOWAIT, READPAST, XLOCK, SNAPSHOT und NOEXPAND. Wenn diese Tabellenhinweise ohne das WITH-Schlüsselwort angegeben werden, sollten die Hinweise allein angegeben werden. Zum Beispiel:  
  
```sql  
FROM t (TABLOCK)  
```  
  
 Wenn der Hinweis mit einer anderen Option angegeben wird, muss er mit dem WITH-Schlüsselwort angegeben werden:  
  
```sql  
FROM t WITH (TABLOCK, INDEX(myindex))  
```  
  
 Es wird empfohlen, Tabellenhinweise durch Kommas voneinander zu trennen.  
  
> [!IMPORTANT]  
>  Hinweise statt durch Kommas durch Leerzeichen zu trennen ist eine veraltete Funktion: [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 NOEXPAND  
 Gibt an, dass indizierte Sichten nicht für den Zugriff auf zugrunde liegende Tabellen erweitert werden, wenn der Abfrageoptimierer die Abfrage verarbeitet. Der Abfrageoptimierer behandelt die Sicht wie eine Tabelle mit einem gruppierten Index. NOEXPAND gilt nur für indizierte Sichten. Weitere Informationen finden Sie in den Hinweisen.  
  
 INDEX **(***index_value* [**,**... *n* ] ) | INDEX =  ( *index_value***)**  
 Mit der INDEX()-Syntax werden die Namen oder IDs der Indizes angegeben, die der Abfrageoptimierer beim Verarbeiten der Anweisung verwenden soll. Die alternative INDEX = Syntax gibt einen einzigen Indexwert an. Pro Tabelle ist nur ein Indexhinweis zulässig.  
  
 Falls ein gruppierter Index vorhanden ist, erzwingt INDEX(0) einen Scan des gruppierten Index, und INDEX(1) erzwingt einen Scan des gruppierten Index oder eine Suche im gruppierten Index. Falls kein gruppierter Index vorhanden ist, erzwingt INDEX(0) einen Tabellenscan, und INDEX(1) wird als Fehler interpretiert.  
  
 Werden mehrere Indizes in einer einzigen Hinweisliste verwendet, werden Duplikate ignoriert, und die übrigen aufgeführten Indizes werden verwendet, um die Zeilen aus der Tabelle abzurufen. Die Reihenfolge der Indizes im Indexhinweis ist von Bedeutung. Mehrere Indexhinweise erzwingen die AND-Verknüpfung der Indizes, und der Abfrageoptimierer versucht, so viele Bedingungen wie möglich auf jeden verwendeten Index anzuwenden. Falls die Auflistung der Indexhinweise nicht alle in der Abfrage referenzierten Spalten umfasst, wird ein Abrufvorgang ausgeführt, um die restlichen Spalten abzurufen, nachdem [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] alle indizierten Spalten abgerufen hat.  
  
> [!NOTE]  
>  Wenn ein Indexhinweis, der auf mehrere Indizes verweist, in der Faktentabelle eines Sternjoins verwendet wird, ignoriert der Optimierer den Indexhinweis und gibt eine Warnmeldung zurück. Außerdem ist die OR-verknüpfte Indexsuche für Tabellen mit einem Indexhinweis nicht zulässig.  
  
 Die maximale Anzahl nicht gruppierter Indizes im Tabellenhinweis beträgt 250.  
  
 KEEPIDENTITY  
 Gilt nur in einer INSERT-Anweisung, wenn die BULK-Option mit [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) verwendet wird.  
  
 Gibt an, dass der oder die Identitätswerte in der importierten Datendatei für die Identitätsspalte verwendet werden sollen. Wird KEEPIDENTITY nicht angegeben, werden die Identitätswerte für diese Spalte zwar überprüft, nicht jedoch importiert, und der Abfrageoptimierer weist auf der Grundlage von Ausgangswerten und den inkrementellen Werten, die beim Erstellen der Tabelle angegeben wurden, eindeutige Werte zu.  
  
> [!IMPORTANT]  
>  Wenn die Datendatei keine Werte für die Identitätsspalte in der Tabelle oder Sicht enthält und die Identitätsspalte nicht die letzte Spalte der Tabelle ist, müssen Sie die Identitätsspalte überspringen. Weitere Informationen finden Sie unter [Auslassen eines Datenfelds mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md). Wenn eine Identitätsspalte erfolgreich übersprungen wird, weist der Abfrageoptimierer der Identitätsspalte in den importierten Tabellenzeilen automatisch eindeutige Werte zu.  
  
 Ein Beispiel für die Verwendung dieses Hinweises in einer INSERT ... SELECT * FROM OPENROWSET(BULK...)-Anweisung finden Sie unter [Beibehalten von Identitätswerten beim Massenimport von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
 Weitere Informationen zum Überprüfen des Identitätswerts für eine Tabelle finden Sie unter [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 KEEPDEFAULTS  
 Gilt nur in einer INSERT-Anweisung, wenn die BULK-Option mit [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) verwendet wird.  
  
 Gibt an, dass statt NULL der Standardwert einer Tabellenspalte (falls vorhanden) einzufügen ist, wenn der Datensatz keinen Wert für die Spalte aufweist.  
  
 Ein Beispiel für die Verwendung dieses Hinweises in einer INSERT ... SELECT * FROM OPENROWSET(BULK...)-Anweisung finden Sie unter [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 FORCESEEK [ **(***index_value***(***index_column_name* [ **,**... *n* ] **))** ]  
 Gibt an, dass der Abfrageoptimierer nur einen Indexsuchvorgang als Zugriffspfad auf die in der Tabelle oder Sicht angegebenen Daten verwenden darf. Ab SQL Server 2008 R2 SP1 können auch Indexparameter angegeben werden. Der Abfrageoptimierer berücksichtigt in diesem Fall nur Indexsuchvorgänge über den angegebenen Index mit mindestens den angegebenen Indexspalten.  
  
 *index_value*  
 Dies ist der Indexname oder der ID-Wert des Indexes. Die Index-ID 0 (Heap) kann nicht angegeben werden. Wenn der Indexname oder die ID zurückgegeben werden soll, fragen Sie die **sys.indexes**-Katalogsicht ab.  
  
 *index_column_name*  
 Dies ist der Name der Indexspalte, die in den Suchvorgang einbezogen werden soll. Die Angabe von FORCESEEK mit Indexparametern ähnelt der Verwendung von FORCESEEK mit einem INDEX-Hinweis. Sie können jedoch eine genauere Steuerung des vom Abfrageoptimierer verwendeten Zugriffspfads erreichen, indem Sie den Index, in dem die Suche stattfinden soll, und außerdem die Indexspalten angeben, die im Suchvorgang berücksichtigt werden sollen. Der Optimierer kann bei Bedarf zusätzliche Spalten einbeziehen. Wenn beispielsweise ein nicht gruppierter Index angegeben wird, kann der Optimierer neben den angegebenen Spalten auch die Schlüsselspalten gruppierter Indizes verwenden.  
  
 Der FORCESEEK-Hinweis kann folgendermaßen angegeben werden:  
  
|Syntax|Beispiel|Description|  
|------------|-------------|-----------------|  
|Ohne Index oder INDEX-Hinweis|`FROM dbo.MyTable WITH (FORCESEEK)`|Der Abfrageoptimierer berücksichtigt nur Indexsuchvorgänge für den Zugriff auf die Tabelle oder Sicht über einen beliebigen relevanten Index.|  
|Mit einem INDEX-Hinweis kombiniert|`FROM dbo.MyTable WITH (FORCESEEK, INDEX (MyIndex))`|Der Abfrageoptimierer berücksichtigt nur Indexsuchvorgänge für den Zugriff auf die Tabelle oder Sicht über den angegebenen Index.|  
|Durch Angabe eines Index und von Indexspalten parametrisiert|`FROM dbo.MyTable WITH (FORCESEEK (MyIndex (col1, col2, col3)))`|Der Abfrageoptimierer berücksichtigt nur Indexsuchvorgänge für den Zugriff auf die Tabelle oder Sicht über den angegebenen Index mit mindestens den angegebenen Indexspalten.|  
  
Beachten Sie bei Verwendung des FORCESEEK-Hinweises (mit oder ohne Parameter) die folgenden Richtlinien:  
  
-   Der Hinweis kann als Tabellenhinweis oder Abfragehinweis angegeben werden. Weitere Informationen zu Abfragehinweisen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
-   Zum Anwenden von FORCESEEK auf eine indizierte Sicht muss auch der NOEXPAND-Hinweis angegeben werden.  
  
-   Der Hinweis kann höchstens einmal pro Tabelle oder Sicht angewendet werden.  
  
-   Der Hinweis kann nicht für eine Remotedatenquelle angegeben werden. Fehler 7377 wird zurückgegeben, wenn FORCESEEK mit einem Indexhinweis angegeben wird, Fehler 8180 wird zurückgegeben, wenn FORCESEEK ohne Indexhinweis angegeben wird.  
  
-   Wenn die Verwendung von FORCESEEK bewirkt, dass kein Plan gefunden wird, dann wird der Fehler 8622 zurückgegeben.  
  
Bei Angabe von FORCESEEK mit Indexparametern gelten die folgenden Richtlinien und Einschränkungen:  
  
-   Der Hinweis kann nicht für Tabellen angegeben werden, die Ziel einer INSERT-, UPDATE- oder DELETE-Anweisung sind.  
  
-   Der Hinweis kann nicht zusammen mit einem INDEX-Hinweis oder einem anderen FORCESEEK-Hinweis angegeben werden.  
  
-   Mindestens eine Spalte muss angegeben werden, bei der es sich um die führende Schlüsselspalte handeln muss.  
  
-   Zusätzliche Indexspalten können angegeben, Schlüsselspalte jedoch nicht übersprungen werden. Wenn der angegebene Index beispielsweise die Schlüsselspalten `a`, `b` und `c` enthält, sind `FORCESEEK (MyIndex (a))` und `FORCESEEK (MyIndex (a, b)` als Syntax gültig. Ungültige Syntax wäre `FORCESEEK (MyIndex (c))` und `FORCESEEK (MyIndex (a, c)`.  
  
-   Die Reihenfolge der im Hinweis angegebenen Spaltennamen muss der Reihenfolge der Spalten im referenzierten Index entsprechen.  
  
-   Spalten, die nicht in der Indexschlüsseldefinition vorhanden sind, können nicht angegeben werden. Beispielsweise können in einem nicht gruppierten Index nur die definierten Indexschlüsselspalten angegeben werden. Gruppierte Schlüsselspalten, die automatisch in den Index einbezogen werden, können nicht angegeben, aber vom Optimierer verwendet werden.  
  
-   Ein speicheroptimierter xVelocity-columnstore-Index kann nicht als Indexparameter angegeben werden. Fehler 366 wird zurückgegeben.  
  
-   Nach einer Änderungen der Indexdefinition (z. B. durch Hinzufügen oder Entfernen von Spalten) können Änderungen an den Abfragen erforderlich sein, die auf den betreffenden Index verweisen.  
  
-   Der Hinweis verhindert, dass der Optimierer räumliche oder XML-Indizes für die Tabelle berücksichtigt.  
  
-   Der Hinweis kann nicht zusammen mit dem FORCESCAN-Hinweis angegeben werden.  
  
-   Bei partitionierten Indizes kann die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implizit hinzugefügte Partitionierungsspalte nicht im FORCESEEK-Hinweise angegeben werden.  
  
> [!CAUTION]  
>  Bei Angabe von FORCESEEK mit Parametern wird die Anzahl von Plänen, die vom Optimierer berücksichtigt werden können, stärker eingeschränkt als bei Angabe von FORCESEEK ohne Parameter. Dies kann in mehreren Fällen zu dem Fehler führen, dass der Plan nicht generiert werden kann. In zukünftigen Versionen können durch interne Änderungen des Optimierers möglicherweise mehr Pläne berücksichtigt werden.  
  
 FORCESCAN  
 Dieser Hinweis wurde in SQL Server 2008 R2 SP1 eingeführt und gibt an, dass der Abfrageoptimierer nur einen Indexscanvorgang als Zugriffspfad für die Tabelle oder Sicht verwenden kann, auf die verweisen wird. Der FORCESCAN-Hinweis kann bei Abfragen nützlich sein, in denen der Optimierer die Anzahl betroffener Zeilen unterschätzt und einen Such- statt eines Scanvorgangs auswählt. In diesem Fall ist der für den Vorgang bereitgestellte Arbeitsspeicher zu klein, was sich negativ auf die Abfrageleistung auswirkt.  
  
 FORCESCAN kann mit oder ohne INDEX-Hinweis angegeben werden. Bei Kombination mit einem Indexhinweis (`INDEX = index_name, FORCESCAN`) berücksichtigt der Abfrageoptimierer beim Zugriff auf die Tabelle, auf die verwiesen wird, nur Scanzugriffspfade über den angegebenen Index. FORCESCAN kann mit dem Indexhinweis INDEX(0) angegeben werden, um einen Tabellenscanvorgang für die Basistabelle zu erzwingen.  
  
 Bei partitionierten Tabellen und Indizes wird FORCESCAN angewendet, nachdem Partitionen durch Abfrageprädikatauswertung gelöscht wurden. Dies bedeutet, dass der Scan nur auf die verbleibenden Partitionen und nicht auf die gesamte Tabelle angewendet wird.  
  
 Der FORCESCAN-Hinweis unterliegt folgenden Einschränkungen:  
  
-   Der Hinweis kann nicht für Tabellen angegeben werden, die Ziel einer INSERT-, UPDATE- oder DELETE-Anweisung sind.  
  
-   Der Hinweis kann nicht mit mehr als einem Indexhinweis verwendet werden.  
  
-   Der Hinweis verhindert, dass der Optimierer räumliche oder XML-Indizes für die Tabelle berücksichtigt.  
  
-   Der Hinweis kann nicht für eine Remotedatenquelle angegeben werden.  
  
-   Der Hinweis kann nicht zusammen mit dem FORCESEEK-Hinweis angegeben werden.  
  
 HOLDLOCK  
 Entspricht der Option SERIALIZABLE. Weitere Informationen finden Sie unter SERIALIZABLE weiter unten in diesem Thema. HOLDLOCK gilt nur für die Tabelle oder Sicht, für die sie angegeben wurde, und nur für die Dauer der Transaktion, die in der Anweisung definiert ist, in der auch HOLDLOCK verwendet wird. HOLDLOCK kann in einer SELECT-Anweisung mit der Option FOR BROWSE nicht verwendet werden.  
  
 IGNORE_CONSTRAINTS  
 Gilt nur in einer INSERT-Anweisung, wenn die BULK-Option mit [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) verwendet wird.  
  
 Gibt an, dass alle für die Tabelle geltenden Einschränkungen vom Massenimportvorgang ignoriert werden. Standardmäßig überprüft INSERT [UNIQUE- und CHECK-Einschränkungen](../../relational-databases/tables/unique-constraints-and-check-constraints.md) und [Primärschlüssel- und Fremdschlüsseleinschränkungen](../../relational-databases/tables/primary-and-foreign-key-constraints.md). Wenn für einen Massenimportvorgang IGNORE_CONSTRAINTS angegeben ist, müssen diese Einschränkungen für eine Zieltabelle von INSERT ignoriert werden. Beachten Sie, dass Sie die Einschränkungen UNIQUE, PRIMARY KEY oder NOT NULL nicht deaktivieren können.  
  
 Sie sollten die Einschränkungen CHECK und FOREIGN KEY z. B. deaktivieren, wenn die Eingabedaten Zeilen enthalten, die Einschränkungen verletzen. Durch das Deaktivieren der Einschränkungen CHECK und FOREIGN KEY können Sie die Daten importieren und dann [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen zum Bereinigen (Cleanup) der Daten verwenden.  
  
 Wenn die CHECK-Einschränkung und die FOREIGN KEY-Einschränkung ignoriert werden, wird jede ignorierte Einschränkung der Tabelle nach dem Vorgang jedoch in der Katalogsicht [sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) oder [sys.foreign_keys](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md) als **is_not_trusted** gekennzeichnet. Irgendwann wird es sinnvoll sein, die Einschränkungen für die gesamte Tabelle zu überprüfen. Wenn die Tabelle vor dem Massenimportvorgang nicht leer war, kann der Aufwand einer erneuten Überprüfung der Einschränkung höher sein als das Anwenden der Einschränkungen CHECK und FOREIGN KEY auf die inkrementellen Daten.  
  
 IGNORE_TRIGGERS  
 Gilt nur in einer INSERT-Anweisung, wenn die BULK-Option mit [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) verwendet wird.  
  
 Gibt an, dass alle für die Tabelle definierten Trigger vom Massenimportvorgang ignoriert werden. Standardmäßig werden Trigger von INSERT angewendet.  
  
 Verwenden Sie IGNORE_TRIGGERS nur, wenn Ihre Anwendung von keinen Triggern abhängig ist und Leistungsmaximierung ein wichtiger Faktor ist.  
  
 NOLOCK  
 Entspricht der Option READUNCOMMITTED. Weitere Informationen finden Sie unter READUNCOMMITTED weiter unten in diesem Thema.  
  
> [!NOTE]  
>  Für UPDATE- oder DELETE-Anweisungen: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 NOWAIT  
 IWeist die [!INCLUDE[ssDE](../../includes/ssde-md.md)] an, eine Nachricht zurückzugeben, sobald eine Sperre für die Tabelle angetroffen wird. NOWAIT entspricht der Angabe von SET LOCK_TIMEOUT 0 für eine bestimmte Tabelle. Der NOWAIT-Hinweis funktioniert nicht, wenn der TABLOCK-Hinweis ebenfalls enthalten ist. Um eine Abfrage bei Verwendung des TABLOCK-Hinweises ohne Wartezeit zu beenden, stellen Sie der Abfrage stattdessen `SETLOCK_TIMEOUT 0;` voran.  
  
 PAGLOCK  
 Setzt Seitensperren entweder in solchen Fällen ein, in denen normalerweise einzelne Sperren für Zeilen oder Schlüssel gesetzt werden, oder in Fällen, in denen normalerweise eine einzelne Tabelle gesperrt wird. Verwendet standardmäßig den für den Vorgang geeigneten Sperrmodus. Wird das Argument in Transaktionen angegeben, die auf der SNAPSHOT-Isolationsstufe ausgeführt werden, werden Seitensperren nur dann verwendet, wenn PAGLOCK mit anderen Tabellenhinweisen kombiniert ist, die Sperren erfordern, wie beispielsweise UPDLOCK und HOLDLOCK.  
  
 READCOMMITTED  
 Gibt an, dass Lesevorgänge den Regeln für die Isolationsstufe READ COMMITTED entsprechen, indem entweder Sperren gesetzt werden oder die Zeilenversionsverwaltung verwendet wird. Wenn die Datenbankoption READ_COMMITTED_SNAPSHOT auf OFF festgelegt wurde, fordert die [!INCLUDE[ssDE](../../includes/ssde-md.md)] beim Lesen der Daten freigegebene Sperren an und hebt diese Sperren nach Abschluss des Lesevorgangs wieder auf. Wenn die Datenbankoption READ_COMMITTED_SNAPSHOT auf ON festgelegt wurde, fordert die [!INCLUDE[ssDE](../../includes/ssde-md.md)] keine Sperren an und verwendet die Zeilenversionsverwaltung. Weitere Informationen zu Isolationsstufen in SQL Server finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
> [!NOTE]  
>  Für UPDATE- oder DELETE-Anweisungen: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 READCOMMITTEDLOCK  
 Gibt an, dass Lesevorgänge den Regeln für die Isolationsstufe READ COMMITTED entsprechen, indem Sperren verwendet werden. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] fordert beim Lesen der Daten freigegebene Sperren an und hebt diese Sperren nach Abschluss des Lesevorgangs wieder auf. Dabei spielt es keine Rolle, welche Einstellung für die Datenbankoption READ_COMMITTED_SNAPSHOT gewählt wurde. Weitere Informationen zu Isolationsstufen in SQL Server finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Dieser Hinweis kann nicht für die Zieltabelle einer INSERT-Anweisung angegeben werden, in diesem Fall wird der Fehler 4140 zurückgegeben.  
  
 READPAST  
 Gibt an, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] keine Zeilen liest, die durch andere Transaktionen gesperrt wurden. Wenn READPAST angegeben ist, werden Sperren auf Zeilenebene übersprungen, Sperren auf Seitenebene allerdings nicht. Das bedeutet: anstatt die aktuelle Transaktion zu blockieren, überspringt das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Zeilen, bis die Sperren aufgehoben werden. Nehmen Sie z. B. an, die `T1`-Tabelle enthält eine Spalte mit einzelnen ganzen Zahlen und den Werten 1, 2, 3, 4, 5. Wenn Transaktion A die Werte 3 bis 8 ändert, jedoch noch kein Commit für sie ausgeführt wurde, ergibt SELECT * FROM T1 (READPAST) die Werte 1, 2, 4, 5. READPAST dient hauptsächlich der Reduzierung von Sperrkonflikten beim Implementieren einer Arbeitswarteschlange, die eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle verwendet. Ein Warteschlangenlesevorgang, der READPAST verwendet, lässt durch andere Transaktionen gesperrte Warteschlangeneinträge aus und liest den nächsten verfügbaren Warteschlangeneintrag, ohne warten zu müssen, bis andere Transaktionen ihre Sperren aufheben.  
  
 READPAST kann für jede Tabelle, auf die in einer UPDATE- oder DELETE-Anweisung verwiesen wird, und für jede Tabelle, auf die in einer FROM-Klausel verwiesen wird, angegeben werden. Wenn Sie den READPAST-Sperrhinweis in einer UPDATE-Anweisung angeben, wird er nur angewendet, wenn Daten gelesen werden, um die Datensätze zu identifizieren, die aktualisiert werden müssen; dabei spielt es keine Rolle, wo in der Anweisung READPAST angegeben wird. READPAST kann nicht für Tabellen in der INTO-Klausel einer INSERT-Anweisung angegeben werden. Aktualisierungs- oder Löschoperationen, die READPAST verwenden, können beim Lesen von Fremdschlüsseln oder indizierten Sichten oder beim Ändern sekundärer Indizes zu Blockierungen führen.  
  
 READPAST kann nur in Transaktionen angegeben werden, die mit den Isolationsstufen READ COMMITTED oder REPEATABLE READ arbeiten. Wird das Argument in Transaktionen angegeben, die auf der SNAPSHOT-Isolationsstufe ausgeführt werden, muss READPAST mit anderen Tabellenhinweisen kombiniert werden, die Sperren erfordern, wie beispielsweise UPDLOCK und HOLDLOCK.  
  
 Der READPAST-Tabellenhinweis kann nicht angegeben werden, wenn die READ_COMMITTED_SNAPSHOT-Datenbankoption auf ON festgelegt ist und eine der folgenden Bedingungen zutrifft.  
  
-   Die Transaktionsisolationsstufe der Sitzung ist READ COMMITTED.  
  
-   Der READCOMMITTED-Tabellenhinweis wird ebenfalls in der Abfrage angegeben.  
  
 Um den READPAST-Hinweis in diesen Fällen anzugeben, entfernen Sie den READCOMMITTED-Tabellenhinweis (sofern vorhanden), und nehmen Sie den READCOMMITTEDLOCK-Tabellenhinweis in die Abfrage auf.  
  
 READUNCOMMITTED  
 Gibt an, dass Dirty Reads zulässig sind. Es werden keine freigegebenen Sperren angefordert, um andere Transaktionen daran zu hindern, von der aktuellen Transaktion gelesene Daten zu ändern, und exklusive Sperren, die von anderen Transaktionen verwendet wurden, hindern die aktuelle Transaktion nicht daran, die gesperrten Daten zu lesen. Das kann eine höhere Parallelität, aber gleichzeitig zur Folge haben, dass Datenänderungen gelesen werden, für die andere Transaktionen dann ein Rollback ausführen. Dadurch können Fehler in der Transaktion auftreten, Daten angezeigt werden, für die nie ein Commit ausgeführt wurde, oder Datensätze zwei Mal (oder gar nicht) dargestellt werden.  
  
 READUNCOMMITTED- und NOLOCK-Hinweise gelten nur für Datensperren. Alle Abfragen, auch solche mit READUNCOMMITTED- und NOLOCK-Hinweisen, aktivieren bei der Kompilierung und Ausführung Sperren des Typs Sch-S (Schemastabilität). Daher werden Abfragen gesperrt, wenn eine gleichzeitige Transaktion eine Schemaänderungssperre (Sch-M) für die Tabelle aufrechterhält. Beispielsweise aktiviert ein DDL-Vorgang (Data Definition Language, Datendefinitionssprache) eine Sch-S-Sperre, bevor die Schemainformationen für die Tabelle geändert werden. Alle gleichzeitigen Abfragen, auch solche mit READUNCOMMITTED- oder NOLOCK-Hinweisen, werden beim Versuch, eine Sch-S-Sperre zu errichten, gesperrt. Umgekehrt blockiert eine Abfrage, die eine Sch-S-Sperre aufrechterhält, eine gleichzeitige Transaktion, die versucht, eine Sch-M-Sperre zu errichten.  
  
 READUNCOMMITTED und NOLOCK können nicht für Tabellen angegeben werden, die durch Einfüge-, Update- oder Löschvorgänge geändert wurden. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer ignoriert die READUNCOMMITTED- und NOLOCK-Hinweise in der FROM-Klausel, die für die Zieltabelle einer UPDATE- oder DELETE-Anweisung gelten.  
  
> [!NOTE]  
>  Die Unterstützung für die Verwendung der READUNCOMMITTED- und NOLOCK-Hinweise in der FROM-Klausel, die sich auf die Zieltabelle einer UPDATE- oder DELETE-Anweisung beziehen, wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Vermeiden Sie die Verwendung dieser Hinweise in diesem Kontext beim Entwickeln neuer Anwendungen, und planen Sie die Änderung von Anwendungen, in denen sie aktuell verwendet werden.  
  
 Sie können Konflikte zwischen Sperren minimieren und zugleich Transaktionen vor Dirty Reads von Datenänderungen, für die kein Commit ausgeführt wurde, auf eine der folgenden Weisen schützen:  
  
-   Verwendung der READ COMMITTED-Isolationsstufe bei Festlegen der Datenbankoption READ_COMMITTED_SNAPSHOT auf ON.  
  
-   Verwendung der SNAPSHOT-Isolationsstufe.  
  
 Weitere Informationen zu Isolationsstufen in SQL Server finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
> [!NOTE]  
>  Haben Sie READUNCOMMITTED angegeben und erhalten die Fehlermeldung 601, lösen Sie den Fehler auf wie einen Deadlockfehler (1205), und wiederholen Sie die Anweisung.  
  
 REPEATABLEREAD  
 Legt fest, dass ein Scan mit derselben Sperrsemantik wie eine Transaktion durchgeführt wird, die auf der Isolationsstufe REPEATABLE READ ausgeführt wird. Weitere Informationen zu Isolationsstufen in SQL Server finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 ROWLOCK  
 Gibt an, das Zeilensperren in solchen Fällen gesetzt werden, in denen normalerweise Seiten- oder Tabellensperren gesetzt werden. Wird das Argument in Transaktionen angegeben, die auf der SNAPSHOT-Isolationsstufe ausgeführt werden, werden Zeilensperren nur dann verwendet, wenn ROWLOCK mit anderen Tabellenhinweisen kombiniert ist, die Sperren erfordern, wie beispielsweise UPDLOCK und HOLDLOCK.  
  
 SERIALIZABLE  
 Entspricht der Option HOLDLOCK. Verstärkt die Einschränkung von freigegebenen Sperren, indem sie aufrechterhalten werden, bis eine Transaktion abgeschlossen ist (anstatt die freigegebene Sperre aufzuheben, sobald die benötigte Tabelle oder Datenseite nicht mehr gebraucht wird, ganz gleich, ob die Transaktion abgeschlossen ist oder nicht). Der Scan wird mit derselben Sperrsemantik wie eine Transaktion durchgeführt, die auf der Isolationsstufe SERIALIZABLE ausgeführt wird. Weitere Informationen zu Isolationsstufen in SQL Server finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 SNAPSHOT  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Auf die speicheroptimierte Tabelle wird unter der SNAPSHOT-Isolation zugegriffen. SNAPSHOT kann nur mit speicheroptimierten Tabellen verwendet werden (nicht mit datenträgerbasierten Tabellen). Weitere Informationen finden Sie unter [Einführung in speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).  
  
```sql 
SELECT * FROM dbo.Customers AS c   
WITH (SNAPSHOT)   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id=oh.customer_id;  
```  
  
 SPATIAL_WINDOW_MAX_CELLS = *integer*  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die maximale Anzahl der Zellen an, die für die Mosaikbearbeitung eines geometry- oder geography-Objekts verwendet werden sollen. *number* muss einen Wert zwischen 1 und 8192 aufweisen.  
  
 Mit dieser Option können Sie die Ausführungszeit von Abfragen optimieren, indem Sie den Zusammenhang zwischen der Ausführungszeit des primären und des sekundären Filters kontrollieren. Ein höherer Wert verringert die Ausführungszeit des sekundären Filters, erhöht jedoch die Ausführungszeit des primären Filters. Ein niedrigerer Wert verringert die Ausführungszeit des primären Filters, erhöht jedoch die Ausführungszeit des sekundären Filters. Bei räumlichen Daten mit größerer Dichte sollte ein höherer Wert durch bessere Angleichung an den primären Filter und Verringerung der Ausführungszeit des sekundären Filters in einer niedrigeren Ausführungszeit resultieren. Bei Daten mit geringer Dichte verringert ein niedrigerer Wert die Ausführungszeit des primären Filters.  
  
 Diese Option funktioniert für sowohl manuelle als auch automatische Rastermosaike.  
  
 TABLOCK  
 Gibt an, dass die abgerufene Sperre auf Tabellenebene aktiviert wird. Der Typ der abgerufenen Sperre hängt von der ausgeführten Anweisung ab. Beispielsweise kann eine SELECT-Anweisung eine gemeinsame Sperre abrufen. Bei Angabe von TABLOCK wird die gemeinsame Sperre auf die gesamte Tabelle statt auf Zeilen- oder Seitenebene angewendet. Wird zusätzlich HOLDLOCK angegeben, wird die Tabellensperre bis zum Transaktionsende aufrechterhalten.  
  
 Wenn Sie Daten mit der INSERT INTO \<target_table> SELECT \<columns> FROM \<source_table>-Anweisung in einen Heap importieren, können Sie optimierte Protokollierung und Sperrung für die Anweisung aktivieren, indem Sie den TABLOCK-Hinweis für die Zieltabelle angeben. Außerdem muss das Wiederherstellungsmodell der Datenbank auf einfach oder massenprotokolliert festgelegt werden. Weitere Informationen finden Sie unter [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
 Wenn der TABLOCK-Hinweis mit dem [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)-Massenrowsetanbieter verwendet wird, um Daten in eine Tabelle zu importieren, ermöglicht er mehreren Clients das gleichzeitige Laden von Daten in die Zieltabelle mit optimierter Protokollierung und Sperrung. Weitere Informationen finden Sie unter [Voraussetzungen für die minimale Protokollierung beim Massenimport](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
 TABLOCKX  
 Gibt an, dass für die Tabelle eine exklusive Sperre verwendet wird.  
  
 UPDLOCK  
 Gibt an, dass Updatesperren zu verwenden und aufrechtzuerhalten sind, bis die Transaktion abgeschlossen ist. UPDLOCK erstellt Updatesperren für Lesevorgänge nur auf Zeilen- oder Seitenebene. Wenn UPDLOCK mit TABLOCK kombiniert wird oder aus einem anderen Grund eine Sperre auf Tabellenebene erstellt wird, wird stattdessen eine exklusive Sperre (X) erstellt.  
  
 Bei Angabe von UPDLOCK werden die Isolationsstufenhinweise READCOMMITTED und READCOMMITTEDLOCK ignoriert. Wenn beispielsweise die Isolationsstufe der Sitzung auf SERIALIZABLE festgelegt ist und eine Abfrage (UPDLOCK, READCOMMITTED) angibt, wird der READCOMMITTED-Hinweis ignoriert, und die Transaktion wird mit der Isolationsstufe SERIALIZABLE ausgeführt.  
  
 XLOCK  
 Gibt an, dass exklusive Sperren zu verwenden und aufrechtzuerhalten sind, bis die Transaktion abgeschlossen ist. Wenn die exklusiven Sperren mit ROWLOCK, PAGLOCK oder TABLOCK angegeben werden, werden sie auf die entsprechende Ebene der Granularität angewendet.  
  
## <a name="remarks"></a>Remarks  
 Tabellenhinweise werden ignoriert, wenn der Abfrageplan nicht auf die Tabelle zugreift. Dies ist möglicherweise darauf zurückzuführen, dass der Optimierer überhaupt nicht auf die Tabelle oder stattdessen auf eine indizierte Sicht zugreift. In letzterem Fall kann der Zugriff auf eine indizierte Sicht verhindert werden, indem der Abfragehinweis OPTION (EXPAND VIEWS) verwendet wird.  
  
 Alle Sperrhinweise werden an alle Tabellen und Sichten weitergeleitet, auf die der Abfrageplan zugreift, auch an Tabellen und Sichten, auf die in einer Sicht verwiesen wird. Zusätzlich nimmt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die entsprechenden Sperrkonsistenzprüfungen vor.  
  
 Die Sperrhinweise ROWLOCK, UPDLOCK und XLOCK, die Sperren auf der Zeilenebene anfordern, platzieren Sperren ggf. auf Indexschlüsseln und nicht auf den eigentlichen Datenzeilen. Wenn eine Tabelle beispielsweise über einen nicht gruppierten Index verfügt und eine SELECT-Anweisung, die einen Sperrhinweis verwendet, von einem abdeckenden Index verarbeitet wird, wird eine Sperre für den Indexschlüssel im abdeckenden Index angefordert, statt für die Datenzeile in der Basistabelle.  
  
 Falls eine Tabelle berechnete Spalten enthält und die berechneten Spalten von Ausdrücken oder Funktionen berechnet werden, die auf Spalten anderer Tabellen zugreifen, werden auf diese Tabellen keine Tabellenhinweise angewendet und es erfolgt keine Weitergabe. Angenommen, für eine Tabelle in der Abfrage wird der NOLOCK-Tabellenhinweis angegeben. Diese Tabelle enthält berechnete Spalten, die von einer Kombination aus Ausdrücken und Funktionen berechnet werden, die auf Spalten in einer anderen Tabelle zugreifen. Die Tabellen, auf die die Ausdrücke und Funktionen verweisen, verwenden den Tabellenhinweis NOLOCK nicht, wenn auf sie zugegriffen wird.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestattet für jede Tabelle in der FROM-Klausel maximal einen Tabellenhinweis aus jeder der folgenden Gruppen:  
  
-   Granularitätshinweise: PAGLOCK, NOLOCK, READCOMMITTEDLOCK, ROWLOCK, TABLOCK oder TABLOCKX.  
  
-   Isolationsstufenhinweise: HOLDLOCK, NOLOCK, READCOMMITTED, REPEATABLEREAD, SERIALIZABLE.  
  
## <a name="filtered-index-hints"></a>Gefilterte Indexhinweise  
 Ein gefilterter Index kann als Tabellenhinweis verwendet werden, bewirkt jedoch, dass der Abfrageoptimierer den Fehler 8622 generiert, wenn er nicht alle Zeilen abdeckt, die durch die Abfrage ausgewählt werden. Es folgt ein Beispiel für einen ungültigen gefilterten Indexhinweis. Im folgenden Beispiel wird der gefilterte Index `FIBillOfMaterialsWithComponentID` erstellt und anschließend als Indexhinweis für eine SELECT-Anweisung verwendet. Das gefilterte Indexprädikat schließt Datenzeilen für die ComponentIDs 533, 324 und 753 ein. Das Abfrageprädikat schließt ebenfalls Datenzeilen für die ComponentIDs 533, 324 und 753 ein, erweitert das Resultset jedoch um die ComponentIDs 855 und 924, die nicht im gefilterten Index enthalten sind. Deshalb kann der Abfrageoptimierer den gefilterten Indexhinweis nicht verwenden und generiert den Fehler 8622. Weitere Informationen finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
```sql  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithComponentID'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithComponentID  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithComponentID"  
    ON Production.BillOfMaterials (ComponentID, StartDate, EndDate)  
    WHERE ComponentID IN (533, 324, 753);  
GO  
SELECT StartDate, ComponentID FROM Production.BillOfMaterials  
    WITH( INDEX (FIBillOfMaterialsWithComponentID) )  
    WHERE ComponentID in (533, 324, 753, 855, 924);  
GO  
```  
  
 Der Abfrageoptimierer berücksichtigt einen Indexhinweis nicht, wenn die SET-Optionen nicht die erforderlichen Werte für die gefilterten Indizes enthalten. Weitere Informationen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="using-noexpand"></a>Verwenden von NOEXPAND  
 NOEXPAND gilt nur für *indizierte Sichten*. Eine indizierte Sicht ist eine Sicht, auf der ein eindeutiger gruppierter Index erstellt wurde. Wenn eine Abfrage Verweise auf Spalten enthält, die in einer indizierten Sicht und in Basistabellen vorhanden sind, und der Abfrageoptimierer festlegt, dass die Verwendung der indizierten Sicht die beste Methode zum Ausführen der Abfrage darstellt, verwendet der Optimierer den Index der Sicht. Diese Funktionalität wird als *Abgleich der indizierten Sicht* bezeichnet. Vor [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 wurde die automatische Verwendung einer indizierten Sicht durch den Abfrageoptimierer nur in bestimmten Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Damit der Optimierer indizierte Sichten für den Abgleich oder die Verwendung einer indizierten Sicht berücksichtigt, auf die mit dem NOEXPAND-Hinweis verwiesen wird, müssen die folgenden SET-Optionen auf ON festgelegt werden.  
 
> [!NOTE]  
>  Azure SQL-Datenbank unterstützt die automatische Verwendung indizierter Sichten ohne Angabe des NOEXPAND-Hinweises.
  
||||  
|-|-|-|  
|ANSI_NULLS|ANSI_WARNINGS|CONCAT_NULL_YIELDS_NULL|  
|ANSI_PADDING|ARITHABORT<sup>1</sup>|QUOTED_IDENTIFIER|  
  
 <sup>1</sup> ARITHABORT wird implizit auf ON festgelegt, wenn ANSI_WARNINGS auf ON festgelegt wurde. Es ist daher nicht erforderlich, diese Einstellung manuell anzupassen.  
  
 Auch muss die Option NUMERIC_ROUNDABORT auf OFF festgelegt sein.  
  
 Damit der Optimierer einen Index für eine indizierte Sicht verwendet, geben Sie die Option NOEXPAND an. Dieser Hinweis kann nur dann verwendet werden, wenn die Sicht ebenfalls in der Abfrage angegeben wurde. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt keinen Hinweis zur Verfügung, um die Verwendung einer bestimmten indizierten Sicht in einer Abfrage, die die Sicht nicht direkt in der FROM-Klausel benennt, zu erzwingen. Der Abfrageoptimierer zieht jedoch die Verwendung indizierter Sichten in Erwägung, selbst wenn in der Abfrage nicht direkt auf sie verwiesen wird.  
  
## <a name="using-a-table-hint-as-a-query-hint"></a>Verwenden eines Tabellenhinweises als Abfragehinweis  
 *Tabellenhinweise* können mit der OPTION (TABLE HINT)-Klausel auch als Abfragehinweis angegeben werden. Es wird empfohlen, einen Tabellenhinweis nur im Kontext einer [Planhinweisliste](../../relational-databases/performance/plan-guides.md) als Abfragehinweis zu verwenden. Für Ad-hoc-Abfragen geben Sie diese Hinweise nur als Tabellenhinweise an. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Für die KEEPIDENTITY, IGNORE_CONSTRAINTS- und IGNORE_TRIGGERS-Hinweise werden ALTER-Berechtigungen für die Tabelle benötigt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-the-tablock-hint-to-specify-a-locking-method"></a>A. Verwenden des TABLOCK-Hinweises zum Angeben einer Sperrmethode  
 Im folgenden Beispiel wird angegeben, dass eine freigegebene Sperre für die `Production.Product`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank eingerichtet und bis zum Ende der UPDATE-Anweisung aufrechterhalten wird.  
  
```sql  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
### <a name="b-using-the-forceseek-hint-to-specify-an-index-seek-operation"></a>B. Verwenden des FORCESEEK-Hinweises zum Angeben eines Indexsuchvorgangs  
 Im folgenden Beispiel wird der Abfrageoptimierer mithilfe des FORCESEEK-Tipps ohne Indexangabe gezwungen, einen Indexsuchvorgang in der `Sales.SalesOrderDetail`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank durchzuführen.  
  
```sql
SELECT *  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d WITH (FORCESEEK)  
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
GO  
  
```  
  
 Im folgenden Beispiel wird der Abfrageoptimierer mithilfe des FORCESEEK-Hinweises mit Index gezwungen, einen Indexsuchvorgang im angegebenen Index und in der angegebenen Indexspalte durchzuführen.  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESEEK (PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID (SalesOrderID)))   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);   
GO  
  
```  
  
### <a name="c-using-the-forcescan-hint-to-specify-an-index-scan-operation"></a>C. Verwenden des FORCESCAN-Hinweises zum Angeben eines Indexscanvorgangs  
 Im folgenden Beispiel wird der Abfrageoptimierer mithilfe eines FORCESCAN-Tipps gezwungen, einen Scanvorgang in der `Sales.SalesOrderDetail`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank durchzuführen.  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESCAN)   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)  
  
  
