---
title: "Unterstützung für Spalten mit geringer Dichte (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d872db9430c2d7b85f4d6e685a3e3f2550eb8015
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sparse-columns-support-odbc"></a>Unterstützung für Spalten mit geringer Dichte (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In diesem Thema wird beschrieben, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Unterstützung für Spalten mit geringer Dichte. Ein Beispiel, ODBC-Unterstützung für Spalten mit geringer Dichte, finden Sie unter [Aufrufen von SQLColumns für eine Tabelle mit Spalten mit geringer Dichte](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md). Weitere Informationen zu Sparsespalten finden Sie unter [Sparse Columns Support in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md).  
  
## <a name="statement-metadata"></a>Anweisungsmetadaten  
 Das Deskriptorfeld für den Anwendungsparameterdeskriptor (APD) und das SQL_SOPT_SS_NAME_SCOPE-Anweisungsattribut akzeptieren die zusätzlichen Werte SQL_SS_NAME_SCOPE_EXTENDED und SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET. Diese Werte geben an, welche Spalten im zurückgegebenes Resultset enthalten sind [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md). Weitere Informationen zu SQL_SOPT_SS_NAME_SCOPE finden Sie unter [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Mithilfe eines neuen Implementierungszeilendeskriptors (IRD), ein schreibgeschütztes SQLSMALLINT-Feld namens SQL_CA_SS_IS_COLUMN_SET, kann bestimmt werden, ob eine Spalte einen XML **column_set** -Wert darstellt. SQL_CA_SS_IS_COLUMN_SET akzeptiert die Werte SQL_TRUE und SQL_FALSE.  
  
## <a name="catalog-metadata"></a>Katalogmetadaten  
 Zwei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bestimmte Spalten (SS_IS_SPARSE und SS_IS_COLUMN_SET) wurden hinzugefügt, um das Resultset für [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="odbc-function-support-for-sparse-columns"></a>ODBC-Funktionsunterstützung für Spalten mit geringer Dichte  
 Die folgenden ODBC-Funktionen wurden aktualisiert, um Sparsespalten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client zu unterstützen:  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
