---
title: "Hinzufügen mehrerer Bedingungen zu einer Geschäftsregel (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: business rules [Master Data Services], multiple conditions
ms.assetid: 5f0f6958-6cf2-444b-bdcd-05b887637a0b
caps.latest.revision: "9"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ab40c3eda3f93bcee19f9d1de4faa0b6f0b6ecb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="add-multiple-conditions-to-a-business-rule-master-data-services"></a>Hinzufügen mehrerer Bedingungen zu einer Geschäftsregel (Master Data Services)
  Sie können einer Geschäftsregel in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]mehrere **AND** - oder **OR** -Bedingungen hinzufügen, um eine komplexere Regel zu erstellen.  
  
> [!NOTE]  
>  Wenn Sie eine Geschäftsregel erstellen, die den **OR** -Operator verwendet, sollten Sie eine separate Regel für jede Bedingungsanweisung erstellen, die unabhängig ausgewertet werden kann. Sie können dann Regeln nach Bedarf ausschließen und so mehr Flexibilität und eine einfachere Problembehandlung bereitstellen.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
-   Eine Geschäftsregel muss vorhanden sein. Weitere Informationen finden Sie unter [Erstellen und Veröffentlichen einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md).  
  
### <a name="to-add-multiple-conditions-to-a-business-rule"></a>So fügen Sie einer Geschäftsregel mehrere Bedingungen hinzu  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Geschäftsregeln**.  
  
3.  Wählen Sie auf der Seite **Geschäftsregeln** in der Dropdownliste **Modell** ein Modell aus.  
  
4.  Wählen Sie in der Dropdownliste **Entität** eine Entität aus.  
  
5.  Wählen Sie in der Dropdownliste **Member Types** (Elementtypen) einen Elementtyp aus.  
  
6.  Klicken Sie auf die Zeile für die Geschäftsregel, die Sie bearbeiten möchten.  
  
7.  Klicken Sie auf **Bearbeiten**.  
  
8.  Wählen Sie unter dem **IF** -Abschnitt auf der linken Seite in der Dropdownliste des logischen Operators **UND/ODER/NICHT**aus.  
  
9. Klicken Sie auf **Hinzufügen**. Ein Bereich wird angezeigt.  
  
10. Wählen Sie ein Attribut aus der Dropdownliste **Attribut** aus.  
  
11. Wählen Sie eine Bedingung aus der Dropdownliste **Operator** aus.  
  
12. Füllen Sie alle Pflichtfelder aus.  
  
13. Klicken Sie auf **Speichern**. Eine neue Zeile wird dem **IF** -Raster hinzugefügt.  
  
14. Um weitere Bedingungen hinzuzufügen, führen Sie ggf. Schritte 8 bis 13 aus.  
  
    > [!TIP]  
    >  Wählen Sie die Bedingung aus, klicken Sie mit der rechten Maustaste darauf, und klicken Sie auf **Löschen**, um eine Bedingung zu löschen.  
  
    > [!TIP]  
    >  Sie können mehrere Kriterien auswählen und mit der rechten Maustaste klicken, um sie in einem logischen Operator zu gruppieren oder um die Gruppierung der Bedingungen in einem bestimmten logischen Operator aufzuheben.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Ändern des Namens einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Konfigurieren von Geschäftsregeln für das Senden von Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
