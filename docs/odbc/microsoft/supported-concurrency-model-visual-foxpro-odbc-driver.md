---
title: "Parallelitätsmodell (Visual FoxPro-ODBC-Treiber) unterstützt | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f3348850a76bb831c236fd1c1ee49fb89b97504
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>Unterstützte Parallelitätsmodell (Visual FoxPro-ODBC-Treiber)
Der Visual FoxPro-ODBC-Treiber unterstützt *schreibgeschützte Parallelität*. Rufen Sie Ihre Anwendung kann [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) mit einer Option SQL_CONCURRENCY SQL_CONCUR_READ_ONLY.  
  
 Weitere Informationen finden Sie unter der [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="read-only-concurrency"></a>Nur-Lese Parallelität  
 Der Cursor kann nicht aktualisiert werden.  
  
## <a name="row-versioning"></a>Zeilenversionsverwaltung  
 Im Wesentlichen Timestamp Unterstützung, in welcher Zeile Versionen zum Zeitpunkt der Aktualisierung verglichen werden.
