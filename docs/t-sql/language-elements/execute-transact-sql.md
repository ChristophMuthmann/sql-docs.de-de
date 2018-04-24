---
title: EXECUTE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EXEC
- EXECUTE_TSQL
- EXECUTE
- EXEC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- command strings [SQL Server]
- extended stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- Transact-SQL statements, executing
- strings [SQL Server], executing
- statements [SQL Server], executing
- context switching [SQL Server], execution context
- user-defined functions [SQL Server], executing
- character strings [SQL Server], executing
- switching execution context
- EXECUTE statement
ms.assetid: bc806b71-cc55-470a-913e-c5f761d5c4b7
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5246803f6ef63d130a0af894fb4230fad8644ae9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="execute-transact-sql"></a>EXECUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Führt eine Befehlszeichenfolge oder eine Zeichenfolge in einem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batch oder einem der folgenden Module aus: gespeicherte Systemprozedur, benutzerdefinierte gespeicherte Prozedur, gespeicherte CLR-Prozedur, benutzerdefinierte Skalarwertfunktion oder erweiterte gespeicherte Prozedur. Die EXECUTE-Anweisung kann zum Senden von Pass-Through-Befehlen an Verbindungsserver verwendet werden. Darüber hinaus kann der Kontext, in dem eine Zeichenfolge oder ein Befehl ausgeführt wird, explizit festgelegt werden. Metadaten für das Resultset können mit den WITH RESULT SETS-Optionen definiert werden.
  
> [!IMPORTANT]  
>  Bevor Sie EXECUTE mit einer Zeichenfolge aufrufen, sollten Sie die Zeichenfolge überprüfen. Führen Sie auf keinen Fall einen aus Benutzereingaben erstellten Befehl aus, der nicht zuvor überprüft wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name [ ;number ] | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH <execute_option> [ ,...n ] ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS { LOGIN | USER } = ' name ' ]  
[;]  
  
Execute a pass-through command against a linked server  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'command_string [ ? ]' } [ + ...n ]  
        [ { , { value | @variable [ OUTPUT ] } } [ ...n ] ]  
    )   
    [ AS { LOGIN | USER } = ' name ' ]  
    [ AT linked_server_name ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML   
}  
```  
  
```  
-- In-Memory OLTP   

Execute a natively compiled, scalar user-defined function  
[ { EXEC | EXECUTE } ]   
    {   
      [ @return_status = ]   
      { module_name | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable   
                           | [ DEFAULT ]   
                           }  
        ]   
      [ ,...n ]   
      [ WITH <execute_option> [ ,...n ] ]   
    }  
<execute_option>::=  
{  
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}  
```  
  
```  
-- Syntax for Azure SQL Database   
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name  | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH RECOMPILE ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS {  USER } = ' name ' ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML  
  
