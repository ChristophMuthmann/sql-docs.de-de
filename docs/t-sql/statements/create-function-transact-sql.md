---
title: CREATE-Funktion (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FUNCTION
- CREATE FUNCTION
- CREATE_FUNCTION_TSQL
- FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- invoking functions
- extended stored procedures [SQL Server], functions
- table-valued parameters
- user-defined functions [SQL Server], creating
- CLR functions [SQL Server]
- CREATE FUNCTION statement
- nondeterministic functions
- user-defined data types
- functions [SQL Server], creating
- inline table-valued functions [SQL Server]
- multi-statement table-valued functions [SQL Server]
- table-valued functions [SQL Server], CREATE FUNCTION
- parameters [SQL Server], functions
- nesting user-defined functions
- deterministic functions
- scalar-valued functions
- functions [SQL Server], invoking
ms.assetid: 864b393f-225f-4895-8c8d-4db59ea60032
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 76b25e852e94ff6a511d8b18adb31f9da883a7fe
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="create-function-transact-sql"></a>CREATE FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine benutzerdefinierte Funktion in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Eine benutzerdefinierte Funktion, die eine [!INCLUDE[tsql](../../includes/tsql-md.md)]- oder CLR-Routine (Common Language Runtime) darstellt, die Parameter annehmen, eine Aktion ausführen (z. B. eine komplexe Berechnung) und das Ergebnis dieser Aktion als Wert zurückgeben kann. Der Rückgabewert kann ein Skalarwert (Einzelwert) oder eine Tabelle sein. Verwenden Sie diese Anweisung zum Erstellen einer wiederverwendbaren Routine, die auf folgende Weise verwendet werden kann:  
  
-   In [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, wie z. B. SELECT  
  
-   In Anwendungen, die die Funktion aufrufen  
  
-   Bei der Definition einer anderen benutzerdefinierten Funktion  
  
-   Zum Parametrisieren einer Sicht oder zur Verbesserung der Funktionalität einer indizierten Sicht  
  
-   Zum Definieren einer Spalte in einer Tabelle  
  
-   Zum Definieren einer CHECK-Einschränkung für eine Spalte  
  
-   Zum Ersetzen einer gespeicherten Prozedur  
  
-   Verwenden Sie eine Inline-Funktion als Filterprädikat für eine Sicherheitsrichtlinie  
  
> [!NOTE]  
>  Die .NET Framework-CLR-Integration in SQL Server wird in diesem Thema erläutert. CLR-Integration gilt nicht für Azure SQL-Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Transact-SQL Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
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
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
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
-- Transact-SQL Multi-Statement Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [READONLY] }   
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
-- CLR Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  
  
```  
-- CLR Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS TABLE <clr_table_type_definition>   
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ ORDER ( <order_clause> ) ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  

```  
-- CLR Function Clauses  
<order_clause> ::=   
{  
   <column_name_in_clr_table_type_definition>  
   [ ASC | DESC ]   
} [ ,...n]   
  
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
-- In-Memory OLTP: Syntax for natively compiled, scalar user-defined function  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] [ READONLY ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
     WITH <function_option> [ ,...n ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])   
        function_body   
        RETURN scalar_expression  
    END  
  
