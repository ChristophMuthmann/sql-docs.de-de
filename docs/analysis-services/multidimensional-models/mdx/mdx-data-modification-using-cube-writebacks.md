---
title: "Verwenden von Cuberückschreiben (MDX) | Microsoft Docs"
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
- writeback [Analysis Services], cubes
- cubes [Analysis Services], modifying
- modifying cubes
- UPDATE CUBE statement
- cubes [Analysis Services], writeback
ms.assetid: ae2385fc-7fa0-4f8e-98d7-dcb0a5f0eeea
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e1a704ba6b69cba4750df3e51e6e27d3626d877
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-data-modification---using-cube-writebacks"></a>MDX - Datenänderung: Verwenden von Cuberückschreiben
  Sie aktualisieren einen Cube, indem Sie die [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) -Anweisung verwenden. Mit dieser Anweisung können Sie ein Tupel mit einem bestimmten Wert aktualisieren. Damit Sie einen Cube mit der UPDATE CUBE-Anweisung effizient aktualisieren können, müssen Sie die Syntax der Anweisung, die Fehlerbedingungen, die auftreten können, und die Auswirkungen kennen, die Updates auf einen Cube haben können.  
  
## <a name="update-cube-statement-syntax"></a>Syntax der UPDATE CUBE-Anweisung  
 Die folgende Syntax beschreibt die UPDATE CUBE-Anweisung:  
  
```  
UPDATE [CUBE] <Cube_Name> SET <tuple>.VALUE = <value> [,<tuple>.VALUE = <value>...]  
 [ USE_EQUAL_ALLOCATION | USE_EQUAL_INCREMENT |  
  USE_WEIGHTED_ALLOCATION [BY <weight value_expression>] |  
  USE_WEIGHTED_INCREMENT [BY <weight value_expression>] ]   
```  
  
 Sind die Koordinaten für das Tupel nicht vollständig angegeben, wird für die nicht angegebenen Koordinaten das Standardelement der Hierarchie verwendet. Das identifizierte Tupel muss auf eine Zelle verweisen, die mit der [Sum](../../../mdx/sum-mdx.md) -Funktion aggregiert ist, und darf kein berechnetes Element als eine der Koordinaten der Zelle verwenden.  
  
 Sie können sich die UPDATE CUBE-Anweisung als Unterroutine vorstellen, die eine Reihe einzelner Rückschreibvorgänge für atomare Zellen generiert. Diese einzelnen Rückschreibvorgänge ergeben dann als Rollup die angegebene Summe.  
  
> [!NOTE]  
>  Wenn sich die aktualisierten Zellen nicht überlagern, kann mithilfe der **Update Isolation Level** -Eigenschaft der Verbindungszeichenfolge das Leistungsverhalten in Bezug auf UPDATE CUBE verbessert werden. Weitere Informationen finden Sie unter <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.  
  
## <a name="example"></a>Beispiel  
 Sie können UPDATE CUBE mithilfe der Sales Targets-Measuregruppe im Adventure Works-Cube testen. Die Measuregruppe enthält mithilfe von SUM aggregierte Measures, da dies eine Voraussetzung für UPDATE CUBE ist.  
  
1.  Aktivieren Sie das Rückschreiben für die Sales Targets-Measuregruppe in der Adventure Works-Datenbank. Klicken Sie in Management Studio mit der rechten Maustaste auf eine Measuregruppe, zeigen Sie auf **Rückschreibeoptionen**, und wählen Sie **Rückschreiben aktivieren**aus.  
  
     Im Ordner Rückschreiben sollte eine neue Rückschreibetabelle angezeigt werden. Der Tabellenname lautet "WriteTable_Fact Sales Quota".  
  
2.  Öffnen Sie ein MDX-Abfragefenster. Führen Sie die folgende SELECT-Anweisung aus, um den ursprünglichen Wert anzuzeigen:  
  
    ```  
    SELECT [Measures].[Sales Amount Quota] on 0 ,  
    [Employee].[Employee Department].[Title].&[Sales Representative].children on 1  
    FROM [Adventure Works]  
  
    ```  
  
     Für jeden Vertriebsmitarbeiter sollten Sollvorgaben angezeigt werden.  
  
