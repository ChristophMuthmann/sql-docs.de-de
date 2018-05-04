---
title: SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 56f6655a7286d0ad2b37210173efa72d2b785e45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Im Manualcommit-Modus führt das Aufrufen von **SQLFreeHandle** für ein Anweisungshandle mit einer offenen Transaktion zu einem Rollback ausstehender Änderungen an der Datenbank. Durch das Aufrufen von **SQLFreeHandle** für ein Anweisungshandle werden immer alle geöffneten Cursor geschlossen und ausstehende Ergebnisse verworfen. Auf diese Weise werden alle zum Anweisungshandle gehörenden Ressourcen freigegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLFreeHandle-Funktion](http://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
