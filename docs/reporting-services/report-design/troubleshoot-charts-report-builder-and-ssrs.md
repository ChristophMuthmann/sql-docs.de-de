---
title: "Problembehandlung bei Diagrammen (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Problembehandlung bei Diagrammen (Berichts-Generator und SSRS)
  Beim Arbeiten mit Diagrammen können diese Punkte hilfreich sein.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Warum zählt das Diagramm die Werte auf der Wertachse, statt sie zu addieren?  
 Die meisten Diagrammtypen erfordern numerische Werte an der Wertachse (normalerweise der y-Achse), damit sie ordnungsgemäß gezeichnet werden. Wenn der Datentyp des Wertfelds **String**lautet, kann das Diagramm keinen numerischen Wert anzeigen, selbst wenn sich in den Feldern Zahlen befinden. Stattdessen zeigt das Diagramm die Anzahl der Zeilen an, die in diesem Feld einen Wert enthalten. Zur Vermeidung dieses Verhaltens sollten Sie sicherstellen, dass die Felder, die Sie für Wertereihen verwenden, numerische Datentypen und keine Zeichenfolgen mit formatierten Zahlen aufweisen.  
  
## Siehe auch  
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  