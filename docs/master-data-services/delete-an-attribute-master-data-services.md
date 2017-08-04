---
title: "Löschen eines Attributs (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [Master Data Services], deleting
- deleting attributes [Master Data Services]
ms.assetid: ec3e66f7-0e35-43d7-a80d-64899948ebfe
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1d36564680430b7d35c415e23586c7fd0c47e084
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="delete-an-attribute-master-data-services"></a>Löschen eines Attributs (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie ein Attribut löschen, wenn Sie das Attribut und alle zugehörigen Attributwerte dauerhaft entfernen möchten.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-an-attribute"></a>So löschen Sie ein Attribut  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** die Zeile der Entität aus, für die Sie ein Attribut erstellen möchten.  
  
4.  Klicken Sie auf **Attribute**.  
  
5.  Fügen Sie auf der Seite **Attribute verwalten** einen der folgenden Schritte aus.  
  
    -   Wenn das Attribut für Blattelemente bestimmt ist, wählen Sie **Blatt** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für konsolidierte Elemente bestimmt ist, wählen Sie **Konsolidiert** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für Sammlungen bestimmt ist, wählen Sie **Sammlung** im Listenfeld **Elementtypen** aus.  
  
6.  Wählen Sie die Zeile für das Attribut aus, das Sie löschen möchten.  
  
    > [!NOTE]  
    >  Das Name-Attribut und das Code-Attribut können nicht gelöscht werden.  
  
7.  Klicken Sie auf **Löschen**.  
  
8.  Klicken Sie im Bestätigungsdialogfeld auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute &#40; Master Data Services &#41;](../master-data-services/attributes-master-data-services.md)   
 [Domänenbasierte Attribute &#40; Master Data Services &#41;](../master-data-services/domain-based-attributes-master-data-services.md)   
 [Erstellen Sie ein Textattribut &#40; Master Data Services &#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [Erstellen Sie ein domänenbasiertes Attribut &#40; Master Data Services &#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
