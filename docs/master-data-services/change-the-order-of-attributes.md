---
title: "&#196;ndern der Reihenfolge von Attributen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 835a032c-e37c-4f35-8ab0-5e4ae25c2e9b
caps.latest.revision: 5
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 5
---
# &#196;ndern der Reihenfolge von Attributen
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie die Reihenfolge der Attribute ändern.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### So ändern Sie die Reihenfolge der Attribute  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** die Zeile der Entität aus, für die Sie ein Attribut erstellen möchten.  
  
4.  Klicken Sie auf **Attribute**.  
  
5.  Fügen Sie auf der Seite **Attribute verwalten** einen der folgenden Schritte aus.  
  
    -   Wenn das Attribut für Blattelemente bestimmt ist, wählen Sie **Blatt** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für konsolidierte Elemente bestimmt ist, wählen Sie **Konsolidiert** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für Sammlungen bestimmt ist, wählen Sie **Sammlung** im Listenfeld **Elementtypen** aus.  
  
6.  Wählen Sie die Zeile für das Attribut aus, dessen Reihenfolge Sie ändern möchten.  
  
    > [!NOTE]  
    >  Die Reihenfolge der Name- oder Code-Attribute kann nicht geändert werden.  
  
7.  Klicken Sie auf **Nach oben** oder **Nach unten**.  
  
## Siehe auch  
 [Attribute &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  