---
title: "Datentypunterstützung | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 147e940dcd37b452e1fe05b3a39f6b184c810397
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-support"></a>Datentypunterstützung
ODBC-Treiber müssen mindestens eine der SQL_CHAR und SQL_VARCHAR unterstützen. Unterstützung für andere Datentypen wird durch das der Treiber oder die Datenquelle SQL-92-Konformitätsgrad bestimmt. Eine Anwendung sollte Aufrufen **SQLGetTypeInfo** um zu bestimmen, die vom Treiber unterstützten Datentypen.  
  
 Weitere Informationen zu Datentypen finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).

