---
title: Verarbeiten von Ergebnissen für gespeicherte Prozeduren | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4b9f238438433a22c6a3911bf104891d40f2f486
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="processing-stored-procedure-results"></a>Verarbeiten von Ergebnissen gespeicherter Prozeduren
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Gespeicherte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozeduren verfügen über vier Mechanismen für die Rückgabe von Daten:  
  
-   Jede SELECT-Anweisung in der Prozedur generiert ein Resultset.  
  
-   Die Prozedur kann Daten über Ausgabeparameter zurückgeben.  
  
-   Ein Cursorausgabeparameter kann einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursor zurück übergeben.  
  
-   Die Prozedur kann einen ganzzahligen Rückgabecode besitzen.  
  
 Anwendungen müssen alle diese Ausgaben gespeicherter Prozeduren verarbeiten können. Die CALL-Anweisung bzw. die EXECUTE-Anweisung sollte Parametermarkierungen für den Rückgabecode und die Ausgabeparameter enthalten. Verwendung [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) sie alle als Ausgabeparameter zu binden und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber überträgt die Ausgabewerte an die gebundenen Variablen. Ausgabeparameter und Rückgabecodes werden die letzten Elemente zurückgegeben, die an den Client von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; sie werden nicht zurückgegeben, an die Anwendung bis [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) gibt SQL_NO_DATA zurück.  
  
 ODBC unterstützt das Binden von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Cursorparametern nicht. Da alle Ausgabeparameter vor der Ausführung einer Prozedur gebunden werden müssen, können gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozeduren, die einen Ausgabecursorparameter enthalten, nicht von ODBC-Anwendungen aufgerufen werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen gespeicherter Prozeduren](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
