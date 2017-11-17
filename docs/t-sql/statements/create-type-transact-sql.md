---
title: Erstellen Sie TYPE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/11/2017
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
- sql13.swb.sysdatatype.properties.f1
- CREATE TYPE
- TYPE_TSQL
- TYPE
- CREATE_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [SQL Server], creating
- CLR user-defined types [SQL Server]
- user-defined table types [SQL Server]
- user-defined types [SQL Server], creating
- CREATE TYPE statement
- alias data types [SQL Server], creating
- data types [SQL Server], creating
ms.assetid: 2202236b-e09f-40a1-bbc7-b8cff7488905
caps.latest.revision: 92
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4e7f411871d98fc6854b97478402567017d28222
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-type-transact-sql"></a>CREATE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt einen Aliasdatentyp oder einen benutzerdefinierten Typ in der aktuellen Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Die Implementierung eines Aliasdatentyps basiert auf einem systemeigenen Typ von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ein benutzerdefinierten Typ wird durch eine Klasse einer Assembly im implementiert die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common Language Runtime (CLR). Um einen benutzerdefinierten Typ an seine Implementierung zu binden, muss die CLR-Assembly, die die Implementierung des Typs enthält zunächst in registriert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md).  
  
 Die Option zum Ausführen von CLR-Code ist standardmäßig in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deaktiviert. Erstellen, ändern und Löschen von Datenbankobjekten, die auf verwaltete Codemodule verweisen, aber diese Verweise werden nicht ausgeführt, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , sofern die [Option Clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) aktiviert ist, mithilfe von [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
 
> [!NOTE]  
>  Die .NET Framework-CLR-Integration in SQL Server wird in diesem Thema erläutert. CLR-Integration gilt nicht für Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Disk-Based Type Syntax  
CREATE TYPE [ schema_name. ] type_name  
{   
    FROM base_type   
    [ ( precision [ , scale ] ) ]  
    [ NULL | NOT NULL ]   
  | EXTERNAL NAME assembly_name [ .class_name ]   
  | AS TABLE ( { <column_definition> | <computed_column_definition> }  
        [ <table_constraint> ] [ ,...n ] )    
} [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   
    [ NULL | NOT NULL ]  
    [   
        DEFAULT constant_expression ]   
      | [ IDENTITY [ ( seed ,increment ) ]   
    ]  
    [ ROWGUIDCOL ] [ <column_constraint> [ ...n ] ]   
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
                [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH ( <index_option> [ ,...n ] )   
        ]  
  | CHECK ( logical_expression )   
}   
  
<computed_column_definition> ::=  
  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH ( <index_option> [ ,...n ] )  
        ]  
    | CHECK ( logical_expression )   
]   
  
<table_constraint> ::=  
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
    ( column [ ASC | DESC ] [ ,...n ] )   
        [   
    WITH ( <index_option> [ ,...n ] )   
        ]  
    | CHECK ( logical_expression )   
}   
  
<index_option> ::=  
{  
    IGNORE_DUP_KEY = { ON | OFF }  
}  
```  
  
```  
-- Memory-Optimized Table Type Syntax  
CREATE TYPE [schema_name. ] type_name  
AS TABLE ( { <column_definition> }  
    |  [ <table_constraint> ] [ ,... n ]    
    | [ <table_index> ] [ ,... n ]    } )
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   [ NULL | NOT NULL ]    [  
      [ IDENTITY [ (1 , 1) ]  
    ]  
    [ <column_constraint> [ ... n ] ]    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
{ PRIMARY KEY {   NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count) 
                | NONCLUSTERED } }  
  
< table_constraint > ::=  
{ PRIMARY KEY { NONCLUSTERED HASH (column [ ,... n ] ) 
                   WITH (BUCKET_COUNT = bucket_count) 
               | NONCLUSTERED  (column [ ASC | DESC ] [ ,... n ] )  } }  
  
<column_index> ::=  
  INDEX index_name  
{ { [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count) 
     | NONCLUSTERED } }  
  
