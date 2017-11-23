---
title: File-Based Treiber diagnostische Beispiel | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6d949d95301c6fb66ad6b027b99113850bea8e9d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
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
