---
title: SQLTables | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTables function
ms.assetid: 77b6c15c-9cf7-4019-b3f0-3d27d23ef656
caps.latest.revision: 38
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4a39911421d0546b9cc35794e9b8aaefcbaa136b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqltables"></a>SQLTables
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLTables kann in einem statischen Servercursor ausgeführt werden. Der Versuch SQLTables in einem aktualisierbaren (dynamischen oder Keyset-) Cursor auszuführen Cursor SQL_SUCCESS_WITH_INFO zurück, der angibt, dass der Cursortyp geändert wurde.  
  
 SQLTables führt Tabellen aus allen Datenbanken auf, wenn die *CatalogName* -Parameter sql_all_catalogs lautet und alle anderen Parameter enthalten Standardwerte (NULL-Zeiger).  
  
 Um verfügbare Kataloge, Schemas und Tabellentypen zu melden, macht SQLTables besondere Verwendung von leeren Zeichenfolgen (mit der Länge Null Byte-Zeiger). Leere Zeichenfolgen sind keine Standardwerte (NULL-Zeiger).  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt die Berichtsinformationen für Tabellen auf Verbindungsservern durch akzeptieren einen zweiteiligen Namen für die *CatalogName* Parameter: *linked_server_name*.  
  
 SQLTables gibt Informationen über alle Tabellen, deren Namen übereinstimmen *TableName* und vom aktuellen Benutzer gehören.  
  
## <a name="sqltables-and-table-valued-parameters"></a>'SQLTables'- und Tabellenwertparameter  
 Wenn das SQL_SOPT_SS_NAME_SCOPE-Anweisungsattribut den Wert SQL_SS_NAME_SCOPE_TABLE_TYPE statt den Standardwert sql_ss_name_scope_table aufweist, werden Informationen über Tabellentypen von SQLTables zurück. Für einen Tabellentyp in Spalte 4 des SQLTables zurückgegebenes Resultset zurückgegebene TABLE_TYPE-Wert ist TABELLENTYP. Weitere Informationen zu SQL_SOPT_SS_NAME_SCOPE finden Sie unter [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Tabellen, Sichten und Synonyme nutzen einen gemeinsamen Namespace, der sich von dem Namespace unterscheidet, den Tabellentypen verwenden. Wenngleich ein und derselbe Namespace nicht eine Tabelle und eine Sicht enthalten kann, ist es hingegen möglich, dass ein Namespace im selben Katalog und Schema eine Tabelle und einen Tabellentypen enthält.  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="example"></a>Beispiel  
  
```  
// Get a list of all tables in the current database.  
SQLTables(hstmt, NULL, 0, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of all tables in all databases.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of databases on the current connection's server.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, (SQLCHAR*)"", 0, (SQLCHAR*)"",  
    0, NULL, 0);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQLTables-Funktion](http://go.microsoft.com/fwlink/?LinkId=59374)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
