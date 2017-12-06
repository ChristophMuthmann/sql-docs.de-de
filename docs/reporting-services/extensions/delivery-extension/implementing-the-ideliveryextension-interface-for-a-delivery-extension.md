---
title: "Implementieren der IDeliveryExtension-Schnittstelle für Übermittlungserweiterungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
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
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
caps.latest.revision: "37"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 726b1cf1f56cf987cb91bde206b269392158d039
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>Implementieren der IDeliveryExtension-Schnittstelle für Übermittlungserweiterungen
  Mit der Klasse der Übermittlungserweiterungen können Sie ausgehend von den Inhalten der Benachrichtigungen Berichtsbenachrichtigungen an Benutzer übermitteln. Die Klasse der Übermittlungserweiterung bietet außerdem eine Infrastruktur zum Validieren der Benutzereinstellungen, die an die Übermittlungserweiterung übergeben werden. Zusätzlich sollte die Übermittlungserweiterung bestimmte Eigenschaften enthalten, mit denen Clients folgende Informationen abrufen können: den Namen der Erweiterung, die von der Erweiterung unterstützten Einstellungen und die Renderingformate, die für diese Übermittlungserweiterung zur Verfügung stehen.  
  
 ![Prozess-in-IDeliveryExtension-Schnittstelle](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "IDeliveryExtension interface process")  
Mithilfe der IdeliveryExtension-Schnittstelle können auch Clients Benutzerdaten validieren und die erforderlichen Übermittlungseinstellungen abrufen.  
  
 Um eine Klasse der Übermittlungserweiterungen zu erstellen, implementieren Sie <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> und <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Über die **IDeliveryExtension**-Schnittstelle kann die Übermittlungserweiterung Berichtsbenachrichtigungen mit der <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A>-Methode übermitteln und die eingehenden Erweiterungseinstellungen mit der <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A>-Methode validieren. Durch die **IExtension**-Schnittstelle kann die Übermittlungserweiterung einen lokalisierten Erweiterungsnamen implementieren und erweiterungsspezifische Konfigurationsdaten verarbeiten, die in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konfigurationsdatei gespeichert sind. Durch die Implementierung von **IExtension** enthält die Übermittlungserweiterung die Eigenschaft <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A>. Die [!INCLUDE[ssRS](../../../includes/ssrs-md.md)]-Übermittlungserweiterungen sollten unbedingt die **LocalizedName**-Eigenschaft unterstützen, damit die Benutzer auf der Benutzeroberfläche, z.B. dem Berichts-Manager, einen bekannten Namen für die Erweiterung vorfinden.  
  
 Die Übermittlungserweiterung muss auch die **ExtensionSettings**-Eigenschaft der **IDeliveryExtension**-Schnittstelle implementieren. Der Berichtsserver verwendet den von der <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A>-Eigenschaft zurückgegebenen Wert, um die für die Übermittlungserweiterung erforderlichen Einstellungen zu überprüfen. Clients, die mit den Übermittlungserweiterungen interagieren, verwenden die <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>-Methode des Berichtsserver-Webdiensts, um eine Liste der Einstellungen für die Übermittlungserweiterung zurückzugeben.  
  
 Sie können auch die Klasse der Übermittlungserweiterungen verwenden, um in der Datei RSReportServer.config gespeicherte, benutzerdefinierte Konfigurationsdaten abzurufen und zu verarbeiten. Weitere Informationen zur Verarbeitung benutzerdefinierter Konfigurationsdaten finden Sie in der Methode <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Eine **IDeliveryExtension**-Beispielklassenimplementierung finden Sie unter [SQL Server Reporting Services-Produktbeispiele](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services Extension Library (Reporting Services-Erweiterungsbibliothek)](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
