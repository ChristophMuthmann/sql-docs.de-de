---
title: Durch Aufrufen von SQLSetPos | Microsoft Docs
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
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a9e7eeeaa8e2268256b103095ef0077329c52cc9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="calling-sqlsetpos"></a>SQLSetPos aufrufen
In ODBC 2. *x*, der Zeiger auf die zeilenstatusarray wurde ein Argument an **SQLExtendedFetch**. Die zeilenstatusarray wurde durch einen Aufruf von später aktualisiert **SQLSetPos**. Einige Treiber wurden basieren auf der Tatsache, dass die dieses Array nicht zwischen ändert **SQLExtendedFetch** und **SQLSetPos**. In ODBC 3. *x*der Zeiger auf das Statusarray einem Beschreibungsfeld und ist daher die Anwendung kann problemlos ändern sie auf ein anderes Array zu verweisen. Dies kann ein Problem bei der Verwendung einer ODBC-3 sein. *x* Anwendung arbeitet mit einer ODBC 2. *X* Treiber jedoch ist das Aufrufen **SQLSetStmtAttr** der Zeiger für den arraystatus festgelegt und ist der Aufruf von **SQLFetchScroll** zum Abrufen von Daten. Ordnet der Treiber-Manager als Sequenz von Aufrufen an diesen **SQLExtendedFetch**. Im folgenden Code ein Fehler würde normalerweise ausgelöst, wenn der Treiber-Manager die zweite ordnet **SQLSetStmtAttr** rufen Sie bei der Arbeit mit einer ODBC 2.*.x* Treiber:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 Gäbe es keine Möglichkeit, den Status Zeilenzeiger in ODBC 2. ändern, würde der Fehler ausgelöst werden. *x* zwischen den Aufrufen **SQLExtendedFetch**. Stattdessen führt der Treiber-Manager die folgenden Schritte aus, bei der Arbeit mit einer ODBC 2.*.x* Treiber:  
  
1.  Initialisiert ein internes Treibermanager-Flag *fSetPosError* auf "true".  
  
2.  Wenn eine Anwendung ruft **SQLFetchScroll**, legt der Treiber-Manager *fSetPosError* auf "false".  
  
3.  Wenn die Anwendung aufruft, **SQLSetStmtAttr** zum Festlegen der SQL_ATTR_ROW_STATUS_PTR der Treiber-Manager setzt *fSetPosError* gleich ToTRUE.  
  
4.  Wenn die Anwendung aufruft, **SQLSetPos**, mit *fSetPosError* gleich "true", der Treiber-Manager löst SQL_ERROR mit SQLSTATE HY011 (Attribut kann nicht jetzt festgelegt werden) gibt an, dass die Anwendung Es wurde versucht, rufen Sie **SQLSetPos** nach dem Ändern des Zeile Status Zeigers jedoch vor dem Aufruf **SQLFetchScroll**.
