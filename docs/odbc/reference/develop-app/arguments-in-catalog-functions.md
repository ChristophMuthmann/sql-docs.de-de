---
title: Argumente im Katalogfunktionen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb973a525b5a978d16566edc02fb4d4651e11406
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="arguments-in-catalog-functions"></a>Argumente im Katalogfunktionen
Alle Katalogfunktionen unterstützen Argumente, mit denen eine Anwendung den Bereich der zurückgegebenen Daten einschränken kann. Beispielsweise die ersten und zweiten Aufrufe **SQLTables** Zurückgeben von Resultsets mit den Informationen zu allen Tabellen während der dritte Aufruf gibt Informationen über die Orders-Tabelle zurück in den folgenden Code:  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 Katalog Zeichenfolge Funktionsargumente lassen sich in vier verschiedene Typen: normale Argument (OA), Muster Wertargument (PV) Argument Bezeichner (ID) und Liste Wertargument (VL). Die meisten Zeichenfolgenargumente können einer von zwei unterschiedlichen Typen, abhängig vom Wert des Attributs SQL_ATTR_METADATA_ID-Anweisung sein. In der folgenden Tabelle listet die Argumente für jede Katalogfunktion und beschreibt den Typ des Arguments für eine Wert SQL_TRUE oder SQL_FALSE SQL_ATTR_METADATA_ID.  
  
|Funktion|Argument|Geben Sie beim SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|Geben Sie beim SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*Katalogname* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID-ID ID-NUMMER|  
|**SQLColumns**|*Katalogname* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|ID-ID ID-NUMMER|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName*  *FKTableName*|OA OA OA OA OA OA|ID-ID ID ID ID-ID|  
|**SQLPrimaryKeys**|*Katalogname* *SchemaName* *TableName*|OA OA OA|ID-ID-NUMMER|  
|**SQLProcedureColumns**|*Katalogname* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID-ID ID-NUMMER|  
|**SQLProcedures**|*Katalogname* *SchemaName* *ProcName*|OA PV PV|ID-ID-NUMMER|  
|**SQLSpecialColumns**|*Katalogname* *SchemaName* *TableName*|OA OA OA|ID-ID-NUMMER|  
|**SQLStatistics**|*Katalogname* *SchemaName* *TableName*|OA OA OA|ID-ID-NUMMER|  
|**SQLTablePrivileges**|*Katalogname* *SchemaName* *TableName*|OA PV PV|ID-ID-NUMMER|  
|**SQLTables**|*Katalogname* *SchemaName* *TableName* *für TableType*|PV PV PV VL|ID-ID ID VL|  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Normale Argumente](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [Argumente des Musterwerts](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [Bezeichnerargumente](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [Argumente der Wertliste](../../../odbc/reference/develop-app/value-list-arguments.md)
