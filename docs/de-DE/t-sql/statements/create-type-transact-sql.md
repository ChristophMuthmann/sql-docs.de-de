---
title: CREATE TYPE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/11/2017
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
manager: craigg
ms.workload: Active
ms.openlocfilehash: be6c818401a74f4f14d6a8381fe696bc02a48e6e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-type-transact-sql"></a>CREATE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt einen Aliasdatentyp oder einen benutzerdefinierten Typ in der aktuellen Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Die Implementierung eines Aliasdatentyps basiert auf einem systemeigenen Typ von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ein benutzerdefinierter Typ wird durch eine Klasse einer Assembly in der Common Language Runtime (CLR) von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] implementiert. Um einen benutzerdefinierten Typ an seine Implementierung zu binden, muss die CLR-Assembly, die die Implementierung des Typs enthält, zuerst in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md) registriert werden.  
  
 Die Option zum Ausführen von CLR-Code ist standardmäßig in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deaktiviert. Sie können Datenbankobjekte, die auf verwaltete Codemodule verweisen, erstellen, ändern und löschen. Diese Verweise werden jedoch nur dann in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt, wenn die Option [clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) mithilfe von [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) aktiviert wird.  
 
> [!NOTE]  
>  Die Integration der .NET Framework-CLR in SQL Server wird in diesem Thema erläutert. Die CLR-Integration gilt nicht für Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
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
  
 *type_name*  
 Der Name des Aliasdatentyps oder benutzerdefinierten Datentyps. Typnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
  
 *base_type*  
 Ist der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellte Datentyp, auf dem der Aliasdatentyp basiert. *base_type* ist vom Datentyp **sysname** und hat keinen Standardwert. Folgende Werte sind möglich:  
  
