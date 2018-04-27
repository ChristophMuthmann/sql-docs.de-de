---
title: Ausschließen einer Geschäftsregel (Master Data Services) | Microsoft-Dokumentation
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
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3d0ca4ae6b01f2a0de0a85cf83e725956a0f14b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="exclude-a-business-rule-master-data-services"></a>Ausschließen einer Geschäftsregel (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie eine Geschäftsregel ausschließen, die nicht zur Datenüberprüfung verwendet, aber auch nicht dauerhaft gelöscht werden soll.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-exclude-a-business-rule"></a>So schließen Sie eine Geschäftsregel aus  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Geschäftsregeln**.  
  
3.  Wählen Sie auf der Seite **Geschäftsregeln** in der Dropdownliste **Modell** ein Modell aus.  
  
4.  Wählen Sie in der Dropdownliste **Entität** eine Entität aus.  
  
5.  Wählen Sie in der Dropdownliste **Member Types** (Elementtypen) einen Elementtyp aus.  
  
6.  Klicken Sie im Raster auf die Zeile der Geschäftsregel, die Sie ausschließen möchten, und klicken Sie auf **Bearbeiten**.  
  
7.  Aktivieren Sie das Kontrollkästchen **Ausgeschlossen** .  
  
8.  Klicken Sie auf **Speichern**.  
  
9. Klicken Sie auf **Alle veröffentlichen**.  
  
10. Klicken Sie im Bestätigungsdialogfeld auf **OK**. Der Wert in der Spalte **Geschäftsregelstatus** lautet **Ausgeschlossen** , und die Spalte **Ausgeschlossen** ist auf **Ja**festgelegt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Löschen einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/delete-a-business-rule-master-data-services.md)   
 [Erstellen und Veröffentlichen einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
