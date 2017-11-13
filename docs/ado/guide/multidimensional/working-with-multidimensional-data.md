---
title: Arbeiten mit mehrdimensionalen Daten | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e14c59fd0620129486408d33339e80624743f02
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="working-with-multidimensional-data"></a>Arbeiten mit mehrdimensionalen Daten
Ein *Cellset* ist das Ergebnis einer Abfrage auf mehrdimensionalen Daten. Er besteht aus einer Auflistung von Achsen, in der Regel nicht mehr als vier Achsen und in der Regel nur zwei oder drei. Ein *Achse* ist eine Auflistung von Elementen aus einer oder mehreren Dimensionen, die suchen oder Filtern bestimmte Werte in einem Cube verwendet wird.  
  
 Ein *Position* entspricht einem Punkt auf einer Achse. Für eine Achse bestehend aus einer einzelnen Dimensions ist sind diese Positionen eine Teilmenge der Dimensionselemente. Wenn eine Achse besteht aus mehreren Dimensionen, jede Position ist eine zusammengesetzte Entität hat  *n*  Teile Where  *n*  ist die Anzahl der Dimensionen, die entlang dieser Achse ausgerichtet. Jeder Teil der Position ist ein Element aus einer einzelnen Dimension.  
  
 Z. B. wenn die geografischen Daten und Dimensionen aus einem Cube mit Verkaufsdaten entlang der x-Achse eines cellSets ausgerichtet sind, kann eine Position entlang dieser Achse die Elemente "USA" und "Agents". enthalten In diesem Beispiel erfordert das Ermitteln einer Position entlang der x-Achse, dass Elemente aus jeder Dimension auf der Achse ausgerichtet sind.  
  
 Ein *Zelle* ist ein Objekt am Schnittpunkt der Achsenkoordinaten positioniert. Jede Zelle verfügt über mehrere Angaben zugeordnet, einschließlich der Daten selbst, eine formatierte Zeichenfolge (anzeigbaren Form von Zellendaten) und den Ordnungswert der Zelle. (Jede Zelle ist eine eindeutige Ordinalwert im Cellset dar. Der Ordnungswert der ersten Zelle im Cellset dar ist 0 (null), während die am weitesten links stehende Zelle in der zweiten Zeile eines cellSets mit acht Spalten einen Ordnungswert des acht müssten.)  
  
 Ein Cube enthält beispielsweise die folgenden sechs Dimensionen (Beachten Sie, dass diese Cubeschema von den in dem Beispiel geringfügig [Übersicht über multidimensionale Schemas und Daten](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   Vertriebsmitarbeiter  
  
-   Geography (natürliche Hierarchie) – Kontinente, Länder, Bundesstaaten und usw.  
  
-   Quartale – Quartale, Monate, Tage  
  
-   Years  
  
-   Measures – Sales Prozent, BudgetedSales  
  
-   Products  
  
 Die folgenden Cellset stellt Sales für 1991 für alle Produkte:  
  
> [!NOTE]
>  Die Zellenwerte im Beispiel können als geordnete Koordinatenpaare Achse Position Ordinalzahlen angezeigt werden, wobei die erste Ziffer Position auf der x-Achse und die zweite Zahl die Position der y-Achse darstellt.  
  
 Die Merkmale dieses Cellset lauten wie folgt:  
  
-   Achsendimensionen: Quartale, Vertriebsmitarbeiter, Geography  
  
-   Filtern von Dimensionen: Measures Jahre Produkte  
  
-   Zwei Achsen: Spalten-(X oder Achse 0) und (y oder Achse 1)  
  
-   x-Achse: zwei geschachtelte Dimensionen, Vertriebsmitarbeiter und Geografie  
  
-   y-Achse: Quartale-Dimension  
  
 Die x-Achse enthält zwei geschachtelte Dimensionen: Verkäufer und Geografie. In Geography, vier Elemente ausgewählt sind: Seattle, Boston, USA Süden und Japan. Zwei Member von Vertriebsmitarbeiter ausgewählt sind: Mein Schatz und Nash. Dies ergibt eine Summe von acht Positionen auf dieser Achse (8 = 4 * 2).  
  
 Jede Koordinate wird als eine Position mit zwei Membern dargestellt – eine von der Dimension Vertriebsmitarbeiter und anderen von der Geography-Dimension:  
  
```  
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Die y-Achse enthält nur eine Dimension mit den folgenden acht Positionen:  
  
```  
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 CellSets, Zellen, Achsen und Positionen werden alle dargestellt in ADO MD durch die entsprechenden Objekte: [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [Zelle](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [Achse](../../../ado/reference/ado-md-api/axis-object-ado-md.md), und [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ADO MD-Objektmodell](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Übersicht über multidimensionale Schemas und Daten](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programmieren mit ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Verwenden von ADO mit ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)