```  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Execute a stored procedure  
[ { EXEC | EXECUTE } ]  
    procedure_name   
        [ { value | @variable [ OUT | OUTPUT ] } ] [ ,...n ] }  
[;]  
  
-- Execute a SQL string  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'tsql_string' } [ +...n ] )  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 @*return_status*  
 Eine optionale ganzzahlige Variable, die den Rückgabestatus eines Moduls speichert. Diese Variable muss im Batch, in der gespeicherten Prozedur oder in der Funktion deklariert werden, bevor sie in einer EXECUTE-Anweisung verwendet wird.  
  
 Bei der Verwendung zum Aufrufen einer benutzerdefinierten Skalarwertfunktion ist für die @*return_status*-Variable jeder skalare Datentyp möglich.  
  
 *module_name*  
 Der vollqualifizierte oder nicht vollqualifizierte Name der aufzurufenden gespeicherten Prozedur oder benutzerdefinierten Skalarwertfunktion. Modulnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Bei den Namen von erweiterten gespeicherten Prozeduren wird immer nach Groß-/Kleinschreibung unterschieden, unabhängig von der Sortierung des Servers.  
  
 Ein Benutzer kann ein in einer anderen Datenbank erstelltes Modul ausführen, wenn er Besitzer des Moduls ist oder die entsprechende Berechtigung dafür hat, es in dieser Datenbank auszuführen. Ein Benutzer kann ein Modul auf einem anderen Server mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen, wenn er die entsprechende Berechtigung besitzt, diesen Server zu verwenden (Remotezugriff) und das Modul in dieser Datenbank auszuführen. Wird ein Servername, aber kein Datenbankname angegeben, sucht [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] das Modul in der Standarddatenbank des Benutzers.  
  
 ;*number*  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Eine optionale ganze Zahl zum Gruppieren von Prozeduren mit dem gleichen Namen. Dieser Parameter wird nicht bei erweiterten gespeicherten Prozeduren verwendet.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Weitere Informationen zu Prozedurgruppen finden Sie unter [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 @*module_name_var*  
 Der Name einer lokal definierten Variablen, die den Namen eines Moduls darstellt.  
  
 Dies kann eine Variable sein, die den Namen einer nativ kompilierten benutzerdefinierten Skalarfunktion enthält.  
  
 @*parameter*  
 Der Parameter für *module_name*, wie er im Modul definiert ist. Parameternamen muss das @-Zeichen vorangestellt werden. Wird das Format @*parameter_name*=*value* verwendet, müssen Parameternamen und Konstanten nicht in der Reihenfolge angegeben werden, wie sie im Modul definiert sind. Wenn jedoch das Format @*parameter_name*=*value* für einen Parameter verwendet wird, ist dies auch für alle nachfolgenden Parameter erforderlich.  
  
 Für Parameter sind standardmäßig NULL-Werte zugelassen.  
  
 *value*  
 Der Wert des Parameters, der an das Modul oder den Pass-Through-Befehl übergeben werden soll. Wenn keine Parameternamen angegeben werden, müssen die Parameterwerte in der Reihenfolge angegeben werden, in der sie im Modul definiert sind.  
  
 Wenn Sie Pass-Through-Befehle für Verbindungsserver ausführen, hängt die Reihenfolge der Parameterwerte vom OLE DB-Anbieter des Verbindungsservers ab. Die meisten OLE DB-Anbieter binden Werte von links nach rechts an Parameter.  
  
 Wenn der Wert eines Parameters ein Objektname oder eine Zeichenfolge ist oder durch den Namen einer Datenbank oder eines Schemas qualifiziert ist, dann muss der gesamte Name in einfache Anführungszeichen eingeschlossen werden. Ist der Wert eines Parameters ein Schlüsselwort, muss das Schlüsselwort in doppelte Anführungszeichen eingeschlossen werden.  
  
 Falls im Modul ein Standardwert definiert ist, kann ein Benutzer das Modul ohne Angabe von Parametern ausführen.  
  
 Der Standardwert kann auch NULL sein. Im Allgemeinen gibt die Moduldefinition die Aktion an, die ausgeführt werden soll, wenn ein Parameter den Wert NULL hat.  
  
 @*variable*  
 Die Variable, die einen Parameter oder einen Rückgabeparameter speichert.  
  
 OUTPUT  
 Gibt an, dass das Modul oder die Befehlszeichenfolge einen Parameter zurückgibt. Der entsprechende Parameter im Modul oder in der Befehlszeichenfolge muss ebenfalls mit dem OUTPUT-Schlüsselwort erstellt worden sein. Dieses Schlüsselwort sollte verwendet werden, wenn Cursorvariablen als Parameter verwendet werden.  
  
 Wenn *value* als OUTPUT eines Moduls definiert ist, das für einen Verbindungsserver ausgeführt wird, werden alle vom OLE DB-Anbieter am entsprechenden @*parameter* vorgenommenen Änderungen am Ende der Modulausführung wieder in die Variable kopiert.  
  
 Wenn OUTPUT-Parameter verwendet werden und die Rückgabewerte in anderen Anweisungen innerhalb des aufrufenden Batches oder Moduls verwendet werden sollen, dann muss der Wert des Parameters als Variable übergeben werden, z.B. im Format @*parameter* = @*variable*. Sie können ein Modul nicht mit der Angabe von OUTPUT für einen Parameter ausführen, der nicht als OUTPUT-Parameter im Modul definiert wurde. Konstanten können nicht mit OUTPUT an ein Modul übergeben werden; der Rückgabeparameter erfordert einen Variablennamen. Vor dem Ausführen der Prozedur muss der Datentyp der Variablen deklariert und ihr ein Wert zugewiesen werden.  
  
 Wenn EXECUTE für eine remote gespeicherte Prozedur verwendet wird, oder um einen Pass-Through-Befehl für einen Verbindungsserver auszuführen, können OUTPUT-Parameter nicht einen der LOB-Datentypen (Large Object) aufweisen.  
  
 Rückgabeparameter können von einem beliebigen Datentyp außer den LOB-Datentypen sein.  
  
 DEFAULT  
 Gibt den im Modul definierten Standardwert des Parameters an. Wenn das Modul einen Wert für einen Parameter erwartet, der keinen definierten Standardwert aufweist, und entweder ein Parameter fehlt oder das DEFAULT-Schlüsselwort angegeben ist, tritt ein Fehler auf.  
  
 @*string_variable*  
 Der Name einer lokalen Variablen. @*string_variable* kann den Datentyp **char**, **varchar**, **nchar** oder **nvarchar** aufweisen. Hierzu zählen auch die **(max)**-Datentypen.  
  
 [N] '*tsql_string*'  
 Eine konstante Zeichenfolge. *tsql_string* kann einen beliebigen **nvarchar**- oder **varchar**-Datentyp aufweisen. Wird das N angegeben, wird die Zeichenfolge als Datentyp **nvarchar** interpretiert.  
  
 AS \<context_specification>  
 Gibt den Kontext an, in dem die Anweisung ausgeführt wird.  
  
 Anmeldung  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt an, dass der Kontext, der als Identität angenommen werden soll, ein Anmeldename ist. Der Identitätswechselbereich ist der Server.  
  
 Benutzer  
 Gibt an, dass der Kontext, der als Identität angenommen werden soll, ein Benutzer in der aktuellen Datenbank ist. Der Identitätswechselbereich ist auf die aktuelle Datenbank beschränkt. Bei einem Kontextwechsel zu einem Datenbankbenutzer werden die Berechtigungen auf Serverebene dieses Benutzers nicht geerbt.  
  
> [!IMPORTANT]  
>  Während der Kontextwechsel zu dem Datenbankbenutzer aktiv ist, wird bei jedem Zugriffsversuch auf Ressourcen außerhalb der Datenbank für die Anweisung ein Fehler gemeldet. Hierzu zählen USE-*Datenbankanweisungen*, verteilte Abfragen und Abfragen, die mit drei- oder vierteiligen Bezeichnern auf eine andere Datenbank verweisen.  
  
 '*name*'  
 Ein gültiger Benutzer- oder Anmeldename. *name* muss ein Mitglied der festen Serverrolle „sysadmin“ sein oder als Prinzipal in [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) bzw. [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vorhanden sein.  
  
 *name* darf kein integriertes Konto sein, wie z.B. NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService oder NT AUTHORITY\LocalSystem.  
  
 Weitere Informationen finden Sie unter [Angeben eines Benutzer- oder Anmeldenamens](#_user) weiter unten in diesem Thema.  
  
 [N] '*command_string*'  
 Eine Konstantenzeichenfolge, die den Befehl enthält, der über den Verbindungsserver übergeben werden soll. Wird das N angegeben, wird die Zeichenfolge als Datentyp **nvarchar** interpretiert.  
  
 [?]  
 Gibt Parameter an, deren Werte im \<arg-list>-Parameter von Pass-Through-Befehlen bereitgestellt werden, die in einer EXEC('…', \<arg-list>) AT \<linkedsrv>-Anweisung verwendet werden.  
  
 AT *linked_server_name*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt an, dass *command_string* für *linked_server_name* ausgeführt wird und dass Ergebnisse ggf. an den Client zurückgegeben werden. *linked_server_name* muss auf die Definition eines vorhandenen Verbindungsservers auf dem lokalen Server verweisen. Verbindungsserver werden mithilfe von [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) definiert.  
  
 WITH \<execute_option>  
 Mögliche Ausführungsoptionen. Die RESULT SETS-Optionen können nicht in einer INSERT…EXEC-Anweisung angegeben werden.  
  
|Begriff|Definition|  
|----------|----------------|  
|RECOMPILE|Erzwingt, dass ein neuer Abfrageplan kompiliert, verwendet und nach der Ausführung des Moduls verworfen wird. Falls bereits ein Abfrageplan für das Modul vorhanden ist, verbleibt dieser Plan im Cache.<br /><br /> Verwenden Sie diese Option, wenn der von Ihnen angegebene Parameter atypisch ist oder sich die Daten erheblich geändert haben. Diese Option wird nicht bei erweiterten gespeicherten Prozeduren verwendet. Es wird empfohlen, diese Option nur selten zu verwenden, da sie aufwändig ist.<br /><br /> **Hinweis:** Sie können WITH RECOMPILE nicht verwenden, wenn Sie eine gespeicherte Prozedur aufrufen, die OPENDATASOURCE-Syntax verwendet. Die WITH RECOMPILE-Option wird ignoriert, wenn ein vierteiliger Objektname angegeben wird.<br /><br /> **Hinweis:** RECOMPILE wird für nativ kompilierte benutzerdefinierte Skalarfunktionen nicht unterstützt. Wenn Sie eine erneute Kompilierung durchführen müssen, verwenden Sie [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md).|  
|**RESULT SETS UNDEFINED**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Bei dieser Option ist nicht sichergestellt, dass, und, wenn ja, welche Ergebnisse zurückgegeben werden, und es wird keine Definition bereitgestellt. Die Anweisung wird ohne Fehler ausgeführt, wenn Ergebnisse zurückgegeben werden oder wenn keine Ergebnisse zurückgegeben werden. RESULT SETS UNDEFINED ist das Standardverhalten, wenn keine result_sets_option angegeben wird.<br /><br /> Diese Option ist bei interpretierten benutzerdefinierten Skalarfunktionen und bei nativ kompilierten benutzerdefinierten Skalarfunktionen nicht funktionsfähig, da die Funktionen niemals ein Resultset zurückgeben.|  
|RESULT SETS NONE|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Stellt sicher, dass von der EXECUTE-Anweisung keine Ergebnisse zurückgegeben werden. Wenn Ergebnisse zurückgegeben werden, wird der Batch abgebrochen.<br /><br /> Diese Option ist bei interpretierten benutzerdefinierten Skalarfunktionen und bei nativ kompilierten benutzerdefinierten Skalarfunktionen nicht funktionsfähig, da die Funktionen niemals ein Resultset zurückgeben.|  
|*\<result_sets_definition>*|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Stellt sicher, dass das Ergebnis wie in der result_sets_definition angegeben zurückgegeben wird. Stellen Sie mehrere *result_sets_definition*-Abschnitte für Anweisungen bereit, die mehrere Resultsets zurückgeben. Schließen Sie jede *result_sets_definition* in Klammern ein, jeweils durch Kommas getrennt. Weitere Informationen finden Sie unter \<result_sets_definition> weiter unten in diesem Thema.<br /><br /> Diese Option führt bei nativ kompilierten benutzerdefinierten Skalarfunktionen immer zu einem Fehler, da die Funktionen niemals ein Resultset zurückgeben.|
  
\<result_sets_definition> **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
 Beschreibt die von den ausgeführten Anweisungen zurückgegebenen Resultsets. Die Klauseln der result_sets_definition haben folgende Bedeutung:  
  
|Begriff|Definition|  
|----------|----------------|  
|{<br /><br /> column_name<br /><br /> data_type<br /><br /> [ COLLATE collation_name]<br /><br /> [NULL &#124; NOT NULL]<br /><br /> }|Siehe Tabelle unten.|  
|db_name|Der Name der Datenbank mit der Tabelle, Sicht oder Tabellenwertfunktion.|  
|schema_name|Der Name des Schemas, das im Besitz der Tabelle, Sicht oder Tabellenwertfunktion ist.|  
|table_name &#124; view_name &#124; table_valued_function_name|Gibt an, dass die zurückgegebenen Spalten den in der Tabelle, Sicht oder Tabellenwertfunktion genannten entsprechen. Tabellenvariablen, temporäre Tabellen und Synonyme werden in AS-Objektsyntax nicht unterstützt.|  
|AS TYPE [schema_name.]table_type_name|Gibt an, dass die zurückgegebenen Spalten den im Tabellentyp angegebenen entsprechen.|  
|AS FOR XML|Gibt an, dass die XML-Ergebnisse aus der Anweisung oder gespeicherten Prozedur, die von der EXECUTE-Anweisung aufgerufen wird, in das Format konvertiert wird, als wären sie durch eine "SELECT ... FOR XML …"-Anweisung generiert worden. verwendet. Die gesamte Formatierung aus den Typdirektiven in der ursprünglichen Anweisung werden entfernt, und die zurückgegebenen Ergebnisse werden so angezeigt, als wäre keine Typdirektive angegeben worden. AS FOR XML konvertiert keine tabellarischen Nicht-XML-Ergebnisse aus der ausgeführten Anweisung bzw. der gespeicherten Prozedur in XML.|  
  
|Begriff|Definition|  
|----------|----------------|  
|column_name|Die Namen der einzelnen Spalten. Wenn sich die Anzahl der Spalten vom Resultset unterscheidet, tritt ein Fehler auf, und der Batch wird abgebrochen. Wenn sich der Name einer Spalte vom Resultset unterscheidet, wird der zurückgegebene Spaltenname auf den definierten Namen festgelegt.|  
|data_type|Die Datentypen der einzelnen Spalten. Wenn die Datentypen abweichen, wird eine implizite Konvertierung in den definierten Datentyp ausgeführt. Wenn die Konvertierung fehlschlägt, wird der Batch abgebrochen|  
|COLLATE collation_name|Die Sortierung der einzelnen Spalten. Wenn es eine Nichtübereinstimmung bei der Sortierung gibt, wird eine implizite Sortierung versucht. Wenn diese fehlschlägt, wird der Batch abgebrochen.|  
|NULL &#124; NOT NULL|Die NULL-Zulässigkeit der einzelnen Spalten. Wenn die definierte NULL-Zulässigkeit NOT NULL ist, und die zurückgegebenen Daten NULLS enthalten, tritt ein Fehler auf, und der Batch wird abgebrochen. Wenn dieses Element nicht angegeben ist, entspricht der Standardwert der Einstellung der Optionen ANSI_NULL_DFLT_ON und ANSI_NULL_DFLT_OFF.|  
  
 Das tatsächliche Resultset, das während der Ausführung zurückgegeben wird, kann sich vom Ergebnis unterscheiden, das mit der WITH RESULT SETS-Klausel auf eine der folgenden Arten definiert wurde: Anzahl der Resultsets, Anzahl der Spalten, Spaltenname, NULL-Zulässigkeit und Datentyp. Wenn die Anzahl der Resultsets abweicht, tritt ein Fehler auf, und der Batch wird abgebrochen.  
  
## <a name="remarks"></a>Remarks  
 Parameter können entweder mit *value* oder mit @*parameter_name*=*value* angegeben werden. angegeben werden. Ein Parameter ist nicht Teil einer Transaktion. Deshalb wird der Wert eines Parameters, der in einer Transaktion geändert wird, nicht wieder auf seinen ursprünglichen Wert zurückgesetzt, wenn für diese Transaktion später ein Rollback ausgeführt wird. Der Wert, der an den Aufrufer zurückgegeben wird, ist immer der Wert zu dem Zeitpunkt, zu dem das Modul beendet wird.  
  
 Die Schachtelung erfolgt, wenn ein Modul ein anderes Modul aufruft oder verwalteten Code durch Verweis auf ein CLR-Modul (Common Language Runtime), einen benutzerdefinierten Typ oder ein Aggregat ausführt. Die Schachtelungsebene wird um eins erhöht, wenn das aufgerufene Modul oder der Verweis auf den verwalteten Code mit der Ausführung beginnt, und wird wieder um eins erniedrigt, wenn das aufgerufene Modul oder der Verweis auf den verwalteten Code beendet ist. Ein Überschreiten der maximal möglichen 32 Schachtelungsebenen führt zu einem Fehler der gesamten Aufrufskette. Die aktuelle Schachtelungsebene wird in der @@NESTLEVEL-Systemfunktion gespeichert.  
  
 Da remote gespeicherte Prozeduren und erweiterte gespeicherte Prozeduren außerhalb des Bereichs einer Transaktion liegen (es sei denn, sie werden innerhalb einer BEGIN DISTRIBUTED TRANSACTION-Anweisung ausgegeben oder mit diversen Konfigurationsoptionen verwendet), kann für Befehle, die durch das Aufrufen solcher Prozeduren ausgeführt werden, kein Rollback ausgeführt werden. Weitere Informationen finden Sie unter [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) und unter [Verteilte Transaktion beginnen &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 Wird beim Verwenden von Cursorvariablen eine Prozedur ausgeführt, die eine Cursorvariable übergibt, für die ein Cursor zugeordnet ist, tritt ein Fehler auf.  
  
 Sie müssen das EXECUTE-Schlüsselwort beim Ausführen von Modulen nicht angeben, wenn es sich dabei um die erste Anweisung in einem Batch handelt.  
  
 Weitere Informationen zu gespeicherten CLR-Prozeduren finden Sie unter Gespeicherte CLR-Prozeduren.  
  
## <a name="using-execute-with-stored-procedures"></a>Verwenden von EXECUTE mit gespeicherten Prozeduren  
 Sie müssen das EXECUTE-Schlüsselwort beim Ausführen von gespeicherten Prozeduren nicht angeben, wenn es sich dabei um die erste Anweisung in einem Batch handelt.  
  
 Gespeicherte Systemprozeduren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beginnen mit den Zeichen sp_. Sie werden physisch in der [Ressourcendatenbank](../../relational-databases/databases/resource-database.md) gespeichert, werden aber logisch im sys-Schema jeder Systemdatenbank und benutzerdefinierten Datenbank angezeigt. Es wird empfohlen, den Namen der gespeicherten Prozedur mit dem sys-Schemanamen zu qualifizieren, wenn Sie eine gespeicherte Prozedur ausführen, entweder in einem Batch oder innerhalb eines Moduls, wie etwa eine benutzerdefinierte gespeicherte Prozedur oder Funktion.  
  
 Erweiterte gespeicherte Systemprozeduren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beginnen mit den Zeichen xp_ und sind im dbo-Schema der master-Datenbank enthalten. Es wird empfohlen, den Namen der gespeicherten Prozedur mit master.dbo zu qualifizieren, wenn Sie eine erweiterte gespeicherte Prozedur ausführen, entweder in einem Batch oder innerhalb eines Moduls, wie etwa eine benutzerdefinierte gespeicherte Prozedur oder Funktion.  
  
 Es wird empfohlen, den Namen der gespeicherten Prozedur mit einem Schemanamen zu qualifizieren, wenn Sie eine benutzerdefinierte gespeicherte Prozedur ausführen, entweder in einem Batch oder innerhalb eines Moduls, wie etwa eine benutzerdefinierte gespeicherte Prozedur oder Funktion. Wir raten davon ab, für eine benutzerdefinierte gespeicherte Prozedur den gleichen Namen wie für eine gespeicherte Systemprozedur zu verwenden. Weitere Informationen zum Ausführen gespeicherter Prozeduren finden Sie unter [Ausführen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/execute-a-stored-procedure.md).  
  
## <a name="using-execute-with-a-character-string"></a>Verwenden von EXECUTE mit einer Zeichenfolge  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind Zeichenfolgen auf 8.000 Bytes beschränkt. Deshalb müssen lange Zeichenfolgen für die dynamische Ausführung verkettet werden. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können die Datentypen **varchar(max)** und **nvarchar(max)** angegeben werden, die Zeichenfolgen mit bis zu 2 Gigabyte an Daten zulassen.  
  
 Eine Änderung des Datenbankkontexts dauert nur so lange, bis die jeweilige EXECUTE-Anweisung beendet ist. Beispielsweise lautet nach der Ausführung von `EXEC` in der folgenden Anweisung der Datenbankkontext master.  
  
```sql  
USE master; EXEC ('USE AdventureWorks2012; SELECT BusinessEntityID, JobTitle FROM HumanResources.Employee;');  
```  
  
## <a name="context-switching"></a>Kontextwechsel  
 Mithilfe der `AS { LOGIN | USER } = ' name '`-Klausel können Sie den Ausführungskontext einer dynamischen Anweisung wechseln. Wenn der Kontextwechsel als `EXECUTE ('string') AS <context_specification>` angegeben wird, ist die Dauer des Kontextwechsels auf den Bereich der ausgeführten Abfrage beschränkt.  
  
###  <a name="_user"></a> Angeben eines Benutzer- oder Anmeldenamens  
 Der in `AS { LOGIN | USER } = ' name '` angegebene Benutzer oder Anmeldename muss als Prinzipal in sys.database_principals bzw. sys.server_principals vorhanden sein. Andernfalls wird für die Anweisung ein Fehler gemeldet. Zudem müssen für den Prinzipal IMPERSONATE-Berechtigungen erteilt worden sein. Falls der Aufrufer nicht der Datenbankbesitzer oder ein Mitglied der festen Serverrolle sysadmin ist, muss der Prinzipal sogar dann vorhanden sein, wenn der Benutzer als Windows-Gruppenmitglied auf die Datenbank oder Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugreift. Stellen Sie sich z. B. folgende Bedingungen vor:  
  
-   Die CompanyDomain\SQLUsers-Gruppe verfügt über Zugriff auf die Sales-Datenbank.  
  
-   CompanyDomain\SqlUser1 ist Mitglied von SQLUsers und besitzt daher implizit Zugriff auf die Sales-Datenbank.  
  
 Obwohl CompanyDomain\SqlUser1 über die Mitgliedschaft in der SQLUsers-Gruppe Zugriff auf die Datenbank hat, wird für die Anweisung `EXECUTE @string_variable AS USER = 'CompanyDomain\SqlUser1'` ein Fehler gemeldet, da `CompanyDomain\SqlUser1` nicht als Prinzipal in der Datenbank vorhanden ist.  
  
### <a name="best-practices"></a>Bewährte Methoden  
 Geben Sie einen Anmeldenamen oder einen Benutzer an, der die mindestens erforderlichen Berechtigungen zum Ausführen der in der Anweisung oder im Modul definierten Vorgänge aufweist. Geben Sie z. B. keinen Anmeldenamen an, der über Berechtigungen auf Serverebene verfügt, wenn nur Berechtigungen auf Datenbankebene notwendig sind; oder geben Sie nur ein Datenbankbesitzer-Konto an, wenn diese Berechtigungen erforderlich sind.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen der EXECUTE-Anweisung sind keine Berechtigungen erforderlich. Es sind jedoch Berechtigungen für die sicherungsfähigen Elemente erforderlich, auf die in der EXECUTE-Zeichenfolge verwiesen wird. Wenn z. B. die Zeichenfolge eine INSERT-Anweisung enthält, benötigt der Aufrufer der EXECUTE-Anweisung die INSERT-Berechtigung für die Zieltabelle. Berechtigungen werden überprüft, wenn die EXECUTE-Anweisung erreicht wird, selbst wenn die EXECUTE-Anweisung innerhalb eines Moduls enthalten ist.  
  
 EXECUTE-Berechtigungen für ein Modul liegen standardmäßig beim Besitzer dieses Moduls. Der Besitzer kann die Berechtigungen an andere Benutzer übertragen. Wird ein Modul ausgeführt, das eine Zeichenfolge ausführt, werden Berechtigungen im Kontext des Benutzers geprüft, der das Modul ausführt, nicht im Kontext des Benutzers, der das Modul erstellt hat. Wenn jedoch derselbe Benutzer Besitzer des aufrufenden Moduls und des aufgerufenen Moduls ist, wird die EXECUTE-Berechtigung für das zweite Modul nicht mehr überprüft.  
  
 Wenn das Modul auf andere Datenbankobjekte zugreift, ist die Ausführung erfolgreich, wenn Sie die EXECUTE-Berechtigung für das Modul haben und eine der folgenden Bedingungen zutrifft:  
  
-   Das Modul ist als EXECUTE AS USER oder SELF gekennzeichnet, und der Modulbesitzer besitzt die entsprechenden Berechtigungen für das Objekt, auf das verwiesen wird. Weitere Informationen zum Identitätswechsel innerhalb eines Moduls finden Sie unter [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
-   Das Modul ist als EXECUTE AS CALLER gekennzeichnet, und Sie besitzen die entsprechenden Berechtigungen für das Objekt.  
  
-   Das Modul ist als EXECUTE AS *user_name* gekennzeichnet, und *user_name* verfügt über die entsprechenden Berechtigungen für das Objekt.  
  
### <a name="context-switching-permissions"></a>Berechtigungen für den Kontextwechsel  
 Um EXECUTE AS für einen Anmeldenamen anzugeben, benötigt der Aufrufer IMPERSONATE-Berechtigungen für den angegebenen Anmeldenamen. Um EXECUTE AS für einen Datenbankbenutzer anzugeben, benötigt der Aufrufer IMPERSONATE-Berechtigungen für den angegebenen Benutzernamen. Wenn kein Ausführungskontext angegeben ist oder wenn EXECUTE AS CALLER angegeben ist, sind keine IMPERSONATE-Berechtigungen erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-execute-to-pass-a-single-parameter"></a>A. Verwenden von EXECUTE, um einen einzelnen Parameter zu übergeben  
 Die gespeicherte Prozedur `uspGetEmployeeManagers` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank erwartet einen Parameter (`@EmployeeID`). In den folgenden Beispielen wird die gespeicherte Prozedur `uspGetEmployeeManagers` mit `Employee ID 6` als zugehörigem Parameterwert ausgeführt.  
  
```  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
 Die Variable kann bei der Ausführung auch ausdrücklich benannt werden:  
  
