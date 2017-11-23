---
title: "Cursortyp und Parallelität Kombinationen | Microsoft Docs"
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
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d9798b819b702b4e984872a19b0c761a8621de2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="cursor-type-and-concurrency-combinations"></a>Cursortyp und Parallelität Kombinationen
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Cursortypen steuern, die Funktionalität des Cursors an den Benutzer bereitgestellt wird. Parallelitätsoptionen aktualisierbarkeit und Sperrverhalten eines Resultsets steuern.  
  
|Cursortyp|Concurrency (zulässige Werte)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1] </sup> Finden Sie unter [Einschränkungen bei der Verwendung keysetgesteuerter Cursor](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md).  
  
 <sup>[2] </sup> SQL_CONCUR_LOCK wird nur unterstützt, wenn die Verbindungsoption SQL_AUTOCOMMIT auf SQL_AUTOCOMMIT_OFF festgelegt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindungsoption](../../odbc/microsoft/connect-options.md)