3.  Führen Sie die UPDATE CUBE-Anweisung aus, um einen neuen Wert zurückzuschreiben. In diesem Beispiel wird die Sollvorgabe auf 0 festgelegt. Weil der neue Wert 0 beträgt, geben Sie keine Zuordnungsmethode an.  
  
    ```  
    UPDATE CUBE [Adventure Works]   
    SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 0  
  
    ```  
  
4.  Führen Sie die SELECT-Anweisung erneut aus. Jetzt sollte für die Vorgaben der Wert 0 angezeigt werden.  
  
 Der Rückschreibewert ist auf die aktuelle Sitzung beschränkt. Um den Wert benutzer- und sitzungsübergreifend beizubehalten, verarbeiten Sie die Rückschreibetabelle. Klicken Sie in Management Studio mit der rechten Maustaste auf WriteTable_Fact Sales Quota, und wählen Sie **Verarbeiten**aus.  
  
 Damit eine Zuordnungsmethode angegeben werden kann, muss der neue Wert größer als 0 sein. In diesem Beispiel beträgt der neue Wert für Sales Amount Quota zwei Millionen und wird durch die Zuordnungsmethode auf alle Vertriebsmitarbeiter verteilt.  
  
```  
UPDATE CUBE [Adventure Works]   
SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 2000000   
USE_EQUAL_ALLOCATION  
```  
  
## <a name="error-conditions"></a>Fehlerbedingungen  
 In der folgenden Tabelle sind sowohl die möglichen Ursachen für Fehler bei Rückschreibvorgängen als auch die Ergebnisse solcher Fehler beschrieben.  
  
|Fehlerbedingung|Ergebnis|  
|---------------------|------------|  
|Das Update beinhaltet Elemente aus derselben Dimension, die es nicht gemeinsam gibt.|Das Update erzeugt einen Fehler. Der Cuberaum enthält nicht die Zelle, auf die verwiesen wird.|  
|Das Update beinhaltet ein Measure, dessen Quelle ein Measure mit einem Datentyp ohne Vorzeichen ist.|Das Update erzeugt einen Fehler. Für Inkremente ist es erforderlich, dass das Measure einen negativen Wert annehmen kann.|  
|Das Update beinhaltet ein Measure, das nicht als Summe aggregiert wird.|Ein Fehler wird ausgelöst.|  
|Das Update wurde für einen Teilcube versucht.|Ein Fehler wird ausgelöst.|  
  
## <a name="affect-of-cube-changes"></a>Auswirkungen von Cubeänderungen  
 Die folgenden Änderungen wirken sich nicht auf ein Rückschreiben aus:  
  
-   Verarbeiten eines Cubes, der Measuregruppen des Cubes oder der Dimensionen des Cubes.  
  
-   Hinzufügen von Attributen zu einer Dimension.  
  
-   Hinzufügen einer neuen Dimension.  
  
-   Löschen einer Dimension, in der das Rückschreiben nicht enthalten ist.  
  
-   Hinzufügen, Ändern oder Entfernen einer Hierarchie.  
  
-   Hinzufügen eines neues Measures.  
  
 Die folgenden Änderungen können nicht vorgenommen werden, ohne die Rückschreibedaten zu entfernen:  
  
-   Löschen eines Attributs oder der Hierarchie des Attributs, wenn das Attribut im Rückschreiben enthalten ist. Dazu gehören explizit das Entfernen des Attributs oder seiner Hierarchie sowie das Entfernen der übergeordneten Dimension des Attributs.  
  
-   Löschen eines Measures, das im Rückschreiben enthalten ist.  
  
-   Hinzufügen eines Attributs ohne eine **(All)** -Ebene zu einer Dimension, die im Rückschreiben enthalten ist.  
  
-   Ändern der Dimensionsgranularität für eine Dimension, die im Rückschreiben enthalten ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Ändern von Daten &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)  
  
  

