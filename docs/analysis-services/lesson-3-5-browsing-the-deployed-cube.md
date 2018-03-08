---
title: Durchsuchen des bereitgestellten Cubes | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 849c6109-1453-4fe4-a892-c49a982cfadb
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8ddbefdcbc54c076c801e5f4d83e107e48ac5ba9
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="lesson-3-5---browsing-the-deployed-cube"></a>Lektion 3 bis 5 – Durchsuchen des bereitgestellten Cubes
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

In der folgenden Aufgabe durchsuchen Sie den [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial-Cube. Da Measures in der Analyse dimensionsübergreifend verglichen werden, verwenden Sie zum Durchsuchen von Daten eine Excel-PivotTable. Mithilfe einer PivotTable lassen sich Kunden-, Datums- und Produktinformationen auf verschiedenen Achsen platzieren. So können Sie verfolgen, wie sich die Internetverkäufe ändern, wenn sie für bestimmte Zeiträume, Kundendemografien und Produktlinien angezeigt werden.  
  
### <a name="to-browse-the-deployed-cube"></a>So durchsuchen Sie den bereitgestellten Cube  
  
1.  Doppelklicken Sie auf den Cube [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]-Tutorial **[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , der sich im Ordner** Cubes **des Projektmappen-Explorers befindet, um zum Cube-Designer in** zu wechseln.  
  
2.  Öffnen Sie die Registerkarte **Browser** , und klicken Sie dann auf der Symbolleiste des Designers auf die Schaltfläche **Verbindung wiederherstellen** .  
  
3.  Klicken Sie auf das Excel-Symbol, um Excel zu starten, wobei die Arbeitsbereichsdatenbank als Datenquelle verwendet wird. Sobald Sie aufgefordert werden, Verbindungen zu aktivieren, klicken Sie auf **Aktivieren**.  
  
4.  Erweitern Sie in der PivotTable-Feldliste **Internet Sales**, und ziehen Sie dann das **Sales Amount** -Measure in den Bereich **Werte** .  
  
5.  Erweitern Sie in der PivotTable-Feldliste den Eintrag **Product**.  
  
6.  Ziehen Sie die **Product Model Lines** -Benutzerhierarchie in den Bereich **Spalten** .  
  
7.  Erweitern Sie in der PivotTable-Feldliste die Option **Customer**, erweitern Sie **Location**, und ziehen Sie die **Customer Geography** -Hierarchie aus dem Anzeigeordner **Location** in der Customer-Dimension in den Bereich Zeilen.  
  
8.  Erweitern Sie in der PivotTable-Feldliste den Eintrag **Order Date**, und ziehen Sie dann die **Order Date.Calendar Date** -Hierarchie in den Bereich **Berichtsfilter** .  
  
9. Klicken Sie auf den Filter rechts vom Filter **Order Date.Calendar Date** im Datenbereich, deaktivieren Sie das Kontrollkästchen für die Ebene **(Alle)** , erweitern Sie **2006**&gt; **H1 CY 2006**&gt; **Q1 CY 2006**, aktivieren Sie das Kontrollkästchen für **Februar 2006**, und klicken Sie anschließend auf **OK**.  
  
    Internetverkäufe nach Region und Produktgruppe für den Monat Februar 2006 werden wie im folgenden Bild angezeigt.  
  
    ![Internetverkäufe nach Region und Produktgruppe](../analysis-services/media/l3-cube-browser-finish.gif "Internetverkäufe nach Region und Produktgruppe")  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 4: Definieren von erweiterten Attributen und Dimensionseigenschaften](../analysis-services/lesson-4-defining-advanced-attribute-and-dimension-properties.md)  
  
  
  
