---
title: "Ändern von Measures | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 350fadc471d30f79b8b1e6b1e8d63cc507f1d484
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-3-1---modifying-measures"></a>Lektion 3: 1-Ändern von Measures
Sie können die **FormatString** -Eigenschaft verwenden, um Formatierungseinstellungen zu definieren, die die Darstellung von Measures steuern. In dieser Aufgabe geben Sie Formatierungseigenschaften für die Währungs- und Prozentsatzmeasures im [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial-Cube an.  
  
### <a name="to-modify-the-measures-of-the-cube"></a>So ändern Sie die Measures des Cubes  
  
1.  Wechseln Sie zur Registerkarte **Cubestruktur** des Cube-Designers für den [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial-Cube, erweitern Sie die **Internet Sales** -Measuregruppe im Bereich **Measures** , klicken Sie mit der rechten Maustaste auf **Order Quantity**, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Klicken Sie im Eigenschaftenfenster auf das Pushpin-Symbol **Automatisch im Hintergrund** , um das Eigenschaftenfenster offen zu halten.  
  
    Das Ändern von Eigenschaften für eine Reihe von Elementen ist einfacher, wenn das Eigenschaftenfenster geöffnet bleibt.  
  
3.  Klicken Sie im Eigenschaftenfenster auf die Liste **FormatString** , und geben Sie anschließend **#,#**ein.  
  
4.  Klicken Sie auf der Symbolleiste der Registerkarte **Cubestruktur** auf der linken Seite auf das Symbol **Measuresraster anzeigen** .  
  
    In der Rasteransicht können Sie mehrere Measures gleichzeitig auswählen.  
  
5.  Wählen Sie eine der folgenden Measures aus. Um mehrere Measures auszuwählen, halten Sie beim Klicken die STRG-TASTE gedrückt:  
  
    -   **Unit Price**  
  
    -   **Extended Amount**  
  
    -   **Discount Amount**  
  
    -   **Product Standard Cost**  
  
    -   **Total Product Cost**  
  
    -   **Sales Amount**  
  
    -   **Tax Amt**  
  
    -   **Freight**  
  
6.  Wählen Sie im Eigenschaftenfenster in der **FormatString** -Liste **Currency**aus.  
  
7.  Wählen Sie im Dropdown-Listenfeld oben im Eigenschaftenfenster (rechts unterhalb der Titelleiste) das Measure **Unit Price Discount Pct**und anschließend in der Liste **FormatString** die Option **Percent** aus.  
  
8.  Ändern Sie im Eigenschaftenfenster die **Name** -Eigenschaft für das **Unit Price Discount Pct** -Measure zu **Unit Price Discount Percentage**.  
  
9. Klicken Sie im Bereich **Measures** auf **Tax Amt** , und ändern Sie den Namen dieses Measures in **Tax Amount**.  
  
10. Klicken Sie im Eigenschaftenfenster auf das Symbol **Automatisch im Hintergrund** , um das Eigenschaftenfenster auszublenden, und anschließend auf der Symbolleiste der Registerkarte **Cubestruktur** auf **Measuresstruktur anzeigen** .  
  
11. Klicken Sie im Menü **Datei** auf **Alle speichern**.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Ändern der Customer-Dimension](../analysis-services/lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>Siehe auch  
[Definieren von Datenbankdimensionen](../analysis-services/multidimensional-models/define-database-dimensions.md)  
[Konfigurieren von Measureeigenschaften](../analysis-services/multidimensional-models/configure-measure-properties.md)  
  
  
  

