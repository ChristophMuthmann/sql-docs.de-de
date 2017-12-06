---
title: "Entfernen einer Übermittlungserweiterung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: "31"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2d03cb6841433eca5bce20348eb6ffac18b90e11
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="removing-a-delivery-extension"></a>Entfernen einer Übermittlungserweiterung
  Sie entfernen eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung, indem Sie einfach das **Erweiterungselement** für die Übermittlungserweiterung aus der Konfigurationsdatei entfernen. Nachdem Sie die Konfigurationsinformationen entfernt haben, steht die Übermittlungserweiterung nicht mehr auf dem Berichtsserver zur Verfügung.  
  
 Wenn das entsprechende **Erweiterungselement** für die Übermittlungserweiterung aus der Konfigurationsdatei entfernt wurde, ist die Übermittlungserweiterung nicht mehr auf dem Berichtsserver registriert. Der Berichtsserver entfernt den Eintrag aus der Liste der Übermittlungserweiterungen und deaktiviert alle Abonnements, die diese Übermittlungserweiterung verwenden. Nachdem Sie eine Übermittlungserweiterung entfernt haben, können Benutzer sie nicht mehr als Benachrichtigungsmethode auswählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services Extension Library (Reporting Services-Erweiterungsbibliothek)](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
