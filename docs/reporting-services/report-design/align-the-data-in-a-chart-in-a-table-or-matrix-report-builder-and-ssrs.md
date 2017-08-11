---
title: Ausrichten von Diagrammdaten in einer Tabelle oder Matrix (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d64ebc0ee2345088419e44ab819c0d94d26274a8
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>Ausrichten von Diagrammdaten in einer Tabelle oder einer Matrix (Berichts-Generator und SSRS)
  Sparklines und Datenbalken sind kleine, einfache Diagramme, die viel Information mit wenig relevanten Details vermitteln. Wenn Sie diese Option in einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Bericht aktivieren, werden die Werte in Ihren Sparklines und Datenbalken in den verschiedenen Zellen in der Tabelle oder Matrix ausgerichtet, selbst wenn in den Daten Werte fehlen, auf denen die Sparklines und Datenbalken basieren.  
  
 ![Rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "Rs_SparklineAlignData")  
  
 In diesem Bild wird das Säulendiagramm für die täglichen Verkäufe jedes Mitarbeiters dargestellt. Beachten Sie, dass Tage, an denen ein Mitarbeiter keine Verkäufe getätigt hat, leer gelassen werden und die nachfolgenden Tage horizontal ausgerichtet werden. Die Diagramme werden auch vertikal ausgerichtet, indem die Größen der unterschiedlichen Diagramme relativ zu einander festgelegt werden. Weitere Informationen finden Sie unter [Sparklines und Datenbalken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="align-the-data-in-a-sparkline-or-data-bar"></a>Ausrichten der Daten in einer Sparkline oder einem Datenbalken  
  
1.  [Fügen Sie eine Sparkline oder einen Datenbalken](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) zu einer Tabelle oder Matrix hinzu.  
  
2. Klicken Sie in die Sparkline oder den Datenbalken, und klicken Sie dann auf **Eigenschaften für Horizontale Achsen** oder **Eigenschaften für vertikale Achsen**.  
  
2.  Aktivieren Sie auf der Registerkarte **Achsenoptionen** das Kontrollkästchen **Achsen ausrichten in** , und wählen Sie dann im Dropdownfeld die Gruppe aus, in der die Achse ausgerichtet werden soll.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Diagramme &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Hinzufügen von Sparklines und Datenbalken &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
