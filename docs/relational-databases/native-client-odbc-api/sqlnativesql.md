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
helpviewer_keywords: SQLNativeSql function
ms.assetid: 2d999fec-9e22-4514-ad5f-22a64b82f95b
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 88253aeb8af1193022eae94f49a8c93d8b7f5f8e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sqlnativesql"></a>SQLNativeSql
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber erfüllt **SQLNativeSql** -Anforderungen, ohne auf den Server zuzugreifen. Die Funktion testet die Syntax von SQL-Anweisungen effizient. Durch die Syntaxüberprüfung wird nicht bestimmt, ob Bezeichner oder die Ergebnisse von Ausdrücken in den SQL-Anweisungen gültig sind, und systemeigene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL-Anweisungen, die von **SQLNativeSql** zurückgegeben werden, können möglicherweise nicht ausgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLNativeSql-Funktion](http://go.microsoft.com/fwlink/?LinkID=59358)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
