---
title: Cursorvorgänge-Bibliothek | Microsoft Docs
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
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0bac09cb2b45274a5589c152a5b0e714b71f8dc1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-library-operations"></a>Cursorvorgänge-Bibliothek
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Wenn eine Anwendung mit dem Arbeiten mit einer ODBC 2.*.x* Treiber nimmt Aufrufe an die ODBC 3. *X* Cursorbibliothek, die Anwendung möglicherweise ODBC 3. *X* Funktionen, die nicht von der ODBC-2 unterstützt werden*.x* Treiber. Der Autor einer Anwendung sollten vorsichtig sein, wie diese Funktionen verwendet werden, jedoch. Verwenden der ODBC-3. *x* Cursorbibliothek führt nicht dazu, dass einer ODBC 2.*.x* Treiber in einer ODBC-3. *X* Treiber.
