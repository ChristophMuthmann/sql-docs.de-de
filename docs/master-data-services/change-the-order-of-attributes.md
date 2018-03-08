---
title: "Ändern der Reihenfolge von Attributen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 835a032c-e37c-4f35-8ab0-5e4ae25c2e9b
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 169ef20e949c2880cf79b9634aeed9e41927726c
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="change-the-order-of-attributes"></a>Ändern der Reihenfolge von Attributen
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie die Reihenfolge der Attribute ändern.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Attribute &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
