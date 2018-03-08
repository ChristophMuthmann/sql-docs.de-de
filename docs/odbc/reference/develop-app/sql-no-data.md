---
title: SQL_NO_DATA | Microsoft Docs
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
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da9e5ffc19d884d2cb182190e11ba4dcf0a915bd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Wenn eine ODBC-3. *x* Anwendung ruft **SQLExecDirect**, **SQLExecute**, oder **SQLParamData** in einer ODBC 2.. *X* Treiber zum Ausführen von mit einem gesuchten Updates oder delete-Anweisung, die keine Zeilen in der Datenquelle des Treibers auswirken sollte SQL_SUCCESS nicht SQL_NO_DATA zurückgegeben. Wenn eine ODBC-2. *x* oder ODBC-3. *X* Anwendung arbeiten mit einem ODBC 3.. *X* Treiber ruft **SQLExecDirect**, **SQLExecute**, oder **SQLParamData** dasselbe Ergebnis erzielt, die ODBC 3.. *X* Treiber sollte SQL_NO_DATA zurückgegeben.