<function_option>::=   
{  
  |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
  
```  
  
## <a name="arguments"></a>Argumente
*ODER ÄNDERN*  
 **Gilt für**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).  
  
 Bedingt ändert die Funktion nur dann, wenn sie bereits vorhanden ist. 
 
> [!NOTE]  
>  Optionale [oder ALTER] Syntax für die CLR-steht ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU1.   
 
 *schema_name*  
 Der Name des Schemas, zu dem die benutzerdefinierte Funktion gehört.  
  
 *Funktionsname*  
 Der Name der benutzerdefinierten Funktion. Funktionsnamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md) und muss innerhalb der Datenbank und für jedes Schema eindeutig sein.  
  
> [!NOTE]  
>  Auf den Funktionsnamen müssen Klammern folgen, selbst wenn kein Parameter angegeben ist.  
  
 @*Parametername*  
 Ein Parameter in der benutzerdefinierten Funktion. Ein oder mehrere Parameter können deklariert werden.  
  
 Eine Funktion kann maximal 2.100 Parameter haben. Der Benutzer muss beim Ausführen einer Funktion den Wert jedes deklarierten Parameters angeben (sofern kein Standardwert für den betreffenden Parameter definiert ist).  
  
 Geben Sie einen Parameternamen an, der mit dem Zeichen (@) beginnt. Der Parametername muss den Regeln für Bezeichner entsprechen. Parameter gelten lokal in der jeweiligen Funktion. Dieselben Parameternamen können in anderen Funktionen verwendet werden. Parameter können nur den Platz von Konstanten einnehmen. Sie können nicht anstelle von Tabellennamen, Spaltennamen oder Namen anderer Datenbankobjekte verwendet werden.  
  
> [!NOTE]  
>  ANSI_WARNINGS wird bei der Übergabe von Parametern in einer gespeicherten Prozedur oder in einer benutzerdefinierten Funktion oder beim Deklarieren und Festlegen von Variablen in einer Batchanweisung nicht berücksichtigt. Angenommen, eine Variable definiert ist, als **char(3)**, und klicken Sie dann auf einen Wert größer als 3 Zeichen festgelegt, die Daten auf die definierte Größe und die Einfügung abgeschnitten oder UPDATE-Anweisung erfolgreich ausgeführt wird.  
  
 [ *Type_schema_name*. ] *Parameter_data_type*  
 Der Parameterdatentyp und optional das Schema, zu dem der Datentyp gehört. Für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, alle Datentypen, einschließlich CLR-benutzerdefinierte Typen und benutzerdefinierte Tabellentypen sind zulässig, mit Ausnahme der **Zeitstempel** -Datentyp. Für CLR-Funktionen sind alle Datentypen, einschließlich CLR-benutzerdefinierte Typen, mit Ausnahme der zugelassen **Text**, **Ntext**, **Image**benutzerdefinierte Tabellentypen und  **Zeitstempel** Datentypen. Die nicht skalaren Typen **Cursor** und **Tabelle**, kann nicht angegeben werden, als Datentyp eines Parameters in einem [!INCLUDE[tsql](../../includes/tsql-md.md)] oder CLR-Funktionen.  
  
 Wenn *Type_schema_name* nicht angegeben wird, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] sucht nach der *Scalar_parameter_data_type* in der folgenden Reihenfolge:  
  
-   Das Schema, das die Namen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentypen enthält  
  
-   Das Standardschema des aktuellen Benutzers in der aktuellen Datenbank  
  
-   Das **dbo** -Schema in der aktuellen Datenbank  
  
 [=*Standard* ]  
 Ein Standardwert für den Parameter. Wenn eine *Standardwert* Wert definiert ist, kann die Funktion ausgeführt werden, ohne einen Wert für diesen Parameter anzugeben.  
  
> [!NOTE]  
>  Standardparameterwerte können angegeben werden, für die CLR-Funktionen mit Ausnahme der **varchar(max)** und **varbinary(max)** Datentypen.  
  
 Wenn ein Parameter der Funktion über einen Standardwert verfügt, muss beim Aufrufen der Funktion das DEFAULT-Schlüsselwort angegeben werden, um den Standardwert abzurufen. In diesem Punkt gibt es einen Unterschied zum Verwenden von Parametern in einer gespeicherten Prozedur. Fehlt im Aufruf einer gespeicherten Prozedur ein Parameter, der einen Standardwert hat, wird automatisch dieser Standardwert verwendet. Beim Aufrufen einer Skalarfunktion mit der EXECUTE-Anweisung ist das DEFAULT-Schlüsselwort jedoch nicht erforderlich.  
  
 READONLY  
 Gibt an, dass der Parameter nicht aktualisiert oder innerhalb der Definition der Funktion geändert werden kann. Wenn der Parametertyp ein benutzerdefinierter Tabellentyp ist, sollte READONLY angegeben werden.  
  
 *return_data_type*  
 Der Rückgabewert einer benutzerdefinierten Skalarfunktion. Für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, alle Datentypen, einschließlich von benutzerdefinierten CLR-Typen sind zulässig, mit Ausnahme der **Zeitstempel** -Datentyp. Für CLR-Funktionen sind alle Datentypen, einschließlich CLR-benutzerdefinierte Typen, zulässig, außer die **Text**, **Ntext**, **Image**, und **Zeitstempel**-Datentypen. Die nicht skalaren Typen **Cursor** und **Tabelle**, kann nicht angegeben werden, als Rückgabedatentyp entweder [!INCLUDE[tsql](../../includes/tsql-md.md)] oder CLR-Funktionen.  
  
 *function_body*  
 Gibt an, dass eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die zusammen keine Nebeneffekte erzeugen, z. B. Ändern einer Tabelle, den Wert der Funktion definiert. *Function_body* wird nur in Skalarfunktionen und Tabellenwertfunktionen mit mehreren Anweisungen verwendet.  
  
 In Skalarfunktionen *Function_body* ist eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, die einen skalaren Wert ergeben.  
  
 In mit mehreren Anweisungen Tabellenwertfunktionen *Function_body* ist eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, die eine Tabelle Auffüllen gibt Variable zurück.  
  
 *"scalar_expression"*  
 Gibt den skalaren Wert an, den die Skalarfunktion zurückgibt.  
  
 TABLE  
 Gibt an, dass der Rückgabewert der Tabellenwertfunktion eine Tabelle ist. Nur Konstanten und @*Local_variables* können an Tabellenwertfunktionen übergeben werden.  
  
 In Inline-Tabellenwertfunktionen wird der TABLE-Rückgabewert durch eine einzige SELECT-Anweisung definiert. Inlinefunktionen haben keine zugeordneten Rückgabevariablen.  
  
 In mit mehreren Anweisungen Tabellenwertfunktionen @*Return_variable* wird eine Tabellenvariable zum Speichern und Sammeln der Zeilen, die als Wert der Funktion zurückgegeben werden sollen. @*Return_variable* kann angegeben werden, nur für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, nicht für CLR-Funktionen.  
  
> [!WARNING]  
>  Verknüpfen mit einer Tabellenwertfunktion Tabellenwertfunktion in einem **FROM** -Klausel ist möglich, aber es kann zu einer schlechten Leistung. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann für einige Anweisungen, die in einer Funktion mit mehreren Anweisungen enthalten sein können, nicht alle optimierten Techniken verwenden, was zu einem suboptimalen Abfrageplan führt. Um die bestmögliche Leistung zu erzielen, sollten nach Möglichkeit anstelle von Funktionen Joins zwischen Basistabellen verwendet werden.  
  
 *select_stmt*  
 Einzelne SELECT-Anweisung, die den Rückgabewert einer Inline-Tabellenwertfunktion definiert.  
  
 Reihenfolge (\<Order_clause >) gibt die Reihenfolge, in der Ergebnisse von der Funktion mit Tabellenrückgabe zurückgegeben wird werden. Weitere Informationen finden Sie im Abschnitt "Leitfaden zur Verwendung der Sortierreihenfolge" weiter unten in diesem Thema.  
  
 EXTERNAL NAME \<Method_specifier > *Assembly_name*. *CLASS_NAME*. *keine Variablenargumentlisten verwenden* **betrifft**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Assembly und die Methode an, auf die der erstellte Funktionsname verweisen soll.  
  
-   *Assembly_name* -übereinstimmen, dass einen Wert in der `name` Spalte   
    `SELECT * FROM sys.assemblies;`installiert haben.  
    Dies ist der Name, der für die `CREATE ASSEMBLY`-Anweisung verwendet wurde.  
  
-   *CLASS_NAME* -übereinstimmen, dass einen Wert in der `assembly_name` Spalte  
    `SELECT * FROM sys.assembly_modules;`installiert haben.  
    Häufig enthält der Wert einen Punkt. In solchen Fällen das Transact-SQL-Syntax erfordert, dass der Wert mit ein Paar von gerade Klammern oder ein Paar von Anführungszeichen umschlossen werden "".  
  
-   *keine Variablenargumentlisten verwenden* -übereinstimmen, dass einen Wert in der `method_name` Spalte   
    `SELECT * FROM sys.assembly_modules;`installiert haben.  
    Die Methode muss statisch sein.  
  
 In einem typischen Beispiel für MyFood.DLL, bei dem sich alle Typen im MyFood-Namespace befinden, könnte der Wert `EXTERNAL NAME` folgender sein:   
`MyFood.[MyFood.MyClass].MyStaticMethod`  
  
> [!NOTE]  
>  Standardmäßig kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keinen CLR-Code ausführen. Sie können erstellen, ändern und Löschen von Datenbankobjekten, die common Language Runtime-Module verweisen; Allerdings kann nicht Ausführen dieser Verweise in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erst nach Aktivierung der [Option Clr-fähig](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Verwenden Sie zum Aktivieren dieser Option [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 *\<*Table_type_definition *>*  ({ \<Column_definition > \<Column_constraint > | \<Computed_column_definition >}    [ \<Table_constraint >] [,...  *n*  ]) Definiert, die der Tabelle für Datentyp eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktion. Die Tabellendeklaration schließt Spaltendefinitionen und Spalten- oder Tabelleneinschränkungen ein. Die Tabelle wird immer in der primären Dateigruppe abgelegt.  
  
 \<Clr_table_type_definition > ({ *Column_name**Data_type* } [,...  *n*  ]) **Betrifft**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Vorschau in einigen Regionen](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)). |  
  
 Definiert die Tabellendatentypen für eine CLR-Funktion. Die Tabellendeklaration schließt nur Spaltennamen und Datentypen ein. Die Tabelle wird immer in der primären Dateigruppe abgelegt.  
  
 NULL | NOT NULL  
 Nur für systemintern kompilierte, skalare benutzerdefinierte Funktionen unterstützt. Weitere Informationen finden Sie unter [Skalarfunktionen für In-Memory OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 NATIVE_COMPILATION  
 Gibt an, ob eine benutzerdefinierte Funktion systemintern kompiliert wird. Dieses Argument ist erforderlich für systemintern kompilierte, skalare benutzerdefinierte Funktionen.  
  
 BEGIN ATOMIC MIT  
 Unterstützt nur für systemintern kompilierte, skalare benutzerdefinierte Funktionen und erforderlich ist. Weitere Informationen finden Sie unter [ATOMIC-Blöcke](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
 SCHEMABINDING  
 Die SCHEMABINDING-Argument ist erforderlich für systemintern kompilierte, skalare benutzerdefinierte Funktionen.  
  
 EXECUTE AS  
 EXECUTE AS ist erforderlich für systemintern kompilierte, skalare benutzerdefinierte Funktionen.  
  
 **\<Function_option >:: = und \<Clr_function_option >:: =** 
  
 Gibt an, dass die Funktion mindestens über eine der folgenden Optionen verfügen wird.  
  
 ENCRYPTION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] den ursprünglichen Text der CREATE FUNCTION-Anweisung in ein verborgenes Format konvertiert. Die Ausgabe der Verbergung ist nicht direkt in den Katalogsichten sichtbar. Benutzer, die keinen Zugriff auf Systemtabellen oder Datenbankdateien haben, können den verborgenen Text nicht abrufen. Jedoch der Text stehen berechtigten Benutzern, die entweder Systemtabellen, über zugreifen können die [DAC-Port](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) oder direkt auf die Datenbankdateien zugreifen. Des Weiteren können Benutzer, die einen Debugger an den Serverprozess anfügen können, die Originalprozedur zur Laufzeit vom Arbeitsspeicher abrufen. Weitere Informationen zum Zugreifen auf Systemmetadaten finden Sie unter [die Konfiguration der Metadatensichtbarkeit](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 Mit dieser Option verhindern Sie, dass die Funktion als Teil der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Replikation veröffentlicht wird. Diese Option kann nicht für CLR-Funktionen angegeben werden.  
  
 SCHEMABINDING  
 Gibt an, dass die Funktion an die Datenbankobjekte gebunden ist, auf die sie verweist. Wenn SCHEMABINDING angegeben ist, können an Basisobjekten keine Änderungen vorgenommen werden, die die Funktionsdefinition betreffen können. Zunächst muss die Funktionsdefinition selbst geändert oder gelöscht werden, um Abhängigkeiten in dem zu ändernden Objekt zu entfernen.  
  
 Die Bindung der Funktion an die Objekte, auf die sie verweist, wird nur bei einer der folgenden Aktionen entfernt: 
  
-   Die Funktion wird gelöscht.  
  
-   Die Funktion wird mithilfe der ALTER-Anweisung geändert, wobei die Option SCHEMABINDING nicht angegeben ist.  
  
 Eine Funktion kann nur dann schemagebunden sein, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Die Funktion ist eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion.  
  
-   Die benutzerdefinierten Funktionen und Sichten, auf die die Funktion verweist, sind ebenfalls schemagebunden.  
  
-   In der Funktion sind die Verweise auf Objekte mithilfe von zweiteiligen Namen angegeben.  
  
-   Die Funktion und die Objekte, auf die sie verweist, gehören zu derselben Datenbank.  
  
-   Der Benutzer, der die CREATE FUNCTION-Anweisung ausgeführt hat, besitzt REFERENCES-Berechtigungen für die Datenbankobjekte, auf die die Funktion verweist.  
  
 GIBT NULL ZURÜCK, AUF NULL INPUT | **FÜR NULL-EINGABE AUFGERUFEN**  
 Gibt an, die **OnNULLCall** Attribut des eine Skalarwertfunktion. Wenn das Attribut nicht angegeben ist, wird standardmäßig CALLED ON NULL INPUT verwendet. Dies bedeutet, dass der Hauptteil der Funktion ausgeführt wird, selbst wenn NULL als ein Argument übergeben wird.  
  
 Wenn RETURNS NULL ON NULL INPUT in einer CLR-Funktion angegeben wird, bedeutet dies, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL zurückgeben kann, wenn eines der ihm zugestellten Argumente NULL ist, ohne den eigentlichen Hauptteil der Funktion aufzurufen. Wenn die Methode einer CLR-Funktion in angegebenen \<Method_specifier > wurde bereits ein benutzerdefiniertes Attribut, das RETURNS NULL ON NULL INPUT angibt, aber die CREATE FUNCTION-Anweisung gibt CALLED ON NULL INPUT, dauert der CREATE FUNCTION-Anweisung an. Rangfolge. Die **OnNULLCall** Attribut kann nicht für CLR-Tabellenwertfunktionen angegeben werden. 
  
 EXECUTE AS-Klausel  
 Gibt den Sicherheitskontext an, in dem die benutzerdefinierte Funktion ausgeführt wird. Deshalb können Sie steuern, welches Benutzerkonto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, um Berechtigungen für eines der Datenbankobjekte, auf die in der Funktion verwiesen wird, zu überprüfen.  
  
> [!NOTE]  
>  EXECUTE AS kann nicht für benutzerdefinierte Inlinefunktionen angegeben werden.  
  
 Weitere Informationen finden Sie unter [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
 **\<Column_definition >:: =** 
  
 Definiert den Tabellendatentyp. Die Tabellendeklaration schließt Spaltendefinitionen und Einschränkungen ein. Für CLR-Funktionen können nur *Column_name* und *Data_type* kann angegeben werden.  
  
 *column_name*  
 Der Name einer Spalte in der Tabelle. Spaltennamen müssen den Regeln für Bezeichner entsprechen und in der Tabelle eindeutig sein. *Column_name* kann zwischen 1 und 128 Zeichen bestehen.  
  
 *data_type*  
 Gibt den Datentyp der Spalte an. Für [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, alle Datentypen, einschließlich von benutzerdefinierten CLR-Typen sind zulässig, außer **Zeitstempel**. Für CLR-Funktionen sind alle Datentypen, einschließlich CLR-benutzerdefinierte Typen, mit Ausnahme der zugelassen **Text**, **Ntext**, **Image**, **Char**, **Varchar**, **varchar(max)**, und **Zeitstempel**. Die nicht skalaren Typ **Cursor** kann nicht angegeben werden, als Datentyp entweder in Spalte [!INCLUDE[tsql](../../includes/tsql-md.md)] oder CLR-Funktionen.  
  
 Standard *Constant_expression*  
 Gibt den Wert an, der für die Spalte bereitgestellt wird, wenn kein Wert explizit angegeben wurde. *Constant_expression* ist eine Konstante, NULL oder ein systemfunktionswert. DEFAULT-Definitionen können auf alle Spalten angewendet werden, mit Ausnahme von Spalten mit der IDENTITY-Eigenschaft. DEFAULT kann nicht für CLR-Tabellenwertfunktionen angegeben werden.  
  
 COLLATE *Collation_name*  
 Gibt die Sortierung für die Spalte an. Wenn keine Sortierung angegeben ist, wird der Spalte die Standardsortierung der Datenbank zugewiesen. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Eine Liste und Weitere Informationen zu Sortierungen finden Sie unter [Windows-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) und [SQL Server-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
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
  
 *column_name*  
 Der Name der berechneten Spalte.  
  
 *computed_column_expression*  
 Ein Ausdruck, der den Wert einer berechneten Spalte definiert.  
  
 **\<Index_option >:: =**  
  
 Gibt die Indexoptionen für den PRIMARY KEY- oder UNIQUE-Index an. Weitere Informationen zu Indexoptionen finden Sie unter [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = {ON | **OFF** }  
 Gibt die Auffüllung von Indizes an. Der Standardwert ist OFF.  
  
 FILLFACTOR = *Fillfactor*  
 Gibt einen Prozentsatz an, der anzeigt, wie weit [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -änderung füllen soll. *FILLFACTOR* muss ein ganzzahliger Wert zwischen 1 und 100 sein. Die Standardeinstellung ist 0.  
  
 IGNORE_DUP_KEY = {ON | **OFF** }  
 Gibt die Fehlermeldung an, wenn ein Einfügevorgang versucht, doppelte Schlüsselwerte in einen eindeutigen Index einzufügen. Die IGNORE_DUP_KEY-Option gilt nur für Einfügevorgänge nach dem Erstellen oder Neuerstellen des Index. Der Standardwert ist OFF.  
  
 STATISTICS_NORECOMPUTE = {ON | **OFF** }  
 Gibt an, ob Verteilungsstatistiken neu berechnet werden. Der Standardwert ist OFF.  
  
 ALLOW_ROW_LOCKS = { **ON** | {OFF}  
 Gibt an, ob Zeilensperren zulässig sind. Der Standardwert ist ON.  
  
 ALLOW_PAGE_LOCKS = { **ON** | {OFF}  
 Gibt an, ob Seitensperren zulässig sind. Der Standardwert ist ON.  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Wenn eine benutzerdefinierte Funktion nicht mit der SCHEMABINDING-Klausel erstellt wurde, können sich die an zugrunde liegenden Objekten vorgenommenen Änderungen auf die Definition der Funktion auswirken und bei Aufruf der Funktion zu unerwarteten Ergebnissen führen. Es wird empfohlen, eine der folgenden Methoden zu implementieren, damit die Funktion aufgrund von Änderungen an den zugrunde liegenden Objekten nicht veraltet ist:  
  
-   Geben Sie beim Erstellen der Funktion die WITH SCHEMABINDING-Klausel an. Hiermit wird sichergestellt, dass die Objekte, auf die in der Funktionsdefinition verwiesen wird, nicht geändert werden können, es sei denn, die Funktion wird auch geändert.  
  
-   Führen Sie die [Sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md) gespeicherte Prozedur nach dem Ändern der jedes Objekt, das in der Definition der Funktion angegeben wird.  
  
## <a name="data-types"></a>Datentypen  
 Wenn der Parameter in einer CLR-Funktion angegeben werden, werden sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Typen wie zuvor definierter für *Scalar_parameter_data_type*. Informationen zum Vergleichen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemdatentypen mit CLR-integrationsdatentypen oder [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common Language Runtime-Datentypen finden Sie unter [Zuordnen von CLR-Parameterdaten](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um die richtige Methode verweisen, wenn es in einer Klasse überlastet ist, wird die Methode im angegebenen \<Method_specifier > muss die folgenden Merkmale aufweisen: 
  
-   Empfangen Sie die gleiche Anzahl von Parametern wie in [,... *n* ].  
  
-   Alle Parameter nach Wert erhalten, nicht nach Verweis.  
  
-   Parametertypen verwenden, die mit den in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktion angegebenen kompatibel sind.  
  
 Wenn der Rückgabedatentyp der CLR-Funktion einen Tabellentyp (RETURNS TABLE), der Rückgabedatentyp der Methode im gibt \<Method_specifier > muss vom Typ **IEnumerator** oder **IEnumerable**, und es wird davon ausgegangen, dass die Schnittstelle vom Ersteller der Funktion implementiert wird. Im Gegensatz zu [!INCLUDE[tsql](../../includes/tsql-md.md)] Funktionen, CLR-Funktionen können nicht in PRIMARY KEY-, UNIQUE- oder CHECK-Einschränkungen enthalten \<Table_type_definition >. Die Datentypen der Spalten im angegebenen \<Table_type_definition > übereinstimmen, dass die Typen der entsprechenden Spalten des Resultsets zurückgegeben werden, von der-Methode in \<Method_specifier > zum Zeitpunkt der Ausführung. Diese Typprüfung wird zum Zeitpunkt der Funktionserstellung nicht durchgeführt. 
  
 Weitere Informationen zum Programmieren von CLR-Funktionen finden Sie unter [benutzerdefinierte CLR-Funktionen](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md).  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Skalarwertfunktionen können dort aufgerufen werden, wo Skalarausdrücke verwendet werden. Hierzu gehören berechnete Spalten und CHECK-Einschränkungsdefinitionen. Skalarwertfunktionen können auch ausgeführt werden, mithilfe der [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) Anweisung. Skalarwertfunktionen müssen mindestens mit dem zweiteiligen Namen der Funktion aufgerufen werden. Weitere Informationen zu mehrteiligen Namen finden Sie unter [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). Tabellenwertfunktionen können dort aufgerufen werden, wo Tabellenausdrücke in der FROM-Klausel der Anweisungen SELECT, INSERT, UPDATE oder DELETE zulässig sind. Weitere Informationen finden Sie unter [Ausführen von benutzerdefinierten Funktionen](../../relational-databases/user-defined-functions/execute-user-defined-functions.md).  
  
## <a name="interoperability"></a>Interoperabilität  
 Die folgenden Anweisungen sind in einer Funktion zulässig:  
  
-   Zuweisungsanweisungen  
  
-   Anweisungen zur Ablaufsteuerung, mit Ausnahme von TRY...CATCH-Anweisungen  
  
-   DECLARE-Anweisungen zum Definieren lokaler Datenbankvariablen und lokaler Cursor  
  
-   SELECT-Anweisungen, die Auswahllisten mit Ausdrücken enthalten, die lokalen Variablen Werte zuweisen.  
  
-   Cursorvorgänge, die auf lokale Cursor verweisen, die in der Funktion deklariert, geöffnet und geschlossen werden und deren Zuordnungen in der Funktion aufgehoben werden. Es sind nur FETCH-Anweisungen zulässig, die lokalen Variablen Werte mit der INTO-Klausel zuweisen. FETCH-Anweisungen, die Daten an den Client zurückgeben, sind nicht zulässig.  
  
-   INSERT-, UPDATE- und DELETE-Anweisungen, die lokale Tabellenvariablen ändern.  
  
-   EXECUTE-Anweisungen, die erweiterte gespeicherte Prozeduren aufrufen.  
  
-   Weitere Informationen finden Sie unter [erstellen Sie eine benutzerdefinierte Funktionen &#40; Datenbankmodul &#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  
### <a name="computed-column-interoperability"></a>Interoperabilität bei berechneten Spalten  
 Funktionen verfügen über die folgenden Eigenschaften. Die Werte dieser Eigenschaften bestimmen, ob Funktionen in permanent berechneten oder indizierten berechneten Spalten verwendet werden können.  
  
|Eigenschaft|Description|Hinweise|  
|--------------|-----------------|-----------|  
|**IsDeterministic**|Die Funktion ist deterministisch oder nicht deterministisch.|Lokaler Datenzugriff ist in deterministischen Funktionen zulässig. Funktionen, die immer dasselbe Ergebnis zurückgeben, wenn sie mit bestimmten Eingabewerten und mit demselben Datenbankstatus aufgerufen werden, werden beispielsweise als deterministisch bezeichnet.|  
|**IsPrecise**|Die Funktion ist präzise oder unpräzise.|Unpräzise Funktionen enthalten Vorgänge wie Gleitkommatransaktionen.|  
|**IsSystemVerified**|Die Präzisions- und Determinismuseigenschaften der Funktion können von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geprüft werden.||  
|**SystemDataAccess**|Die Funktion greift auf Systemdaten (Systemkataloge oder virtuelle Systemtabellen) in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu.||  
|**UserDataAccess**|Die Funktion greift auf Benutzerdaten in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu.|Schließt benutzerdefinierte Tabellen und temporäre Tabellen ein, jedoch keine Tabellenvariablen.|  
  
 Die Präzisions- und Determinismuseigenschaften von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen werden automatisch von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bestimmt. Die Datenzugriffs- und Determinismuseigenschaften von CLR-Funktionen können vom Benutzer angegeben werden. Weitere Informationen finden Sie unter [Übersicht der CLR-Integration benutzerdefinierte Attribute](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820).  
  
 Um die aktuellen Werte für diese Eigenschaften anzuzeigen, verwenden [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
 Damit Funktionen deterministisch sind, müssen sie mit der Schemabindung erstellt werden.  
  
 Eine berechnete Spalte, die eine benutzerdefinierte Funktion aufruft, kann in einem Index verwendet werden, sofern die benutzerdefinierte Funktion über folgende Eigenschaftswerte verfügt:  
  
-   **IsDeterministic** = "true"  
  
-   **IsSystemVerified** = "true" (sofern es sich um eine permanent berechnete Spalte)  
  
-   **UserDataAccess** = "false"  
  
-   **SystemDataAccess** = "false"  
  
 Weitere Informationen finden Sie unter [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
### <a name="calling-extended-stored-procedures-from-functions"></a>Aufrufen erweiterter gespeicherter Prozeduren aus Funktionen  
 Eine erweiterte gespeicherte Prozedur kann, wenn sie aus einer Funktion heraus aufgerufen wird, keine Resultsets an den Client zurückgeben. Jede ODS-API, die Resultsets an den Client zurückgibt, gibt FAIL zurück. Eine erweiterte gespeicherte Prozedur kann eine Verbindung zurück zu einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen. Diese Prozedur sollte allerdings nicht versuchen, Bestandteil der gleichen Transaktion zu werden, zu der die Funktion gehört, die die erweiterte gespeicherte Prozedur aufgerufen hat.  
  
 Ähnlich wie Aufrufe aus einem Batch oder einer gespeicherten Prozedur wird auch eine erweiterte gespeicherte Prozedur im Kontext des Windows-Sicherheitskontos ausgeführt, unter dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Besitzer der gespeicherten Prozedur sollte dies bedenken, wenn er anderen Benutzern für die gespeicherte Prozedur EXECUTE-Berechtigungen erteilt.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Mit benutzerdefinierten Funktionen können keine Aktionen ausgeführt werden, die den Status einer Datenbank ändern.  
  
 Benutzerdefinierte Funktion dürfen keine OUTPUT INTO-Klausel enthalten, deren Ziel eine Tabelle ist.  
  
 Die folgenden [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Anweisungen können nicht in die Definition einer benutzerdefinierten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion eingeschlossen werden:  
  
-   BEGIN DIALOG CONVERSATION  
  
-   END CONVERSATION  
  
-   GET CONVERSATION GROUP  
  
-   MOVE CONVERSATION  
  
-   RECEIVE  
  
-   SEND  
  
 Benutzerdefinierte Funktionen können geschachtelt werden. Dies bedeutet, dass eine benutzerdefinierte Funktion eine andere aufrufen kann. Die Schachtelungsebene wird um eins erhöht, wenn die aufgerufene Funktion mit der Ausführung beginnt, und wird wieder um eins erniedrigt, wenn die aufgerufene Funktion die Ausführung beendet. Benutzerdefinierte Funktionen unterstützen bis zu 32 geschachtelte Ebenen. Ein Überschreiten der maximalen Schachtelungsebenen verursacht das Fehlschlagen der gesamten Funktionsaufrufskette. Alle Verweise auf verwalteten Code von einer benutzerdefinierten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion aus gelten hinsichtlich des Maximums von 32 Schachtelungsebenen als eine Ebene. Methoden, die aus verwaltetem Code aufgerufen werden, werden nicht mitgezählt.  
  
### <a name="using-sort-order-in-clr-table-valued-functions"></a>Verwenden der Sortierreihenfolge in CLR-Tabellenwertfunktionen  
 Beachten Sie die folgenden Richtlinien, wenn Sie die ORDER-Klausel in CLR-Tabellenwertfunktionen verwenden:  
  
-   Sie müssen sicherstellen, dass die Ergebnisse immer in der angegebenen Reihenfolge sortiert werden. Wenn die Ergebnisse nicht in der angegebenen Reihenfolge sortiert sind, generiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Fehlermeldung beim Ausführen der Abfrage.  
  
-   Wenn eine ORDER-Klausel angegeben wird, muss die Ausgabe der Tabellenwertfunktion entsprechend der Spaltensortierung (explizit oder implizit) sortiert sein. Wenn (in der DDL für die Tabellenwertfunktion oder über die Datenbanksortierung) beispielsweise Chinesisch für die Spaltensortierung angegeben ist, müssen die zurückgegebenen Ergebnisse entsprechend den Sortierregeln für Chinesisch sortiert werden.  
  
-   Die ORDER-Klausel wird, sofern angegeben, bei der Rückgabe von Ergebnissen immer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft. Dies ist unabhängig davon, ob sie vom Abfrageprozessor zur weiteren Optimierung verwendet wird oder nicht. Verwenden Sie die ORDER-Klausel nur, wenn Sie wissen, dass sie für den Abfrageprozessor nützlich ist.  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageprozessor verwendet die ORDER-Klausel automatisch in den folgenden Fällen:  
  
    -   Bei Einfügeabfragen, bei denen die ORDER-Klausel mit einem Index kompatibel ist.  
  
    -   Bei ORDER BY-Klauseln, die mit der ORDER-Klausel kompatibel sind.  
  
    -   Bei Aggregaten, bei denen GROUP BY mit der ORDER-Klausel kompatibel ist.  
  
    -   Bei DISTINCT-Aggregaten, bei denen verschiedene Spalten mit der ORDER-Klausel kompatibel sind.  
  
 Durch die ORDER-Klausel wird keine bestimmte Ergebnisreihenfolge bei der Ausführung einer SELECT-Abfrage sichergestellt, es sei denn, in der Abfrage selbst ist ebenfalls ORDER BY angegeben. Finden Sie unter [Sys. function_order_columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-function-order-columns-transact-sql.md) Informationen zum Abfragen von Spalten, die in der Sortierreihenfolge für Tabellenwertfunktionen enthalten.  
  
## <a name="metadata"></a>Metadaten  
 In der folgenden Tabelle werden die Systemkatalogsichten aufgelistet, die Sie verwenden können, um Metadaten zu benutzerdefinierten Funktionen zurückzugeben.  
  
|Systemsicht|Description|  
|-----------------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|Siehe Beispiel E im Abschnitt "Beispiele" weiter unten.|  
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Zeigt Informationen zu benutzerdefinierten CLR-Funktionen an.|  
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|Zeigt Informationen zu den Parametern an, die in benutzerdefinierten Funktionen definiert sind.|  
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)|Zeigt die zugrunde liegenden Objekte an, auf die von einer Funktion verwiesen wird.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE FUNCTION-Berechtigung in der Datenbank und die ALTER-Berechtigung für das Schema, in dem die Funktion erstellt wird. Wenn die Funktion einen benutzerdefinierten Typ angibt, wird die EXECUTE-Berechtigung für den Typ benötigt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-a-scalar-valued-user-defined-function-that-calculates-the-iso-week"></a>A. Verwenden einer benutzerdefinierten Skalarwertfunktion zur Berechnung der ISO-Woche  
 Im folgenden Beispiel wird die benutzerdefinierte Funktion `ISOweek` erstellt. Diese Funktion nimmt ein Datumsargument und berechnet die Nummer der ISO-Woche. Damit diese Funktion richtig rechnet, muss `SET DATEFIRST 1` aufgerufen werden, bevor die Funktion aufgerufen wird.  
  
 Das Beispiel zeigt auch das Verwenden der [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) -Klausel, um den Sicherheitskontext angeben, in dem eine gespeicherte Prozedur ausgeführt werden kann. In dem gezeigten Beispiel gibt die Option `CALLER` an, dass die Prozedur im Kontext des Benutzers, der die Prozedur aufruft, ausgeführt wird. Die anderen Optionen, die Sie angeben können, sind SELF, OWNER und *User_name*.  
  
 Im Folgenden wird der Funktionsaufruf aufgeführt. Beachten Sie, dass `DATEFIRST` auf `1` festgelegt ist.  
  
```sql
CREATE FUNCTION dbo.ISOweek (@DATE datetime)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
     DECLARE @ISOweek int;  
     SET @ISOweek= DATEPART(wk,@DATE)+1  
          -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104');  
--Special cases: Jan 1-3 may belong to the previous year  
     IF (@ISOweek=0)   
          SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1   
               AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1;  
--Special case: Dec 29-31 may belong to the next year  
     IF ((DATEPART(mm,@DATE)=12) AND   
          ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28))  
          SET @ISOweek=1;  
     RETURN(@ISOweek);  
