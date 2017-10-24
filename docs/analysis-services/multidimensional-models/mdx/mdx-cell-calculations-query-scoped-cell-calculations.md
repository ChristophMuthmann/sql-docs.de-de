---
title: Erstellen die Abfrage Zellberechnungen (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITH keyword
- query-scoped cell calculations [MDX]
ms.assetid: 45987daa-4400-41e9-add7-2428fd75709b
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8c2d0cffb212b062f1c1ff8f39929e201dc642c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-cell-calculations---query-scoped-cell-calculations"></a>MDX-Zellenberechnungen - Zellenberechnungen im Bereich einer Abfrage
  Sie verwenden das **WITH** -Schlüsselwort in MDX (Multidimensional Expressions) dazu, berechnete Zellen im Kontext einer Abfrage zu beschreiben. Das **WITH** -Schlüsselwort hat die folgende Syntax:  
  
```  
WITH CELL CALCULATION Cube_Name.CellCalc_Identifier  String_Expression  
```  
  
 Der `CellCalc_Identifier` -Wert ist der Name der berechneten Zellen. Der `String_Expression` -Wert enthält eine Liste aus orthogonalen, eindimensionalen MDX-Mengenausdrücken. Für jeden dieser Mengenausdrücke gilt, dass sein Wert zu einer der Kategorien gehören muss, die in der folgenden Tabelle aufgeführt sind.  
  
|Kategorie|Beschreibung|  
|--------------|-----------------|  
|Leere Menge|Ein MDX-Mengenausdruck, der zu einer leeren Menge aufgelöst wird. In diesem Fall ist der Gültigkeitsbereich der berechneten Zelle gleich dem gesamten Cube.|  
|Menge mit einem einzelnen Element|Ein MDX-Mengenausdruck, der zu einem einzelnen Element aufgelöst wird.|  
|Menge von Ebenenelementen|Ein MDX-Mengenausdruck, der zu den Elementen einer einzelnen Ebene aufgelöst wird. Ein Beispiel für einen solchen Mengenausdruck ist die MDX-Funktion *Level_Expression*.**Members** . Verwenden Sie zum Einzuschließen berechneter Elemente die MDX-Funktion *Level_Expression*.**AllMembers**. Weitere Informationen finden Sie unter [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md).|  
|Menge nachfolgender Werte|Ein MDX-Mengenausdruck, der zu den nachfolgenden Werten eines angegebenen Elements aufgelöst wird. Ein Beispiel für einen solchen Mengenausdruck ist die MDX-Funktion **Descendants**(*Member_Expression*, *Level_Expression*, *Desc_Flag*). Weitere Informationen finden Sie unter [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md).|  
  
 Wenn das `String_Expression` -Argument eine Dimension nicht beschreibt, nimmt MDX an, dass alle Elemente beim Erstellen des Berechnungsteilcubes eingeschlossen werden. Daher gilt die Definition berechneter Zellen für den gesamten Cube, wenn das `String_Expression` -Argument den Wert NULL hat.  
  
 Das `MDX_Expression` -Argument enthält einen MDX-Ausdruck, der zu einem Zellwert für alle im `String_Expression` -Argument definierten Zellen ausgewertet wird.  
  
## <a name="additional-considerations"></a>Weitere Überlegungen  
 MDX verarbeitet die in der **CONDITION** -Eigenschaft angegebene Berechnungsbedingung nur einmal. Diese einmalige Verarbeitung verbessert die Leistung bei der Auswertung mehrerer Definitionen berechneter Zellen. Dies gilt insbesondere, wenn berechnete Zellen in Cubedurchläufen überlappen.  
  
 Wann diese einmalige Verarbeitung erfolgt, hängt davon ab, für welchen Gültigkeitsbereich die Definition der berechneten Zellen erstellt wurde:  
  
-   Wurde sie im globalen Gültigkeitsbereich als Teil eines Cubes erstellt, verarbeitet MDX die Berechnungsbedingung, wenn der Cube verarbeitet wird. Wenn Zellen in dem Cube geändert werden und die Zellen im Berechnungsteilcube einer Definition berechneter Zellen enthalten sind, ist die Berechnungsbedingung möglicherweise fehlerhaft, bis der Cube erneut verarbeitet wird. Änderungen an Zellen können sich z. B. aus Rückschreibevorgängen ergeben. Die Berechnungsbedingung wird bei der erneuten Verarbeitung des Cubes erneut verarbeitet.  
  
-   Wenn die Berechnungsbedingung im Gültigkeitsbereich einer Sitzung erstellt wurde, wird sie von MDX verarbeitet, wenn die Anweisung während der Sitzung ausgegeben wird. Genauso wie bei im globalen Gültigkeitsbereich erstellten Definitionen berechneter Zellen gilt bei einer Änderung von Zellen, dass die Berechnungsbedingung möglicherweise für die Definition berechneter Zellen fehlerhaft ist.  
  
-   Wenn die Berechnungsbedingung im Gültigkeitsbereich einer Abfrage erstellt wurde, wird sie von MDX verarbeitet, wenn die Abfrage ausgeführt wird. Hier tritt ebenfalls das Problem der Zellenänderungen auf, obwohl Probleme der Datenlatenzzeit minimal sind, da die Verarbeitungszeit bei der Ausführung einer MDX-Abfrage sehr kurz ist.  
  
 Andererseits verarbeitet MDX die Berechnungsformel immer dann, wenn eine MDX-Abfrage für den Cube ausgegeben wird, bei der Zellen aus der Definition berechneter Zellen betroffen sind. Diese Verarbeitung erfolgt unabhängig vom Gültigkeitsbereich bei der Erstellung.  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE CELL CALCULATION-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-cell-calculation.md)  
  
  

