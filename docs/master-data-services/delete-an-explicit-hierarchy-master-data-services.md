---
title: "Löschen einer expliziten Hierarchie (Master Data Services) | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- explicit hierarchies, deleting
- deleting explicit hierarchies [Master Data Services]
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: c1e0b7164a6ca7d43c2a223839cff9df1960df60
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>Löschen einer expliziten Hierarchie (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie eine explizite Hierarchie löschen, die Sie nicht mehr benötigen.  
  
> [!WARNING]  
>  Wenn Sie eine explizite Hierarchie löschen, werden alle konsolidierten Elemente in der Hierarchie ebenfalls gelöscht. Wenn Sie alle expliziten Hierarchien für eine Entität löschen, werden auch alle Auflistungen für die Entität gelöscht und die Entität ist nicht mehr für explizite Hierarchien und Auflistungen aktiviert.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-an-explicit-hierarchy"></a>So löschen Sie eine explizite Hierarchie  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** im Raster die Zeile für die Entität aus, die die explizite Hierarchie enthält, die Sie löschen möchten.  
  
4.  Klicken Sie auf **explizite Hierarchien**.  
  
5.  Klicken Sie auf der Seite **Explizite Hierarchie verwalten** auf die zu löschende explizite Hierarchie.  
  
6.  Klicken Sie auf **Bearbeiten**.  
  
7.  Klicken Sie im Bestätigungsdialogfeld auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer expliziten Hierarchie &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
