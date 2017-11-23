---
title: Abrufen von Resultsetinformationen (ODBC) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd99d4fe84bf7ceb09b90d19dd5ec12b26c272c9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="processing-results---retrieve-result-set-information"></a>Verarbeiten von Ergebnissen - Abrufen von Resultsetinformationen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-get-information-about-a-result-set"></a>So rufen Sie Informationen zu einem Resultset ab  
  
1.  Rufen Sie [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) auf die Anzahl von Spalten im Resultset abzurufen.  
  
2.  Für jede Spalte im Resultset führt die Anwendung nun Folgendes aus:  
  
    -   Rufen Sie [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) beim Abrufen von Informationen über die Ergebnisspalte.  
  
     oder  
  
    -   Rufen Sie [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) um spezifische Deskriptorinformationen über die Ergebnisspalte abzurufen.  
  
## <a name="see-also"></a>Siehe auch  
[Verarbeiten Sie Ergebnisse &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[Bestimmen die Merkmale eines Resultsets &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
