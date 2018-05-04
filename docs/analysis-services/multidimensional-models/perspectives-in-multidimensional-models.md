---
title: Perspektiven in mehrdimensionalen Modellen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e5e8a1748e54ea08b124b1db1b6048fce456b2f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="perspectives-in-multidimensional-models"></a>Perspektiven in mehrdimensionalen Modellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Bei einer Perspektive handelt es sich um eine für eine bestimmte Anwendung oder Benutzergruppe erstellte Teilmenge eines Cubes. Der Cube selbst stellt die Standardperspektive dar. Eine Perspektive wird auf einem Client als Cube verfügbar gemacht. Wenn ein Benutzer eine Perspektive anzeigt, wird diese wie ein weiterer Cube angezeigt. Alle Änderungen, die an den Cubedaten durch Rückschreibevorgänge in der Perspektive vorgenommen wurden, erfolgen am Originalcube. Weitere Informationen zu den in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]enthaltenen Sichten finden Sie unter [Perspektiven](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md).  
  
 Verwenden Sie im Cube-Designer die Registerkarte **Perspektiven** , um Perspektiven in einem Cube zu erstellen oder zu ändern. Die erste Spalte der Registerkarte **Perspektiven** ist die Spalte **Cubeobjekte** , in der alle Objekte des Cubes aufgelistet sind. Diese Spalte entspricht der Standardperspektive des Cubes, mit der der Cube selbst dargestellt wird.  
  
## <a name="creating-or-deleting-perspectives"></a>Erstellen oder Löschen von Perspektiven  
 Sie können der Registerkarte **Perspektiven** eine Perspektive hinzufügen, indem Sie im Menü **Cube** auf **Neue Perspektive** klicken. Klicken Sie alternativ auf der Symbolleiste auf die Schaltfläche **Neue Perspektive** oder mit der rechten Maustaste auf eine beliebige Stelle im Bereich und dann im Kontextmenü auf **Neue Perspektive** . Sie können einem Cube eine beliebige Anzahl von Perspektiven hinzufügen.  
  
 Klicken Sie zum Entfernen einer Perspektive zunächst auf eine beliebige Zelle in der Spalte der zu löschenden Perspektive. Klicken Sie dann im Menü **Cube** auf **Perspektive löschen**. Klicken Sie alternativ auf der Symbolleiste auf die Schaltfläche **Perspektive löschen** oder mit der rechten Maustaste auf eine beliebige Zelle der zu löschenden Perspektive und dann im Kontextmenü auf **Perspektive löschen** .  
  
## <a name="renaming-perspectives"></a>Umbenennen von Perspektiven  
 In der ersten Zeile der jeweiligen Perspektive wird der Name der Perspektive angezeigt. Beim Erstellen einer Perspektive lautet der Name zunächst Perspektive (gefolgt von der Ordnungszahl, beginnend mit 1, falls eine Perspektive mit dem Namen Perspektive bereits vorhanden ist). Sie können auf den Namen klicken, um ihn zu bearbeiten.  
  
## <a name="hiding-objects-from-a-perspective"></a>Ausblenden von Objekten aus einer Perspektive  
 Deaktivieren Sie zum Ausblenden eines Objekts aus einer Perspektive das Kontrollkästchen in der Zeile, die dem Objekt in der Spalte der Perspektive entspricht. Die Cubeobjekte, die aus einer Perspektive ausgeblendet werden können, sind die folgenden:  
  
-   Measuregruppen  
  
-   Measures  
  
-   Dimensionen  
  
-   Hierarchien  
  
-   Benannte Mengen  
  
-   KPIs (Key Performance Indicators)  
  
-   Aktionen  
  
-   Berechnete Elemente  
  
 Erweitern Sie zum Anzeigen eines Objekts die Kategorie (**Measuregruppen**, **Dimensionen**, **KPIs**, **Berechnungen**oder **Aktionen**) für einen beliebigen Objekttyp unter **Cubeobjekte**. Erweitern Sie zunächst eine Dimension, und erweitern Sie dann die Zeile **Hierarchien** , um die Hierarchien einer Dimension anzuzeigen, oder die Zeile **Attribute** , um die Attribute einer Dimension anzuzeigen. Erweitern Sie die Measuregruppe, um die in einer Measuregruppe enthaltenen Measures anzuzeigen.  
  
## <a name="see-also"></a>Siehe auch  
 [Cubes in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
