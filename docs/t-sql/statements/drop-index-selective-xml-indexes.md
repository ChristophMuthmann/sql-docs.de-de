---
title: DROP INDEX (selektive XML-Indizes) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DROP XML INDEX statement
dev_langs: TSQL
ms.assetid: 4779ae84-e5f4-4d04-8fc1-e24a6631b428
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffe5e33598d0af816f31888c6c0fabfa9ac3ad94
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="drop-index-selective-xml-indexes"></a>DROP INDEX (selektive XML-Indizes)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Löscht einen vorhandenen selektiven XML-Index oder sekundären selektiven XML-Index in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Selektive XML-Indizes &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP INDEX index_name ON <object>  
    [ WITH ( <drop_index_option> [ ,...n ] ) ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
        table_or_view_name  
}  
  
<drop_index_option> ::=  
{  
    MAXDOP = max_degree_of_parallelism  
    | ONLINE = { ON | OFF }  
}  
```  
  
##  <a name="Arguments"></a> Argumente  
 *index_name*  
 Der Name des vorhandenen, zu löschenden Indexes.  
  
 *\<Objekt >* ist die Tabelle, die indizierte XML-Spalte enthält. Verwenden Sie eines der folgenden Formate:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 *\<Drop_index_option >* Informationen zu den Drop Index-Optionen finden Sie unter [DROP INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-index-transact-sql.md).  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Die ALTER-Berechtigung für die Tabelle oder Ansicht ist erforderlich, um DROP INDEX auszuführen. Über diese Berechtigung verfügen standardmäßig die Mitglieder der festen Serverrolle sysadmin und die Mitglieder der festen Datenbankrollen db_ddladmin und db_owner.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine DROP INDEX-Anweisung veranschaulicht.  
  
```  
DROP INDEX sxi_index ON tbl;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Selektive XML-Indizes &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Erstellen, Ändern und Löschen selektiver XML-Indizes](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  

