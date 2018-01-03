---
title: Treiber | Microsoft Docs
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
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2c7299dbbb9cce2f3c97344df33acf27d89c39f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="drivers"></a>Treiber
*Treiber* sind Bibliotheken, die die Funktionen der ODBC-API zu implementieren. Jede bezieht sich auf ein bestimmtes DBMS; z. B. keinen Treiber für Oracle direkten Zugriff auf Daten in einer Informix-DBMS. Treiber verfügbar machen, das die Funktionen des zugrunde liegenden DBMS. Sie sind nicht erforderlich, zum Implementieren von Funktionen, die nicht vom DBMS unterstützt. Sollten Sie den Treiber z. B. wenn das zugrunde liegende DBMS outer-Joins dann weder nicht unterstützt. Nur wichtige Ausnahme ist, dass die Treiber für DBMS-Systeme, die keine eigenständigen Datenbankmodule, z. B. Xbase, eine Datenbank-Engine implementieren müssen, die mindestens eine minimale Menge an SQL unterstützt.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Treiber-Aufgaben](../../odbc/reference/driver-tasks.md)  
  
-   [Treiberarchitektur](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Von Microsoft gelieferte ODBC-Treiber](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