```  
EXEC dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
 Falls es sich bei der folgenden Anweisung um die erste Anweisung in einem Batch oder in einem **osql**- oder **sqlcmd**-Skript handelt, ist die Angabe von EXEC nicht erforderlich.  
  
```  
dbo.uspGetEmployeeManagers 6;  
GO  
--Or  
dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
### <a name="b-using-multiple-parameters"></a>B. Verwenden mehrerer Parameter  
 Im folgenden Beispiel wird die gespeicherte Prozedur `spGetWhereUsedProductID` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank ausgeführt. Sie übergibt zwei Parameter: Der erste Parameter ist eine Produkt-ID (`819`), und der zweite Parameter, `@CheckDate,` ist ein `datetime`-Wert.  
  
```  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
### <a name="c-using-execute-tsqlstring-with-a-variable"></a>C. Verwenden von EXECUTE 'tsql_string' mit einer Variablen  
 Das folgende Beispiel zeigt, wie `EXECUTE` dynamisch erstellte Zeichenfolgen behandelt, die Variablen enthalten. In diesem Beispiel wird der `tables_cursor`-Cursor erstellt, der eine Liste aller benutzerdefinierten Tabellen in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank enthält. Anschließend werden mithilfe dieser Liste alle Indizes für die Tabellen neu erstellt.  
  
```  
DECLARE tables_cursor CURSOR  
   FOR  
   SELECT s.name, t.name   
   FROM sys.objects AS t  
   JOIN sys.schemas AS s ON s.schema_id = t.schema_id  
   WHERE t.type = 'U';  
