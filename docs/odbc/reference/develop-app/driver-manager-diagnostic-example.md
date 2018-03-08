---
title: "Beispiel für die Diagnose-Treiber-Manager | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 23fac7bede1173a27b61da3940864b4842cc6ff3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="driver-manager-diagnostic-example"></a>Treiber-Manager-Diagnose-Beispiel
Der Treiber-Manager können auch diagnosemeldungen generieren. Angenommen, eine Anwendung eine ungültige Richtungsoption zum übergeben **SQLDataSources**, der Treiber-Manager möglicherweise formatieren und die folgenden Rückgabewerte von **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Aufgrund des Fehlers im Treiber-Manager werden Präfixe, die diagnosemeldung für seine Lieferanten (Microsoft) und ihres Bezeichners ([ODBC-Treiber-Manager]) hinzugefügt.
