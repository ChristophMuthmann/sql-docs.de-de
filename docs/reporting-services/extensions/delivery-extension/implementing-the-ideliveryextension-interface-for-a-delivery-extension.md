---
title: "Implementieren der IDeliveryExtension-Schnittstelle für eine Übermittlungserweiterung | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
caps.latest.revision: 37
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 82bf0172d2ad744d5a34945596814cd584888d95
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>Implementieren der IDeliveryExtension-Schnittstelle für Übermittlungserweiterungen
  Mit der Klasse der Übermittlungserweiterungen können Sie ausgehend von den Inhalten der Benachrichtigungen Berichtsbenachrichtigungen an Benutzer übermitteln. Die Klasse der Übermittlungserweiterung bietet außerdem eine Infrastruktur zum Validieren der Benutzereinstellungen, die an die Übermittlungserweiterung übergeben werden. Zusätzlich sollte die Übermittlungserweiterung bestimmte Eigenschaften enthalten, mit denen Clients folgende Informationen abrufen können: den Namen der Erweiterung, die von der Erweiterung unterstützten Einstellungen und die Renderingformate, die für diese Übermittlungserweiterung zur Verfügung stehen.  
  
 ![IDeliveryExtension-schnittstellenprozess](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "IDeliveryExtension interface process")  
Mithilfe der IdeliveryExtension-Schnittstelle können auch Clients Benutzerdaten validieren und die erforderlichen Übermittlungseinstellungen abrufen.  
  
 Um eine Klasse der Übermittlungserweiterungen zu erstellen, implementieren Sie <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> und <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Die **IDeliveryExtension** Schnittstelle kann die übermittlungserweiterung zum Übermitteln von berichtsbenachrichtigungen mit der <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> Methode und zur Überprüfung der eingehenden erweiterungseinstellungen mit der <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A> Methode. Die **IExtension** Schnittstelle kann die übermittlungserweiterung einen lokalisierten Erweiterungsnamen implementieren und erweiterungsspezifische Konfigurationsdaten in gespeicherten verarbeiten die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Konfigurationsdatei. Durch die Implementierung **IExtension**, enthält die übermittlungserweiterung die <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A> Eigenschaft. Es wird dringend empfohlen, die [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] unterstützen die **LocalizedName** -Eigenschaft, sodass Benutzern eine vertraute Name für die Erweiterung in einer Benutzeroberfläche, z. B. den Berichts-Manager auftreten.  
  
 Die übermittlungserweiterung muss auch implementieren die **ExtensionSettings** Eigenschaft von der **IDeliveryExtension** Schnittstelle. Der Berichtsserver verwendet den von der <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A>-Eigenschaft zurückgegebenen Wert, um die für die Übermittlungserweiterung erforderlichen Einstellungen zu überprüfen. Clients, die mit den Übermittlungserweiterungen interagieren, verwenden die <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>-Methode des Berichtsserver-Webdiensts, um eine Liste der Einstellungen für die Übermittlungserweiterung zurückzugeben.  
  
 Sie können auch die Klasse der Übermittlungserweiterungen verwenden, um in der Datei RSReportServer.config gespeicherte, benutzerdefinierte Konfigurationsdaten abzurufen und zu verarbeiten. Weitere Informationen zur Verarbeitung benutzerdefinierter Konfigurationsdaten finden Sie in der Methode <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Ein Beispiel **IDeliveryExtension** -klassenimplementierung, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Siehe auch  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