OPEN tables_cursor;  
DECLARE @schemaname sysname;  
DECLARE @tablename sysname;  
FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN;  
   EXECUTE ('ALTER INDEX ALL ON ' + @schemaname + '.' + @tablename + ' REBUILD;');  
   FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
END;  
PRINT 'The indexes on all tables have been rebuilt.';  
CLOSE tables_cursor;  
DEALLOCATE tables_cursor;  
GO  
  
```  
  
### <a name="d-using-execute-with-a-remote-stored-procedure"></a>D. Verwenden von EXECUTE mit einer remote gespeicherten Prozedur  
 Im folgenden Beispiel wird die gespeicherte Prozedur `uspGetEmployeeManagers` auf dem Remoteserver `SQLSERVER1` ausgeführt und der Rückgabestatus, der anzeigt, ob die Ausführung erfolgreich war oder nicht, in `@retstat` gespeichert.  
  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
DECLARE @retstat int;  
EXECUTE @retstat = SQLSERVER1.AdventureWorks2012.dbo.uspGetEmployeeManagers @BusinessEntityID = 6;  
```  
  
### <a name="e-using-execute-with-a-stored-procedure-variable"></a>E. Verwenden von EXECUTE mit einer Variablen für eine gespeicherte Prozedur  
 Das folgende Beispiel erstellt eine Variable, die den Namen einer gespeicherten Prozedur darstellt.  
  
