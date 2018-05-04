---
title: Konvertierung von Datentypen | Microsoft Docs
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
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0501e4bf627d8dafddfbf5020345d43135af9d6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-conversions"></a>Datentypkonvertierungen
Daten konvertiert werden können von einem Typ in einen anderen an einem der vier Mal: Wenn Daten übertragen aus einer Anwendungsvariablen in eine andere (C#, C) Sendens von Daten in einer Anwendungsvariablen an einen Anweisungsparameter (C zu SQL) zurückgegebenen Daten in einer Resultsetspalte eine Anwendungsvariable (SQL zu C), und wenn Daten aus einer Spalte für die Datenquelle an eine andere (SQL to SQL) übertragen wird.  
  
 Für jede Konvertierung, die auftritt, wenn Daten aus einer Anwendungsvariablen auf einen anderen übertragen werden, liegt außerhalb des Bereichs dieses Dokuments.  
  
 Wenn eine Anwendung einem Ergebnis Spalte(n) Anweisung Mengenparameter für eine Variable gebunden, gibt die Anwendung einen datentypkonvertierungsfehler implizit in seiner Wahl des Datentyps der Anwendungsvariablen. Nehmen Sie beispielsweise an, dass eine Spalte ganzzahlige Daten enthält. Wenn die Anwendung auf die Spalte eine ganzzahlige Variable bindet, gibt es an, dass keine Konvertierung ausgeführt werden; Wenn die Anwendung eine Zeichenvariable auf die Spalte bindet, gibt es an, dass die Daten aus Ganzzahl in Zeichen konvertiert werden.  
  
 ODBC definiert, wie Daten zwischen jeder SQL- und C-Datentyp konvertiert werden. Im Grunde ODBC unterstützt alle angemessene Konvertierungen, z. B. ein Zeichen-, Integer und ganze Zahl, "float", und unterstützt keine Standardschaltfläche Konvertierungen, z. B. "float", um Datum. Treiber sind erforderlich, um alle Konvertierungen für jeden SQL-Datentyp unterstützen, die sie unterstützen. Eine vollständige Liste der Konvertierung zwischen SQL und C-Datentypen finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) und [Konvertieren von Daten von C-in SQL-Datentypen](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) in Anhang D:-Datentypen.  
  
 ODBC definiert auch eine skalare Funktion zum Konvertieren von Daten von einem SQL-Datentyp in einen anderen. Die **konvertieren** skalare Funktion wird vom Treiber auf die zugrunde liegenden skalaren Funktion oder Funktionen, die zum Durchführen von Konvertierungen in der Datenquelle definiert zugeordnet. Da diese Funktion DBMS-spezifische Funktionen zugeordnet ist, werden keine ODBC definiert, Funktionsweise dieser Konvertierungen oder welche Konvertierungen unterstützt werden müssen. Eine Anwendung ermittelt, welche Konvertierungen von einem bestimmten Treiber und einer Datenquelle durch die SQL_CONVERT Optionen in unterstützt werden **SQLGetInfo**. Weitere Informationen zu den **konvertieren** Skalarfunktion, finden Sie unter [Escapesequenzen in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) und [explizite Umwandlungsfunktion für Datentyp](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
