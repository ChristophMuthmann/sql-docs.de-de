---
title: Reihenfolge der Statusdatensätze | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb0062575595b98932ba8e178e18218707cd90cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sequence-of-status-records"></a>Sequenz der Statusdatensätze
Wenn zwei oder mehr Statusdatensätze zurückgegeben werden, Ihre Rangordnung der Treiber-Manager und die Treiber nach den folgenden Regeln. Der Datensatz mit dem höchsten Rang ist der erste Datensatz. Die Quelle eines Datensatzes (Treiber-Manager, Treiber, Gateway, usw.) wird nicht berücksichtigt, wenn Datensätze Rangfolge.  
  
-   **Fehler** Statusdatensätze, die Fehler zu beschreiben, haben den höchsten Rang. Zwischen Fehlerdatensätze outrank Datensätze, die Angabe eines Transaktionsfehler oder mögliche Transaktionsfehler alle anderen Einträge. Wenn zwei oder mehr Datensätze die gleiche fehlerbedingung beschreiben, outrank SQLSTATEs, die von der Open Group-CLI-Spezifikation (Klassen 03 durch HZ) definierten ODBC definiert und treiberdefinierten SQLSTATEs an.  
  
-   **Die Implementierung definiertes keine Datenwerte** Statusdatensätze, die beschreiben, treiberdefinierten keine Daten Werte (Klasse 02) haben die zweite höchsten Rang.  
  
-   **Warnungen** Statusdatensätze, die beschreiben, Warnungen (01-Klasse) haben die niedrigsten Rang. Wenn zwei oder mehr Datensätze die gleichen warnungsbedingung, Warnung von der Open Group-CLI-Spezifikation definierten SQLSTATEs beschreiben outrank ODBC definiert und treiberdefinierten SQLSTATEs.  
  
 Wenn zwei oder mehr Datensätze mit dem höchsten Rang vorhanden sind, ist nicht definiert, welcher Datensatz des ersten Datensatzes ist. Die Reihenfolge der alle anderen Einträge ist nicht definiert. Insbesondere, da Warnungen vor dem Fehler angezeigt werden können, sollten Anwendungen alle Statusdatensätze überprüfen, wenn eine Funktion einen Wert als SQL_SUCCESS zurückgibt.
