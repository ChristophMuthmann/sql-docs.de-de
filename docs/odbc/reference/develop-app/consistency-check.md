---
title: "Überprüfung der Projektkonsistenz | Microsoft Docs"
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
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f1148984210013a8d5c0c6d9096d04ac21141d2a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="consistency-check"></a>Konsistenzprüfung
Eine konsistenzprüfung wird automatisch vom Treiber ausgeführt, wenn eine Anwendung das SQL_DESC_DATA_PTR-Feld des APD, ARD oder IPD festlegt. Dieses Feld festgelegt ist, überprüft der Treiber an, dass der Wert des Felds SQL_DESC_TYPE und die Werte für das SQL_DESC_TYPE-Feld in den gleichen Datensatz sind gültig und konsistent.  
  
 Das SQL_DESC_DATA_PTR-Feld eine IPD ist normalerweise nicht festgelegt. Allerdings erreichen eine Anwendung, um eine konsistenzprüfung des IPD-Feldern zu erzwingen. Der Wert, der das SQL_DESC_DATA_PTR-Feld der IPD festgelegt ist, werden eigentlich nicht gespeichert und kann nicht abgerufen werden, durch den Aufruf von **SQLGetDescField** oder **SQLGetDescRec**; die Einstellung erfolgt nur für das Erzwingen der Überprüfung der Projektkonsistenz. Eine konsistenzprüfung kann nicht auf eine IRD ausgeführt werden.  
  
 Weitere Informationen für die konsistenzprüfung finden Sie unter [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
