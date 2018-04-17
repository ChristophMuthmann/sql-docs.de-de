---
title: Umgebungshandles | Microsoft Docs
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
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffbc2ed4c1c496833237c3bda6d6e2c306a50cac
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="environment-handles"></a>Umgebungshandles
Ein *Umgebung* wird von ein globaler Kontext, in dem auf Daten zugegriffen; alle Informationen, die global in der Art, wie z. B. eine Umgebung zugeordnet ist:  
  
-   Status der Umgebung  
  
-   Die aktuelle Umgebung Anwendungsebene-Diagnose  
  
-   Die Ziehpunkte der Verbindungen, die für die Umgebung derzeit zugeordneten  
  
-   Die aktuellen Einstellungen der einzelnen Attribute Umgebung  
  
 Innerhalb eines Codeabschnitts, die ODBC (der Treiber-Manager oder eines Treibers) implementiert, gibt ein Umgebungshandle eine Struktur, um diese Informationen enthalten.  
  
 Umgebungshandles werden in ODBC-Anwendungen nicht häufig verwendet werden. Sie werden immer in Aufrufen verwendet **SQLDataSources** und **SQLDrivers** und manchmal in Aufrufen verwendet **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**, und **SQLGetDiagRec**.  
  
 Jeden Codeabschnitt, der ODBC (der Treiber-Manager oder eines Treibers) implementiert enthält eine oder mehrere-Umgebungshandles. Der Treiber-Manager führt beispielsweise eine separate Umgebungshandle für jede Anwendung, die mit ihm verbunden ist. Umgebungshandles zugeordnet **SQLAllocHandle** und mit freigegebenen **SQLFreeHandle**.