```sql  
DECLARE @proc_name varchar(30);  
SET @proc_name = 'sys.sp_who';  
EXEC @proc_name;  
  
```  
  
### <a name="f-using-execute-with-default"></a>F. Verwenden von EXECUTE mit DEFAULT  
 Das folgende Beispiel erstellt eine gespeicherte Prozedur mit Standardwerten für den ersten und dritten Parameter. Beim Ausführen der Prozedur werden diese Standardwerte für den ersten und dritten Parameter eingefügt, falls beim Aufruf kein Wert übergeben oder DEFAULT angegeben wird. Beachten Sie, wie verschiedenartig das `DEFAULT`-Schlüsselwort verwendet werden kann.  
  
```  
IF OBJECT_ID(N'dbo.ProcTestDefaults', N'P')IS NOT NULL  
   DROP PROCEDURE dbo.ProcTestDefaults;  
GO  
-- Create the stored procedure.  
CREATE PROCEDURE dbo.ProcTestDefaults (  
@p1 smallint = 42,   
@p2 char(1),   
@p3 varchar(8) = 'CAR')  
AS   
   SET NOCOUNT ON;  
   SELECT @p1, @p2, @p3  
;  
GO  
  
```  
  
 Die gespeicherte Prozedur `Proc_Test_Defaults` kann in verschiedenen Kombinationen ausgeführt werden.  
  
