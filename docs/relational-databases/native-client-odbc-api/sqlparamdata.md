---
title: SQLParamData | Microsoft Docs
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
helpviewer_keywords: SQLParamData function
ms.assetid: 92349482-ea22-4a6a-8484-e9c6566794fa
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45722414519c1b838a68aa4c3662122c25d2a65e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sqlparamdata"></a>SQLParamData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Wenn SQLParamData gibt die *ValuePtrPtr* mit einem Tabellenwertparameter verknüpft ist, sollte die Anwendung mit SQLPutData Aufrufen *StrLen_Or_Ind*. Wenn *StrLen_Or_Ind* verfügt über einen Wert größer als 0 (null) bedeutet, dass die Anwendung bereit für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Parameterdaten für die nächste Zeile für den Tabellenwertparameter zu sammeln. Wenn *StrLen_Or_Ind* verfügt über einen Wert von 0 bedeutet keine weiteren Zeilen von Daten für den Tabellenwertparameter vorhanden sind. Weitere Informationen finden Sie unter [Bindung und Data Transfer of Table-Valued-Parametern und Spaltenwerte](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLParamData](http://go.microsoft.com/fwlink/?LinkId=80706)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
