---
title: "Rückgabe von SQL_NO_DATA | Microsoft Docs"
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
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5539f9d2951913163ac6011695709e3664d8acb1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="returning-sqlnodata"></a>Rückgabe von SQL_NO_DATA
Wenn eine ODBC-2. *x* Anwendung arbeiten, eine ODBC 3.*.x* Treiber ruft **SQLExecDirect**, **SQLExecute**, oder **SQLParamData**, und ein gesuchtes Update oder Delete-Anweisung ausgeführt wurde, aber keine Auswirkungen auf Zeilen in der Datenquelle, die ODBC 3.*.x* Treiber sollte SQL_SUCCESS zurück. Wenn eine ODBC 3.*.x* Anwendung arbeiten mit einem ODBC 3.*.x* Treiber ruft **SQLExecDirect**, **SQLExecute**, oder ** SQLParamData** dasselbe Ergebnis erzielt, die ODBC 3.*.x* Treiber sollte SQL_NO_DATA zurückgegeben.  
  
 Wenn eine gesuchte update oder-Anweisung in DELETE ein Batch von Anweisungen wirkt sich keine Zeilen in der Datenquelle **SQLMoreResults** gibt SQL_SUCCESS zurück. Es kann keine SQL_NO_DATA, zurückgeben, da bedeuten würde, dass es keine weiteren Ergebnisse, nicht, die es einem Ergebnis aus einem gesuchten Update/Delete, die keine Zeilen betroffen sind.

