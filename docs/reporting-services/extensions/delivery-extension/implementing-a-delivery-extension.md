---
title: "Implementieren von Übermittlungserweiterungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
caps.latest.revision: "32"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b34cb389c2bbc8a2aaabe81a38e1c3048f2b2b91
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="implementing-a-delivery-extension"></a>Implementieren von Übermittlungserweiterungen
  Mithilfe von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] können Benutzer Berichte erstellen und veröffentlichen, die nach der Erstellung und Veröffentlichung an diverse Orte übermittelt werden können. Außerdem enthält [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] verschiedene Übermittlungserweiterungen und eine Übermittlungs-API, mit der Entwickler zusätzliche Übermittlungserweiterungen erstellen können, um die Übermittlungsfunktionen in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] noch zu erweitern.  
  
 Eine Beispielimplementierung einer Übermittlungserweiterung finden Sie unter [SQL Server Reporting Services-Produktbeispiele](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Delivery Extensions Overview (Übersicht über Übermittlungserweiterungen)](../../../reporting-services/extensions/delivery-extension/delivery-extensions-overview.md)  
 Erläutert, wie eine benutzerdefinierte Übermittlungserweiterung für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] geschrieben wird.  
  
 [Preparing to Implement a Delivery Extension (Vorbereiten der Implementierung von Übermittlungserweiterungen)](../../../reporting-services/extensions/delivery-extension/preparing-to-implement-a-delivery-extension.md)  
 Beschreibt die verfügbaren Schnittstellen und Klassen beim Implementieren einer [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung sowie die Themen, die vor der Implementierung berücksichtigt werden sollten.  
  
 [Creating a Delivery Extension Library (Erstellen einer Bibliothek für Übermittlungserweiterungen)](../../../reporting-services/extensions/delivery-extension/creating-a-delivery-extension-library.md)  
 Beschreibt die Zuordnung eines Namespace für die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung und die Kompilierung der Übermittlungserweiterung in eine DLL-Bibliothek.  
  
 [Implementing the IDeliveryExtension Interface for a Delivery Extension (Implementieren der IDeliveryExtension-Schnittstelle für Übermittlungserweiterungen)](../../../reporting-services/extensions/delivery-extension/implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 Beschreibt die Attribute einer Übermittlungserweiterung und die Art der Implementierung einer eigenen Klasse für die Übermittlungserweiterung.  
  
 [Using a Notification Class for a Delivery Extension (Verwenden einer Notification-Klasse für eine Übermittlungserweiterung)](../../../reporting-services/extensions/delivery-extension/using-a-notification-class-for-a-delivery-extension.md)  
 Beschreibt die Attribute der **Notification**-Klasse und die Verwendungsweise in Ihrer Implementierung der Übermittlungserweiterung  
  
 [Using the Setting Class for a Delivery Extension (Verwenden der Setting-Klasse für eine Übermittlungserweiterung)](../../../reporting-services/extensions/delivery-extension/using-the-setting-class-for-a-delivery-extension.md)  
 Beschreibt die Attribute der **Setting**-Klasse und die Verwendungsweise in Ihrer Implementierung der Übermittlungserweiterung  
  
 [Using the IDeliveryReportServerInformation Interface for a Delivery Extension (Verwenden der IDeliveryReportServerInformation-Schnittstelle für Übermittlungserweiterungen)](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 Beschreibt die Attribute der **IDeliveryReportServerInformation**-Klasse und die Verwendungsweise in Ihrer Implementierung der Übermittlungserweiterung  
  
 [Using the Report Class for a Delivery Extension (Verwenden der Report-Klasse für eine Übermittlungserweiterung)](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)  
 Beschreibt die Attribute der **Report**-Klasse und die Verwendungsweise in Ihrer Implementierung der Übermittlungserweiterung  
  
 [Using the RenderedOutputFile Class for a Delivery Extension (Verwenden der RenderedOutputFile-Klasse für eine Übermittlungserweiterung)](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 Beschreibt die Attribute der **RenderedOutputFile**-Klasse und die Verwendungsweise in Ihrer Implementierung der Übermittlungserweiterung  
  
 [Implementieren der ISubscriptionBaseUIUserControl-Schnittstelle für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 Beschreibt die Attribute eines Steuerelements für die Übermittlungserweiterung und die Art der Implementierung einer eigenen Schnittstelle für das Abonnement.  
  
 [Bereitstellen von Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
 Beschreibt, wie Sie eine Übermittlungserweiterung anwenden  
  
 [Debugging Delivery Extension Code (Debuggen von Übermittlungserweiterungscode)](../../../reporting-services/extensions/delivery-extension/debugging-delivery-extension-code.md)  
 Beschreibt, wie Sie Code in der Übermittlungserweiterung debuggen  
  
 [Removing a Delivery Extension (Entfernen von Übermittlungserweiterungen)](../../../reporting-services/extensions/delivery-extension/removing-a-delivery-extension.md)  
 Beschreibt, wie Sie eine Übermittlungserweiterung von einem Berichtsserver entfernen  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterungen für Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services Extension Library (Reporting Services-Erweiterungsbibliothek)](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
