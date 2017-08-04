---
title: "Löschen einer Geschäftsregel (Master Data Services) | Microsoft Docs"
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
- deleting business rules [Master Data Services]
- business rules [Master Data Services], deleting
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ae93d3c89386382b88b470cbfa3a455302c00c2
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="delete-a-business-rule-master-data-services"></a>Löschen einer Geschäftsregel (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] können Sie eine Geschäftsregel löschen, die Sie nicht mehr benötigen.  
  
> [!NOTE]  
>  Sie können die Überprüfung von Daten anhand einer Geschäftsregel unterbinden, indem Sie die Geschäftsregel ausschließen, anstatt sie zu löschen. Weitere Informationen finden Sie unter [Exclude a Business Rule &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-a-business-rule"></a>So löschen Sie eine Geschäftsregel  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Geschäftsregeln**.  
  
3.  Wählen Sie auf der Seite **Geschäftsregeln** in der Dropdownliste **Modell** ein Modell aus.  
  
4.  Wählen Sie in der Dropdownliste **Entität** eine Entität aus.  
  
5.  Wählen Sie in der Dropdownliste **Member Types** (Elementtypen) einen Typ des Elements aus, auf das die Geschäftsregel angewendet werden soll.  
  
6.  Klicken Sie im Raster auf die Zeile der Geschäftsregel, die Sie löschen möchten.  
  
7.  Klicken Sie auf **Löschen**.  
  
8.  Klicken Sie im Bestätigungsdialogfeld auf **OK**. Der Wert in der Spalte **Geschäftsregelstatus** ist **Löschen ausstehend**.  
  
9. Klicken Sie auf **Alle veröffentlichen**.  
  
10. Klicken Sie im Bestätigungsdialogfeld auf **OK**. Die gelöschten Geschäftsregel wird nicht mehr im Raster angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausschließen einer Geschäftsregel &#40; Master Data Services &#41;](../master-data-services/exclude-a-business-rule-master-data-services.md)   
 [Erstellen Sie und veröffentlichen Sie einer Geschäftsregel &#40; Master Data Services &#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Geschäftsregeln &#40; Master Data Services &#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