```  
-- Specifying a value only for one parameter (@p2).  
EXECUTE dbo.ProcTestDefaults @p2 = 'A';  
-- Specifying a value for the first two parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'B';  
-- Specifying a value for all three parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'C', 'House';  
-- Using the DEFAULT keyword for the first parameter.  
EXECUTE dbo.ProcTestDefaults @p1 = DEFAULT, @p2 = 'D';  
-- Specifying the parameters in an order different from the order defined in the procedure.  
EXECUTE dbo.ProcTestDefaults DEFAULT, @p3 = 'Local', @p2 = 'E';  
-- Using the DEFAULT keyword for the first and third parameters.  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'H', DEFAULT;  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'I', @p3 = DEFAULT;  
  
```  
  
### <a name="g-using-execute-with-at-linkedservername"></a>G. Verwenden von EXECUTE mit AT linked_server_name  
 Das folgende Beispiel übergibt eine Befehlszeichenfolge an einen Remoteserver. Der Verbindungsserver `SeattleSales` wird erstellt, der auf eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verweist und eine DDL-Anweisung (`CREATE TABLE`) auf diesem Verbindungsserver ausführt.  
  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
EXECUTE ( 'CREATE TABLE AdventureWorks2012.dbo.SalesTbl   
(SalesID int, SalesName varchar(10)) ; ' ) AT SeattleSales;  
GO  
```  
  
### <a name="h-using-execute-with-recompile"></a>H. Verwenden von EXECUTE WITH RECOMPILE  
 Im folgenden Beispiel wird die gespeicherte Prozedur `Proc_Test_Defaults` ausgeführt und erzwungen, dass ein neuer Abfrageplan kompiliert, verwendet und nach der Ausführung des Moduls verworfen wird.  
  
```  
EXECUTE dbo.Proc_Test_Defaults @p2 = 'A' WITH RECOMPILE;  
GO  
```  
  
### <a name="i-using-execute-with-a-user-defined-function"></a>I. Verwenden von EXECUTE mit einer benutzerdefinierten Funktion  
 Im folgenden Beispiel wird die benutzerdefinierte Skalarfunktion `ufnGetSalesOrderStatusText` in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank ausgeführt. Die `@returnstatus`-Variable wird zum Speichern des Werts verwendet, der von der Funktion zurückgegeben wird. Diese Funktion erwartet einen Eingabeparameter, `@Status`. Dieser ist als Datentyp **tinyint** definiert.  
  
```  
DECLARE @returnstatus nvarchar(15);  
SET @returnstatus = NULL;  
EXEC @returnstatus = dbo.ufnGetSalesOrderStatusText @Status = 2;  
PRINT @returnstatus;  
GO  
```  
  
### <a name="j-using-execute-to-query-an-oracle-database-on-a-linked-server"></a>J. Verwenden von EXECUTE zum Abfragen einer Oracle-Datenbank auf einem Verbindungsserver  
 Das folgende Beispiel führt mehrere `SELECT`-Anweisungen auf dem Oracle-Remoteserver aus. Zunächst wird der Oracle-Server als Verbindungsserver hinzugefügt und der Anmeldename für den Verbindungsserver erstellt.  
  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
-- Setup the linked server.  
EXEC sp_addlinkedserver    
        @server='ORACLE',  
        @srvproduct='Oracle',  
        @provider='OraOLEDB.Oracle',   
        @datasrc='ORACLE10';  
  
EXEC sp_addlinkedsrvlogin   
    @rmtsrvname='ORACLE',  
    @useself='false',   
    @locallogin=null,   
    @rmtuser='scott',   
    @rmtpassword='tiger';  
  
EXEC sp_serveroption 'ORACLE', 'rpc out', true;  
GO  
  
-- Execute several statements on the linked Oracle server.  
EXEC ( 'SELECT * FROM scott.emp') AT ORACLE;  
GO  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', 7902) AT ORACLE;  
GO  
DECLARE @v INT;   
SET @v = 7902;  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', @v) AT ORACLE;  
GO   
```  
  
### <a name="k-using-execute-as-user-to-switch-context-to-another-user"></a>K. Verwenden von EXECUTE AS USER zum Wechseln des Kontexts zu einem anderen Benutzer  
 Das folgende Beispiel führt eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Zeichenfolge aus, mit der eine Tabelle erstellt und die `AS USER`-Klausel zum Umschalten des Ausführungskontexts der Anweisung vom Aufrufer zu `User1` angegeben wird. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] überprüft beim Ausführen der Anweisung die Berechtigungen von `User1`. `User1` muss als Benutzer in der Datenbank vorhanden sein und benötigt die Berechtigung zum Erstellen von Tabellen im `Sales`-Schema. Andernfalls kann die Anweisung nicht ausgeführt werden.  
  
