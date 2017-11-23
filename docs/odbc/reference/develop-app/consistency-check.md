---
title: "Überprüfung der Projektkonsistenz | Microsoft Docs"
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
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b661526c69d6dbe88e47d4eace4f13c603f5e16
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="consistency-check"></a>Konsistenzprüfung
Eine konsistenzprüfung wird automatisch vom Treiber ausgeführt, wenn eine Anwendung das SQL_DESC_DATA_PTR-Feld des APD, ARD oder IPD festlegt. Dieses Feld festgelegt ist, überprüft der Treiber an, dass der Wert des Felds SQL_DESC_TYPE und die Werte für das SQL_DESC_TYPE-Feld in den gleichen Datensatz sind gültig und konsistent.  
  
 Das SQL_DESC_DATA_PTR-Feld eine IPD ist normalerweise nicht festgelegt. Allerdings erreichen eine Anwendung, um eine konsistenzprüfung des IPD-Feldern zu erzwingen. Der Wert, der das SQL_DESC_DATA_PTR-Feld der IPD festgelegt ist, werden eigentlich nicht gespeichert und kann nicht abgerufen werden, durch den Aufruf von **SQLGetDescField** oder **SQLGetDescRec**; die Einstellung erfolgt nur für das Erzwingen der Überprüfung der Projektkonsistenz. Eine konsistenzprüfung kann nicht auf eine IRD ausgeführt werden.  
  
 Weitere Informationen für die konsistenzprüfung finden Sie unter [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).
