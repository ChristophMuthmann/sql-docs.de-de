---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 74b184ae4a11ffbba4a9a3d0f52de4d7f0c904cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Bei ausgeführten Anweisungen geht der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ist nicht besuchen Sie den Server aus, um die Anzahl der Spalten in einem Resultset zu melden. In diesem Fall **SQLNumResultCols** keinen Serverroundtrip herbei. Wie [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) und [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)Aufrufen **SQLNumResultCols** für vorbereitete, aber nicht ausgeführte Anweisungen generiert eine Server-Roundtrip erstellt.  
  
 Wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder ein Anweisungsbatch mehrere Resultsets für Zeilen zurückgibt, kann die Anzahl der Resultset-Spalten sich von einem Set zum nächsten ändern. **SQLNumResultCols** für jeden Set aufgerufen werden soll. Wenn sich die Anzahl der Spalten ändert, sollte die Anwendung Datenwerte vor dem Abrufen von Zeilenergebnissen erneut binden. Finden Sie weitere Informationen zum Arbeiten mit mehreren resultsetergebnissen [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Verbesserungen im Datenbankmodul ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SQLNumResultCols genauere Beschreibungen der erwarteten Ergebnisse abrufen können. Diese genaueren Ergebnisse unterscheidet sich möglicherweise von der Rückgabewerte SQLNumResultCols in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Metadatenermittlung](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLNumResultCols-Funktion](http://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
