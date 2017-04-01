---
title: "&#220;berpr&#252;fen von bestimmten Elementen auf Gesch&#228;ftsregeln (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anwenden von Geschäftsregeln [Master Data Services]"
  - "Geschäftsregeln [Master Data Services], Anwenden auf ausgewählte Elemente"
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# &#220;berpr&#252;fen von bestimmten Elementen auf Gesch&#228;ftsregeln (Master Data Services)
  Wenn Sie Teilmengen von Elementen aktualisieren oder mit Geschäftsregeln abgleichen möchten, können Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]Geschäftsregeln selektiv anwenden.  
  
> [!NOTE]  
>  Wenn Sie Geschäftsregeln auf alle Elemente in einer Version eines Modells anwenden möchten, gehen Sie auf die Seite [Überprüfen einer Version anhand von Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
-   Sie müssen mindestens die Berechtigung **Aktualisieren** für das Modellobjekt haben, auf das Sie Geschäftsregeln anwenden möchten.  
  
### So wenden Sie Geschäftsregeln selektiv an  
  
1.  Wählen Sie auf der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]-Startseite aus der Dropdownliste **Modell** ein Modell aus.  
  
2.  Wählen Sie aus der Dropdownliste **Version** eine Version aus.  
  
3.  Klicken Sie auf die Registerkarte **Explorer** .  
  
4.  Zeigen Sie in der Menüleiste auf **Entitäten** und klicken Sie auf den Namen der Entität mit den Elementen, auf die Sie Regeln anwenden möchten.  
  
5.  Klicken Sie auf **Regeln anwenden**. Die Geschäftsregeln werden nur auf die im Raster angezeigten Elemente angewendet.  
  
## Siehe auch  
 [Überprüfen einer Version anhand von Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  