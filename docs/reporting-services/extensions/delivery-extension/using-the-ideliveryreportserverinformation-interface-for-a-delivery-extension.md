---
title: "Verwenden der IDeliveryReportServerInformation-Schnittstelle für eine Übermittlungserweiterung | Microsoft Docs"
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
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4a3c2ea843dbfe19b797da7b792d10220018a595
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>Verwenden der IDeliveryReportServerInformation-Schnittstelle für Übermittlungserweiterungen
  Die <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>-Schnittstelle macht mehrere Eigenschaften verfügbar, die Sie verwenden können, um Informationen über einen Berichtsserver abzurufen. Sie können diese Informationen verwenden, um Benachrichtigungen und Berichte zu übermitteln. Beim Implementieren der Übermittlungserweiterung implementieren Sie die <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A>-Eigenschaft wie von der <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>-Schnittstelle gefordert. Die <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A>-Eigenschaft gibt ein Objekt zurück, das die <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>-Schnittstelle implementiert. Von diesem Objekt können Sie eine Liste der Renderingerweiterungen abrufen, die derzeit vom Berichtsserver unterstützt werden.  
  
 Die folgenden **für** Schleife konnte verwendet werden, um eine Liste der derzeit verfügbaren Renderingerweiterungen zu speichern, auf dem Berichtsserver in eine **ArrayList** Objekt.  
  
```vb  
Dim renderFormats As New ArrayList()  
Dim e As Microsoft.ReportingServices.Interfaces.Extension  
For Each e In  ReportServerInformation.RenderingExtension  
   If e.Visible Then  
      renderFormats.Add(e.Name)  
   End If  
Next e  
```  
  
```csharp  
ArrayList renderFormats = new ArrayList();  
foreach (Microsoft.ReportingServices.Interfaces.Extension e in ReportServerInformation.RenderingExtension)  
{   
   if (e.Visible)  
   {  
      renderFormats.Add(e.Name);  
   }  
}  
```  
  
 Weitere Informationen zu den <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> Benutzeroberfläche, siehe [verwenden der IDeliveryReportServerInformation-Schnittstelle für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