```  
EXECUTE ('CREATE TABLE Sales.SalesTable (SalesID int, SalesName varchar(10));')  
AS USER = 'User1';  
GO  
```  
  
### <a name="l-using-a-parameter-with-execute-and-at-linkedservername"></a>L. Verwenden eines Parameters mit EXECUTE und AT linked_server_name  
 Im folgenden Beispiel wird eine Befehlszeichenfolge an einen Remoteserver übergeben, indem ein Fragezeichen (`?`) als Platzhalter für einen Parameter verwendet wird. Im Beispiel wird zunächst ein Verbindungsserver `SeattleSales` erstellt, der auf eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verweist. Anschließend wird eine `SELECT`-Anweisung auf diesem Verbindungsserver ausgeführt. In der `SELECT`-Anweisung wird das Fragezeichen als Platzhalter für den `ProductID`-Parameter (`952`) verwendet, der hinter der Anweisung angegeben wird.  
  
**Gilt für** : [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
-- Setup the linked server.  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
-- Execute the SELECT statement.  
EXECUTE ('SELECT ProductID, Name   
    FROM AdventureWorks2012.Production.Product  
    WHERE ProductID = ? ', 952) AT SeattleSales;  
GO  
```  
  
### <a name="m-using-execute-to-redefine-a-single-result-set"></a>M. Neudefinieren eines einzelnen Resultsets mithilfe von EXECUTE  
 In einigen der vorangehenden Beispiele wurde `EXEC dbo.uspGetEmployeeManagers 6;` ausgeführt, und 7 Spalten wurden zurückgegeben. Im folgenden Beispiel wird veranschaulicht, wie mit der `WITH RESULT SET`-Syntax die Namen und Datentypen des zurückgebenden Resultsets geändert werden.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```  
EXEC uspGetEmployeeManagers 16  
WITH RESULT SETS  
(   
   ([Reporting Level] int NOT NULL,  
    [ID of Employee] int NOT NULL,  
    [Employee First Name] nvarchar(50) NOT NULL,  
    [Employee Last Name] nvarchar(50) NOT NULL,  
    [Employee ID of Manager] nvarchar(max) NOT NULL,  
    [Manager First Name] nvarchar(50) NOT NULL,  
    [Manager Last Name] nvarchar(50) NOT NULL )  
);  
  
```  
  
### <a name="n-using-execute-to-redefine-a-two-result-sets"></a>N. Neudefinieren zweier Resultsets mithilfe von EXECUTE  
 Wenn Sie eine Anweisung ausführen, die mehr als ein Resultset zurückgibt, definieren Sie jedes erwartete Resultset. Im folgenden Beispiel in [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] wird eine Prozedur erstellt, die zwei Resultsets zurückgibt. Anschließend wird die Prozedur mit der **WITH RESULT SETS**-Klausel ausgeführt, und es werden zwei Resultsetdefinitionen angegeben.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```  
--Create the procedure  
CREATE PROC Production.ProductList @ProdName nvarchar(50)  
AS  
-- First result set  
SELECT ProductID, Name, ListPrice  
    FROM Production.Product  
    WHERE Name LIKE @ProdName;  
-- Second result set   
SELECT Name, COUNT(S.ProductID) AS NumberOfOrders  
    FROM Production.Product AS P  
    JOIN Sales.SalesOrderDetail AS S  
        ON P.ProductID  = S.ProductID   
    WHERE Name LIKE @ProdName  
    GROUP BY Name;  
GO  
  
-- Execute the procedure   
EXEC Production.ProductList '%tire%'  
WITH RESULT SETS   
(  
    (ProductID int,   -- first result set definition starts here  
    Name Name,  
    ListPrice money)  
    ,                 -- comma separates result set definitions  
    (Name Name,       -- second result set definition starts here  
    NumberOfOrders int)  
);  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="example-o-basic-procedure-execution"></a>Beispiel O: Ausführung einfacher Prozeduren  
 Ausführen einer gespeicherten Prozedur:  
  
```  
EXEC proc1;  
```  
  
 Aufrufen einer gespeicherten Prozedur, deren Name zur Laufzeit bestimmt wird:  
  
```  
EXEC ('EXEC ' + @var);  
```  
  
 Aufrufen einer gespeicherten Prozedur aus einer gespeicherten Prozedur:  
  
```  
CREATE sp_first AS EXEC sp_second; EXEC sp_third;  
```  
  
### <a name="example-p-executing-strings"></a>Beispiel P: Ausführen von Zeichenfolgen  
 Ausführen einer SQL-Zeichenfolge:  
  
```  
EXEC ('SELECT * FROM sys.types');  
```  
  
 Ausführen einer geschachtelten Zeichenfolge:  
  
```  
EXEC ('EXEC (''SELECT * FROM sys.types'')');  
```  
  
 Ausführen einer Zeichenfolgenvariablen:  
  
```  
DECLARE @stringVar nvarchar(100);  
SET @stringVar = N'SELECT name FROM' + ' sys.sql_logins';  
EXEC (@stringVar);  
```  
  
### <a name="example-q-procedures-with-parameters"></a>Beispiel Q: Prozeduren mit Parametern  
 Im folgenden Beispiel wird eine Prozedur mit Parametern erstellt, und es werden drei Möglichkeiten zur Ausführung der Prozedur veranschaulicht:  
  
```  
-- Uses AdventureWorks  
  
CREATE PROC ProcWithParameters  
    @name nvarchar(50),  
@color nvarchar (15)  
AS   
SELECT ProductKey, EnglishProductName, Color FROM [dbo].[DimProduct]  
WHERE EnglishProductName LIKE @name  
AND Color = @color;  
GO  
  
-- Executing using positional parameters  
EXEC ProcWithParameters N'%arm%', N'Black';  
-- Executing using named parameters in order  
EXEC ProcWithParameters @name = N'%arm%', @color = N'Black';  
-- Executing using named parameters out of order  
EXEC ProcWithParameters @color = N'Black', @name = N'%arm%';  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [@@NESTLEVEL &#40;Transact-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md)   
 [DEKLARIEREN SIE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [Hilfsprogramm „osql“](../../tools/osql-utility.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md)   
 [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [OPENDATASOURCE (Transact-SQL)](../../t-sql/functions/opendatasource-transact-sql.md)   
 [Benutzerdefinierte Skalarfunktionen für In-Memory-OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)  
  
  
