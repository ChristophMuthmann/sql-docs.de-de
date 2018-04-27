---
title: Löschen eines Elements oder einer Auflistung (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e5eab65acaac91a255aed5c9fa30e6e0508d8090
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="delete-a-member-or-collection-master-data-services"></a>Löschen eines Elements oder einer Auflistung (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]können Sie ein Element oder eine Auflistung löschen, das bzw. die Sie nicht mehr benötigen. Wenn Sie Elemente in einer Massenoperation löschen möchten, verwenden Sie stattdessen Stagingtabellen. Weitere Informationen finden Sie unter [Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md).  
  
> [!NOTE]  
>  Sie können kein Element löschen, das als domänenbasierter Attributwert für ein anderes Element verwendet wird.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
-   Bei Elementen müssen Sie mindestens über die Berechtigung **Löschen** für das Blattmodellobjekt verfügen, aus dem Sie ein Element löschen.  
  
-   Bei Auflistungen müssen Sie für das zu löschende Blattauflistungsobjekt mindestens über die Berechtigung **Aktualisieren** verfügen.  
  
### <a name="to-delete-a-member-or-collection"></a>So löschen Sie ein Element oder eine Auflistung  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Reaktivieren eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [Elemente &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  
