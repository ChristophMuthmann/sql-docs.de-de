---
title: "Ändern der Reihenfolge von Attributen | Microsoft-Dokumentation"
ms.custom: SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 835a032c-e37c-4f35-8ab0-5e4ae25c2e9b
caps.latest.revision: "5"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09ebbdb35575c7ebe75aa4ae76c0b5f727833f0b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="change-the-order-of-attributes"></a>Ändern der Reihenfolge von Attributen
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie die Reihenfolge der Attribute ändern.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-change-the-order-of-an-attribute"></a>So ändern Sie die Reihenfolge der Attribute  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Attribute &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
