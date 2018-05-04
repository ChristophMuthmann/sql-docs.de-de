---
title: Überprüfung der Unterstützung von Funktionen und die Variabilität | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 82b8a0c2c50e557e055ef14a4ac34a486611304d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="checking-feature-support-and-variability"></a>Überprüfung der Unterstützung von Funktionen und die Variabilität
Um die Unterstützung von Funktionen und Variierbarkeit zu überprüfen,-Anwendungen in der Regel rufen **SQLGetInfo**, **SQLGetFunctions**, und **SQLGetTypeInfo**. Ein guter Ausgangspunkt ist der Treiber-API und SQL-Grammatik Übereinstimmungsebenen. Diese Verfahren beschreiben allgemeine Ebenen der Unterstützung von Funktionen. Die Anwendung kann dann aufrufen **SQLGetInfo** mit anderen Optionen, um zu bestimmen, die Unterstützung oder Variabilität der Funktionen, die es benötigt, **SQLGetFunctions** bestimmen muss, ob die Funktionen über das zurückgegebene Konformitätsgrad werden unterstützt, und **SQLGetTypeInfo** um zu bestimmen, welche SQL-Datentypen unterstützt werden.  
  
 Eine Anwendung kann bestimmen, ob ein Attribut-Anweisung oder die Verbindung durch den Aufruf unterstützt wird **SQLSetStmtAttr** oder **SQLSetConnectAttr** mit diesem Attribut. Wenn die Funktion SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgibt, wird das Attribut unterstützt. Wenn die Rückgabe von SQL_ERROR und SQLSTATE HYC00 (optionales Feature nicht implementiert), das Attribut wird nicht unterstützt.  
  
 Anwendungen können auch bestimmen, eine begrenzte Menge an Informationen vor dem Verbinden mit dem Treiber durch den Aufruf **SQLDrivers**.
