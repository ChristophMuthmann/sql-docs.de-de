---
title: Anweisungsattribute | Microsoft Docs
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
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9c5ccfeb2d7cf3ba4b0db5767ced1eeeee92c960
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="statement-attributes"></a>Anweisungsattribute
Anweisungsattribute sind Eigenschaften der Anweisung. Ob Sie Lesezeichen und welche Art von verwenden Cursor für die Verwendung mit der Anweisung Ergebnis festgelegt sind, z. B. Anweisungsattribute.  
  
 Anweisungsattribute werden mit festgelegt **SQLSetStmtAttr** und mit ihren aktuellen Einstellungen abgerufen **SQLGetStmtAttr**. Es ist nicht erforderlich, dass eine Anwendung Anweisungsattribute festlegen. Alle Anweisungsattribute haben Standardwerte, von die einige Treiber-spezifisch sind.  
  
 Wenn ein Anweisungsattribut festgelegt werden können, hängt das Attribut selbst ab. Die Anweisungsattribute SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE SQL_ATTR_SIMULATE_CURSOR und SQL_ATTR_USE_BOOKMARKS müssen festgelegt werden, bevor die Anweisung ausgeführt wird. Die Anweisungsattribute SQL_ATTR_ASYNC_ENABLE und SQL_ATTR_NOSCAN können zu einem beliebigen Zeitpunkt festgelegt werden, jedoch werden nicht angewendet werden, bis die Anweisung erneut verwendet wird. SQL_ATTR_MAX_LENGTH und SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT Anweisungsattribute können zu einem beliebigen Zeitpunkt festgelegt werden allerdings handelt es sich treiberspezifische gibt an, ob sie angewendet werden, bevor die Anweisung erneut verwendet wird. Die verbleibenden Anweisungsattribute können zu einem beliebigen Zeitpunkt festgelegt werden.  
  
> [!NOTE]  
>  Die Fähigkeit zum Festlegen von Anweisungsattribute auf der Verbindungsebene durch Aufrufen von **SQLSetConnectAttr** in ODBC 3. ist veraltet. *X*. ODBC-3. *x* Anwendungen Anweisungsattribute auf Verbindungsebene darf nicht festgelegt werden. ODBC-3. *x* Treiber müssen nur diese Funktionalität unterstützen, wenn sie mit ODBC 2. funktionieren sollte. *X* Anwendungen. Weitere Informationen finden Sie unter [SQLSetConnectOption Zuordnung](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
>   
>  Eine Ausnahme ist die SQL_ATTR_METADATA_ID und SQL_ATTR_ASYNC_ENABLE-Attribute, die Verbindungsattribute und Anweisungsattribute werden und entweder auf der Verbindungsebene oder Anweisungsebene festgelegt werden können.  
>   
>  Keines der Anweisungsattribute in ODBC 3. eingeführt. *x* (mit Ausnahme von SQL_ATTR_METADATA_ID) kann auf der Verbindungsebene festgelegt werden.  
  
 Weitere Informationen finden Sie unter der [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) funktionsbeschreibung.
