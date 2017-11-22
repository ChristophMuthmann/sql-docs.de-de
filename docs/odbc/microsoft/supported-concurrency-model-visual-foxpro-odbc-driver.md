---
title: "Parallelitätsmodell (Visual FoxPro-ODBC-Treiber) unterstützt | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e06adec755df6c412d13fd8c2b892db8977b3a53
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Unterstützte Parallelitätsmodell (Visual FoxPro-ODBC-Treiber)
Der Visual FoxPro-ODBC-Treiber unterstützt *schreibgeschützte Parallelität*. Rufen Sie Ihre Anwendung kann [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) mit einer Option SQL_CONCURRENCY SQL_CONCUR_READ_ONLY.  
  
 Weitere Informationen finden Sie unter der [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>Nur-Lese Parallelität  
 Der Cursor kann nicht aktualisiert werden.  
  
## <a name="row-versioning"></a>Zeilenversionsverwaltung  
 Im Wesentlichen Timestamp Unterstützung, in welcher Zeile Versionen zum Zeitpunkt der Aktualisierung verglichen werden.
