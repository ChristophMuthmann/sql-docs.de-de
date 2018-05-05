---
title: SQL_NO_DATA | Microsoft Docs
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
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff7ba5184642f419a62ffef0610bfc08995ed6b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Wenn eine ODBC-3. *x* Anwendung ruft **SQLExecDirect**, **SQLExecute**, oder **SQLParamData** in einer ODBC 2. *X* Treiber zum Ausführen von mit einem gesuchten Updates oder delete-Anweisung, die keine Zeilen in der Datenquelle des Treibers auswirken sollte SQL_SUCCESS nicht SQL_NO_DATA zurückgegeben. Wenn eine ODBC-2. *x* oder ODBC-3. *X* Anwendung arbeiten mit einem ODBC 3. *X* Treiber ruft **SQLExecDirect**, **SQLExecute**, oder **SQLParamData** dasselbe Ergebnis erzielt, die ODBC 3. *X* Treiber sollte SQL_NO_DATA zurückgegeben.