< table_index > ::=  
  INDEX constraint_name  
{ { [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count) 
 |  [NONCLUSTERED]  (column [ ASC | DESC ] [ ,... n ] )} }  
  
<table_option> ::=  
{  
    [MEMORY_OPTIMIZED = {ON | OFF}]  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, dem der Aliasdatentyp oder benutzerdefinierte Typ angehört.  
  
 *TYPE_NAME*  
 Der Name des Aliasdatentyps oder benutzerdefinierten Datentyps. Typnamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 *base_type*  
 Ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellte Datentyp, auf denen der Aliasdatentyp basiert. *Base_type* ist **Sysname**, hat keinen Standardwert und kann die folgenden Werte sind möglich:  
  
|||||  
|-|-|-|-|  
|**bigint**|**Binär (**  *n*  **)**|**bit**|**Char (**  *n*  **)**|  
|**Datum**|**datetime**|**datetime2**|**datetimeoffset**|  
|**decimal**|**float**|**image**|**int**|  
|**money**|**NCHAR (**  *n*  **)**|**ntext**|**numeric**|  
|**Nvarchar (**  *n*  &#124; **max)**|**real**|**smalldatetime**|**smallint**|  
|**smallmoney**|**sql_variant**|**text**|**Uhrzeit**|  
|**tinyint**|**uniqueidentifier**|**Varbinary (**  *n*  &#124; **max)**|**Varchar (**  *n*  &#124; **max)**|  
  
 *Base_type* kann außerdem jedes Synonym für Datentypen, das einem dieser Systemdatentypen zugeordnet, sein.  
  
 *precision*  
 Für **decimal** oder **numerischen**, ist eine nicht Negative ganze Zahl, die die maximale Gesamtanzahl von Dezimalstellen angibt, nach links und rechts vom Dezimaltrennzeichen gespeichert werden können. Weitere Informationen finden Sie unter ["Decimal und Numeric" &#40; Transact-SQL &#41; ](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *scale*  
 Für **decimal** oder **numerischen**, ist eine nicht Negative ganze Zahl, der die maximale Anzahl von Dezimalstellen angibt, die rechts neben dem Dezimalzeichen gespeichert werden können, und er muss kleiner oder gleich der Genauigkeit . Weitere Informationen finden Sie unter ["Decimal und Numeric" &#40; Transact-SQL &#41; ](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 **NULL** | NOT NULL  
 Gibt an, ob für den Typ NULL-Werte zulässig sind. Wird keine Angabe gemacht, ist NULL der Standardwert.  
  
 *AssemblyName*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assembly, die die Implementierung des benutzerdefinierten Typs in der common Language Runtime verweist. *Assembly_name* übereinstimmen, eine vorhandene Assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der aktuellen Datenbank.  
  
> [!NOTE]  
>  EXTERNAL_NAME ist in einer eigenständigen Datenbank nicht verfügbar.  
  
 **[.** *CLASS_NAME***]**   
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Klasse innerhalb der Assembly an, die den benutzerdefinierten Typ implementiert. *CLASS_NAME* muss ein gültiger Bezeichner sein und als Klasse in der Assembly mit Assemblysichtbarkeit vorhanden sein. *CLASS_NAME* wird Groß-/Kleinschreibung beachtet, unabhängig von der datenbanksortierung, und muss genau dem Klassennamen in der entsprechenden Assembly entsprechen. Der Klassenname einen Namespace qualifizierten Namen in eckige Klammern eingeschlossen sein kann (**[]**) Wenn die Programmiersprache ab, die zum Schreiben der Klasse verwendet wird, das Konzept von Namespaces, z. B. c# verwendet. Wenn *Class_name* nicht angegeben ist, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird angenommen, sie entspricht dem *Type_name*.  
  
 \<Column_definition >  
 Definiert die Spalten für einen benutzerdefinierten Tabellentyp.  
  
 \<Datentyp >  
 Definiert die Datentypen in einer Spalten für einen benutzerdefinierten Tabellentyp. Weitere Informationen zu Datentypen finden Sie unter [Datentypen &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md). Weitere Informationen zu Tabellen finden Sie unter [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<Column_constraint >  
 Definiert die Spalteneinschränkungen für einen benutzerdefinierten Tabellentyp. Unterstützte Einschränkungen schließen PRIMARY KEY, UNIQUE und CHECK ein. Weitere Informationen zu Tabellen finden Sie unter [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<Computed_column_definition >  
 Definiert einen berechneten Spaltenausdruck in einem benutzerdefinierten Tabellentyp als Spalte. Weitere Informationen zu Tabellen finden Sie unter [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<Table_constraint >  
 Definiert eine Spalteneinschränkung für einen benutzerdefinierten Tabellentyp. Unterstützte Einschränkungen schließen PRIMARY KEY, UNIQUE und CHECK ein.  
  
 \<Index_option >  
 Gibt die Fehlerantwort auf doppelte Schlüsselwerte beim Einfügen mehrerer Zeilen für einen eindeutigen gruppierten oder einen eindeutigen nicht gruppierten Index an. Weitere Informationen zu Indexoptionen finden Sie unter [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
 INDEX  
 Sie müssen Spalten- und Tabellenindizes als Teil der CREATE TABLE-Anweisung angeben. CREATE INDEX und DROP INDEX werden für speicheroptimierte Tabellen nicht unterstützt.  
  
 MEMORY_OPTIMIZED  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, ob der Tabellentyp speicheroptimiert ist. Diese Option ist standardmäßig deaktiviert; die Tabelle (der Tabellentyp) ist keine speicheroptimierte Tabelle (kein speicheroptimierter Tabellentyp). Speicheroptimierte Tabellentypen sind speicheroptimierte Benutzertabellen, deren Schema auf dem Datenträger ähnlich anderen Benutzertabellen beibehalten wird.  
  
 BUCKET_COUNT  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt die Anzahl der Buckets an, die im Hashindex erstellt werden sollen. Der maximale Wert für BUCKET_COUNT in Hashindizes beträgt 1.073.741.824. Weitere Informationen zu bucketanzahlen finden Sie unter [Indizes für Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md). *Bucket_count* ist ein erforderliches Argument.  
  
 HASH  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass ein HASH-Index erstellt wird. Hash-Indizes werden nur für Speicheroptimierte Tabellen unterstützt.  
  
## <a name="remarks"></a>Hinweise  
 Die Klasse der Assembly, auf das verweist *Assembly_name*, und ihre Methoden sollten alle Anforderungen zum Implementieren eines benutzerdefinierten Typs in erfüllen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen zu diesen Anforderungen finden Sie unter [benutzerdefinierte CLR-Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
 Noch einige zusätzliche Überlegungen:  
  
-   Die Klasse kann überlastete Methoden umfassen, aber diese Methoden können nur innerhalb von verwaltetem Code aufgerufen werden und nicht aus [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Irgendwelche statischen Member müssen deklariert werden, als **const** oder **Readonly** Wenn *Assembly_name* SAFE oder EXTERNAL_ACCESS festgelegt ist.  
  
 Innerhalb einer Datenbank kann nur ein benutzerdefinierter Typ für einen angegebenen Typ registriert werden, der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von der CLR hochgeladen wurde. Wenn ein benutzerdefinierter Typ für einen CLR-Typ erstellt wurde, für den in der Datenbank bereits ein benutzerdefinierter Typ vorhanden ist, schlägt CREATE TYPE fehl und gibt einen Fehler aus. Diese Einschränkung ist erforderlich, um eine Mehrdeutigkeit bei der Zuordnung des SQL-Typs zu vermeiden, wenn ein CLR-Typ mehr als einem benutzerdefinierten Typ zugeordnet werden kann.  
  
 Wenn eine Mutatormethode im Typ nicht zurückgibt *"void"*, die CREATE TYPE-Anweisung wird nicht ausgeführt.  
  
 Zum Ändern eines benutzerdefinierten Typs müssen Sie den Typ mit einer DROP TYPE-Anweisung löschen und ihn dann erneut erstellen.  
  
 Im Gegensatz zu benutzerdefinierten Typen, die mit erstellt werden **Sp_addtype**, **öffentlichen** Datenbankrolle wird nicht automatisch gewährt, REFERENCES-Berechtigung für Typen, die mithilfe von CREATE TYPE erstellt werden. Diese Berechtigung muss separat erteilt werden.  
  
 In benutzerdefinierten Tabellentypen strukturierte benutzerdefinierte Typen, die in verwendet werden *Column_name* \<Datentyp > sind Teil des Datenbankbereichs-Schema in dem der Tabellentyp definiert wird. Um auf strukturierte benutzerdefinierte Typen in einem anderen Bereich innerhalb der Datenbank zuzugreifen, verwenden Sie zweiteilige Namen.  
  
 In benutzerdefinierten Tabellentypen muss der Primärschlüssel für berechnete Spalten PERSISTED und NOT NULL sein.  
  
## <a name="memory-optimized-table-types"></a>Speicheroptimierte Tabellentypen  
 Ab [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] kann die Verarbeitung von Daten in einem Tabellentyp im Primärspeicher und nicht auf dem Datenträger erfolgen. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Codebeispiele, die zum Erstellen von speicheroptimierten Tabellentypen veranschaulichen, finden Sie unter [Erstellen einer speicheroptimierten Tabelle und einer systemintern kompilierten gespeicherten Prozedur](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE TYPE-Berechtigung für die aktuelle Datenbank und die ALTER-Berechtigung für *schema_name*. Wenn *schema_name* nicht angegeben wird, gelten die Standardregeln für die Namensauflösung, um das Schema für den aktuellen Benutzer zu bestimmen. Wenn *Assembly_name* angegeben wird, ein Benutzer muss Besitzer der Assembly oder darauf REFERENCES-Berechtigung haben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-an-alias-type-based-on-the-varchar-data-type"></a>A. Erstellen eines Aliastyps anhand des varchar-Datentyps  
 Im folgenden Beispiel wird ein Aliastyp erstellt, der auf dem vom System bereitgestellten Datentyp `varchar` basiert.  
  
```  
CREATE TYPE SSN  
FROM varchar(11) NOT NULL ;  
```  
  
### <a name="b-creating-a-user-defined-type"></a>B. Erstellen eines benutzerdefinierten Typs  
 Das folgende Beispiel erstellt einen Typ `Utf8String` , die auf Klasse verweist `utf8string` in der Assembly `utf8string`. Vor dem Erstellen des Typs wird die Assembly `utf8string` in der lokalen Datenbank registriert. Ersetzen Sie den binären Teil der CREATE ASSEMBLY-Anweisung durch eine gültige Beschreibung.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE ASSEMBLY utf8string  
AUTHORIZATION [dbi]   
FROM 0x4D... ;  
GO  
CREATE TYPE Utf8String   
EXTERNAL NAME utf8string.[Microsoft.Samples.SqlServer.utf8string] ;  
GO  
```  
  
### <a name="c-creating-a-user-defined-table-type"></a>C. Erstellen eines benutzerdefinierten Tabellentyps  
 Das folgende Beispiel zeigt, wie ein benutzerdefinierter Tabellentyp mit zwei Spalten erstellt wird: Weitere Informationen zum Erstellen und Verwenden von Tabellenwertparametern finden Sie unter [Tabellenwertparametern &#40; Datenbankmodul &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
```  
CREATE TYPE LocationTableType AS TABLE   
    ( LocationName VARCHAR(50)  
    , CostRate INT );  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie die ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP-Typ &#40; Transact-SQL &#41;](../../t-sql/statements/drop-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

