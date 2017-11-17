---
title: ALTER INDEX (selektive XML-Indizes) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
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
ms.assetid: cca96a8f-7737-42d2-bbcc-03d5f858dcc1
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e7854dd1d9365f97628341c4160c368f97308302
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-index-selective-xml-indexes"></a>ALTER INDEX (selektive XML-Indizes)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Ändert einen vorhandenen selektiven XML-Index. Die ALTER INDEX-Anweisung ändert eines oder mehrere der folgenden Elemente:  
  
-   Die Liste der indizierten Pfade (FOR-Klausel).  
  
-   Die Liste der Namespaces (WITH XMLNAMESPACES-Klausel).  
  
-   Die Indexoptionen (WITH-Klausel).  
  
 Sie können sekundäre selektive XML-Indizes nicht ändern. Weitere Informationen finden Sie unter [Create, Alter und Drop sekundäre selektive XML-Indizes](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER INDEX index_name  
    ON <table_object>   
    [WITH XMLNAMESPACES ( <xmlnamespace_list> )]  
    FOR ( <promoted_node_path_action_list> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ [database_name. [schema_name ] . | schema_name. ] table_name }  
<promoted_node_path_action_list> ::=   
<promoted_node_path_action_item> [, <promoted_node_path_action_list>]  
  
<promoted_node_path_action_item>::=   
<add_node_path_item_action> | <remove_node_path_item_action>  
  
<add_node_path_item_action> ::=  
ADD <path_name> = <promoted_node_path_item>  
  
<promoted_node_path_item>::=  
<xquery_node_path_item> | <sql_values_node_path_item>  
  
<remove_node_path_item_action> ::= REMOVE <path_name>   
  
<path_name_or_typed_node_path>::=   
<path_name> | <typed_node_path>  
  
<typed_node_path> ::=   
<node_path> [[AS XQUERY <xsd_type_ext>] | [AS SQL <sql_type>]]  
  
<xquery_node_path_item> ::=   
<node_path> [AS XQUERY <xsd_type_or_node_hint>] [SINGLETON]  
  
<xsd_type_or_node_hint> ::=   
[<xsd_type>] [MAXLENGTH(x)] | 'node()'  
  
<sql_values_node_path_item> ::=   
<node_path> AS SQL <sql_type> [SINGLETON]  
  
<node_path> ::=   
character_string_literal  
  
<xsd_type_ext> ::=   
character_string_literal  
  
<sql_type> ::=   
identifier  
  
<path_name> ::=   
identifier  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
<xmlnamespace_uri> AS <xmlnamespace_prefix>  
  
<xml_namespace_uri> ::= character_string_literal  
<xml_namespace_prefix> ::= identifier  
  
<index_options> ::=   
(   
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY =OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE =OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> Argumente  
 *index_name*  
 Der Name des vorhandenen, zu ändernden Indexes.  
  
 *\<Table_object >*  
 Die Tabelle, die die zu indizierende XML-Spalte enthält. Verwenden Sie eines der folgenden Formate:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 [WITH XMLNAMESPACES **(** \<Xmlnamespace_list > **)**]  
 Die Liste der von den zu indizierenden Pfaden verwendeten Namespaces. Informationen zur Syntax von WITH XMLNAMESPACES-Klausel finden Sie unter [WITH XMLNAMESPACES &#40; Transact-SQL &#41; ](../../t-sql/xml/with-xmlnamespaces.md).  
  
 FÜR **(** \<Promoted_node_path_action_list > **)**  
 Die Liste der hinzuzufügenden oder zu entfernenden indizierten Pfade.  
  
-   **Fügen Sie einen Pfad an.** Wenn Sie einen Pfad HINZUFÜGEN, verwenden Sie die gleiche Syntax, die zur Erstellung von Pfaden mit der CREATE SELECTIVE XML INDEX-Anweisung verwendet wird. Weitere Informationen zu den Pfaden, die Sie in der CREATE- oder ALTER-Anweisung angeben können, finden Sie unter [angeben von Pfaden und Optimierungshinweisen für selektive XML-Indizes](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md).  
  
-   **Entfernen Sie einen Pfad an.** Wenn Sie einen Pfad ENTFERNEN, geben Sie den Namen an, der dem Pfad bei seiner Erstellung zugewiesen wurde.  
  
 [Mit **(** \<Index_options > **)**]  
 Sie können nur angeben, \<Index_options > Wenn Sie ALTER INDEX verwenden, ohne die FOR-Klausel. Wenn Sie ALTER INDEX verwenden, um Pfade im Index hinzuzufügen oder sie daraus zu entfernen, sind die Indexoptionen keine gültigen Argumente. Informationen zu den Indexoptionen finden Sie unter [CREATE XML INDEX &#40; Selektive XML-Indizes &#41; ](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="remarks"></a>Hinweise  
  
> [!IMPORTANT]  
>  Wenn Sie eine ALTER INDEX-Anweisung ausführen, wird der selektive XML-Index immer neu erstellt. Beachten Sie unbedingt die Auswirkungen dieses Prozesses auf Serverressourcen.  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 ALTER-Berechtigung in der Tabelle oder Ansicht ist erforderlich, um ALTER INDEX auszuführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine ALTER INDEX-Anweisung veranschaulicht. Mit dieser Anweisung wird der Pfad `'/a/b/m'` dem XQuery-Teil des Indexes hinzugefügt und der Pfad `'/a/b/e'` vom SQL-Teil des Indexes, der im Beispiel im Thema [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md) erstellt wurde, gelöscht. Der zu löschende Pfad ist anhand des Namens zu erkennen, der ihm bei der Erstellung zugewiesen wurde.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
);  
```  
  
 Im folgenden Beispiel wird eine ALTER INDEX-Anweisung, die Indexoptionen angibt, veranschaulicht. Indexoptionen sind erlaubt, da die Anweisung keine FOR-Klausel verwendet, um Pfade hinzuzufügen oder zu entfernen.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
PAD_INDEX = ON;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Selektive XML-Indizes &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Erstellen Sie, ändern und löschen Sie Selektiver XML-Indizes](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)   
 [Angeben von Pfaden und Optimierungshinweisen für selektive XML-Indizes](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)  
  
  

