---
title: ALTER FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 62
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3da4c3a8e76a48db0eee940e969ddf24dc147149
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-function-transact-sql"></a>ALTER FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

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
  
 *Funktionsname*  
 Die benutzerdefinierte Funktion, die geändert werden soll.  
  
> [!NOTE]  
>  Auf den Funktionsnamen müssen Klammern folgen, selbst wenn kein Parameter angegeben ist.  
  
 **@***Parameter_name*  
 Ein Parameter in der benutzerdefinierten Funktion. Ein oder mehrere Parameter können deklariert werden.  
  
 Eine Funktion kann maximal 2.100 Parameter haben. Der Benutzer muss beim Ausführen einer Funktion den Wert jedes deklarierten Parameters angeben (sofern kein Standardwert für den betreffenden Parameter definiert ist).  
  
 Geben Sie einen Parameternamen an, mit einem at-Zeichen (**@**) als erstes Zeichen. Der Parametername muss den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Parameter gelten lokal in der jeweiligen Funktion. Dieselben Parameternamen können in anderen Funktionen verwendet werden. Parameter können nur den Platz von Konstanten einnehmen. Sie können nicht anstelle von Tabellennamen, Spaltennamen oder Namen anderer Datenbankobjekte verwendet werden.  
  
> [!NOTE]  
>  ANSI_WARNINGS wird beim Übergeben von Parametern in einer gespeicherten Prozedur oder einer benutzerdefinierten Funktion oder beim Deklarieren und Festlegen von Variablen in einer Batchanweisung nicht berücksichtigt. Angenommen, eine Variable definiert ist, als **char(3)**, und klicken Sie dann auf einen Wert größer als 3 Zeichen festgelegt, die Daten auf die definierte Größe und die Einfügung abgeschnitten oder UPDATE-Anweisung erfolgreich ausgeführt wird.  
  
 [ *Type_schema_name.* ] *Parameter_data_type*  
 Der Parameterdatentyp und optional das Schema, zu dem der Datentyp gehört. Für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, alle Datentypen, einschließlich von benutzerdefinierten CLR-Typen sind zulässig, mit Ausnahme der **Zeitstempel** -Datentyp. Für CLR-Funktionen sind alle Datentypen, einschließlich CLR-benutzerdefinierte Typen, mit Ausnahme der zugelassen **Text**, **Ntext**, **Image**, und **Zeitstempel** Datentypen. Die nicht skalaren Typen **Cursor** und **Tabelle** kann nicht angegeben werden, als Datentyp eines Parameters in einem [!INCLUDE[tsql](../../includes/tsql-md.md)] oder CLR-Funktionen.  
  
 Wenn *Type_schema_name* nicht angegeben wird, die [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)] sucht nach der *Parameter_data_type* in der folgenden Reihenfolge:  
  
-   Das Schema, das die Namen von SQL Server-Systemdatentypen enthält  
  
-   Das Standardschema des aktuellen Benutzers in der aktuellen Datenbank  
  
-   Das **dbo** -Schema in der aktuellen Datenbank  
  
 [  **=**  *Standard* ]  
 Ein Standardwert für den Parameter. Wenn eine *Standardwert* Wert definiert ist, kann die Funktion ausgeführt werden, ohne einen Wert für diesen Parameter anzugeben.  
  
