---
title: Reihenfolge der Statusdatensätze | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: c4b1e2ceea30ecb62dd96be283bb150d2e43385a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sequence-of-status-records"></a>Sequenz der Statusdatensätze
Wenn zwei oder mehr Statusdatensätze zurückgegeben werden, Ihre Rangordnung der Treiber-Manager und die Treiber nach den folgenden Regeln. Der Datensatz mit dem höchsten Rang ist der erste Datensatz. Die Quelle eines Datensatzes (Treiber-Manager, Treiber, Gateway, usw.) wird nicht berücksichtigt, wenn Datensätze Rangfolge.  
  
-   **Fehler** Statusdatensätze, die Fehler zu beschreiben, haben den höchsten Rang. Zwischen Fehlerdatensätze outrank Datensätze, die Angabe eines Transaktionsfehler oder mögliche Transaktionsfehler alle anderen Einträge. Wenn zwei oder mehr Datensätze die gleiche fehlerbedingung beschreiben, outrank SQLSTATEs, die von der Open Group-CLI-Spezifikation (Klassen 03 durch HZ) definierten ODBC definiert und treiberdefinierten SQLSTATEs an.  
  
-   **Die Implementierung definiertes keine Datenwerte** Statusdatensätze, die beschreiben, treiberdefinierten keine Daten Werte (Klasse 02) haben die zweite höchsten Rang.  
  
-   **Warnungen** Statusdatensätze, die beschreiben, Warnungen (01-Klasse) haben die niedrigsten Rang. Wenn zwei oder mehr Datensätze die gleichen warnungsbedingung, Warnung von der Open Group-CLI-Spezifikation definierten SQLSTATEs beschreiben outrank ODBC definiert und treiberdefinierten SQLSTATEs.  
  
 Wenn zwei oder mehr Datensätze mit dem höchsten Rang vorhanden sind, ist nicht definiert, welcher Datensatz des ersten Datensatzes ist. Die Reihenfolge der alle anderen Einträge ist nicht definiert. Insbesondere, da Warnungen vor dem Fehler angezeigt werden können, sollten Anwendungen alle Statusdatensätze überprüfen, wenn eine Funktion einen Wert als SQL_SUCCESS zurückgibt.