END;  
GO  
SET DATEFIRST 1;  
SELECT dbo.ISOweek(CONVERT(DATETIME,'12/26/2004',101)) AS 'ISO Week';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
``` 
ISO Week  
----------------  
52  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. Erstellen einer Inline-Tabellenwertfunktion  
 Das folgende Beispiel gibt eine Inline-Tabellenwertfunktion in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurück. Es gibt drei Spalten `ProductID`, `Name` sowie das Aggregat der Jahr-bis-heute Summen nach Geschäft als `YTD Total` für jedes Produkt, das an das Geschäft verkauft wurde.  
  
```sql  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```

 Rufen Sie die Funktion mit dieser Abfrage auf.    

```sql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
### <a name="c-creating-a-multi-statement-table-valued-function"></a>C. Erstellen einer Tabellenwertfunktion mit mehreren Anweisungen  
 Im folgenden Beispiel wird die Tabellenwertfunktion `fn_FindReports(InEmpID)` in der AdventureWorks2012-Datenbank erstellt. Wenn der Funktion eine gültige Mitarbeiter-ID bereitgestellt wird, gibt sie eine Tabelle zurück, die allen Mitarbeitern entspricht, die dem Mitarbeiter entweder direkt oder indirekt unterstellt sind. Die Funktion verwendet eine rekursive Abfrage (Common Table Expression, CTE), um eine hierarchische Mitarbeiterliste zu erstellen. Weitere Informationen zu rekursiven CTEs finden Sie unter [WITH Common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
```sql  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        -- Get the initial list of Employees for Manager n
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0   
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        -- Join recursive member to anchor
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1   
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);   
  
GO  
```  
  
### <a name="d-creating-a-clr-function"></a>D. Erstellen einer CLR-Funktion  
 Das Beispiel erstellt die CLR-Funktion `len_s`. Bevor die Funktion erstellt wird, wird die Assembly `SurrogateStringFunction.dll` in der lokalen Datenbank registriert.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
DECLARE @SamplesPath nvarchar(1024);  
-- You may have to modify the value of this variable if you have  
-- installed the sample in a location other than the default location.  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 
                                              'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
    FROM master.sys.database_files   
    WHERE name = 'master';  
  
CREATE ASSEMBLY [SurrogateStringFunction]  
FROM @SamplesPath + 'StringManipulate\CS\StringManipulate\bin\debug\SurrogateStringFunction.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION [dbo].[len_s] (@str nvarchar(4000))  
RETURNS bigint  
AS EXTERNAL NAME [SurrogateStringFunction].[Microsoft.Samples.SqlServer.SurrogateStringFunction].[LenS];  
GO  
```  
  
 Ein Beispiel zum Erstellen einer CLR-Tabellenwertfunktion, finden Sie unter [Tabellenfunktionen](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md).  
  
### <a name="e-displaying-the-definition-of-includetsqlincludestsql-mdmd-user-defined-functions"></a>E. Anzeigen der Definition [!INCLUDE[tsql](../../includes/tsql-md.md)] von benutzerdefinierten Funktionen  
  
```sql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o ON m.object_id = o.object_id   
    AND type IN ('FN', 'IF', 'TF');  
GO  
```  
  
 Die Definition von Funktionen, die mithilfe der ENCRYPTION-Option erstellt wurden, können nicht mit sys.sql_modules angezeigt werden. Im Gegensatz dazu werden andere Informationen zu den verschlüsselten Funktionen jedoch angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [DROP FUNCTION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [OBJECTPROPERTYEX &#40; Transact-SQL &#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Benutzerdefinierte CLR-Funktionen](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Erstellen Sie die SICHERHEITSRICHTLINIE &#40; Transact-SQL &#41;](../../t-sql/statements/create-security-policy-transact-sql.md)  
  
 