> [!NOTE]  
>  Standardparameterwerte können angegeben werden, für die CLR-Funktionen mit Ausnahme von **varchar(max)** und **varbinary(max)** Datentypen.  
  
 Wenn ein Parameter der Funktion über einen Standardwert verfügt, muss beim Aufrufen der Funktion das DEFAULT-Schlüsselwort angegeben werden, um den Standardwert abzurufen. In diesem Punkt gibt es einen Unterschied zum Verwenden von Parametern in einer gespeicherten Prozedur. Fehlt im Aufruf einer gespeicherten Prozedur ein Parameter, der einen Standardwert hat, wird automatisch dieser Standardwert verwendet.  
  
 *return_data_type*  
 Der Rückgabewert einer benutzerdefinierten Skalarfunktion. Für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, alle Datentypen, einschließlich von benutzerdefinierten CLR-Typen sind zulässig, mit Ausnahme der **Zeitstempel** -Datentyp. Für CLR-Funktionen sind alle Datentypen, einschließlich CLR-benutzerdefinierte Typen, mit Ausnahme der zugelassen **Text**, **Ntext**, **Image**, und **Zeitstempel** Datentypen. Die nicht skalaren Typen **Cursor** und **Tabelle** kann nicht angegeben werden, als Rückgabedatentyp entweder [!INCLUDE[tsql](../../includes/tsql-md.md)] oder CLR-Funktionen.  
  
 *function_body*  
 Gibt an, dass eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die zusammen keine Nebeneffekte erzeugen, z. B. Ändern einer Tabelle, den Wert der Funktion definiert. *Function_body* wird nur in Skalarfunktionen und Tabellenwertfunktionen mit mehreren Anweisungen verwendet.  
  
 In Skalarfunktionen *Function_body* ist eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, die einen skalaren Wert ergeben.  
  
 In mit mehreren Anweisungen Tabellenwertfunktionen *Function_body* ist eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, die eine Tabelle Auffüllen gibt Variable zurück.  
  
 *"scalar_expression"*  
 Gibt an, dass die Skalarfunktion einen skalaren Wert zurückgibt.  
  
 TABLE  
 Gibt an, dass der Rückgabewert der Tabellenwertfunktion eine Tabelle ist. Nur Konstanten und  **@**  *Local_variables* können an Tabellenwertfunktionen übergeben werden.  
  
 In Inline-Tabellenwertfunktionen wird der TABLE-Rückgabewert durch eine einzige SELECT-Anweisung definiert. Inlinefunktionen haben keine zugeordneten Rückgabevariablen.  
  
 In mit mehreren Anweisungen Tabellenwertfunktionen  **@**  *Return_variable* wird eine Tabellenvariable zum Speichern und Sammeln der Zeilen, die als Wert der Funktion zurückgegeben werden sollen. **@***Return_variable* kann angegeben werden, nur für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, nicht für CLR-Funktionen.  
  
 *SELECT-Anweisung.*  
 Einzelne SELECT-Anweisung, die den Rückgabewert einer Inline-Tabellenwertfunktion definiert.  
  
 EXTERNAL NAME \<Method_specifier >*assembly_name.class_name*. *keine Variablenargumentlisten verwenden*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Methode an, mit der eine Assembly eine Bindung mit der Funktion herstellt. *Assembly_name* übereinstimmen eine vorhandene Assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der aktuellen Datenbank mit eingeschalteter Sichtbarkeit. *CLASS_NAME* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Bezeichner und als Klasse in der Assembly vorhanden sein. Wenn die Klasse einen Namespace qualifizierten Namen verfügt, die einen Punkt verwendet (**.**) um die einzelnen Bestandteile des Namespace voneinander zu trennen, muss der Klassenname durch eckige Klammern begrenzt werden (**[]**) oder Anführungszeichen (**""**). *keine Variablenargumentlisten verwenden* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Bezeichner und als statische Methode in der angegebenen Klasse vorhanden sein.  
  
