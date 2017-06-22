---
title: "Hervorheben von Diagrammdaten durch Hinzufügen von Bereichsstreifen (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: addd6137-4b6e-4e88-a7e8-9600fcd1ccce
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 04bc46bc61a1091d715e348e44ac7ee22e4a891d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs"></a>Hervorheben von Diagrammdaten durch Hinzufügen von Bereichsstreifen (Berichts-Generator und SSRS)
  Bereichsstreifen oder Streifen sind horizontale oder vertikale Bereiche, die den Hintergrund des Diagramms in regelmäßigen oder benutzerdefinierten Abständen schattieren. Mithilfe von Bereichsstreifen können Sie Folgendes tun:  
  
-   Die Lesbarkeit für das Suchen nach einzelnen Werten im Diagramm verbessern. Geben Sie in regelmäßigen Abständen Bereichsstreifen an, damit die verschiedenen Datenpunkte beim Lesen des Diagramms leichter erkennbar sind.  
  
-   Termine hervorheben, die in regelmäßigen Abständen auftreten. Beispielsweise können Sie in einem Verkaufsbericht Bereichsstreifen verwenden, um Wochenenddatenpunkte zu identifizieren.  
  
-   Einen bestimmten Schlüsselbereich hervorheben. Unter Verwendung des vorherigen Beispiels können Sie z. B. mithilfe eines Bereichsstreifens den höchsten Verkaufszahlenbereich hervorheben (80-100 €).  
  
 Bereichsstreifen können auf die Diagrammtypen Form oder Polar nicht angewendet werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-interlaced-strip-lines-at-regular-intervals-on-a-chart"></a>So zeigen Sie in einem Diagramm in regelmäßigen Abständen Zeilensprungstreifen an  
  
1.  Klicken Sie zum Anzeigen horizontaler Bereichsstreifen mit der rechten Maustaste auf die vertikale Diagrammachse, und klicken Sie auf **Eigenschaften für vertikale Achsen**.  
  
     Klicken Sie zum Anzeigen vertikaler Bereichsstreifen mit der rechten Maustaste auf die horizontale Diagrammachse, und klicken Sie auf **Eigenschaften für horizontale Achsen**.  
  
2.  Wählen Sie die Option **Zeilensprung verwenden** aus. Auf dem Diagramm werden graue Bereichsstreifen angezeigt.  
  
3.  (Optional) Geben Sie über die nebenstehende Dropdownliste **Farbe** eine Farbe für die Bereichsstreifen an.  
  
### <a name="to-display-interlaced-strip-lines-at-custom-intervals-on-a-chart"></a>So zeigen Sie in einem Diagramm in benutzerdefinierten Abständen Zeilensprungstreifen an  
  
1.  Klicken Sie zum Anzeigen horizontaler Bereichsstreifen mit der rechten Maustaste auf die vertikale Diagrammachse, und klicken Sie auf **Eigenschaften für vertikale Achsen**.  
  
     Klicken Sie zum Anzeigen vertikaler Bereichsstreifen mit der rechten Maustaste auf die horizontale Diagrammachse, und klicken Sie auf **Eigenschaften für horizontale Achsen**.  
  
     Die Achseneigenschaften werden im Fenster "Eigenschaften" angezeigt.  
  
2.  Klicken Sie im Abschnitt **Darstellung** des Eigenschaftenbereichs für die Eigenschaft StripLines auf die Schaltfläche „Auflistung bearbeiten(…)“, um den **ChartStripLine Auflistungs-Editor**zu öffnen.  
  
3.  Klicken Sie auf **Hinzufügen** , um der Auflistung einen neuen Bereichsstreifen hinzuzufügen.  
  
4.  Klicken Sie auf StripWidth, um die Breite des Bereichsstreifens anzugeben, der im Bericht in Zoll ausgegeben wird. Wenn Sie Datumsangaben oder Uhrzeiten hervorheben, klicken Sie auf StripWidthType, und wählen Sie ein Zeitintervall aus.  
  
5.  Geben Sie einen Wert oder einen Ausdruck für das Intervall ein, um anzugeben, wie oft der Bereichsstreifen wiederholt wird.  Wenn Sie beispielsweise als Intervall 10 angeben und der Bereichsstreifen eine Stärke von 5 aufweist, werden bei den Werten 0 bis 5, 15 bis 20, 30 bis 35 usw. Bereichsstreifen angezeigt.  
  
> [!NOTE]  
>  Standardmäßig wird die Eigenschaft „Interval“ auf „Auto“ festgelegt. Das bedeutet, dass das Diagramm kein Intervall für benutzerdefinierte Bereichsstreifen berechnet. Das Diagramm berechnet nur Intervalle für Bereichsstreifen, wenn ein Intervallwert festgelegt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Achsenbezeichnungen in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatieren eines Diagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Hinzufügen eines gleitenden Durchschnitts zu einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)  
  
  
