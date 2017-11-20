---
title: Betroffen von ODBC-Komponenten | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a316cf7760534530b5663782532ada9fd6990662
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="affected-odbc-components"></a>Betroffene ODBC-Komponenten
Abwärtskompatibilität beschreibt, wie durch die Einführung einer neuen Version der Treiber-Manager-Anwendungen, Treiber-Manager und Treiber betroffen sind. Dies wirkt sich auf Anwendungen und Treiber, wenn eine oder beide Zertifikate in der alten Version bleiben. Es gibt daher drei Typen von Abwärtskompatibilität berücksichtigt werden, wie in der folgenden Tabelle gezeigt.  
  
|Typ|Version des Data Mining|Version der Anwendung|Version des Treibers|  
|----------|-------------------|----------------------------|-----------------------|  
|Abwärtskompatibilität des Treiber-Managers|3*.x*|2.*x*|2.*x*|  
|Abwärtskompatibilität des Treibers [1]|3*.x*|2.*x*|3.*x*|  
|Abwärtskompatibilität der Anwendung|3.*x*|3.*x*|2.*x*|  
  
 [1] die Abwärtskompatibilität der Treiber wird in erster Linie in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität erläutert.  
  
> [!NOTE]  
>  Eine mit Standards kompatible Anwendung – z. B. eine Anwendung, die in Übereinstimmung mit den Open Group oder ISO-CLI-Standards geschrieben wurden – wird sichergestellt, dass zum Arbeiten mit einer ODBC-3*.x* Treiber über die ODBC 3.*.x*-Treiber-Manager. Es wird vorausgesetzt, dass die Funktionalität, die die Anwendung nutzt im Treiber verfügbar ist. Des weiteren wird vorausgesetzt, dass die Standards kompatible Anwendung mit der ODBC 3. kompiliert wurde*.x* Headerdateien.

