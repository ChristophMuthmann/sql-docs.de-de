---
title: 'Anhang G: Treiber Richtlinien für die Abwärtskompatibilität | Microsoft Docs'
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
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca8032b7eda2f96b4c8e8275c131dadd96d27538
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Anhang G: Treiber Richtlinien für die Abwärtskompatibilität
Dieser Anhang enthält Informationen für Treiber Writer auf ODBC 3. arbeiten. *x* Treiber, die ODBC-2 unterstützt werden müssen. *X* Anwendungen. Weitere Informationen zur Abwärtskompatibilität finden Sie unter [Abwärtskompatibilität und zur Einhaltung von Standards](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität für ODBC 3.x-Treiber](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) – neuen Funktionen sind Funktionen, die in ODBC 3. *X* und nicht in der ODBC-2. *X*. ODBC-3. *x* Treiber in der Regel keine Abwärtskompatibilität mit neuen Funktionen kümmern können, da ODBC 2. *X* Anwendungen verwenden nie diese. Die einzigen Ausnahmen sind Funktionen, die im Zusammenhang mit **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, und **SQLExtendedFetch**; Weitere Informationen Informationen finden Sie unter weiter unten in diesem Anhang.  
  
-   [Zuordnen von Funktionen als veraltet markiert](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) – doppeltes Funktionen sind Funktionen, die in ODBC 3. auf andere Weise implementiert werden. *X* und ODBC 2. *X*. ODBC-3. *x* Treiber müssen keine Abwärtskompatibilität mit doppelt vorhandenen Funktionen kümmern, da der Treiber-Manager immer ODBC 2. abgebildet. *X* -Funktionen, die ODBC 3. *X* Funktionen, wenn eine ODBC 3. aufrufen. *X* Treiber. Daher einen ODBC 3. *x* Treiber erkennt nur ODBC 3. *X* Funktionen. Weitere Informationen zu diesen Zuordnungen finden Sie unter weiter unten in diesem Anhang.  
  
-   [Verhaltensänderungen und ODBC 3.x-Treibern](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) – verhaltensänderungen sind Funktionen, die in ODBC 3. anders behandelt werden. *X* und ODBC 2. *X*. ODBC-3. *x* Treiber müssen das Verhalten ändert sich Gedanken machen, und fungieren als Antwort auf SQL_ATTR_ODBC_VERSION Umgebung Attributsatz von der Anwendung.
