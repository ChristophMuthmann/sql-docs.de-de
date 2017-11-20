---
title: SQL_NO_DATA | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4c42213c629c5fa79cd5c6522f4a36f29f36bd8c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlnodata"></a>SQL_NO_DATA
Wenn eine ODBC-3. *x* Anwendung ruft **SQLExecDirect**, **SQLExecute**, oder **SQLParamData** in einer ODBC 2..* X* Treiber zum Ausführen von mit einem gesuchten Updates oder delete-Anweisung, die keine Zeilen in der Datenquelle des Treibers auswirken sollte SQL_SUCCESS nicht SQL_NO_DATA zurückgegeben. Wenn eine ODBC-2. *x* oder ODBC-3.* X* Anwendung arbeiten mit einem ODBC 3..* X* Treiber ruft **SQLExecDirect**, **SQLExecute**, oder **SQLParamData** dasselbe Ergebnis erzielt, die ODBC 3..* X* Treiber sollte SQL_NO_DATA zurückgegeben.

