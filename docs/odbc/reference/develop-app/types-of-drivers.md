---
title: Treibertypen | Microsoft Docs
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
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 711e71809a4c75eb4cb4507fc6528efa10dd07ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="types-of-drivers"></a>Treibertypen
ODBC-Treiber können wie folgt klassifiziert werden:  
  
-   **32-Bit-ODBC-2.**  
     ***X* Treiber** eine 32-Bit-Treiber, die:  
  
    -   Nur ODBC 2. exportiert*.x* Funktionen.  
  
    -   Weist auf ODBC 2. *x* Verhalten für verhaltensänderungen.  
  
-   **ISO "und" Open Group-kompatibler Treiber** eine 32-Bit-Treiber, die:  
  
    -   Exportiert alle Funktionen, die in den Dokumenten Open Group oder ISO-CLI dokumentiert sind. Dies schließt einige der Funktionen, die als veraltet markiert werden, in ODBC.  
  
    -   Ist das Verhalten der ODBC 3.0 für verhaltensänderungen.  
  
    -   Ist nicht unbedingt über ODBC 3.0-Treiber-Manager geleitet.  
  
-   **ODBC 3.0-Treiber** eine 32-Bit-Treiber, die:  
  
    -   Exporte nur Funktionen, die in ODBC 3.0 minus sind veraltete Funktionen.  
  
    -   Ist in der ODBC 2. Fehler. *x* Verhalten oder die ODBC 3.0-Verhalten in Bezug auf Änderungen am Systemverhalten basiert auf dem SQL_ATTR_APP_ODBC_VERSION-Umgebung-Attribut.  
  
-   **ODBC 3.5 (oder höher)-ANSI-Treiber** eine 32-Bit-Treiber, die:  
  
    -   Exporte nur Funktionen, die in ODBC 3.5 minus sind veraltete Funktionen.  
  
    -   Ist in der ODBC 2. Fehler. *x* Verhalten oder ODBC 3.0 Verhalten oder ODBC 3.5-Verhalten in Bezug auf Änderungen am Systemverhalten basiert auf dem SQL_ATTR_APP_ODBC_VERSION-Umgebung-Attribut.  
  
-   **ODBC-Treiber mit dem Unicode-3.5 (oder höher)** eine 32-Bit-Treiber, die:  
  
    -   Unterstützt alle Funktionen des ODBC 3.5 ANSI-Treibers.  
  
    -   Exportiert die Versionen von Unicode-Zeichenfolge für alle ODBC-APIs.  
  
    -   Speichern und Verarbeiten von Unicode-Daten in der Datenquelle.  
  
> [!NOTE]  
>  16-Bit-ODBC-Treiber funktioniert nicht direkt mit der ODBC-3. *x* -Treiber-Manager. Es ist jedoch möglich, dass 16-Bit-Treiber zum Arbeiten mit der 2.0-ODBC-Treiber-Manager das anschließend bis zu 3 Thunks. *x* -Treiber-Manager.