|||||  
|-|-|-|-|  
|**bigint**|**binary(** *n* **)**|**bit**|**char(** *n* **)**|  
|**Datum**|**datetime**|**datetime2**|**datetimeoffset**|  
|**decimal**|**float**|**image**|**int**|  
|**money**|**nchar(** *n* **)**|**ntext**|**numeric**|  
|**nvarchar(** *n* | **max)**|**real**|**smalldatetime**|**smallint**|  
|**smallmoney**|**sql_variant**|**text**|**Uhrzeit**|  
|**tinyint**|**uniqueidentifier**|**varbinary(** *n* | **max)**|**varchar(** *n* | **max)**|  
  
 *base_type* kann außerdem jedes Synonym für Datentypen sein, das einem dieser Systemdatentypen zugeordnet wird.  
  
 *precision*  
 Für **decimal** oder **numeric**: Eine nicht negative ganze Zahl, die die maximale Anzahl von Dezimalstellen angibt, die vor und nach dem Dezimaltrennzeichen gespeichert werden können. Weitere Informationen finden Sie unter [decimal und numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *scale*  
 Für **decimal** oder **numeric**: Eine nicht negative ganze Zahl, die die maximale Anzahl von Dezimalstellen angibt, die nach dem Dezimalzeichen gespeichert werden können. Diese Zahl muss kleiner oder gleich der Gesamtzahl der Stellen sein. Weitere Informationen finden Sie unter [decimal und numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 **NULL** | NOT NULL  
 Gibt an, ob für den Typ NULL-Werte zulässig sind. Wird keine Angabe gemacht, ist NULL der Standardwert.  
  
 *assembly_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Assembly an, die auf die Implementierung des benutzerdefinierten Typs in der Common Language Runtime (CLR) verweist. *assembly_name* sollte einer vorhandenen Assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der aktuellen Datenbank entsprechen.  
  
> [!NOTE]  
>  EXTERNAL_NAME ist in einer eigenständigen Datenbank nicht verfügbar.  
  
 **[.** *class_name*  **]**  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Klasse innerhalb der Assembly an, die den benutzerdefinierten Typ implementiert. *class_name* muss ein gültiger Bezeichner sein und als Klasse mit Assemblysichtbarkeit in der Assembly vorhanden sein. Bei *class_name* muss unabhängig von der Datenbanksortierung die Groß-/Kleinschreibung beachtet werden, und der Wert muss genau dem Klassennamen in der entsprechenden Assembly entsprechen. Der Klassenname kann ein mit einem Namespace qualifizierter Name sein, der in eckigen Klammern (**[ ]**) steht, wenn die Programmiersprache, die zum Schreiben der Klasse verwendet wird, das Konzept von Namespaces verwendet, wie z.B. C#. Wenn *class_name* nicht angegeben ist, geht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] davon aus, dass der Wert mit *type_name* identisch ist.  
  
 \<column_definition>  
 Definiert die Spalten für einen benutzerdefinierten Tabellentyp.  
  
 \<data type>  
 Definiert die Datentypen in einer Spalten für einen benutzerdefinierten Tabellentyp. Weitere Informationen zu Datentypen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md). Weitere Informationen zu Tabellen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<column_constraint>  
 Definiert die Spalteneinschränkungen für einen benutzerdefinierten Tabellentyp. Unterstützte Einschränkungen schließen PRIMARY KEY, UNIQUE und CHECK ein. Weitere Informationen zu Tabellen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<computed_column_definition>  
 Definiert einen berechneten Spaltenausdruck in einem benutzerdefinierten Tabellentyp als Spalte. Weitere Informationen zu Tabellen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<table_constraint>  
 Definiert eine Spalteneinschränkung für einen benutzerdefinierten Tabellentyp. Unterstützte Einschränkungen schließen PRIMARY KEY, UNIQUE und CHECK ein.  
  
 \<index_option>  
 Gibt die Fehlerantwort auf doppelte Schlüsselwerte beim Einfügen mehrerer Zeilen für einen eindeutigen gruppierten oder einen eindeutigen nicht gruppierten Index an. Weitere Informationen zu Indexoptionen finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 INDEX  
 Sie müssen Spalten- und Tabellenindizes als Teil der CREATE TABLE-Anweisung angeben. CREATE INDEX und DROP INDEX werden für speicheroptimierte Tabellen nicht unterstützt.  
  
 MEMORY_OPTIMIZED  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, ob der Tabellentyp speicheroptimiert ist. Diese Option ist standardmäßig deaktiviert; die Tabelle (der Tabellentyp) ist keine speicheroptimierte Tabelle (kein speicheroptimierter Tabellentyp). Speicheroptimierte Tabellentypen sind speicheroptimierte Benutzertabellen, deren Schema auf dem Datenträger ähnlich anderen Benutzertabellen beibehalten wird.  
  
 BUCKET_COUNT  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt die Anzahl der Buckets an, die im Hashindex erstellt werden sollen. Der maximale Wert für BUCKET_COUNT in Hashindizes beträgt 1.073.741.824. Weitere Informationen zu Indizes für speicheroptimierte Tabellen finden Sie unter [Indexes for Memory-Optimized Tables (Indizes für speicheroptimierte Tabellen)](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md). *bucket_count* ist ein erforderliches Argument.  
  
 HASH  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass ein HASH-Index erstellt wird. Hashindizes werden nur für speicheroptimierte Tabellen unterstützt.  
  
## <a name="remarks"></a>Remarks  
 Die Klasse der Assembly, auf die in *assembly_name* verwiesen wird, und ihre Methoden sollten alle Anforderungen zum Implementieren eines benutzerdefinierten Typs in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfüllen. Weitere Informationen zu diesen Anforderungen finden Sie unter [CLR User-Defined Types (Benutzerdefinierte CLR-Typen)](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
 Noch einige zusätzliche Überlegungen:  
  
-   Die Klasse kann überlastete Methoden umfassen, aber diese Methoden können nur innerhalb von verwaltetem Code aufgerufen werden und nicht aus [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Alle statischen Elemente müssen als **const** oder **readonly** deklariert werden, wenn für *assembly_name* entweder SAFE oder EXTERNAL_ACCESS festgelegt wurde.  
  
 Innerhalb einer Datenbank kann nur ein benutzerdefinierter Typ für einen angegebenen Typ registriert werden, der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von der CLR hochgeladen wurde. Wenn ein benutzerdefinierter Typ für einen CLR-Typ erstellt wurde, für den in der Datenbank bereits ein benutzerdefinierter Typ vorhanden ist, schlägt CREATE TYPE fehl und gibt einen Fehler aus. Diese Einschränkung ist erforderlich, um eine Mehrdeutigkeit bei der Zuordnung des SQL-Typs zu vermeiden, wenn ein CLR-Typ mehr als einem benutzerdefinierten Typ zugeordnet werden kann.  
  
 Gibt eine Mutatormethode im Typ nicht *void* zurück, wird die CREATE TYPE-Anweisung nicht ausgeführt.  
  
 Zum Ändern eines benutzerdefinierten Typs müssen Sie den Typ mit einer DROP TYPE-Anweisung löschen und ihn dann erneut erstellen.  
  
 Im Gegensatz zu benutzerdefinierten Typen, die mit **sp_addtype** erstellt wurden, wird der Datenbankrolle **public** nicht automatisch die REFERENCES-Berechtigung für Typen erteilt, die mit CREATE TYPE erstellt wurden. Diese Berechtigung muss separat erteilt werden.  
  
 Strukturierte benutzerdefinierte Typen, die in *column_name* \<data type> verwendet werden, gehören in benutzerdefinierten Tabellentypen zum Bereich des Datenbankschemas, in dem der Tabellentyp definiert wird. Um auf strukturierte benutzerdefinierte Typen in einem anderen Bereich innerhalb der Datenbank zuzugreifen, verwenden Sie zweiteilige Namen.  
  
 In benutzerdefinierten Tabellentypen muss der Primärschlüssel für berechnete Spalten PERSISTED und NOT NULL sein.  
  
## <a name="memory-optimized-table-types"></a>Speicheroptimierte Tabellentypen  
 Ab [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] kann die Verarbeitung von Daten in einem Tabellentyp im Primärspeicher und nicht auf dem Datenträger erfolgen. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Codebeispiele, die das Erstellen speicheroptimierter Tabellentypen veranschaulichen, finden Sie unter [Erstellen einer speicheroptimierten Tabelle und einer systemintern kompilierten gespeicherten Prozedur](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE TYPE-Berechtigung für die aktuelle Datenbank und die ALTER-Berechtigung für *schema_name*. Wenn *schema_name* nicht angegeben wird, gelten die Standardregeln für die Namensauflösung, um das Schema für den aktuellen Benutzer zu bestimmen. Wird *assembly_name* angegeben, muss ein Benutzer entweder Besitzer der Assembly sein oder die REFERENCES-Berechtigung für die Assembly besitzen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-an-alias-type-based-on-the-varchar-data-type"></a>A. Erstellen eines Aliastyps anhand des varchar-Datentyps  
 Im folgenden Beispiel wird ein Aliastyp erstellt, der auf dem vom System bereitgestellten Datentyp `varchar` basiert.  
  
```  
CREATE TYPE SSN  
FROM varchar(11) NOT NULL ;  
```  
  
### <a name="b-creating-a-user-defined-type"></a>B. Erstellen eines benutzerdefinierten Typs  
 Im folgenden Beispiel wird der Typ `Utf8String` erstellt, der auf die Klasse `utf8string` in der Assembly `utf8string` verweist. Vor dem Erstellen des Typs wird die Assembly `utf8string` in der lokalen Datenbank registriert. Ersetzen Sie den binären Teil der CREATE ASSEMBLY-Anweisung durch eine gültige Beschreibung.  
  
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
 Das folgende Beispiel zeigt, wie ein benutzerdefinierter Tabellentyp mit zwei Spalten erstellt wird: Weitere Informationen zum Erstellen und Verwenden von Tabellenwertparametern finden Sie unter [Use Table-Valued Parameters &#40;Database Engine&#41; (Verwenden von Tabellenwertparametern &#40;Datenbank-Engine&#41;)](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
```  
CREATE TYPE LocationTableType AS TABLE   
    ( LocationName VARCHAR(50)  
    , CostRate INT );  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
