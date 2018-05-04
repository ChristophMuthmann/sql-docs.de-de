---
title: Beispiel für die Diagnose-Treiber-Manager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c383dda247d3309ed38744609afb5ca12e3c38f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="driver-manager-diagnostic-example"></a>Treiber-Manager-Diagnose-Beispiel
Der Treiber-Manager können auch diagnosemeldungen generieren. Angenommen, eine Anwendung eine ungültige Richtungsoption zum übergeben **SQLDataSources**, der Treiber-Manager möglicherweise formatieren und die folgenden Rückgabewerte von **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Aufgrund des Fehlers im Treiber-Manager werden Präfixe, die diagnosemeldung für seine Lieferanten (Microsoft) und ihres Bezeichners ([ODBC-Treiber-Manager]) hinzugefügt.
