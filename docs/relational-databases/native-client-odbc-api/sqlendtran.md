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
ms.technology: docset-sql-devref
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
ms.openlocfilehash: 0ae667a2fa572a12a8b00fc68a87faa676027c5b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In der Standardeinstellung schließt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber den mit einer Anweisung verknüpften Cursor, wenn **SQLEndTran** für einen Vorgang ein Commit oder Rollback ausführt. Servercursor werden nicht geschlossen, wenn sie statisch sind. Wenn **SQLEndTran** für einen Vorgang ein Commit oder Rollback ausführt, wird das Verhalten des mit der Anweisung verknüpften Cursors vom Wert des treiberspezifischen ODBC-Verbindungsattributs SQL_COPT_SS_PRESERVE_CURSORS bestimmt, das von [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)festgelegt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran-Funktion](http://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
