---
title: SQLPrimaryKeys | Microsoft Docs
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
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f4a3309af7a9eadf8eb2ecceefda41b7fbd4e2b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Möglicherweise eine Tabelle eine Spalte oder Spalten, die als eindeutiger Zeilenbezeichner dienen können, und Tabellen ohne eine PRIMARY KEY-Einschränkung erstellt geben ein leeres Resultset SQLPrimaryKeys zurück. Der ODBC-Funktion [SQLSpecialColumns](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md) meldet zeilenbezeichnerkandidaten für Tabellen ohne Primärschlüssel.  
  
 SQLPrimaryKeys gibt SQL_SUCCESS zurück, unabhängig davon, ob Werte für vorhanden *CatalogName*, *SchemaName*, oder *TableName* Parameter. SQLFetch gibt SQL_NO_DATA zurück, wenn in diesen Parametern ungültige Werte verwendet werden.  
  
 SQLPrimaryKeys kann in einem statischen Servercursor ausgeführt werden. Der Versuch SQLPrimaryKeys auf einem aktualisierbaren (dynamischen oder Keyset-) Cursor auszuführen Cursor SQL_SUCCESS_WITH_INFO zurück, der angibt, dass der Cursortyp geändert wurde.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt die Berichtsinformationen für Tabellen auf Verbindungsservern durch akzeptieren einen zweiteiligen Namen für die *CatalogName* Parameter: *linked_server_name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys und Tabellenwertparameter  
 Wenn das SQL_SOPT_SS_NAME_SCOPE-Anweisungsattribut den Wert SQL_SS_NAME_SCOPE_TABLE_TYPE statt den Standardwert sql_ss_name_scope_table aufweist, wird die SQLPrimaryKeys Informationen zu Primärschlüsselspalten von Tabellentypen zurück. Weitere Informationen zu SQL_SOPT_SS_NAME_SCOPE finden Sie unter [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLPrimaryKeys-Funktion](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
