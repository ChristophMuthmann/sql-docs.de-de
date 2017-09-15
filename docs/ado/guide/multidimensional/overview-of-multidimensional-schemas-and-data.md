---
title: "Übersicht über multidimensionale Schemas und Daten | Microsoft Docs"
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
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf3e8d6bebd5860df9f52236eecf4d1f287a8f9d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="overview-of-multidimensional-schemas-and-data"></a>Übersicht über multidimensionale Schemas und Daten
## <a name="understanding-multidimensional-schemas"></a>Grundlegendes zu MDX-Schemas  
 Das zentrale Metadatenobjekt in ADO MD ist die *Cube*, die besteht aus einem strukturierten Satz von verwandten Dimensionen, Hierarchien, Ebenen und Elemente.  
  
 Ein *Dimension* ist eine unabhängige Kategorie von Daten aus der mehrdimensionalen Datenbank, die Geschäftseinheiten abgeleitet. Eine Dimension enthält i. d. r. Elemente als die Abfragekriterien für die Measures der Datenbank verwendet werden.  
  
 Ein *Hierarchie* entspricht dem Pfad der Aggregation einer Dimension. Eine Dimension möglicherweise mehrere Ebenen der Granularität, die über-/ unterordnungsbeziehungen haben. Eine Hierarchie definiert, wie diese Ebenen verknüpft sind.  
  
 Ein *Ebene* ist ein Schritt der Aggregation in einer Hierarchie. Für Dimensionen mit mehreren Ebenen von Informationen ist jede Ebene einer Ebene.  
  
 Ein *Member* ist ein Datenelement in einer Dimension. In der Regel erstellen eine Beschriftung oder ein Maß für die Datenbank mithilfe von Membern beschreiben.  
  
 Cubes werden durch dargestellt [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) Objekte im ADO MD. Dimensionen, Hierarchien, Ebenen und Elemente werden auch durch die entsprechenden ADO MD-Objekte dargestellt: [Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [Hierarchie](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md), und [ Member](../../../ado/reference/ado-md-api/member-object-ado-md.md).  
  
### <a name="dimensions"></a>Dimensionen  
 Die Dimensionen eines Cubes hängen davon ab, die Geschäftseinheiten und die Typen von Daten in der Datenbank erstellt werden. In der Regel ist jede Dimension eine unabhängige Einstiegspunkt oder Mechanismus zum Auswählen von Daten.  
  
 Ein Cube mit Verkaufsdaten hat beispielsweise die folgenden fünf Dimensionen: Vertriebsmitarbeiter, Geography, Zeit, Produkte und Measures. Die Measures-Dimension enthält tatsächlichen Umsatzdaten Werte, während die andere Dimensionen darstellen Möglichkeiten zum Kategorisieren und gruppiert die Umsatzdaten Werte.  
  
 Die Geography-Dimension sind die folgenden Elemente:  
  
```  
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>Hierarchien  
 Definieren von Hierarchien die Möglichkeiten, in denen die Ebenen einer Dimension "Rollup" oder gruppiert werden können. Eine Dimension kann mehr als eine Hierarchie aufweisen. Eine natürliche Hierarchie ist in der Geography-Dimension vorhanden:  
  
### <a name="levels"></a>Levels  
 In der in der vorherigen Abbildung dargestellte Beispiel Geography-Dimension stellt jedes Feld eine Ebene in der Hierarchie dar.  
  
 Jede Ebene weist eine Menge von Elementen, wie folgt aus:  
  
-   die Welt`= {All}`  
  
-   Kontinente`= {North America, Europe}`  
  
-   Ländern`= {Canada, USA, UK, Germany}`  
  
-   Regionen`= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   Städte`= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>Element  
 Elemente auf der Blattebene einer Hierarchie haben keine untergeordneten Elemente und Elemente auf der Stammebene gibt es kein übergeordnetes. Alle anderen Elemente verfügen über mindestens ein übergeordnetes Element und mindestens ein untergeordnetes Element. Ein partielle Durchlauf der Hierarchie in der Geography-Dimension ergibt z. B. die folgenden über-und untergeordneten Beziehungen:  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 Mitglieder können entlang einer oder mehrerer Hierarchien pro Dimension konsolidiert werden. Betrachten Sie eine Zeitdimension, es zwei Möglichkeiten gibt, auf der Year-Ebene auf der Ebene Tage Rollup:  
  
 Dieses Beispiel zeigt darüber hinaus ein weiteres Merkmal: Einige Member der Ebene der Hierarchie Jahr-Woche-Woche werden nicht in jeder Ebene der Hierarchie Quartal eines Jahres angezeigt. Eine Hierarchie muss daher nicht alle Elemente einer Dimension enthalten.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO MD-Objektmodell](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Programmieren mit ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Verwenden von ADO mit ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Arbeiten mit mehrdimensionalen Daten](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
