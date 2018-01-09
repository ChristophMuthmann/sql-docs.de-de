---
title: SQLEndTran | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 68a3d0f6df87f316e3bf2055365aa09493135b97
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In der Standardeinstellung schließt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber den mit einer Anweisung verknüpften Cursor, wenn **SQLEndTran** für einen Vorgang ein Commit oder Rollback ausführt. Servercursor werden nicht geschlossen, wenn sie statisch sind. Wenn **SQLEndTran** für einen Vorgang ein Commit oder Rollback ausführt, wird das Verhalten des mit der Anweisung verknüpften Cursors vom Wert des treiberspezifischen ODBC-Verbindungsattributs SQL_COPT_SS_PRESERVE_CURSORS bestimmt, das von [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)festgelegt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran-Funktion](http://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
