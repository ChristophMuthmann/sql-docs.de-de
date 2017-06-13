---
title: "Entfernen einer Übermittlungserweiterung | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: 31
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 81cadbc6eb9b176555b8d5dd5f63ac827e84d7f6
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="removing-a-delivery-extension"></a>Entfernen einer Übermittlungserweiterung
  So entfernen Sie eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] übermittlungserweiterung, entfernen Sie einfach die **Erweiterung** -Element für die übermittlungserweiterung aus der Konfigurationsdatei. Nachdem Sie die Konfigurationsinformationen entfernt haben, steht die Übermittlungserweiterung nicht mehr auf dem Berichtsserver zur Verfügung.  
  
 Sobald eine übermittlungserweiterung entsprechende **Erweiterung** Element aus der Konfigurationsdatei entfernt wird, nicht mehr mit dem Berichtsserver registriert ist. Der Berichtsserver entfernt den Eintrag aus der Liste der Übermittlungserweiterungen und deaktiviert alle Abonnements, die diese Übermittlungserweiterung verwenden. Nachdem Sie eine Übermittlungserweiterung entfernt haben, können Benutzer sie nicht mehr als Benachrichtigungsmethode auswählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
