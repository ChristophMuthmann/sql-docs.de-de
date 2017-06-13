---
title: Verwenden der Detail-Eigenschaft zur Handhabung bestimmter Fehler | Microsoft Docs
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
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
caps.latest.revision: 30
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 096e12d3b87eeb12092915dcec3a43f7ac585656
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>Verwenden der Detail-Eigenschaft zur Handhabung bestimmter Fehler
  Um weiteren Klassifizierung von Ausnahmen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] gibt zusätzliche Fehlerinformationen in die **InnerText** Eigenschaft der untergeordneten Elemente in der SOAP-Ausnahme **Detail** Eigenschaft. Da die **Detail** Eigenschaft ist ein **XmlNode** -Objekts können Sie erreichen den inneren Text des der **Nachricht** untergeordnetes Element mit dem folgenden Code.  
  
 Eine Liste aller verfügbaren untergeordneten Elemente in der **Detail** Eigenschaft finden Sie unter [Detaileigenschaft](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md). Weitere Informationen finden Sie unter "Detaileigenschaft" in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   ' The exception is a SOAP exception, so use  
   ' the Detail property's Message element.  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   // The exception is a SOAP exception, so use  
   // the Detail property's Message element.  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   If ex.Detail("ErrorCode").InnerXml = "rsInvalidItemName" Then  
   End If ' Perform an action based on the specific error code  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   if (ex.Detail["ErrorCode"].InnerXml == "rsInvalidItemName")  
   {  
      // Perform an action based on the specific error code  
   }  
}  
```  
  
 Folgende Codezeile gibt den spezifischen Fehlercode wieder, der in der SOAP-Ausnahme zur Konsole zurückgegeben wird. Sie können den Fehlercode auch auswerten und bestimmte Aktionen ausführen.  
  
```vb  
Console.WriteLine(ex.Detail("ErrorCode").InnerXml)  
```  
  
```csharp  
Console.WriteLine(ex.Detail["ErrorCode"].InnerXml);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Einführung in die Ausnahmebehandlung in Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services-SoapException-Klasse](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Tabelle für SoapException-Fehler](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
