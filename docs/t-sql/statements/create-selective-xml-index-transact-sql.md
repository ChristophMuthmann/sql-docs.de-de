---
title: Erstellen Sie SELEKTIVEN XML-INDEX (Transact-SQL) | Microsoft Docs
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
dev_langs:
- TSQL
ms.assetid: 1d769f62-f646-4057-b93a-bf5f90e935ed
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 29a2a6eaec3ebbbafef0fcead331835921c7da44
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-selective-xml-index-transact-sql"></a>CREATE SELECTIVE XML INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Erstellt für die angegebene Tabelle und XML-Spalte einen neuen selektiven XML-Index. Selektive XML-Indizes verbessern die Leistung von XML-Indizierung und -Abfragen, da lediglich die Teilmenge der Knoten indiziert wird, die Sie in der Regel abfragen. Sie können auch sekundäre selektive XML-Indizes erstellen. Informationen finden Sie unter [Create, Alter und Drop sekundäre selektive XML-Indizes](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE SELECTIVE XML INDEX index_name  
    ON <table_object> (xml_column_name)  
    [WITH XMLNAMESPACES (<xmlnamespace_list>)]  
    FOR (<promoted_node_path_list>)  
    [WITH (<index_options>)]  
  
<table_object> ::=  
 { [database_name. [schema_name ] . | schema_name. ] table_name }  
  
<promoted_node_path_list> ::=   
<named_promoted_node_path_item> [, <promoted_node_path_list>]  
  
<named_promoted_node_path_item> ::=   
<path_name> = <promoted_node_path_item>  
  
<promoted_node_path_item>::=  
<xquery_node_path_item> | <sql_values_node_path_item>  
  
<xquery_node_path_item> ::=   
<node_path> [AS XQUERY <xsd_type_or_node_hint>] [SINGLETON]  
  
<xsd_type_or_node_hint> ::=   
[<xsd_type>] [MAXLENGTH(x)] | node()  
  
<sql_values_node_path_item> ::=  
<node_path> AS SQL <sql_type> [SINGLETON]  
  
<node_path> ::=   
character_string_literal  
  
<xsd_type> ::=   
character_string_literal  
  
<sql_type> ::=   
identifier  
  
<path_name> ::=   
identifier  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
<xmlnamespace_uri> AS <xmlnamespace_prefix>  
  
<xml_namespace_uri> ::=   
character_string_literal  
  
<xml_namespace_prefix> ::=   
identifier  
  
<index_options> ::=   
(   
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> Argumente  
 *index_name*  
 Ist der Name des neuen Indexes zu erstellen. Indexnamen müssen innerhalb einer Tabelle eindeutig sein, können aber innerhalb einer Datenbank mehrfach vorkommen. Indexnamen müssen den Regeln der [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 *\<Table_object >* ist die Tabelle, die die Spalte XML-Index enthält. Verwenden Sie eines der folgenden Formate:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 *xml_column_name*  
 Der Name der XML-Spalte, die die zu indizierenden Pfade enthält.  
  
 [WITH XMLNAMESPACES **(**\<Xmlnamespace_list >**)**] ist die Liste der Namespaces, die zum Indizieren von Pfade verwendet. Informationen zur Syntax von WITH XMLNAMESPACES-Klausel finden Sie unter [WITH XMLNAMESPACES &#40; Transact-SQL &#41; ](../../t-sql/xml/with-xmlnamespaces.md).  
  
 FÜR **(**\<Promoted_node_path_list >**)** ist die Liste der zu indizierende mit optionalen Optimierungshinweisen Pfade. Weitere Informationen über die Pfade und die Optimierungshinweise aufgeführt, die Sie in der CREATE- oder ALTER-Anweisung angeben können, finden Sie unter [angeben von Pfaden und Optimierungshinweisen für selektive XML-Indizes](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md).  
  
 MIT  *\<Index_options >* Informationen zu den Indexoptionen finden Sie unter [CREATE XML INDEX &#40; Selektive XML-Indizes &#41; ](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Im Hinblick auf eine bessere Leistung und einen effizienteren Speicher erstellen Sie in den meisten Fällen einen selektiven XML-Index anstatt eines gewöhnlichen XML-Indexes. Ein selektiver XML-Index wird jedoch nicht empfohlen, wenn eine der beiden folgenden Bedingungen zutrifft:  
  
-   Sie müssen eine große Anzahl an Knotenpfaden zuordnen.  
  
-   Sie müssen Abfragen von unbekannten Elementen oder Elementen an einem unbekannten Speicherort unterstützen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Informationen über Begrenzungen und Einschränkungen finden Sie unter [selektive XML-Indizes &#40; SXI &#41; ](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Syntax zum Erstellen eines selektiven XML-Indexes veranschaulicht. Zudem werden mehrere Variationen der Syntax, die die zu indizierenden Pfade beschreibt, mit optionalen Optimierungshinweisen angegeben.  
  
```  
CREATE TABLE Tbl ( id INT PRIMARY KEY, xmlcol XML );  
GO  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()',  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON,  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
);  
```  
  
 Das folgende Beispiel enthält eine WITH XMLNAMESPACES-Klausel.  
  
```  
CREATE SELECTIVE XML INDEX on T1(C1)  
WITH XMLNAMESPACES ('http://www.tempuri.org/' as myns)  
FOR ( path1 = '/myns:book/myns:author/text()' );  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Selektive XML-Indizes &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Erstellen Sie, ändern und löschen Sie Selektiver XML-Indizes](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)   
 [Angeben von Pfaden und Optimierungshinweisen für selektive XML-Indizes](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)  
  
  


