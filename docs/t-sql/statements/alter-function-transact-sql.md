---
title: ALTER FUNCTION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_FUNCTION_TSQL
- ALTER FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER FUNCTION statement
- modifying functions
- functions [SQL Server], modifying
ms.assetid: 89f066ee-05ac-4439-ab04-d8c3d5911179
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4b1008715d9cfd3e48945d0651f454253bc4e4bc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-function-transact-sql"></a>ALTER FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  Ändert eine vorhandene zuvor (durch Ausführen der CREATE FUNCTION-Anweisung) erstellte [!INCLUDE[tsql](../../includes/tsql-md.md)]- oder CLR-Funktion, ohne Berechtigungen zu ändern und ohne abhängige Funktionen, gespeicherte Prozeduren oder Trigger zu beeinflussen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Transact-SQL Scalar Function Syntax    
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]
```  

```
-- Transact-SQL Inline Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS TABLE  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    RETURN [ ( ] select_stmt [ ) ]  
[ ; ]  
```
  
```
-- Transact-SQL Multistatement Table-valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS @return_variable TABLE <table_type_definition>  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN  
    END  
[ ; ]  
```

```  
-- Transact-SQL Function Clauses   
<function_option>::=   
{  
    [ ENCRYPTION ]  
  | [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
} 

<table_type_definition>:: =   
( { <column_definition> <column_constraint>   
  | <computed_column_definition> }   
    [ <table_constraint> ] [ ,...n ]  
)   
<column_definition>::=  
{  
    { column_name data_type }  
    [ [ DEFAULT constant_expression ]   
      [ COLLATE collation_name ] | [ ROWGUIDCOL ]  
    ]  
    | [ IDENTITY [ (seed , increment ) ] ]  
    [ <column_constraint> [ ...n ] ]   
}  

<column_constraint>::=   
{  
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( < index_option > [ , ...n ] )  
      [ ON { filegroup | "default" } ]  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<computed_column_definition>::=  
column_name AS computed_column_expression   
  
<table_constraint>::=  
{   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      ( column_name [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( <index_option> [ , ...n ] )  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<index_option>::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS ={ ON | OFF }   
}  
```
  
```
-- CLR Scalar and Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type | TABLE <clr_table_type_definition> }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```
  
```
-- CLR Function Clauses
<method_specifier>::=  
    assembly_name.class_name.method_name  
 
  
<clr_function_option>::=  
}  
    [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<clr_table_type_definition>::=   
( { column_name data_type } [ ,...n ] )  
  
```  
  
```  
-- Syntax for In-Memory OLTP: Natively compiled, scalar user-defined function  
ALTER FUNCTION [ schema_name. ] function_name    
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])  
        function_body   
        RETURN scalar_expression  
    END  
    
<function_option>::=   
{ |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
```   
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem die benutzerdefinierte Funktion gehört.  
  
 *function_name*  
 Die benutzerdefinierte Funktion, die geändert werden soll.  
  
> [!NOTE]  
>  Auf den Funktionsnamen müssen Klammern folgen, selbst wenn kein Parameter angegeben ist.  
  
 **@** *parameter_name*  
 Ein Parameter in der benutzerdefinierten Funktion. Ein oder mehrere Parameter können deklariert werden.  
  
 Eine Funktion kann maximal 2.100 Parameter haben. Der Benutzer muss beim Ausführen einer Funktion den Wert jedes deklarierten Parameters angeben (sofern kein Standardwert für den betreffenden Parameter definiert ist).  
  
 Geben Sie einen Parameternamen an, der mit dem Zeichen (**@**) beginnt. Der Parametername muss den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Parameter gelten lokal in der jeweiligen Funktion. Dieselben Parameternamen können in anderen Funktionen verwendet werden. Parameter können nur den Platz von Konstanten einnehmen. Sie können nicht anstelle von Tabellennamen, Spaltennamen oder Namen anderer Datenbankobjekte verwendet werden.  
  
> [!NOTE]  
>  ANSI_WARNINGS wird beim Übergeben von Parametern in einer gespeicherten Prozedur oder einer benutzerdefinierten Funktion oder beim Deklarieren und Festlegen von Variablen in einer Batchanweisung nicht berücksichtigt. Wird beispielsweise eine Variable als **char(3)** definiert und dann auf einen Wert festgelegt, der länger als drei Zeichen ist, werden die Daten auf die definierte Größe abgeschnitten, und die Anweisung INSERT oder UPDATE wird erfolgreich ausgeführt.  
  
 [ *type_schema_name.* ] *parameter_data_type*  
 Der Parameterdatentyp und optional das Schema, zu dem der Datentyp gehört. Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen sind abgesehen vom **timestamp**-Datentyp alle Datentypen zulässig, einschließlich benutzerdefinierter CLR-Typen. Für CLR-Funktionen sind abgesehen von den Datentypen **text**, **ntext**, **image** und **timestamp** alle Datentypen zulässig, einschließlich benutzerdefinierter CLR-Typen. Die nicht skalaren Typen **cursor** und **table** können weder in [!INCLUDE[tsql](../../includes/tsql-md.md)]- noch in CLR-Funktionen als Parameterdatentyp angegeben werden.  
  
 Wenn *type_schema_name* nicht angegeben ist, sucht die [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)] nach *parameter_data_type* in der folgenden Reihenfolge:  
  
-   Das Schema, das die Namen von SQL Server-Systemdatentypen enthält  
  
-   Das Standardschema des aktuellen Benutzers in der aktuellen Datenbank  
  
-   Das **dbo** -Schema in der aktuellen Datenbank  
  
 [ **=***default* ]  
 Ein Standardwert für den Parameter. Wenn ein *default*-Wert definiert ist, kann die Funktion ausgeführt werden, ohne dass ein Wert für diesen Parameter angegeben werden muss.  
  
> [!NOTE]  
>  Standardparameterwerte können mit Ausnahme der Datentypen **varchar(max)** und **varbinary(max)** für CLR-Funktionen angegeben werden.  
  
 Wenn ein Parameter der Funktion über einen Standardwert verfügt, muss beim Aufrufen der Funktion das DEFAULT-Schlüsselwort angegeben werden, um den Standardwert abzurufen. In diesem Punkt gibt es einen Unterschied zum Verwenden von Parametern in einer gespeicherten Prozedur. Fehlt im Aufruf einer gespeicherten Prozedur ein Parameter, der einen Standardwert hat, wird automatisch dieser Standardwert verwendet.  
  
 *return_data_type*  
 Der Rückgabewert einer benutzerdefinierten Skalarfunktion. Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen sind abgesehen vom **timestamp**-Datentyp alle Datentypen zulässig, einschließlich benutzerdefinierter CLR-Typen. Für CLR-Funktionen sind abgesehen von den Datentypen **text**, **ntext**, **image** und **timestamp** alle Datentypen zulässig, einschließlich benutzerdefinierter CLR-Typen. Die nicht skalaren Typen **cursor** und **table** können weder in [!INCLUDE[tsql](../../includes/tsql-md.md)]- noch in CLR-Funktionen als Rückgabedatentyp angegeben werden.  
  
 *function_body*  
 Gibt an, dass eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die zusammen keine Nebeneffekte erzeugen, z. B. Ändern einer Tabelle, den Wert der Funktion definiert. *function_body* wird nur in Skalarfunktionen sowie in Tabellenwertfunktionen mit mehreren Anweisungen verwendet.  
  
 In Skalarfunktionen entspricht *function_body* einer Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die zusammen einen skalaren Wert ergeben.  
  
 In Tabellenwertfunktionen mit mehreren Anweisungen entspricht *function_body* einer Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die eine TABLE-Rückgabevariable auffüllen.  
  
 *scalar_expression*  
 Gibt an, dass die Skalarfunktion einen skalaren Wert zurückgibt.  
  
 TABLE  
 Gibt an, dass der Rückgabewert der Tabellenwertfunktion eine Tabelle ist. Nur Konstanten und **@***local_variables* können an Tabellenwertfunktionen übergeben werden.  
  
 In Inline-Tabellenwertfunktionen wird der TABLE-Rückgabewert durch eine einzige SELECT-Anweisung definiert. Inlinefunktionen haben keine zugeordneten Rückgabevariablen.  
  
 In Tabellenwertfunktionen mit mehreren Anweisungen ist **@***return_variable* eine TABLE-Variable, die zum Speichern und Sammeln der Zeilen verwendet wird, die als Wert der Funktion zurückgegeben werden sollen. **@***return_variable* kann nur für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen, nicht für CLR-Funktionen angegeben werden.  
  
 *select-stmt*  
 Einzelne SELECT-Anweisung, die den Rückgabewert einer Inline-Tabellenwertfunktion definiert.  
  
 EXTERNAL NAME \<method_specifier>*assembly_name.class_name*.*method_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Methode an, mit der eine Assembly eine Bindung mit der Funktion herstellt. *assembly_name* muss einer vorhandenen Assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der aktuellen Datenbank mit aktivierter Sichtbarkeit entsprechen. *class_name* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner und als Klasse in der Assembly vorhanden sein. Wenn die Klasse einen mit einem Namespace qualifizierten Namen hat, in dem ein Punkt (**.**) zur Trennung der Bestandteile des Namespace verwendet wird, muss der Klassenname mithilfe von Klammern (**[]**) oder mit Anführungszeichen (**""**) getrennt werden. *method_name* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner und als statische Methode in der angegebenen Klasse vorhanden sein.  
  
> [!NOTE]  
>  Standardmäßig kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keinen CLR-Code ausführen. Sie können Datenbankobjekte, die auf CLR-Module (Common Language Runtime) verweisen, erstellen, ändern und löschen. Bevor Sie diese Verweise in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen können, müssen Sie jedoch die Option [clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) aktivieren. Verwenden Sie dazu [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 *\<*table_type_definition*>***(** { \<column_definition> \<column_constraint> | \<computed_column_definition> } [ \<table_constraint> ] [ **,**...*n* ]**)**  
 Definiert den Tabellendatentyp für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion. Die Tabellendeklaration schließt Spaltendefinitionen und Spalten- oder Tabelleneinschränkungen ein.  
  
\< clr_table_type_definition > **(** { *column_name**data_type* } [ **,**...*n* ] **)** **Gilt für:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Vorschauversion in einigen Regionen](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).  
  
 Definiert die Tabellendatentypen für eine CLR-Funktion. Die Tabellendeklaration schließt nur Spaltennamen und Datentypen ein.  
  
 NULL|NOT NULL  
 Nur für nativ kompilierte, benutzerdefinierte Skalarfunktionen unterstützt. Weitere Informationen dazu finden Sie unter [Benutzerdefinierte Skalarfunktionen für In-Memory-OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 NATIVE_COMPILATION  
 Gibt an, ob eine benutzerdefinierte Funktion nativ kompiliert wird. Dieses Argument ist für nativ kompilierte, benutzerdefinierte Skalarfunktionen erforderlich.  
  
 Das Argument NATIVE_COMPILATION ist notwendig, wenn Sie die Funktion mit einer ALTER-Anweisung ändern, und kann nur verwendet werden, wenn die Funktion mit dem Argument NATIVE_COMPILATION erstellt wurde.  
  
 BEGIN ATOMIC WITH  
 Nur für nativ kompilierte, benutzerdefinierte Skalarfunktionen unterstützt und erforderlich. Weitere Informationen finden Sie unter [ATOMIC-Blöcke](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
 SCHEMABINDING  
 Das Argument SCHEMABINDING ist für nativ kompilierte, benutzerdefinierte Skalarfunktionen erforderlich.  
  
 **\<function_option>::= and \<clr_function_option>::=**  
  
 Gibt an, dass die Funktion mindestens über eine der folgenden Optionen verfügen wird.  
  
 ENCRYPTION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass die [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Katalogsichtspalten, die den Text der ALTER FUNCTION-Anweisung enthalten, verschlüsselt. Mit ENCRYPTION verhindern Sie, dass die Funktion als Teil der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Replikation veröffentlicht wird. ENCRYPTION kann nicht für CLR-Funktionen angegeben werden.  
  
 SCHEMABINDING  
 Gibt an, dass die Funktion an die Datenbankobjekte gebunden ist, auf die sie verweist. Dadurch wird verhindert, dass die Funktion geändert wird, wenn andere schemagebundene Objekte auf sie verweisen.  
  
 Die Bindung der Funktion an die Objekte, auf die sie verweist, wird nur bei einer der folgenden Aktionen entfernt:  
  
-   Die Funktion wird gelöscht.  
  
-   Die Funktion wird mithilfe der ALTER-Anweisung geändert, wobei die Option SCHEMABINDING nicht angegeben ist.  
  
Eine Liste der Bedingungen, die erfüllt sein müssen, damit eine Funktion an ein Schema gebunden sein kann, finden Sie unter [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
 RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT  
 Gibt das **OnNULLCall**-Attribut einer Skalarwertfunktion an. Wenn das Attribut nicht angegeben ist, wird standardmäßig CALLED ON NULL INPUT verwendet. Dies bedeutet, dass der Hauptteil der Funktion ausgeführt wird, selbst wenn NULL als ein Argument übergeben wird.  
  
 Wenn RETURNS NULL ON NULL INPUT in einer CLR-Funktion angegeben wird, bedeutet dies, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL zurückgeben kann, wenn eines der ihm zugestellten Argumente NULL ist, ohne den eigentlichen Hauptteil der Funktion aufzurufen. Wenn die in \<method_specifier> angegebene Methode bereits über ein benutzerdefiniertes Attribut verfügt, das RETURNS NULL ON NULL INPUT angibt, die ALTER FUNCTION-Anweisung jedoch CALLED ON NULL INPUT angibt, hat die ALTER FUNCTION-Anweisung Vorrang. Das **OnNULLCall**-Attribut kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 EXECUTE AS-Klausel  
 Gibt den Sicherheitskontext an, in dem die benutzerdefinierte Funktion ausgeführt wird. Deshalb können Sie steuern, welches Benutzerkonto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, um Berechtigungen für eines der Datenbankobjekte zu überprüfen, auf die in der Funktion verwiesen wird.  
  
> [!NOTE]  
>  EXECUTE AS kann nicht für benutzerdefinierte Inlinefunktionen angegeben werden.  
  
 Weitere Informationen finden Sie unter [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
**\< column_definition >::=**
  
 Definiert den Tabellendatentyp. Die Tabellendeklaration schließt Spaltendefinitionen und Einschränkungen ein. Für CLR-Funktionen können nur *column_name* und *data_type* angegeben werden.  
  
 *column_name*  
 Der Name einer Spalte in der Tabelle. Spaltennamen müssen den Regeln für Bezeichner entsprechen und in der Tabelle eindeutig sein. *column_name* kann zwischen 1 und 128 Zeichen haben.  
  
 *data_type*  
 Gibt den Datentyp der Spalte an. Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen sind abgesehen von **timestamp** alle Datentypen zulässig, einschließlich benutzerdefinierter CLR-Typen. Für CLR-Funktionen sind abgesehen von **text**, **ntext**, **image**, **char**, **varchar**, **varchar(max)** und **timestamp** alle Datentypen zulässig, einschließlich benutzerdefinierter CLR-Typen. Der nicht skalare Typ **cursor** kann weder in [!INCLUDE[tsql](../../includes/tsql-md.md)]- noch in CLR-Funktionen als Spaltendatentyp angegeben werden.  
  
 DEFAULT *constant_expression*  
 Gibt den Wert an, der für die Spalte bereitgestellt wird, wenn kein Wert explizit angegeben wurde. *constant_expression* ist ein konstanter Wert, ein NULL-Wert oder ein Systemfunktionswert. DEFAULT-Definitionen können auf alle Spalten angewendet werden, mit Ausnahme von Spalten mit der IDENTITY-Eigenschaft. DEFAULT kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 COLLATE *collation_name*  
 Gibt die Sortierung für die Spalte an. Wenn keine Sortierung angegeben ist, wird der Spalte die Standardsortierung der Datenbank zugewiesen. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Eine Liste und weitere Informationen finden Sie unter [Name der Windows-Sortierung &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) und [SQL Server-Sortierungsname &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Mit der COLLATE-Klausel können Sie nur die Sortierungen von Spalten der Datentypen **char**, **varchar**, **nchar** und **nvarchar** ändern.  
  
 COLLATE kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 ROWGUIDCOL  
 Gibt an, dass die neue Spalte eine Spalte mit für alle Zeilen global eindeutigen Bezeichnern ist. Nur eine **uniqueidentifier**-Spalte pro Tabelle kann als ROWGUIDCOL-Spalte gekennzeichnet werden. Die ROWGUIDCOL-Eigenschaft kann nur einer **uniqueidentifier**-Spalte zugewiesen werden.  
  
 Die ROWGUIDCOL-Eigenschaft erzwingt keine Eindeutigkeit der in der Spalte gespeicherten Werte. Sie erzeugt auch nicht automatisch Werte für neue Zeilen, die in die Tabelle eingefügt werden. Um eindeutige Werte für jede Spalte zu erzeugen, verwenden Sie die NEWID-Funktion in INSERT-Anweisungen. Ein Standardwert kann angegeben werden, NEWID wird jedoch nicht als Standardwert unterstützt.  
  
 IDENTITY  
 Gibt an, dass es sich bei der neuen Spalte um eine Identitätsspalte handelt. Wenn der Tabelle eine neue Zeile hinzugefügt wird, stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen eindeutigen, inkrementellen Wert für die Spalte bereit. Identitätsspalten werden normalerweise zusammen mit PRIMARY KEY-Einschränkungen verwendet, um als eindeutiger Zeilenbezeichner für die Tabelle zu dienen. Die IDENTITY-Eigenschaft kann folgenden Spalten zugewiesen werden: **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)** oder **numeric(p,0)**. Es kann nur eine Identitätsspalte pro Tabelle erstellt werden. Gebundene Standardwerte und DEFAULT-Einschränkungen können nicht mit einer Identitätsspalte verwendet werden. Sie müssen entweder *seed* und den *increment* oder keinen von beiden angeben. Wurden Ausgangswert und inkrementeller Wert nicht angegeben, ist der Standardwert (1,1).  
  
 IDENTITY kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 *seed*  
 Der ganzzahlige Wert, der der ersten Zeile in der Tabelle zugewiesen werden soll.  
  
 *increment*  
 Der ganzzahlige Wert, der dem *seed*-Wert für nachfolgende Zeilen in der Tabelle hinzugefügt werden soll.  
  
**\< column_constraint >::= and \< table_constraint>::=**
  
 Definiert die Einschränkung für eine bestimmte Spalte oder Tabelle. Für CLR-Funktionen ist der einzige zulässige Einschränkungstyp NULL. Benannte Einschränkungen sind nicht zulässig.  
  
 NULL | NOT NULL  
 Bestimmt, ob Nullwerte in der Spalte zulässig sind. NULL ist genau genommen keine Einschränkung, kann jedoch wie NOT NULL verwendet werden. NOT NULL kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 PRIMARY KEY  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte durch einen eindeutigen Index erzwingt. In benutzerdefinierten Tabellenwertfunktionen kann die PRIMARY KEY-Einschränkung nur auf einer Spalte pro Tabelle erstellt werden. PRIMARY KEY kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 UNIQUE  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte (oder Spalten) durch einen eindeutigen Index bereitstellt. Eine Tabelle kann mehrere UNIQUE-Einschränkungen haben. UNIQUE kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 CLUSTERED | NONCLUSTERED  
 Gibt an, dass ein gruppierter oder nicht gruppierter Index für die PRIMARY KEY- oder UNIQUE-Einschränkung erstellt wird. PRIMARY KEY-Einschränkungen verwenden CLUSTERED, und UNIQUE-Einschränkungen verwenden NONCLUSTERED.  
  
 CLUSTERED kann nur für eine einzelne Einschränkung angegeben werden. Wenn neben CLUSTERED für eine UNIQUE-Einschränkung auch eine PRIMARY KEY-Einschränkung angegeben wird, verwendet die Einschränkung PRIMARY KEY den Wert NONCLUSTERED.  
  
 CLUSTERED und NONCLUSTERED können nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 CHECK  
 Eine Einschränkung, die Domänenintegrität erzwingt, indem die möglichen Eingabewerte für eine oder mehrere Spalten beschränkt wird. CHECK-Einschränkungen können nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 *logical_expression*  
 Ein logischer Ausdruck, der TRUE oder FALSE zurückgibt.  
  
 **\<computed_column_definition>::=**  
  
 Gibt eine berechnete Spalte an. Weitere Informationen zu berechneten Spalten finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 *column_name*  
 Der Name der berechneten Spalte.  
  
 *computed_column_expression*  
 Ein Ausdruck, der den Wert einer berechneten Spalte definiert.  
  
 **\<index_option>::=**  
  
 Gibt die Indexoptionen für den PRIMARY KEY- oder UNIQUE-Index an. Weitere Informationen zu Indexoptionen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = { ON | OFF }  
 Gibt die Auffüllung von Indizes an. Der Standardwert ist OFF.  
  
 FILLFACTOR = *fillfactor*  
 Gibt einen Prozentsatz an, der anzeigt, wie weit [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -änderung füllen soll. *fillfactor* muss ein ganzzahliger Wert zwischen 1 und 100 sein. Die Standardeinstellung ist 0.  
  
 IGNORE_DUP_KEY = { ON | OFF }  
 Gibt die Fehlermeldung an, wenn ein Einfügevorgang versucht, doppelte Schlüsselwerte in einen eindeutigen Index einzufügen. Die IGNORE_DUP_KEY-Option gilt nur für Einfügevorgänge nach dem Erstellen oder Neuerstellen des Index. Der Standardwert ist OFF.  
  
 STATISTICS_NORECOMPUTE = { ON | OFF }  
 Gibt an, ob Verteilungsstatistiken neu berechnet werden. Der Standardwert ist OFF.  
  
 ALLOW_ROW_LOCKS = { ON | OFF }  
 Gibt an, ob Zeilensperren zulässig sind. Der Standardwert ist ON.  
  
 ALLOW_PAGE_LOCKS = { ON | OFF }  
 Gibt an, ob Seitensperren zulässig sind. Der Standardwert ist ON.  
  
## <a name="remarks"></a>Remarks  
 ALTER FUNCTION kann nicht verwendet werden, um eine Skalarwertfunktion in eine Tabellenwertfunktion oder umgekehrt zu ändern. Ebenso kann ALTER FUNCTION nicht verwendet werden, um eine Inlinefunktion in eine Funktion mit mehreren Anweisungen oder umgekehrt zu ändern. ALTER FUNCTION kann nicht zum Ändern einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion in eine CLR-Funktion und umgekehrt verwendet werden.  
  
 Die folgenden Service Broker-Anweisungen können nicht in die Definition einer benutzerdefinierten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion aufgenommen werden:  
  
-   BEGIN DIALOG CONVERSATION  
-   END CONVERSATION  
-   GET CONVERSATION GROUP  
-   MOVE CONVERSATION  
-   RECEIVE  
-   SEND  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung auf der Funktion oder auf dem Schema. Wenn die Funktion einen benutzerdefinierten Typ angibt, wird die EXECUTE-Berechtigung für den Typ benötigt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
