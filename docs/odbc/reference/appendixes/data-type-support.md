---
title: "Datentypunterstützung | Microsoft Docs"
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
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b0d3f96885ba2f317759280e859fdcdc4977a5e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="data-type-support"></a>Datentypunterstützung
ODBC-Treiber müssen mindestens eine der SQL_CHAR und SQL_VARCHAR unterstützen. Unterstützung für andere Datentypen wird durch das der Treiber oder die Datenquelle SQL-92-Konformitätsgrad bestimmt. Eine Anwendung sollte Aufrufen **SQLGetTypeInfo** um zu bestimmen, die vom Treiber unterstützten Datentypen.  
  
 Weitere Informationen zu Datentypen finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).
