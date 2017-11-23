---
title: Trennen von einer Quelle oder Treiber | Microsoft Docs
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
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e993502194d1d6a0ec5150db69f5cf436633e817
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Trennen von einer Quelle oder Treiber
Wenn eine Anwendung mithilfe einer Datenquelle abgeschlossen ist, ruft er **SQLDisconnect**. **SQLDisconnect** freigegeben alle Anweisungen, die für die Verbindung zugewiesen werden, und trennt den Treiber aus der Datenquelle. Es gibt einen Fehler zurück, wenn eine Transaktion durchgeführt wird.  
  
 Nach dem Trennen der Verbindung kann die Anwendung aufrufen kann **SQLFreeHandle** um die Verbindung freizugeben. Nach der Freigabe der Verbindungs, ist es ein anwendungsprogrammierungsfehler Fehler, die Verbindung Handle zu einem Aufruf von einer ODBC-Funktion zu verwenden. Dies hat sich nicht definierte, aber wahrscheinlich schwerwiegende Folgen. Wenn **SQLFreeHandle** aufgerufen wird, wird der Treiberversionen, die die Struktur zum Speichern von Informationen über die Verbindung verwendet.  
  
 Die Anwendung kann außerdem die Verbindung entweder zum Herstellen einer Verbindung mit einer anderen Datenquelle bzw. Erneutes Verbinden mit der gleichen Datenquelle wiederverwenden. Die Entscheidung, verbunden ist, im Gegensatz zu trennen und später, bleiben muss, dass der Autor der Anwendung die relativen Kosten für jede Option berücksichtigen; sowohl Herstellen einer Verbindung mit einer Datenquelle und die verbleibenden verbundenen können je nach Verbindungsmedium relativ kostspielig sein. In der Sie einen richtigen Kompromiss vornehmen, muss die Anwendung auch Annahmen über die Wahrscheinlichkeit und die zeitliche Steuerung von weitere Vorgänge auf die gleiche Datenquelle vornehmen.