> [!NOTE]  
>  Standardmäßig kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keinen CLR-Code ausführen. Sie können erstellen, ändern und Löschen von Datenbankobjekten, die common Language Runtime-Module verweisen; Allerdings kann nicht Ausführen dieser Verweise in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erst nach Aktivierung der [Option Clr-fähig](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Verwenden Sie zum Aktivieren der Option [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 *\<*Table_type_definition*>***(** { \<Column_definition > \<Column_constraint > | \<Computed_column_definition >} [ \<Table_constraint >] [ **,**... *n* ]**)**  
 Definiert den Tabellendatentyp für eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion. Die Tabellendeklaration schließt Spaltendefinitionen und Spalten- oder Tabelleneinschränkungen ein.  
  
\<Clr_table_type_definition > **(** { *Column_name**Data_type* } [ **,**...  *n*  ] **)** **Betrifft**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Vorschau in einigen Regionen](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).  
  
 Definiert die Tabellendatentypen für eine CLR-Funktion. Die Tabellendeklaration schließt nur Spaltennamen und Datentypen ein.  
  
 NULL | NOT NULL  
 Nur für systemintern kompilierte, skalare benutzerdefinierte Funktionen unterstützt. Weitere Informationen finden Sie unter [Skalarfunktionen für In-Memory OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 NATIVE_COMPILATION  
 Gibt an, ob eine benutzerdefinierte Funktion systemintern kompiliert wird. Dieses Argument ist erforderlich für systemintern kompilierte, skalare benutzerdefinierte Funktionen.  
  
 Das NATIVE_COMPILATION-Argument ist erforderlich, wenn Sie die Funktion ändern, und nur verwendet werden können, wenn die Funktion mit dem Argument NATIVE_COMPILATION erstellt wurde.  
  
 BEGIN ATOMIC MIT  
 Unterstützt nur für systemintern kompilierte, skalare benutzerdefinierte Funktionen und erforderlich ist. Weitere Informationen finden Sie unter [ATOMIC-Blöcke](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
 SCHEMABINDING  
 Die SCHEMABINDING-Argument ist erforderlich für systemintern kompilierte, skalare benutzerdefinierte Funktionen.  
  
 **\<Function_option >:: = und \<Clr_function_option >:: =**  
  
 Gibt an, dass die Funktion mindestens über eine der folgenden Optionen verfügen wird.  
  
 ENCRYPTION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass die [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Katalogsichtspalten, die den Text der ALTER FUNCTION-Anweisung enthalten, verschlüsselt. Mit ENCRYPTION verhindern Sie, dass die Funktion als Teil der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Replikation veröffentlicht wird. ENCRYPTION kann nicht für CLR-Funktionen angegeben werden.  
  
 SCHEMABINDING  
 Gibt an, dass die Funktion an die Datenbankobjekte gebunden ist, auf die sie verweist. Dadurch wird verhindert, dass die Funktion geändert wird, wenn andere schemagebundene Objekte auf sie verweisen.  
  
 Die Bindung der Funktion an die Objekte, auf die sie verweist, wird nur bei einer der folgenden Aktionen entfernt:  
  
-   Die Funktion wird gelöscht.  
  
-   Die Funktion wird mithilfe der ALTER-Anweisung geändert, wobei die Option SCHEMABINDING nicht angegeben ist.  
  
Eine Liste von Bedingungen, die erfüllt sein müssen, bevor eine Funktion schemagebunden sein kann, finden Sie unter [CREATE FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
 RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT  
 Gibt an, die **OnNULLCall** Attribut des eine Skalarwertfunktion. Wenn das Attribut nicht angegeben ist, wird standardmäßig CALLED ON NULL INPUT verwendet. Dies bedeutet, dass der Hauptteil der Funktion ausgeführt wird, selbst wenn NULL als ein Argument übergeben wird.  
  
 Wenn RETURNS NULL ON NULL INPUT in einer CLR-Funktion angegeben wird, bedeutet dies, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL zurückgeben kann, wenn eines der ihm zugestellten Argumente NULL ist, ohne den eigentlichen Hauptteil der Funktion aufzurufen. Wenn die Methode im angegebenen \<Method_specifier > wurde bereits ein benutzerdefiniertes Attribut, das RETURNS NULL ON NULL INPUT, aber die ALTER FUNCTION-Anweisung gibt CALLED ON NULL INPUT, ALTER FUNCTION-Anweisung hat Vorrang vor angibt. Die **OnNULLCall** Attribut kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 EXECUTE AS-Klausel  
 Gibt den Sicherheitskontext an, in dem die benutzerdefinierte Funktion ausgeführt wird. Deshalb können Sie steuern, welches Benutzerkonto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, um Berechtigungen für eines der Datenbankobjekte zu überprüfen, auf die in der Funktion verwiesen wird.  
  
> [!NOTE]  
>  EXECUTE AS kann nicht für benutzerdefinierte Inlinefunktionen angegeben werden.  
  
 Weitere Informationen finden Sie unter [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
**\<Column_definition >:: =**
  
 Definiert den Tabellendatentyp. Die Tabellendeklaration schließt Spaltendefinitionen und Einschränkungen ein. Für CLR-Funktionen können nur *Column_name* und *Data_type* kann angegeben werden.  
  
 *Spaltenname*  
 Der Name einer Spalte in der Tabelle. Spaltennamen müssen den Regeln für Bezeichner entsprechen und in der Tabelle eindeutig sein. *Column_name* kann zwischen 1 und 128 Zeichen bestehen.  
  
 *data_type*  
 Gibt den Datentyp der Spalte an. Für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, alle Datentypen, einschließlich von benutzerdefinierten CLR-Typen sind zulässig, außer **Zeitstempel**. Für CLR-Funktionen sind alle Datentypen, einschließlich CLR-benutzerdefinierte Typen, mit Ausnahme der zugelassen **Text**, **Ntext**, **Image**, **Char**, **Varchar**, **varchar(max)**, und **Zeitstempel**. Die nicht skalaren Typ **Cursor** kann nicht angegeben werden, als Datentyp entweder in Spalte [!INCLUDE[tsql](../../includes/tsql-md.md)] oder CLR-Funktionen.  
  
 Standard *Constant_expression*  
 Gibt den Wert an, der für die Spalte bereitgestellt wird, wenn kein Wert explizit angegeben wurde. *Constant_expression* ist eine Konstante, NULL oder ein systemfunktionswert. DEFAULT-Definitionen können auf alle Spalten angewendet werden, mit Ausnahme von Spalten mit der IDENTITY-Eigenschaft. DEFAULT kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 COLLATE *Collation_name*  
 Gibt die Sortierung für die Spalte an. Wenn keine Sortierung angegeben ist, wird der Spalte die Standardsortierung der Datenbank zugewiesen. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Eine Liste und Weitere Informationen finden Sie unter [Windows-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) und [SQL Server-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Die COLLATE-Klausel kann verwendet werden, so ändern Sie nur die Sortierungen von Spalten von der **Char**, **Varchar**, **Nchar**, und **Nvarchar** Datentypen.  
  
 COLLATE kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 ROWGUIDCOL  
 Gibt an, dass die neue Spalte eine Spalte mit für alle Zeilen global eindeutigen Bezeichnern ist. Nur ein **"uniqueidentifier"** -Spalte pro Tabelle kann als ROWGUIDCOL-Spalte gekennzeichnet werden. Die ROWGUIDCOL-Eigenschaft kann nur für zugewiesen werden eine **"uniqueidentifier"** Spalte.  
  
 Die ROWGUIDCOL-Eigenschaft erzwingt keine Eindeutigkeit der in der Spalte gespeicherten Werte. Sie erzeugt auch nicht automatisch Werte für neue Zeilen, die in die Tabelle eingefügt werden. Um eindeutige Werte für jede Spalte zu erzeugen, verwenden Sie die NEWID-Funktion in INSERT-Anweisungen. Ein Standardwert kann angegeben werden, NEWID wird jedoch nicht als Standardwert unterstützt.  
  
 IDENTITY  
 Gibt an, dass es sich bei der neuen Spalte um eine Identitätsspalte handelt. Wenn der Tabelle eine neue Zeile hinzugefügt wird, stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen eindeutigen, inkrementellen Wert für die Spalte bereit. Identitätsspalten werden normalerweise zusammen mit PRIMARY KEY-Einschränkungen verwendet, um als eindeutiger Zeilenbezeichner für die Tabelle zu dienen. Die IDENTITY-Eigenschaft zugewiesen werden kann **"tinyint"**, **"smallint"**, **Int**, **"bigint"**, **decimal(p,0)**, oder **numeric(p,0)** Spalten. Es kann nur eine Identitätsspalte pro Tabelle erstellt werden. Gebundene Standardwerte und DEFAULT-Einschränkungen können nicht mit einer Identitätsspalte verwendet werden. Geben Sie sowohl die *Ausgangswert* und *Inkrement* oder keines von beiden. Wurden Ausgangswert und inkrementeller Wert nicht angegeben, ist der Standardwert (1,1).  
  
 IDENTITY kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 *Startwert*  
 Der ganzzahlige Wert, der der ersten Zeile in der Tabelle zugewiesen werden soll.  
  
 *Inkrement*  
 Ist der ganzzahlige Wert hinzufügen zu den *Ausgangswert* -Wert nachfolgende Zeilen in der Tabelle.  
  
**\<Column_constraint >:: = und \< Table_constraint >:: =**
  
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
  
 *Logical_Expression*  
 Ein logischer Ausdruck, der TRUE oder FALSE zurückgibt.  
  
 **\<Computed_column_definition >:: =**  
  
 Gibt eine berechnete Spalte an. Weitere Informationen zu berechneten Spalten finden Sie unter [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 *Spaltenname*  
 Der Name der berechneten Spalte.  
  
 *computed_column_expression*  
 Ein Ausdruck, der den Wert einer berechneten Spalte definiert.  
  
 **\<Index_option >:: =**  
  
 Gibt die Indexoptionen für den PRIMARY KEY- oder UNIQUE-Index an. Weitere Informationen zu Indexoptionen finden Sie unter [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = { ON | OFF }  
 Gibt die Auffüllung von Indizes an. Der Standardwert ist OFF.  
  
 FILLFACTOR = *Fillfactor*  
 Gibt einen Prozentsatz an, der anzeigt, wie weit [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -änderung füllen soll. *FILLFACTOR* muss ein ganzzahliger Wert zwischen 1 und 100 sein. Die Standardeinstellung ist 0.  
  
 IGNORE_DUP_KEY = { ON | OFF }  
 Gibt die Fehlermeldung an, wenn ein Einfügevorgang versucht, doppelte Schlüsselwerte in einen eindeutigen Index einzufügen. Die IGNORE_DUP_KEY-Option gilt nur für Einfügevorgänge nach dem Erstellen oder Neuerstellen des Index. Der Standardwert ist OFF.  
  
 STATISTICS_NORECOMPUTE = { ON | OFF }  
 Gibt an, ob Verteilungsstatistiken neu berechnet werden. Der Standardwert ist OFF.  
  
 ALLOW_ROW_LOCKS = { ON | OFF }  
 Gibt an, ob Zeilensperren zulässig sind. Der Standardwert ist ON.  
  
 ALLOW_PAGE_LOCKS = { ON | OFF }  
 Gibt an, ob Seitensperren zulässig sind. Der Standardwert ist ON.  
  
## <a name="remarks"></a>Hinweise  
 ALTER FUNCTION kann nicht verwendet werden, um eine Skalarwertfunktion in eine Tabellenwertfunktion oder umgekehrt zu ändern. Ebenso kann ALTER FUNCTION nicht verwendet werden, um eine Inlinefunktion in eine Funktion mit mehreren Anweisungen oder umgekehrt zu ändern. ALTER FUNCTION kann nicht zum Ändern einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion in eine CLR-Funktion und umgekehrt verwendet werden.  
  
 Die folgenden Service Broker-Anweisungen können nicht enthalten sein, in der Definition einer [!INCLUDE[tsql](../../includes/tsql-md.md)] User-defined Function:  
  
-   BEGIN DIALOG CONVERSATION  
-   END CONVERSATION  
-   GET CONVERSATION GROUP  
-   MOVE CONVERSATION  
-   RECEIVE  
-   SEND  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung auf der Funktion oder auf dem Schema. Wenn die Funktion einen benutzerdefinierten Typ angibt, wird die EXECUTE-Berechtigung für den Typ benötigt.  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [DROP FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

