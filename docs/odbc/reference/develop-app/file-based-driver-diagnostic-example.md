---
title: File-Based Treiber diagnostische Beispiel | Microsoft Docs
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
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d58072bebac57eca8976064b85a25999475a9586
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="file-based-driver-diagnostic-example"></a>File-Based Treiber Diagnostic-Beispiel
Ein dateibasierter Treiber fungiert als ein ODBC-Treiber sowohl als Datenquelle. Sie können daher Fehler und Warnungen, die sowohl als eine Komponente in einer ODBC-Verbindung und als Datenquelle generieren. Da es auch die Komponente, das mit der Treiber-Manager kommuniziert handelt, formatiert und gibt die Argumente für **SQLGetDiagRec**.  
  
 Z. B. wenn ein Treiber Microsoft® dBASE nicht genügend Arbeitsspeicher zuordnen kann, es möglicherweise die folgenden Werte zurückgeben aus **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Da dieser Fehler nicht mit der Datenquelle verbunden war, hinzugefügt der Treiber nur Präfixe die diagnosemeldung für den Anbieter (Microsoft) und der Treiber ([ODBC dBASE-Treiber]).  
  
 Wenn der Treiber nicht die Datei nützlich finden konnte, können sie die folgenden Werte aus zurückgeben **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Da dieser Fehler mit der Datenquelle verknüpft wurde, hinzugefügt der Treiber das Dateiformat der Datenquelle (dBASE) als Präfix an die diagnosemeldung. Da der Treiber auch die Komponente, die mit der Datenquelle verbunden wurde, wurde jedoch Präfixe für den Anbieter (Microsoft) und der Treiber ([ODBC dBASE-Treiber]) hinzugefügt.
