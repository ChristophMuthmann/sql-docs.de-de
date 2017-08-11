---
title: Implementing a Delivery Extension | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 5db9bf52437c018bc1dcb40e7fa8a8ce2824fa12
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-a-delivery-extension"></a>Implementieren von Übermittlungserweiterungen
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ermöglicht Benutzern das Erstellen und Veröffentlichen von Berichten, die einmal erstellt und veröffentlicht, an diverse Orte übermittelt werden können. Außerdem enthält [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] verschiedene Übermittlungserweiterungen und eine Übermittlungs-API, mit der Entwickler zusätzliche Übermittlungserweiterungen erstellen können, um die Übermittlungsfunktionen in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] noch zu erweitern.  
  
 Eine beispielimplementierung einer übermittlungserweiterung, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Übersicht über übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/delivery-extensions-overview.md)  
 Erläutert, wie eine benutzerdefinierte Übermittlungserweiterung für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] geschrieben wird.  
  
 [Vorbereiten der Implementierung von Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/preparing-to-implement-a-delivery-extension.md)  
 Beschreibt die verfügbaren Schnittstellen und Klassen beim Implementieren einer [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung sowie die Themen, die vor der Implementierung berücksichtigt werden sollten.  
  
 [Erstellen einer Bibliothek für Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/creating-a-delivery-extension-library.md)  
 Beschreibt die Zuordnung eines Namespace für die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung und die Kompilierung der Übermittlungserweiterung in eine DLL-Bibliothek.  
  
 [Implementieren der IDeliveryExtension-Schnittstelle für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 Beschreibt die Attribute einer Übermittlungserweiterung und die Art der Implementierung einer eigenen Klasse für die Übermittlungserweiterung.  
  
 [Verwenden einer Notification-Klasse für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/using-a-notification-class-for-a-delivery-extension.md)  
 Beschreibt die Attribute einer **Benachrichtigung** Klassen- und wie es in Ihrer Implementierung der übermittlungserweiterung verwendet.  
  
 [Verwenden der Setting-Klasse für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/using-the-setting-class-for-a-delivery-extension.md)  
 Beschreibt die Attribute einer **Einstellung** Klassen- und wie es in Ihrer Implementierung der übermittlungserweiterung verwendet.  
  
 [Verwenden der IDeliveryReportServerInformation-Schnittstelle für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 Beschreibt die Attribute einer **IDeliveryReportServerInformation** -Schnittstelle und zu dessen Verwendung in Ihrer Implementierung der übermittlungserweiterung.  
  
 [Verwenden den Berichtklasse für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)  
 Beschreibt die Attribute einer **Bericht** Klassen- und wie es in Ihrer Implementierung der übermittlungserweiterung verwendet.  
  
 [Verwenden der RenderedOutputFile-Klasse für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 Beschreibt die Attribute einer **RenderedOutputFile** Klasse und wie es in Ihrer Implementierung der übermittlungserweiterung verwendet.  
  
 [Implementieren der ISubscriptionBaseUIUserControl-Schnittstelle für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 Beschreibt die Attribute eines Steuerelements für die Übermittlungserweiterung und die Art der Implementierung einer eigenen Schnittstelle für das Abonnement.  
  
 [Bereitstellen von Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
 Beschreibt, wie Sie eine Übermittlungserweiterung anwenden  
  
 [Debuggen von Übermittlungserweiterungscode](../../../reporting-services/extensions/delivery-extension/debugging-delivery-extension-code.md)  
 Beschreibt, wie Sie Code in der Übermittlungserweiterung debuggen  
  
 [Entfernen einer Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/removing-a-delivery-extension.md)  
 Beschreibt, wie Sie eine Übermittlungserweiterung von einem Berichtsserver entfernen  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
