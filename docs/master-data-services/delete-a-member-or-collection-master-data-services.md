---
title: "L&#246;schen eines Elements oder einer Auflistung (Master Data Services) | Microsoft Docs"
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
  - "Sammlungen [Master Data Services], löschen"
  - "Blattelemente [Master Data Services], löschen"
  - "Löschen von Elementen [Master Data Services]"
  - "Elemente [Master Data Services], löschen"
  - "Konsolidierte Elemente [Master Data Services], löschen"
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# L&#246;schen eines Elements oder einer Auflistung (Master Data Services)
  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]können Sie ein Element oder eine Auflistung löschen, das bzw. die Sie nicht mehr benötigen. Wenn Sie Elemente in einer Massenoperation löschen möchten, verwenden Sie stattdessen Stagingtabellen. Weitere Informationen finden Sie unter [Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md).  
  
> [!NOTE]  
>  Sie können kein Element löschen, das als domänenbasierter Attributwert für ein anderes Element verwendet wird.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
-   Bei Elementen müssen Sie mindestens über die Berechtigung **Löschen** für das Blattmodellobjekt verfügen, aus dem Sie ein Element löschen.  
  
-   Bei Auflistungen müssen Sie für das zu löschende Blattauflistungsobjekt mindestens über die Berechtigung **Aktualisieren** verfügen.  
  
### So löschen Sie ein Element oder eine Auflistung  
  
1.  Wählen Sie auf der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Startseite aus der Liste **Modell** ein Modell aus.  
  
2.  Wählen Sie aus der Liste **Version** eine Version aus.  
  
3.  Klicken Sie auf **Explorer**.  
  
4.  Zum Löschen  
  
    -   eines Elements zeigen Sie auf der Menüleiste auf **Entitäten** und klicken auf den Namen der Entität, in der das Element enthalten ist.  
  
    -   eines konsolidierten Elements zeigen Sie auf der Menüleiste auf **Hierarchien** und klicken auf den Namen der Hierarchie, in der das Element enthalten ist. Klicken Sie dann auf den Knoten in der Hierarchie, die das Element enthält.  
  
    -   einer Sammlung zeigen Sie auf der Menüleiste auf **Sammlungen** und klicken auf den Namen der Entität, in der die Sammlung enthalten ist.  
  
5.  Klicken Sie im Raster auf die Zeile mit dem Element oder der Sammlung, das bzw. die Sie löschen möchten.  
  
6.  Klicken Sie auf **Element löschen**, **Löschen**oder **Sammlung löschen**.  
  
7.  Entitätsadministratoren wird auch eine Menüoption zum Bereinigen (endgültigen Löschen) aller vorläufig gelöschten Elemente in der Entitätsversion angezeigt.  
  
8.  Klicken Sie im Bestätigungsdialogfeld auf **OK**.  
  
## Siehe auch  
 [Reaktivieren eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [Elemente &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  