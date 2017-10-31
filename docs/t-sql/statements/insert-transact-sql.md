---
title: INSERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INSERT_TSQL
- INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- inserting multiple rows
- user-defined types [SQL Server], inserting values
- DML [SQL Server], INSERT statement
- bulk load [SQL Server]
- row additions [SQL Server], INSERT statement
- inserting rows
- table value constructor [SQL Server]
- adding data
- INSERT statement [SQL Server], about INSERT statement
- INSERT statement [SQL Server]
- UDTs [SQL Server], inserting values
- adding rows
- INSERT INTO statement
- data manipulation language [SQL Server], INSERT statement
- inserting data
ms.assetid: 1054c76e-0fd5-4131-8c07-a6c5d024af50
caps.latest.revision: 136
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ef8387c2bbbc109ad7ec325e4faf632a983d96c9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="insert-transact-sql"></a>INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Fügt einer Tabelle oder Sicht in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine oder mehrere Zeilen hinzu. Beispiele finden Sie unter [Beispiele](#InsertExamples).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ ( column_list ) ]   
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
  table_or_view_name  
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  
```  
  
```  
-- External tool only syntax  

INSERT   
{  
    [BULK]  
    [ database_name . [ schema_name ] . | schema_name . ]  
    [ table_name | view_name ]  
    ( <column_definition> )  
    [ WITH (  
        [ [ , ] CHECK_CONSTRAINTS ]  
        [ [ , ] FIRE_TRIGGERS ]  
        [ [ , ] KEEP_NULLS ]  
        [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]  
        [ [ , ] ROWS_PER_BATCH = rows_per_batch ]  
        [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]  
        [ [ , ] TABLOCK ]  
    ) ]  
}  
  
[; ] <column_definition> ::=  
 column_name <data_type>  
    [ COLLATE collation_name ]  
    [ NULL | NOT NULL ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

INSERT INTO [ database_name . [ schema_name ] . | schema_name . ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    {   
      VALUES ( { NULL | expression } )  
      | SELECT <select_criteria>  
    }  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 MIT \<Common_table_expression >  
 Gibt das (auch als allgemeiner Tabellenausdruck bezeichnete) temporäre benannte Resultset an, das innerhalb des Bereichs der INSERT-Anweisung definiert ist. Das Resultset wird von einer SELECT-Anweisung abgeleitet. Weitere Informationen finden Sie unter [WITH Common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Nach oben (*Ausdruck*) [%]  
 Gibt die Anzahl oder den Prozentsatz willkürlicher Zeilen an, die eingefügt werden. *expression* kann eine Anzahl oder ein Prozentsatz der Zeilen sein. Weitere Informationen finden Sie unter [nach oben &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 INTO  
 Ein optionales Schlüsselwort, das zwischen INSERT und der Zieltabelle verwendet werden kann.  
  
 *Servername*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Der Name des Verbindungsservers, auf dem sich die Tabelle oder Sicht befinden. *Server_name* kann angegeben werden, als ein [Verbindungsserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) Namen, oder indem Sie die [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) Funktion.  
  
 Wenn *Server_name* angegeben ist, als Verbindungsserver, *Database_name* und *Schema_name* erforderlich sind. Wenn *Server_name* mit OPENDATASOURCE angegeben wird *Database_name* und *Schema_name* gelten möglicherweise nicht für alle Datenquellen und unterliegen den Funktionen der OLE DB Anbieter, der das Remoteobjekt zugreift.  
  
 *database_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle oder Sicht gehört.  
  
 *Table_or view_name*  
 Der Name der Tabelle oder Sicht, die die Daten empfangen soll.  
  
 Ein [Tabelle](../../t-sql/data-types/table-transact-sql.md) -Variable in ihrem Gültigkeitsbereich kann als Tabellenquelle in einer INSERT-Anweisung verwendet werden.  
  
 Die Sicht verweist *Table_or_view_name* muss aktualisierbar sein und auf genau eine Basistabelle in der FROM-Klausel der Sicht verweisen. Beispielsweise muss eine Einfügung in eine Sicht mit mehreren Tabellen verwenden ein *Column_list* , die nur auf Spalten einer einzigen Basistabelle verweist. Weitere Informationen zu aktualisierbaren Sichten finden Sie unter [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Handelt es sich um die [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) oder [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) Funktion. Die Verwendung dieser Funktionen unterliegt den Funktionen des OLE DB-Anbieters, der auf das Remoteobjekt zugreift.  
  
 MIT ( \<Table_hint_limited > [... *n* ] )  
 Gibt mindestens einen Tabellenhinweis an, der für eine Zieltabelle zulässig ist. Das WITH-Schlüsselwort und die Klammern sind erforderlich.  
  
 READPAST, NOLOCK und READUNCOMMITTED sind nicht zulässig. Weitere Informationen zu Tabellenhinweisen finden Sie unter [Tabellenhinweise &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
> [!IMPORTANT]  
>  Die Möglichkeit, die Hinweise HOLDLOCK, SERIALIZABLE, READCOMMITTED, REPEATABLEREAD oder UPDLOCK für Tabellen anzugeben, bei denen es sich um Ziele von INSERT-Anweisungen handelt, wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Diese Hinweise beeinträchtigen die Leistung von INSERT-Anweisungen nicht. Vermeiden Sie ihre Verwendung bei neuen Entwicklungsarbeiten, und planen Sie die Änderung von Anwendungen, in denen sie aktuell verwendet werden.  
  
 Das Angeben eines TABLOCK-Hinweises für eine Tabelle, die das Ziel einer INSERT-Anweisung ist, hat dieselbe Wirkung wie das Angeben eines TABLOCKX-Hinweises. Auf die Tabelle wird eine exklusive Sperre angewendet.  
  
 (*Column_list*)  
 Eine Liste mit einer oder mehreren Spalten, in die Daten eingefügt werden sollen. *Column_list* muss in Klammern eingeschlossen und durch Kommas getrennt werden.  
  
 Wenn eine Spalte nicht im *Column_list*, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] muss in der Lage, bieten Wert basierend auf der Definition der Spalte; andernfalls, die die Zeile kann nicht geladen werden kann. [!INCLUDE[ssDE](../../includes/ssde-md.md)] stellt automatisch einen Wert für die Spalte bereit, wenn für sie eine der folgenden Bedingungen erfüllt ist:  
  
-   Besitzt eine IDENTITY-Eigenschaft. Der nächste inkrementelle Identitätswert wird verwendet.  
  
-   Verfügt über einen Standardwert. Der Standardwert der Spalte wird verwendet.  
  
-   Verfügt über eine **Zeitstempel** -Datentyp. Der aktuelle Zeitstempelwert wird verwendet.  
  
-   Lässt NULL-Werte zu. Ein NULL-Wert wird verwendet.  
  
-   Ist eine berechnete Spalte an. Der berechnete Wert wird verwendet.  
  
*Column_list* muss beim Einfügen von expliziten Werten in eine Identity-Spalte und die Option SET IDENTITY_INSERT ON, für die Tabelle werden muss verwendet werden.  
  
OUTPUT-Klausel  
 Gibt eingefügte Zeilen als Teil des Einfügevorgangs zurück. Die Ergebnisse können an die Verarbeitungsanwendung zurückgegeben bzw. zur weiteren Verarbeitung in eine Tabelle oder eine Tabellenvariable eingefügt werden.  
  
 Die [OUTPUT-Klausel](../../t-sql/queries/output-clause-transact-sql.md) wird nicht unterstützt in DML-Anweisungen, die auf lokale partitionierte Sichten, verteilte partitionierte Sichten oder Remotetabellen verweisen, oder INSERT-Anweisungen, die enthalten eine *Execute_statement*. Die OUTPUT INTO-Klausel wird nicht unterstützt, in der INSERT-Anweisungen, die enthalten eine \<Dml_table_source >-Klausel. 
  
 VALUES  
 Steht vor der Liste oder den Listen der Datenwerte, die eingefügt werden sollen. Es muss ein Datenwert für jede Spalte in *Column_list*, falls angegeben, oder in der Tabelle. Die Werteliste muss in Klammern eingeschlossen werden.  
  
 Wenn die Werte in der Werteliste nicht im dieselbe Reihenfolge der Spalten in der Tabelle oder einen Wert für jede Spalte in der Tabelle verfügen nicht über *Column_list* muss verwendet werden, um explizit die Spalte angeben, die eingehender Wert jeweils gespeichert.  
  
 Mit dem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Zeilenkonstruktor (auch Tabellenwertkonstruktor genannt) können mehrere Zeilen in einer einzelnen INSERT-Anweisung angegeben werden. Der Zeilenkonstruktor besteht aus einer einzelnen VALUES-Klausel mit mehreren Wertelisten, die in Klammern eingeschlossen und durch ein Komma getrennt sind. Weitere Informationen finden Sie unter [Tabellenwertkonstruktor &#40; Transact-SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 DEFAULT  
 Erzwingt, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] den für eine Spalte definierten Standardwert lädt. Wenn für die Spalte kein Standardwert vorhanden ist und die Spalte NULL-Werte zulässt, wird NULL eingefügt. Für eine Spalte mit definiert die **Zeitstempel** -Datentyp, der nächste Zeitstempelwert eingefügt wird. DEFAULT ist für eine Identitätsspalte nicht zulässig.  
  
 *expression*  
 Eine Konstante, eine Variable oder ein Ausdruck. Der Ausdruck darf keine EXECUTE-Anweisung enthalten.  
  
 Beim Verweisen auf die Unicode-Zeichen-Datentypen **Nchar**, **Nvarchar**, und **Ntext**, "*Ausdruck*" vorangestellt werden die Großbuchstabe ' n '. Wenn "N" nicht angegeben wird, konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Zeichenfolge in die Codepage, die der Standardsortierung der Datenbank oder Spalte entspricht. Alle Zeichen, die in der betreffenden Codepage nicht gefunden werden, gehen verloren.  
  
 *derived_table*  
 Eine gültige SELECT-Anweisung, die in die Tabelle zu ladende Datenzeilen zurückgibt. Die SELECT-Anweisung kann keinen allgemeinen Tabellenausdruck (Common Table Expression, CTE) enthalten.  
  
 *execute_statement*  
 Eine gültige EXECUTE-Anweisung, die Daten mithilfe von SELECT- oder READTEXT-Anweisungen zurückgibt. Weitere Informationen finden Sie unter [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 Die RESULT SETS-Optionen der EXECUTE-Anweisung können in einer INSERT…EXEC-Anweisung nicht angegeben werden.  
  
 Wenn *Execute_statement* werden mit INSERT, muss jedes Resultset mit den Spalten in der Tabelle oder im kompatibel sein *Column_list*.  
  
 *Execute_statement* zum Ausführen gespeicherter Prozeduren auf dem gleichen Server oder einem Remoteserver verwendet werden können. Die Prozedur auf dem Remoteserver wird ausgeführt, und die Resultsets werden an den lokalen Server gesendet. Anschließend werden sie in die Tabelle auf dem lokalen Server geladen. In einer verteilten Transaktion *Execute_statement* kann nicht für einen Loopback-Verbindungsserver ausgegeben werden, wenn die Verbindung mehrere aktive Resultsets (MARS) aktiviert ist.  
  
 Wenn *Execute_statement* gibt Daten zurück, mit der READTEXT-Anweisung kann jede READTEXT-Anweisung maximal 1 MB (1024 KB) Daten zurückgeben. *Execute_statement* kann auch mit erweiterten Prozeduren verwendet werden. *Execute_statement* fügt die Daten durch den Hauptthread der erweiterten Prozedur zurückgegeben; jedoch der Ausgabe von anderen Threads als dem Hauptthread nicht eingefügt werden.  
  
 Sie können keinen Tabellenwertparameter als Ziel einer INSERT EXEC-Anweisung angeben; er kann jedoch als Quelle in der INSERT EXEC-Zeichenfolge oder der gespeicherten Prozedur angegeben werden. Weitere Informationen finden Sie unter [Use Table-Valued Parameters &#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
 \<Dml_table_source >  
 Gibt an, dass es sich bei den in die Zieltabelle eingefügten Zeilen um die von der OUTPUT-Klausel in der INSERT-, UPDATE-, DELETE- oder MERGE-Anweisung zurückgegebenen Zeilen handelt, die optional durch eine WHERE-Klausel gefiltert werden. Wenn \<Dml_table_source > angegeben ist, wird das Ziel der äußeren INSERT-Anweisung erfüllt die folgenden Einschränkungen: 
  
-   Die Tabelle muss eine Basistabelle sein, keine Sicht.  
  
-   Die Tabelle darf keine Remotetabelle sein.  
  
-   Die Tabelle darf keine Definition von aktivierten Triggern besitzen.  
  
-   Die Tabelle darf an keinen Primär-/Fremdschlüsselbeziehungen teilnehmen.  
  
-   Sie darf nicht an Mergereplikationen oder aktualisierbaren Abonnements für Transaktionsreplikationen teilnehmen.  
  
 Der Kompatibilitätsgrad der Datenbank muss auf 100 oder höher festgelegt sein. Weitere Informationen finden Sie unter [OUTPUT-Klausel &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 \<Select_list >  
 Eine durch Trennzeichen getrennte Liste, die angibt, welche von der OUTPUT-Klausel zurückgegebenen Spalten eingefügt werden sollen. Die Spalten in \<Select_list > müssen mit den Spalten, die in die Werte eingefügt werden kompatibel sein. \<Select_list > kann nicht auf Aggregatfunktionen oder TEXTPTR verweisen. 
  
> [!NOTE]  
>  In der SELECT-Liste aufgeführten Variablen verweisen auf ihre ursprünglichen Werte, unabhängig von der alle Änderungen, die im \<Dml_statement_with_output_clause >.  
  
 \<Dml_statement_with_output_clause >  
 Eine gültige INSERT-, UPDATE-, DELETE- oder MERGE-Anweisung, die betroffene Zeilen in einer OUTPUT-Klausel zurückgibt. Die Anweisung darf keine WITH-Klausel enthalten und sich nicht auf Remotetabellen oder partitionierte Sichten beziehen. Wenn UPDATE oder DELETE angegeben wird, darf kein cursorbasiertes UPDATE oder DELETE verwendet werden. Auf Quellzeilen darf nicht als geschachtelte DML-Anweisungen verwiesen werden.  
  
 WOBEI \<Search_condition >  
 Ist WHERE-Klausel enthält einen gültigen \<Search_condition >, die von zurückgegebenen Zeilen filtert \<Dml_statement_with_output_clause >. Weitere Informationen finden Sie unter [Suchbedingung &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md). Wenn in diesem Kontext verwendet \<Search_condition > sind keine Unterabfragen, benutzerdefinierten Skalarfunktionen, die den Datenzugriff, Aggregatfunktionen, TEXTPTR oder Prädikate der Volltextsuche ausführen. 
  
 DEFAULT VALUES  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Erzwingt, dass die neue Zeile den für jede Spalte definierten Standardwert enthält.  
  
 BULK  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Wird von externen Tools verwendet, um einen Binärdatenstrom hochzuladen. Diese Option dient nicht zur Verwendung mit Tools wie z. B. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], SQLCMD, OSQL oder Daten zugreifen datenzugriffsanwendungs-Programmierschnittstellen wie z. B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 FIRE_TRIGGERS  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass INSERT-Trigger, die für die Zieltabelle definiert sind, während des Binärdatenstrom-Uploads ausgeführt werden. Weitere Informationen finden Sie unter [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 CHECK_CONSTRAINTS  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass alle Einschränkungen, die für die Zieltabelle oder -sicht gelten, während des Binärdatenstrom-Uploads überprüft werden müssen. Weitere Informationen finden Sie unter [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 KEEPNULLS  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass leere Spalten während des Binärdatenstrom-Uploads einen NULL-Wert beibehalten sollen. Weitere Informationen finden Sie unter [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 KILOBYTES_PER_BATCH = kilobytes_per_batch  
 Gibt die ungefähre Anzahl der Kilobytes (KB) an Daten pro Batch als *Kilobytes_per_batch*. Weitere Informationen finden Sie unter [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 ROWS_PER_BATCH =*Rows_per_batch*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die ungefähre Anzahl von Datenzeilen im Binärdatenstrom an. Weitere Informationen finden Sie unter [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
>  [!NOTE]
>  Ein Syntaxfehler ausgelöst, wenn eine Spaltenliste nicht bereitgestellt wird.  

## <a name="remarks"></a>Hinweise  
Informationen zum Einfügen von Daten in SQL-Diagramm Tabellen finden Sie unter [INSERT (SQL-Diagramm)](../../t-sql/statements/insert-sql-graph.md). 

## <a name="best-practices"></a>Bewährte Methoden  
 Verwenden der @@ROWCOUNT Funktion zum Zurückgeben der Anzahl der eingefügten Zeilen an die Clientanwendung. Weitere Informationen finden Sie unter [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).  
  
### <a name="best-practices-for-bulk-importing-data"></a>Bewährte Methoden für den Massenimport von Daten  
  
#### <a name="using-insert-intoselect-to-bulk-import-data-with-minimal-logging"></a>Verwenden von INSERT INTO…SELECT für den Massenimport von Daten mit minimaler Protokollierung  
 Sie können `INSERT INTO <target_table> SELECT <columns> FROM <source_table>` effizient eine große Anzahl von Zeilen aus einer Tabelle, wie eine Stagingtabelle in eine andere Tabelle mit minimaler Protokollierung übertragen. Die minimale Protokollierung kann die Leistung der Anweisung verbessern und die Wahrscheinlichkeit senken, dass der Vorgang den verfügbaren Transaktionsprotokoll-Speicherplatz während der Transaktion auffüllt.  
  
 Bei der minimalen Protokollierung für diese Anweisung müssen die folgenden Voraussetzungen erfüllt sein:  
  
-   Das Wiederherstellungsmodell der Datenbank ist auf einfach oder massenprotokolliert festgelegt.  
  
-   Die Zieltabelle ist ein leerer oder nicht leerer Heap.  
  
-   Die Zieltabelle wird nicht in der Replikation verwendet.  
  
-   Der TABLOCK-Hinweis wird für die Zieltabelle angegeben.  
  
Zeilen, die infolge einer Einfügeaktion in eine MERGE-Anweisung in einen Heap eingefügt werden, können ebenfalls minimal protokolliert werden.  
  
 Im Gegensatz zur BULK INSERT-Anweisung, die eine weniger restriktive Massenupdatesperre enthält, weist INSERT INTO…SELECT mit dem TABLOCK-Hinweis eine exklusive Sperre (X) für die Tabelle auf. Das bedeutet, dass Sie keine Zeilen mit parallelen Einfügevorgängen einfügen können.  
  
#### <a name="using-openrowset-and-bulk-to-bulk-import-data"></a>Verwenden von OPENROWSET und BULK für den Massenimport von Daten  
 Von der OPENROWSET-Funktion können die folgenden Tabellenhinweise akzeptiert werden, die Massenladeoptimierungen mit der INSERT-Anweisung bereitstellen:  
  
-   Der TABLOCK-Hinweis kann die Anzahl der Protokolldatensätze für den Einfügevorgang minimieren. Das Wiederherstellungsmodell der Datenbank muss auf einfach oder massenprotokolliert festgelegt werden, und die Zieltabelle kann nicht in der Replikation verwendet werden. Weitere Informationen finden Sie unter [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
-   Durch den IGNORE_CONSTRAINTS-Hinweis kann vorübergehend die FOREIGN KEY- und CHECK-Einschränkungsüberprüfung deaktiviert werden.  
  
-   Durch den IGNORE_TRIGGERS-Hinweis kann vorübergehend die Ausführung des Triggers deaktiviert werden.  
  
-   Der KEEPDEFAULTS-Hinweis ermöglicht das Einfügen eines Standardwerts für eine Tabellenspalte (falls vorhanden) anstelle von NULL, wenn der Datensatz keinen Wert für die Spalte aufweist.  
  
-   Der KEEPIDENTITY-Hinweis ermöglicht die Verwendung der Identitätswerte in der importierten Datendatei für die Identitätsspalte in der Zieltabelle.  
  
Diese Optimierungen sind mit denen vergleichbar, die mit dem BULK INSERT-Befehl verfügbar sind. Weitere Informationen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
## <a name="data-types"></a>Datentypen  
 Beachten Sie beim Einfügen von Zeilen das folgende Datentypverhalten:  
  
-   Wenn Sie ein Wert in Spalten mit geladen wird eine **Char**, **Varchar**, oder **Varbinary** -Datentyp, der Auffüllung oder Abschneiden nachfolgender Leerstellen (Leerzeichen bei  **Char** und **Varchar**, Nullen bei **Varbinary**) richtet sich nach der SET ANSI_PADDING-Einstellung für die Spalte definiert werden, wenn die Tabelle erstellt wurde. Weitere Informationen finden Sie unter [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
     Die folgende Tabelle zeigt den Standardvorgang für SET ANSI_PADDING OFF.  
  
    |Datentyp|Standardvorgang|  
    |---------------|-----------------------|  
    |**char**|Füllt den Wert mit Leerzeichen auf, bis die definierte Breite der Spalte erreicht ist.|  
    |**varchar**|Löscht nachfolgende Leerzeichen bis zum ersten Zeichen, das kein Leerzeichen ist, oder alle Zeichen bis auf eines, wenn die Zeichenfolge nur aus Leerzeichen besteht.|  
    |**varbinary**|Löscht nachfolgende Nullen.|  
  
-   Wenn eine leere Zeichenfolge ("") wird geladen, in eine Spalte mit einer **Varchar** oder **Text** -Datentyp, der Standardvorgang ist eine Zeichenfolge der Länge 0 (null) zu laden.  
  
-   Einfügen von null-Wert in einer **Text** oder **Image** Spalte erstellt keinen gültigen Textzeiger noch ist eine 8-KB-Textseite Vorabzuordnung.  
  
-   Spalten mit erstellt die **"uniqueidentifier"** Daten enthalten speziell formatierte 16-Byte-Binärwerte. Im Gegensatz zu mit Identity-Spalten, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] generiert Werte für Spalten mit nicht automatisch die **"uniqueidentifier"** -Datentyp. Bei einem Einfügevorgang können Variablen mit einem Typ **"uniqueidentifier"** und Zeichenfolgenkonstanten der Form *Xxxxxxxx-Xxxx-Xxxx-Xxxx-Xxxxxxxxxxxx* (36 Zeichen inklusive Bindestriche, wobei *x* eine Hexadezimalziffer im Bereich 0-9 bzw. a-f) kann verwendet werden, für die **"uniqueidentifier"** Spalten. Beispielsweise ist 6F9619FF-8B86-D011-B42D-00C04FC964FF ein gültiger Wert für eine **"uniqueidentifier"** Variable oder Spalte. Verwenden der [NEWID()](../../t-sql/functions/newid-transact-sql.md) Funktion, um eine global eindeutige ID (GUID) zu erhalten.  
  
### <a name="inserting-values-into-user-defined-type-columns"></a>Einfügen von Werten in Spalten eines benutzerdefinierten Typs  
 Sie können Werte in Spalten eines benutzerdefinierten Typs einfügen, indem Sie eine der folgenden Methoden verwenden:  
  
-   Bereitstellen eines Werts des benutzerdefinierten Typs  
  
-   Bereitstellen eines Werts eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyps, sofern der benutzerdefinierte Typ implizite oder explizite Konvertierung von diesem Typ unterstützt. Im folgende Beispiel wird gezeigt, wie zum Einfügen eines Werts in einer Spalte des benutzerdefinierten Typs `Point`, durch explizites konvertieren aus einer Zeichenfolge.  
  
    ```  
    INSERT INTO Cities (Location)  
    VALUES ( CONVERT(Point, '12.3:46.2') );  
    ```  
  
     Ein binärer Wert kann auch ohne explizite Konvertierung bereitgestellt werden, da alle benutzerdefinierten Typen implizit aus binären Werten konvertierbar sind.  
  
-   Aufrufen einer benutzerdefinierten Funktion, die einen Wert des benutzerdefinierten Typs zurückgibt. Das folgende Beispiel verwendet die benutzerdefinierte Funktion `CreateNewPoint()`, um einen neuen Wert des benutzerdefinierten Typs `Point` zu erstellen und den Wert in die `Cities`-Tabelle einzufügen.  
  
    ```  
    INSERT INTO Cities (Location)  
    VALUES ( dbo.CreateNewPoint(x, y) );  
    ```  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Sie können die Fehlerbehandlung für die INSERT-Anweisung durch Angeben der Anweisung in einem TRY…CATCH-Konstrukt implementieren.  
  
 Wenn eine INSERT-Anweisung eine Einschränkung oder Regel verletzt bzw. die Anweisung einen Wert enthält, der mit dem Datentyp der Spalte nicht kompatibel ist, schlägt die Anweisung fehl, und eine Fehlermeldung wird zurückgegeben.  
  
 Wenn INSERT mehrere Zeilen mit SELECT oder EXECUTE lädt, bewirkt eine Verletzung einer Regel oder Einschränkung beim Laden der Werte, dass die Anweisung beendet und keine Zeile geladen wird.  
  
 Wenn in einer INSERT-Anweisung bei der Auswertung eines Ausdrucks ein arithmetischer Fehler (Überlauf, Division durch Null oder Domänenfehler) auftritt, behandelt [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Fehler so, als wäre SET ARITHABORT auf ON festgelegt. Der Batch wird beendet, und eine Fehlermeldung wird zurückgegeben. Wenn in einer Anweisung INSERT, DELETE oder UPDATE ein arithmetischer Fehler (Überlauf, Division durch 0 (null) oder Bereichsfehler) bei der Auswertung eines Ausdrucks auftritt und SET ARITHABORT und SET ANSI_WARNINGS auf OFF festgelegt ist, fügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen NULL-Wert ein oder aktualisiert ihn. Wenn die Zielspalte keine NULL-Werte zulässt, schlägt das Einfügen oder Aktualisieren fehl, und dem Benutzer wird ein Fehler angezeigt.  
  
## <a name="interoperability"></a>Interoperabilität  
 Wenn ein INSTEAD OF-Trigger für INSERT-Aktionen für eine Tabelle oder Sicht definiert ist, wird der Trigger anstelle der INSERT-Anweisung ausgeführt. Weitere Informationen zu INSTEAD OF-Trigger finden Sie unter [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Wenn in Remotetabellen Werte eingefügt und nicht alle Werte für alle Spalten angegeben werden, müssen Sie die Spalten identifizieren, in denen die angegebenen Werte eingefügt werden sollen.  
  
 Wenn TOP mit INSERT verwendet wird, werden die Zeilen, auf die verwiesen wird, nicht auf bestimmte Weise angeordnet, und die ORDER BY-Klausel kann in dieser Anweisung nicht direkt angegeben werden. Wenn Sie die TOP-Klausel verwenden müssen, um Zeilen in einer sinnvollen Reihenfolge einzufügen, müssen Sie sie zusammen mit einer ORDER BY-Klausel in einer untergeordneten SELECT-Anweisung verwenden. Weitere Informationen finden Sie im Abschnitt "Beispiele" in diesem Thema.
 
INSERT-Abfragen, mit denen Wählen mit ORDER BY zum Auffüllen von Zeilen Garantien wie Identitätswerte berechnet werden, aber nicht die Reihenfolge, in der die Zeilen eingefügt werden.    
  
## <a name="logging-behavior"></a>Protokollierungsverhalten  
 Die INSERT-Anweisung wird außer immer vollständig protokolliert, wenn die OPENROWSET-Funktion mit dem BULK-Schlüsselwort verwenden oder bei Verwendung `INSERT INTO <target_table> SELECT <columns> FROM <source_table>`. Für diese Vorgänge ist eine minimale Protokollierung möglich. Weitere Informationen finden Sie im Abschnitt "Bewährte Methoden zum Massenladen von Daten" weiter oben in diesem Thema.  
  
## <a name="security"></a>Sicherheit  
 Im Verlauf der Verbindung mit einem Verbindungsserver stellt der sendende Server einen Benutzernamen und ein Kennwort bereit, um eine Verbindung mit dem empfangenden Server in dessen Auftrag aufzubauen. Für diese Verbindung funktioniert, müssen Sie erstellen eine anmeldenamenzuordnung zwischen den Verbindungsservern mit [Sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md).  
  
 Für die Verwendung von OPENROWSET(BULK…) ist es wichtig, nachvollziehen zu können, wie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit Identitätswechseln umgegangen wird. Weitere Informationen finden Sie unter "Sicherheitsüberlegungen" im [Importieren von Massendaten durch Verwenden von BULK INSERT oder OPENROWSET &#40; BULK... &#41; &#40; SQLServer &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Berechtigungen  
 Die INSERT-Berechtigung ist für die Zieltabelle erforderlich.  
  
 Legen Sie Berechtigungen erhalten standardmäßig Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** und **Db_datawriter** festen Datenbankrollen und der Besitzer der Tabelle. Mitglieder der **Sysadmin**, **Db_owner**, und die **Db_securityadmin** Rollen sowie der Tabellenbesitzer können Berechtigungen an andere Benutzer übertragen.  
  
 Zum Ausführen von INSERT mit der Option BULK der OPENROWSET-Funktion muss ein Mitglied der **Sysadmin** feste Serverrolle oder die **Bulkadmin** festen Serverrolle.  
  
##  <a name="InsertExamples"></a> Beispiele  
  
|Kategorie|Funktionssyntaxelemente|  
|--------------|------------------------------|  
|[Grundlegende syntax](#BasicSyntax)|INSERT • Tabellenwertkonstruktor|  
|[Behandlung von Spaltenwerten](#ColumnValues)|IDENTITY • NEWID • Standardwerte • Benutzerdefinierte Typen|  
|[Einfügen von Daten aus anderen Tabellen](#OtherTables)|INSERT…SELECT • INSERT…EXECUTE • WITH Allgemeiner Tabellenausdruck • TOP • OFFSET FETCH|  
|[Angeben von Zielobjekten keine Standardtabellen sind](#TargetObjects)|Views • Tabellenvariablen|  
|[Einfügen von Zeilen in einer Remotetabelle](#RemoteTables)|Verbindungsserver • OPENQUERY-Rowsetfunktion • OPENDATASOURCE-Rowsetfunktion|  
|[Laden von Daten aus Tabellen oder Datendateien Massenimport](#BulkLoad)|INSERT…SELECT • OPENROWSET-Funktion|  
|[Überschreiben das Standardverhalten des Abfrageoptimierers mithilfe von Hinweisen](#TableHints)|Tabellenhinweise|  
|[Erfassen der Ergebnisse der INSERT-Anweisung](#CaptureResults)|OUTPUT-Klausel|  
  
###  <a name="BasicSyntax"></a>Grundlegende Syntax  
 Anhand von Beispielen in diesem Abschnitt wird die grundlegende Funktion der INSERT-Anweisung mithilfe der mindestens erforderlichen Syntax veranschaulicht.  
  
#### <a name="a-inserting-a-single-row-of-data"></a>A. Einfügen einer einzelnen Datenzeile  
 Im folgenden Beispiel wird eine Zeile in die `Production.UnitMeasure`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank eingefügt. Die Spalten in dieser Tabelle heißen `UnitMeasureCode`, `Name` und `ModifiedDate`. Da Werte für alle Spalten bereitgestellt werden und werden in der gleichen Reihenfolge wie die Spalten in der Tabelle aufgeführt, die Spaltennamen müssen nicht in der Spaltenliste angegeben werden*.*  
  
```  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT', N'Feet', '20080414');  
```  
  
#### <a name="b-inserting-multiple-rows-of-data"></a>B. Einfügen mehrerer Datenzeilen  
 Im folgenden Beispiel wird die [tabellenwertkonstruktor](../../t-sql/queries/table-value-constructor-transact-sql.md) zum Einfügen von drei Zeilen in der `Production.UnitMeasure` -Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank in einer einzelnen INSERT­Anweisung. Da Werte für alle Spalten bereitgestellt werden und in der Reihenfolge der Spalten in der Tabelle aufgelistet sind, müssen die Spaltennamen nicht in der Spaltenliste angegeben werden.  
  
```  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923')
    , (N'Y3', N'Cubic Yards', '20080923');  
```  
  
#### <a name="c-inserting-data-that-is-not-in-the-same-order-as-the-table-columns"></a>C. Einfügen von Daten, deren Reihenfolge nicht mit der Reihenfolge der Tabellenspalten übereinstimmt  
 Im folgenden Beispiel wird eine Spaltenliste verwendet, um die in jede Spalte einzufügenden Werte explizit anzugeben. Die Spaltenreihenfolge in der `Production.UnitMeasure` -Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank ist `UnitMeasureCode`, `Name`, `ModifiedDate`jedoch die Spalten sind nicht aufgeführt, in dieser Reihenfolge in *Column_list*.  
  
```  
INSERT INTO Production.UnitMeasure (Name, UnitMeasureCode,  
    ModifiedDate)  
VALUES (N'Square Yards', N'Y2', GETDATE());  
```  
  
###  <a name="ColumnValues"></a>Behandlung von Spaltenwerten  
 Beispiele in diesem Abschnitt veranschaulichen Methoden zum Einfügen von Werten in Spalten, die mit einer Identitätseigenschaft Standardwert definiert sind, oder werden mit Datentypen wie z. B. definiert **uniqueidentifier** oder UDT-Spalten.  
  
#### <a name="d-inserting-data-into-a-table-with-columns-that-have-default-values"></a>D. Einfügen von Daten in eine Tabelle mit Spalten, die Standardwerte enthalten  
 Im folgenden Beispiel wird das Einfügen von Zeilen in eine Tabelle mit Spalten gezeigt, die automatisch einen Wert generieren oder einen Standardwert haben. `Column_1` ist eine berechnete Spalte, die automatisch einen Wert generiert, indem eine Zeichenfolge mit dem in `column_2` eingefügten Wert verkettet wird. `Column_2` wird als Standardeinschränkung definiert. Wenn für diese Spalte kein Wert angegeben ist, wird der Standardwert verwendet. `Column_3`wird definiert, mit der **Rowversion** -Datentyp, der automatisch eine eindeutige, inkrementelle Binärzahl generiert. `Column_4` generiert nicht automatisch einen Wert. Wird für diese Spalte kein Wert definiert, wird NULL eingefügt. Die INSERT-Anweisungen fügen Zeilen ein, die Werte für einige (aber nicht alle) Spalten enthalten. In der letzten INSERT-Anweisung werden keine Spalten angegeben, und nur die Standardwerte werden mithilfe der DEFAULT VALUES-Klausel eingefügt.  
  
```  
CREATE TABLE dbo.T1   
(  
    column_1 AS 'Computed column ' + column_2,   
    column_2 varchar(30)   
        CONSTRAINT default_name DEFAULT ('my column default'),  
    column_3 rowversion,  
    column_4 varchar(40) NULL  
);  
GO  
INSERT INTO dbo.T1 (column_4)   
    VALUES ('Explicit value');  
INSERT INTO dbo.T1 (column_2, column_4)   
    VALUES ('Explicit value', 'Explicit value');  
INSERT INTO dbo.T1 (column_2)   
    VALUES ('Explicit value');  
INSERT INTO T1 DEFAULT VALUES;   
GO  
SELECT column_1, column_2, column_3, column_4  
FROM dbo.T1;  
GO  
```  
  
#### <a name="e-inserting-data-into-a-table-with-an-identity-column"></a>E. Einfügen von Daten in eine Tabelle mit einer Identitätsspalte  
 Im folgenden Beispiel werden verschiedene Methoden zum Einfügen von Daten in eine Identitätsspalte gezeigt. Die ersten beiden INSERT-Anweisungen ermöglichen das Generieren von Identitätswerten für die neuen Zeilen. Die dritte INSERT-Anweisung überschreibt die IDENTITY-Eigenschaft für die Spalte mit der SET IDENTITY_INSERT-Anweisung und fügt in die Identitätsspalte einen expliziten Wert ein.  
  
```  
CREATE TABLE dbo.T1 ( column_1 int IDENTITY, column_2 VARCHAR(30));  
GO  
INSERT T1 VALUES ('Row #1');  
INSERT T1 (column_2) VALUES ('Row #2');  
GO  
SET IDENTITY_INSERT T1 ON;  
GO  
INSERT INTO T1 (column_1,column_2)   
    VALUES (-99, 'Explicit identity value');  
GO  
SELECT column_1, column_2  
FROM T1;  
GO  
```  
  
#### <a name="f-inserting-data-into-a-uniqueidentifier-column-by-using-newid"></a>F. Einfügen von Daten in eine uniqueidentifier-Spalte mithilfe von NEWID()  
 Im folgenden Beispiel wird die [NEWID](../../t-sql/functions/newid-transact-sql.md)()-Funktion zum Abrufen einer GUID für `column_2`. Im Gegensatz zu für Identity-Spalten, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] generiert Werte für Spalten mit nicht automatisch die ["uniqueidentifier"](../../t-sql/data-types/uniqueidentifier-transact-sql.md) -Datentyp, wie durch den zweiten gezeigt `INSERT` Anweisung.  
  
```  
CREATE TABLE dbo.T1   
(  
    column_1 int IDENTITY,   
    column_2 uniqueidentifier,  
);  
GO  
INSERT INTO dbo.T1 (column_2)   
    VALUES (NEWID());  
INSERT INTO T1 DEFAULT VALUES;   
GO  
SELECT column_1, column_2  
FROM dbo.T1;  
  
```  
  
#### <a name="g-inserting-data-into-user-defined-type-columns"></a>G. Einfügen von Daten in Spalten eines benutzerdefinierten Typs  
 Mit den folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen werden drei Zeilen in die `PointValue`-Spalte der `Points`-Tabelle eingefügt. Diese Spalte verwendet eine [CLR-benutzerdefinierten Typ](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) (UDT). Der `Point`-Datentyp besteht aus X- und Y-Ganzzahlwerten, die als Eigenschaften des benutzerdefinierten Typs verfügbar gemacht werden. Verwenden Sie entweder die CAST- oder CONVERT-Funktion, um die durch Kommas getrennten X- und Y-Werte in den `Point`-Typ umzuwandeln. Die ersten beiden Anweisungen verwenden die CONVERT-Funktion zum Konvertieren eines Zeichenfolgenwertes in der `Point` Typ und die dritte Anweisung verwendet die CAST-Funktion. Weitere Informationen finden Sie unter [Bearbeiten von UDT-Daten](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-manipulating-udt-data.md).  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
###  <a name="OtherTables"></a>Einfügen von Daten aus anderen Tabellen  
 Anhand von Beispielen in diesem Abschnitt werden Methoden zum Einfügen von Zeilen aus einer Tabelle in eine andere Tabelle gezeigt.  
  
#### <a name="h-using-the-select-and-execute-options-to-insert-data-from-other-tables"></a>H. Verwenden der SELECT- und EXECUTE-Option zum Einfügen von Daten aus anderen Tabellen  
 Im folgenden Beispiel wird gezeigt, wie Daten mithilfe von INSERT…SELECT oder INSERT…EXECUTE aus einer Tabelle in eine andere Tabelle eingefügt werden. Jede Methode basiert auf einer SELECT-Anweisung mit mehreren Tabellen, die einen Ausdruck und einen Literalwert in der Spaltenliste enthält.  
  
 Die erste INSERT-Anweisung verwendet eine SELECT-Anweisung, um die Daten aus den Quelltabellen abgeleitet werden (`Employee`, `SalesPerson`, und `Person`) in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank und speichern Sie das Resultset in der `EmployeeSales` Tabelle. Für die zweite INSERT-Anweisung wird die EXECUTE-Klausel verwendet, um eine gespeicherte Prozedur aufzurufen, die die SELECT-Anweisung enthält, wohingegen für die dritte INSERT-Anweisung mithilfe der EXECUTE-Klausel auf die SELECT-Anweisung als Literalzeichenfolge verwiesen wird.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( DataSource   varchar(20) NOT NULL,  
  BusinessEntityID   varchar(11) NOT NULL,  
  LastName     varchar(40) NOT NULL,  
  SalesDollars money NOT NULL  
);  
GO  
CREATE PROCEDURE dbo.uspGetEmployeeSales   
AS   
    SET NOCOUNT ON;  
    SELECT 'PROCEDURE', sp.BusinessEntityID, c.LastName,   
        sp.SalesYTD   
    FROM Sales.SalesPerson AS sp    
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY sp.BusinessEntityID, c.LastName;  
GO  
--INSERT...SELECT example  
INSERT INTO dbo.EmployeeSales  
    SELECT 'SELECT', sp.BusinessEntityID, c.LastName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY sp.BusinessEntityID, c.LastName;  
GO  
--INSERT...EXECUTE procedure example  
INSERT INTO dbo.EmployeeSales   
EXECUTE dbo.uspGetEmployeeSales;  
GO  
--INSERT...EXECUTE('string') example  
INSERT INTO dbo.EmployeeSales   
EXECUTE   
('  
SELECT ''EXEC STRING'', sp.BusinessEntityID, c.LastName,   
    sp.SalesYTD   
    FROM Sales.SalesPerson AS sp   
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE ''2%''  
    ORDER BY sp.BusinessEntityID, c.LastName  
');  
GO  
--Show results.  
SELECT DataSource,BusinessEntityID,LastName,SalesDollars  
FROM dbo.EmployeeSales;  
```  
  
#### <a name="i-using-with-common-table-expression-to-define-the-data-inserted"></a>I. Definieren der eingefügten Daten mithilfe von WITH (allgemeiner Tabellenausdruck)  
 Im folgenden Beispiel wird die `NewEmployee`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank erstellt. Durch einen allgemeinen Tabellenausdruck (`EmployeeTemp`) werden die aus mindestens einer Tabelle in die `NewEmployee`-Tabelle einzufügenden Zeilen definiert. Die INSERT-Anweisung verweist auf die Spalten im allgemeinen Tabellenausdruck.  
  
```  
CREATE TABLE HumanResources.NewEmployee  
(  
    EmployeeID int NOT NULL,  
    LastName nvarchar(50) NOT NULL,  
    FirstName nvarchar(50) NOT NULL,  
    PhoneNumber Phone NULL,  
    AddressLine1 nvarchar(60) NOT NULL,  
    City nvarchar(30) NOT NULL,  
    State nchar(3) NOT NULL,   
    PostalCode nvarchar(15) NOT NULL,  
    CurrentFlag Flag  
);  
GO  
WITH EmployeeTemp (EmpID, LastName, FirstName, Phone,   
                   Address, City, StateProvince,   
                   PostalCode, CurrentFlag)  
AS (SELECT   
       e.BusinessEntityID, c.LastName, c.FirstName, pp.PhoneNumber,  
       a.AddressLine1, a.City, sp.StateProvinceCode,   
       a.PostalCode, e.CurrentFlag  
    FROM HumanResources.Employee e  
        INNER JOIN Person.BusinessEntityAddress AS bea  
        ON e.BusinessEntityID = bea.BusinessEntityID  
        INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
        INNER JOIN Person.PersonPhone AS pp  
        ON e.BusinessEntityID = pp.BusinessEntityID  
        INNER JOIN Person.StateProvince AS sp  
        ON a.StateProvinceID = sp.StateProvinceID  
        INNER JOIN Person.Person as c  
        ON e.BusinessEntityID = c.BusinessEntityID  
    )  
INSERT INTO HumanResources.NewEmployee   
    SELECT EmpID, LastName, FirstName, Phone,   
           Address, City, StateProvince, PostalCode, CurrentFlag  
    FROM EmployeeTemp;  
GO  
```  
  
#### <a name="j-using-top-to-limit-the-data-inserted-from-the-source-table"></a>J. Beschränken der aus der Quelltabelle eingefügten Daten mit TOP  
 Im folgenden Beispiel wird die `EmployeeSales`-Tabelle erstellt. Anschließend werden der Name und die Verkaufszahlen des laufenden Jahres für die ersten 5 zufälligen Mitarbeiter aus der `HumanResources.Employee`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank eingefügt. Die INSERT-Anweisung wählt fünf beliebige Zeilen aus, die von der `SELECT`-Anweisung zurückgegeben werden. Mit der OUTPUT-Klausel werden die Zeilen angezeigt, die in die `EmployeeSales`-Tabelle eingefügt werden. Beachten Sie, dass die ersten 5 Mitarbeiter in der SELECT-Anweisung nicht mit der ORDER BY-Klausel ermittelt werden.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   nvarchar(11) NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  YearlySales  money NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, 
        inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
```  
  
 Wenn Sie die TOP-Klausel verwenden müssen, um Zeilen in einer sinnvollen Reihenfolge einzufügen, müssen Sie sie zusammen mit einer ORDER BY-Klausel in einer untergeordneten SELECT-Anweisung verwenden, wie im folgenden Beispiel veranschaulicht. Mit der OUTPUT-Klausel werden die Zeilen angezeigt, die in die `EmployeeSales`-Tabelle eingefügt werden. Beachten Sie, dass die ersten 5 Mitarbeiter jetzt anhand der Ergebnisse der ORDER BY-Klausel und nicht anhand zufälliger Zeilen eingefügt werden.  
  
```  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, 
        inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
```  
  
###  <a name="TargetObjects"></a>Angeben von Zielobjekten keine Standardtabellen sind  
 In den Beispielen in diesem Abschnitt wird veranschaulicht, wie Zeilen durch Angeben einer Sicht oder Tabellenvariablen eingefügt werden.  
  
#### <a name="k-inserting-data-by-specifying-a-view"></a>K. Einfügen von Daten durch Angeben einer Sicht  
 Im folgenden Beispiel wird ein Sichtname als Zielobjekt angegeben. Die neue Zeile wird jedoch in die zugrunde liegende Basistabelle eingefügt. Die Reihenfolge der Werte in der `INSERT`-Anweisung muss mit der Reihenfolge der Spalten in der Sicht übereinstimmen. Weitere Informationen finden Sie unter [Ändern von Daten über eine Sicht](../../relational-databases/views/modify-data-through-a-view.md).  
  
```  
CREATE TABLE T1 ( column_1 int, column_2 varchar(30));  
GO  
CREATE VIEW V1 AS   
SELECT column_2, column_1   
FROM T1;  
GO  
INSERT INTO V1   
    VALUES ('Row 1',1);  
GO  
SELECT column_1, column_2   
FROM T1;  
GO  
SELECT column_1, column_2  
FROM V1;  
GO  
```  
  
#### <a name="l-inserting-data-into-a-table-variable"></a>L. Einfügen von Daten in eine Tabellevariable  
 Im folgenden Beispiel wird eine Tabellenvariable als Zielobjekt in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank angegeben.  
  
```  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    LocationID int NOT NULL,  
    CostRate smallmoney NOT NULL,  
    NewCostRate AS CostRate * 1.5,  
    ModifiedDate datetime);  
  
-- Insert values into the table variable.  
INSERT INTO @MyTableVar (LocationID, CostRate, ModifiedDate)  
    SELECT LocationID, CostRate, GETDATE() 
    FROM Production.Location  
    WHERE CostRate > 0;  
  
-- View the table variable result set.  
SELECT * FROM @MyTableVar;  
GO  
```  
  
###  <a name="RemoteTables"></a>Einfügen von Zeilen in einer Remotetabelle  
 Beispiele in diesem Abschnitt veranschaulichen, wie zum Einfügen von Zeilen in einer remotezieltabelle mit einem [Verbindungsserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) oder ein [Rowsetfunktion](../../t-sql/functions/rowset-functions-transact-sql.md) auf die Remotetabelle zu verweisen.  
  
#### <a name="m-inserting-data-into-a-remote-table-by-using-a-linked-server"></a>M. Einfügen von Daten in eine Remotetabelle mithilfe eines Verbindungsservers  
 Im folgenden Beispiel werden Zeilen in eine Remotetabelle eingefügt. Im Beispiel wird zuerst erstellen einen Link zur Remotedatenquelle mithilfe [Sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Der Name des Verbindungsservers `MyLinkServer`, angegeben als Teil des vierteiligen Objektnamens in der Form *server.catalog.schema.object*.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  
```  
  
```  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
INSERT INTO MyLinkServer.AdventureWorks2012.HumanResources.Department (Name, GroupName)  
VALUES (N'Public Relations', N'Executive General and Administration');  
GO  
```  
  
#### <a name="n-inserting-data-into-a-remote-table-by-using-the-openquery-function"></a>N. Einfügen von Daten in eine Remotetabelle mithilfe der OPENQUERY-Funktion  
 Das folgende Beispiel fügt eine Zeile in eine Remotetabelle durch Angabe der [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) Rowset-Funktion. Der im vorherigen Beispiel erstellte Name des Verbindungsservers wird hier verwendet.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
INSERT OPENQUERY (MyLinkServer, 
    'SELECT Name, GroupName 
     FROM AdventureWorks2012.HumanResources.Department')  
VALUES ('Environmental Impact', 'Engineering');  
GO  
```  
  
#### <a name="o-inserting-data-into-a-remote-table-by-using-the-opendatasource-function"></a>O. Einfügen von Daten in eine Remotetabelle mithilfe der OPENDATASOURCE-Funktion  
 Das folgende Beispiel fügt eine Zeile in eine Remotetabelle durch Angabe der [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) Rowset-Funktion. Geben Sie einen gültigen Servernamen für die Datenquelle mithilfe des Formats *Server_name* oder *Server_name\instance_name*.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_nameinstance_name.  
  
INSERT INTO OPENDATASOURCE('SQLNCLI',  
    'Data Source= <server_name>; Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department (Name, GroupName)  
    VALUES (N'Standards and Methods', 'Quality Assurance');  
GO  
```  
  
#### <a name="p-inserting-into-an-external-table-created-using-polybase"></a>P. Einfügen in eine externe Tabelle erstellten mithilfe von PolyBase  
 Exportieren von Daten aus SQL Server in Hadoop oder Azure Storage Erstellen Sie zuerst eine externe Tabelle, die auf die Zieldatei oder das Verzeichnis verweist. Verwenden Sie dann INSERT INTO zum Exportieren von Daten aus einer lokalen SQL Server-Tabelle in eine externe Datenquelle. Die INSERT INTO-Anweisung erstellt die Zieldatei oder das Verzeichnis, falls nicht vorhanden, und die Ergebnisse der SELECT-Anweisung werden zu einem angegebenen Speicherort im angegebenen Dateiformat exportiert.  Weitere Informationen finden Sie unter [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)(Erste Schritte mit PolyBase).  
  
**Gilt für**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
-- Create an external table.   
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
        [FirstName] char(25) NOT NULL,   
        [LastName] char(25) NOT NULL,   
        [YearlyIncome] float NULL,   
        [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
        LOCATION='/old_data/2009/customerdata.tbl',  
        DATA_SOURCE = HadoopHDP2,  
        FILE_FORMAT = TextFileFormat,  
        REJECT_TYPE = VALUE,  
        REJECT_VALUE = 0  
);  
  
-- Export data: Move old data to Hadoop while keeping 
-- it query-able via external table.  

INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  
  
###  <a name="BulkLoad"></a>Massenladen von Daten aus Tabellen oder Datendateien  
 In den Beispielen in diesem Abschnitt werden zwei Methoden zum Massenladen von Daten in eine Tabelle mithilfe der INSERT-Anweisung vorgestellt.  
  
#### <a name="q-inserting-data-into-a-heap-with-minimal-logging"></a>Q. Einfügen von Daten mit minimaler Protokollierung in einen Heap  
 Im folgenden Beispiel wird eine neue Tabelle (ein Heap) erstellt, und es werden Daten aus einer anderen Tabelle in die neu erstellte Tabelle eingefügt. Dazu wird minimale Protokollierung verwendet. Im Beispiel wird davon ausgegangen, dass das Wiederherstellungsmodell der `AdventureWorks2012`-Datenbank auf FULL festgelegt wird. Um sicherzustellen, dass die minimale Protokollierung verwendet wird, wird das Wiederherstellungsmodell der `AdventureWorks2012`-Datenbank auf BULK_LOGGED festgelegt, bevor Zeilen eingefügt und nach der INSERT INTO…-SELECT-Anweisung auf FULL zurückgesetzt werden. Außerdem wird der TABLOCK-Hinweis für die `Sales.SalesHistory`-Zieltabelle angegeben. Dadurch wird sichergestellt, dass die Anweisung minimalen Speicherplatz im Transaktionsprotokoll verwendet und effektiv ausgeführt wird.  
  
```  
-- Create the target heap.  
CREATE TABLE Sales.SalesHistory(  
    SalesOrderID int NOT NULL,  
    SalesOrderDetailID int NOT NULL,  
    CarrierTrackingNumber nvarchar(25) NULL,  
    OrderQty smallint NOT NULL,  
    ProductID int NOT NULL,  
    SpecialOfferID int NOT NULL,  
    UnitPrice money NOT NULL,  
    UnitPriceDiscount money NOT NULL,  
    LineTotal money NOT NULL,  
    rowguid uniqueidentifier ROWGUIDCOL  NOT NULL,  
    ModifiedDate datetime NOT NULL );  
GO  
-- Temporarily set the recovery model to BULK_LOGGED.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY BULK_LOGGED;  
GO  
-- Transfer data from Sales.SalesOrderDetail to Sales.SalesHistory  
INSERT INTO Sales.SalesHistory WITH (TABLOCK)  
    (SalesOrderID,   
     SalesOrderDetailID,  
     CarrierTrackingNumber,   
     OrderQty,   
     ProductID,   
     SpecialOfferID,   
     UnitPrice,   
     UnitPriceDiscount,  
     LineTotal,   
     rowguid,   
     ModifiedDate)  
SELECT * FROM Sales.SalesOrderDetail;  
GO  
-- Reset the recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
#### <a name="r-using-the-openrowset-function-with-bulk-to-bulk-load-data-into-a-table"></a>R. Verwenden der OPENROWSET-Funktion mit BULK zum Massenladen von Daten in eine Tabelle  
 Im folgenden Beispiel werden durch Angabe der OPENROWSET-Funktion Zeilen aus einer Datendatei in eine Tabelle eingefügt. Der IGNORE_TRIGGERS-Tabellenhinweis wird zur Leistungsoptimierung angegeben. Weitere Beispiele finden Sie unter [Importieren von Massendaten durch Verwenden von BULK INSERT oder OPENROWSET &#40; BULK... &#41; &#40; SQLServer &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
INSERT INTO HumanResources.Department WITH (IGNORE_TRIGGERS) (Name, GroupName)  
SELECT b.Name, b.GroupName   
FROM OPENROWSET (  
    BULK 'C:SQLFilesDepartmentData.txt',  
    FORMATFILE = 'C:SQLFilesBulkloadFormatFile.xml',  
    ROWS_PER_BATCH = 15000)AS b ;  
```  
  
###  <a name="TableHints"></a>Überschreiben das Standardverhalten des Abfrageoptimierers mithilfe von Hinweisen  
 Die Beispiele in diesem Abschnitt zeigen, wie [Tabellenhinweise](../../t-sql/queries/hints-transact-sql-table.md) zeitweise das Standardverhalten des Abfrageoptimierers überschrieben wird, beim Verarbeiten der INSERT-Anweisung.  
  
> [!CAUTION]  
>  Da der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer in der Regel den optimalen Ausführungsplan für eine Abfrage auswählt, wird empfohlen, dass erfahrene Entwickler und Datenbankadministratoren Hinweise nur dann verwenden, wenn alle anderen Möglichkeiten sich als unzureichend erwiesen haben.  
  
#### <a name="s-using-the-tablock-hint-to-specify-a-locking-method"></a>S. Verwenden des TABLOCK-Hinweises zum Angeben einer Sperrmethode  
 Im folgenden Beispiel wird angegeben, dass eine exklusive Sperre (X) für die Production.Location-Tabelle eingerichtet und bis zum Ende der INSERT-Anweisung aufrechterhalten wird.  
  
**Gilt für**: [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].  
  
```  
INSERT INTO Production.Location WITH (XLOCK)  
(Name, CostRate, Availability)  
VALUES ( N'Final Inventory', 15.00, 80.00);  
```  
  
###  <a name="CaptureResults"></a>Erfassen der Ergebnisse der INSERT-Anweisung  
 Die Beispiele in diesem Abschnitt zeigen, wie die [OUTPUT-Klausel](../../t-sql/queries/output-clause-transact-sql.md) zum Zurückgeben von Informationen aus bzw. Ausdrücke basierend auf an, die für jede Zeile von einer INSERT-Anweisung betroffen sind. Diese Ergebnisse können an die verarbeitende Anwendung zurückgegeben werden, die sie z. B. für Bestätigungen, Archivierungen und andere Anwendungsanforderungen verwendet.  
  
#### <a name="t-using-output-with-an-insert-statement"></a>T. Verwenden von OUTPUT mit einer INSERT-Anweisung  
 Im folgenden Beispiel wird eine Zeile in die `ScrapReason`-Tabelle eingefügt, und die `OUTPUT`-Klausel wird verwendet, um die Ergebnisse der Anweisung an die `@MyTableVar`-Tabellenvariable zurückzugeben. Da die `ScrapReasonID`-Spalte mit einer `IDENTITY`-Eigenschaft definiert ist, wird kein Wert für diese Spalte in der `INSERT`-Anweisung angegeben. Beachten Sie jedoch, dass der von [!INCLUDE[ssDE](../../includes/ssde-md.md)] für diese Spalte generierte Wert in der `OUTPUT`-Klausel in der `INSERTED.ScrapReasonID`-Spalte zurückgegeben wird.  
  
```  
DECLARE @MyTableVar table( NewScrapReasonID smallint,  
                           Name varchar(50),  
                           ModifiedDate datetime);  
INSERT Production.ScrapReason  
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate  
        INTO @MyTableVar  
VALUES (N'Operator error', GETDATE());  
  
--Display the result set of the table variable.  
SELECT NewScrapReasonID, Name, ModifiedDate FROM @MyTableVar;  
--Display the result set of the table.  
SELECT ScrapReasonID, Name, ModifiedDate   
FROM Production.ScrapReason;  
```  
  
#### <a name="u-using-output-with-identity-and-computed-columns"></a>U. Verwenden von OUTPUT mit Identitätsspalten und berechneten Spalten  
 Im folgenden Beispiel wird die `EmployeeSales`-Tabelle erstellt, und es werden mehrere Zeilen mithilfe einer INSERT-Anweisung mit einer SELECT-Anweisung zum Abrufen der Daten aus den Quelltabellen in die Tabelle eingefügt. Die `EmployeeSales`-Tabelle enthält eine Identitätsspalte (`EmployeeID`) und eine berechnete Spalte (`ProjectedSales`). Da diese Werte während des Einfügevorgangs von [!INCLUDE[ssDE](../../includes/ssde-md.md)] generiert werden, kann keine dieser Spalten in `@MyTableVar` definiert werden.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   int IDENTITY (1,5)NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales AS CurrentSales * 1.10   
);  
GO  
DECLARE @MyTableVar table(  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL  
  );  
  
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)  
  OUTPUT INSERTED.LastName,   
         INSERTED.FirstName,   
         INSERTED.CurrentSales  
  INTO @MyTableVar  
    SELECT c.LastName, c.FirstName, sp.SalesYTD  
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY c.LastName, c.FirstName;  
  
SELECT LastName, FirstName, CurrentSales  
FROM @MyTableVar;  
GO  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM dbo.EmployeeSales;  
```  
  
#### <a name="v-inserting-data-returned-from-an-output-clause"></a>V. Einfügen von Daten, die von einer OUTPUT-Klausel zurückgegeben wurden  
 Im folgenden Beispiel werden aus der OUTPUT-Klausel einer MERGE-Anweisung zurückgegebene Daten erfasst und in eine andere Tabelle eingefügt. Die MERGE-Anweisung aktualisiert die `Quantity`-Spalte der `ProductInventory`-Tabelle täglich auf der Grundlage der Bestellungen, die in der `SalesOrderDetail`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verarbeitet werden. Außerdem werden die Zeilen für Produkte gelöscht, deren Bestand auf 0 (null) fällt. Das Beispiel erfasst die gelöschten Zeilen und fügt sie in einer anderen Tabelle (`ZeroInventory`) ein, in der Produkte ohne Bestand gespeichert werden.  
  
```  
--Create ZeroInventory table.  
CREATE TABLE Production.ZeroInventory (DeletedProductID int, RemovedOnDate DateTime);  
GO  
  
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)  
SELECT ProductID, GETDATE()  
FROM  
(   MERGE Production.ProductInventory AS pi  
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
           JOIN Sales.SalesOrderHeader AS soh  
           ON sod.SalesOrderID = soh.SalesOrderID  
           AND soh.OrderDate = '20070401'  
           GROUP BY ProductID) AS src (ProductID, OrderQty)  
    ON (pi.ProductID = src.ProductID)  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0  
        THEN DELETE  
    WHEN MATCHED  
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)  
WHERE Action = 'DELETE';  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were inserted';  
GO  
SELECT DeletedProductID, RemovedOnDate FROM Production.ZeroInventory;  
```  

#### <a name="w-inserting-data-using-the-select-option"></a>W. Einfügen von Daten mithilfe der Option "auswählen"  
 Das folgende Beispiel veranschaulicht das Einfügen mehrerer Datenzeilen, die mithilfe einer INSERT-Anweisung mit einer SELECT-Option. Die erste `INSERT` -Anweisung verwendet eine `SELECT` -Anweisung direkt zum Abrufen von Daten aus der Quelltabelle, und legen Sie dann zum Speichern des Ergebnisses der `EmployeeTitles` Tabelle.  
  
```  
CREATE TABLE EmployeeTitles  
( EmployeeKey   INT NOT NULL,  
  LastName     varchar(40) NOT NULL,  
  Title      varchar(50) NOT NULL  
);  
INSERT INTO EmployeeTitles  
    SELECT EmployeeKey, LastName, Title   
    FROM ssawPDW.dbo.DimEmployee  
    WHERE EndDate IS NULL;  
```  
  
#### <a name="x-specifying-a-label-with-the-insert-statement"></a>X. Eine Bezeichnung angeben mit der INSERT-Anweisung  
 Das folgende Beispiel zeigt die Verwendung einer Bezeichnung mit einer INSERT-Anweisung.  
  
```  
-- Uses AdventureWorks  
  
INSERT INTO DimCurrency   
VALUES (500, N'C1', N'Currency1')  
OPTION ( LABEL = N'label1' );  
```  
  
#### <a name="y-using-a-label-and-a-query-hint-with-the-insert-statement"></a>Y. Verwenden eine Bezeichnung und einen Abfragehinweis mit der INSERT-Anweisung  
 Diese Abfrage zeigt die grundlegende Syntax für die INSERT-Anweisung eine Bezeichnung und einen Join-Abfragehinweis mit. Nachdem die Abfrage, mit dem Steuerungsknoten übermittelt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], auf den Serverknoten ausgeführt wird, gilt die Hash-Join-Strategie beim Generieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abfrageplan. Weitere Informationen zu joinhinweise und wie Sie die OPTION-Klausel verwenden, finden Sie unter [OPTION (SQL Server PDW)](http://msdn.microsoft.com/en-us/72bbce98-305b-42fa-a19f-d89620621ecc).  
  
```  
-- Uses AdventureWorks  
  
INSERT INTO DimCustomer (CustomerKey, CustomerAlternateKey, 
    FirstName, MiddleName, LastName )   
SELECT ProspectiveBuyerKey, ProspectAlternateKey, 
    FirstName, MiddleName, LastName  
FROM ProspectiveBuyer p JOIN DimGeography g ON p.PostalCode = g.PostalCode  
WHERE g.CountryRegionCode = 'FR'  
OPTION ( LABEL = 'Add French Prospects', HASH JOIN);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [IDENTITY &#40;Eigenschaft&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [NEWID &#40; Transact-SQL &#41;](../../t-sql/functions/newid-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40; Transact-SQL &#41;](../../t-sql/statements/merge-transact-sql.md)   
 [OUTPUT-Klausel &#40; Transact-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [Verwenden der Tabellen inserted und deleted](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)  
  
  




