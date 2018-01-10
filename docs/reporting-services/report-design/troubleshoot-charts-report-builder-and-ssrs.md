---
title: Problembehandlung bei Diagrammen (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 76e6a49e935ea5744686be628f6a7138d6feed91
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Problembehandlung bei Diagrammen (Berichts-Generator und SSRS)
  Beim Arbeiten mit Diagrammen können diese Punkte hilfreich sein.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>Warum zählt das Diagramm die Werte auf der Wertachse, statt sie zu addieren?  
 Die meisten Diagrammtypen erfordern numerische Werte an der Wertachse (normalerweise der y-Achse), damit sie ordnungsgemäß gezeichnet werden. Wenn der Datentyp des Wertfelds **String**lautet, kann das Diagramm keinen numerischen Wert anzeigen, selbst wenn sich in den Feldern Zahlen befinden. Stattdessen zeigt das Diagramm die Anzahl der Zeilen an, die in diesem Feld einen Wert enthalten. Zur Vermeidung dieses Verhaltens sollten Sie sicherstellen, dass die Felder, die Sie für Wertereihen verwenden, numerische Datentypen und keine Zeichenfolgen mit formatierten Zahlen aufweisen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
