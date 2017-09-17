---
title: Trennen von einer Quelle oder Treiber | Microsoft Docs
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
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a08f5de9829ee006c51ef6a2e795b44967c43a99
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Trennen von einer Quelle oder Treiber
Wenn eine Anwendung mithilfe einer Datenquelle abgeschlossen ist, ruft er **SQLDisconnect**. **SQLDisconnect** freigegeben alle Anweisungen, die für die Verbindung zugewiesen werden, und trennt den Treiber aus der Datenquelle. Es gibt einen Fehler zurück, wenn eine Transaktion durchgeführt wird.  
  
 Nach dem Trennen der Verbindung kann die Anwendung aufrufen kann **SQLFreeHandle** um die Verbindung freizugeben. Nach der Freigabe der Verbindungs, ist es ein anwendungsprogrammierungsfehler Fehler, die Verbindung Handle zu einem Aufruf von einer ODBC-Funktion zu verwenden. Dies hat sich nicht definierte, aber wahrscheinlich schwerwiegende Folgen. Wenn **SQLFreeHandle** aufgerufen wird, wird der Treiberversionen, die die Struktur zum Speichern von Informationen über die Verbindung verwendet.  
  
 Die Anwendung kann außerdem die Verbindung entweder zum Herstellen einer Verbindung mit einer anderen Datenquelle bzw. Erneutes Verbinden mit der gleichen Datenquelle wiederverwenden. Die Entscheidung, verbunden ist, im Gegensatz zu trennen und später, bleiben muss, dass der Autor der Anwendung die relativen Kosten für jede Option berücksichtigen; sowohl Herstellen einer Verbindung mit einer Datenquelle und die verbleibenden verbundenen können je nach Verbindungsmedium relativ kostspielig sein. In der Sie einen richtigen Kompromiss vornehmen, muss die Anwendung auch Annahmen über die Wahrscheinlichkeit und die zeitliche Steuerung von weitere Vorgänge auf die gleiche Datenquelle vornehmen.
