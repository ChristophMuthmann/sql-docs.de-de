---
title: SQLNativeSql | Microsoft Docs
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
helpviewer_keywords:
- SQLNativeSql function
ms.assetid: 2d999fec-9e22-4514-ad5f-22a64b82f95b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab7c5b2a62367ce9fc52568ed18cd93f0c3b55aa
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="sqlnativesql"></a>SQLNativeSql
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber erfüllt **SQLNativeSql** -Anforderungen, ohne auf den Server zuzugreifen. Die Funktion testet die Syntax von SQL-Anweisungen effizient. Durch die Syntaxüberprüfung wird nicht bestimmt, ob Bezeichner oder die Ergebnisse von Ausdrücken in den SQL-Anweisungen gültig sind, und systemeigene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL-Anweisungen, die von **SQLNativeSql** zurückgegeben werden, können möglicherweise nicht ausgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLNativeSql-Funktion](http://go.microsoft.com/fwlink/?LinkID=59358)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
