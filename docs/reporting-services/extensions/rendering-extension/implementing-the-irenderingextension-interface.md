---
title: Implementieren der IRenderingExtension-Schnittstelle | Microsoft Docs
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
- IRenderingExtension interface
- rendering extensions [Reporting Services], IRenderingExtension interface
ms.assetid: 74b2f2b7-6796-42da-ab7d-b05891ad4001
caps.latest.revision: 43
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3b5772901cfaabedab1b42db39dcd85c49119509
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-the-irenderingextension-interface"></a>Implementieren der IRenderingExtension-Schnittstelle
  Die Renderingerweiterung nimmt die Ergebnisse von einer Berichtsdefinition, die mit den tatsächlichen Daten kombiniert wird, und rendert die resultierenden Daten zu einem Format, das verwendbar ist. Die Transformation der kombinierten Daten und der Formatierung wird mit einer Common Language Runtime (CLR)-Klasse ausgeführt, die <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> implementiert. Dies wandelt das Objektmodell in ein Ausgabeformat um, das durch einen Viewer, Drucker oder ein anderes Ausgabeziel konsumierbar ist.  
  
 <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension> verfügt über drei Methoden, die codiert werden müssen.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A> – rendert den Bericht.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A> – rendert einen bestimmten Datenstrom aus dem Bericht.  
  
-   <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A>- ruft weitere Informationen ab, z. B. Symbole, die für den Bericht erforderlich sind.  
  
 In den folgenden Abschnitten werden diese Methoden ausführlicher erörtert.  
  
## <a name="render-method"></a>Render-Methode  
 Die <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A>-Methode enthält Argumente, die folgende Objekte darstellen:  
  
-   Die *Bericht* , den Sie rendern möchten. Dieses Objekt enthält Eigenschaften, Daten und Layoutinformationen für den Bericht. Der Bericht ist der Stamm für die Modellstruktur des Berichtsobjekts.  
  
-   Die *ServerParameters* , die Zeichenfolgen-Wörterbuchobjekt mit den Parametern für den Berichtsserver enthalten, sofern vorhanden.  
  
-   Die *DeviceInfo* Parameter, die die geräteeinstellungen enthalten. Weitere Informationen finden Sie unter [übergeben von Geräteinformationseinstellungen an Renderingerweiterungen](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
-   Die *ClientCapabilities* Parameter, der enthält einem <xref:System.Collections.Specialized.NameValueCollection> Dictionary-Objekt, das Informationen über den Client umfasst, zu dem Sie den Rendervorgang.  
  
-   Die *RenderProperties* , die Informationen zum Renderingergebnis enthält.  
  
-   Die *CreateAndRegisterStream* ist eine Delegatfunktion, die aufgerufen werden, um ein Datenstrom hineingerendert abzurufen.  
  
### <a name="deviceinfo-parameter"></a>deviceInfo-Parameter  
 Die *DeviceInfo* -Parameter enthält Renderingparameter, nicht Berichtsparameter. Diese Renderingparameter werden an die Renderingerweiterung übergeben. Die *DeviceInfo* Werte konvertiert in eine <xref:System.Collections.Specialized.NameValueCollection> Objekt durch den Berichtsserver. Elemente in der *DeviceInfo* Parameter werden als Groß-/Kleinschreibung Werte behandelt. Wenn die Renderinganforderung als Ergebnis des URL stammt den Zugriff auf die URL-Parameter in der Form `rc:key=value` werden konvertiert, um Schlüssel/Wert-Paare in der *DeviceInfo* Dictionary-Objekt. Der Browser Erkennung-Code bietet auch die folgenden Elemente in der *ClientCapabilities* Wörterbuch: EcmaScriptVersion, JavaScript, MajorVersion, MinorVersion, Win32, Typ und "AcceptLanguage". Jedes Name/Wert-Paar der *DeviceInfo* Parameter, der von der Renderingerweiterung nicht interpretiert werden kann, wird ignoriert. Das folgende Codebeispiel zeigt eine <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A>-Methode, die Symbole abruft:  
  
```csharp  
public void GetRenderingResource (CreateStream createStreamCallback, NameValueCollection deviceInfo)  
{  
    string[] iconTagValues = deviceInfo.GetValues("Icon");  
    if ((iconTagValues != null) && (iconTagValues.Length > 0) )  
    {  
        // Create a stream to output to.  
        Stream outputStream = createStreamCallback(m_iconResourceName, "gif", null, "image/gif", false);  
        // Get the GIF image for one of the buttons on the toolbar  
        Image requiredImage = (Image) m_resourcemanager.GetObject(m_iconResourceName  
        // Write the image to the output stream  
        requiredImage.Save(outputStream, requiredImage.RawFormat);  
    }  
    return;  
}  
```  
  
## <a name="renderstream-method"></a>RenderStream-Methode  
 Die <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.RenderStream%2A>-Methode rendert einen besonderen Datenstrom aus dem Bericht. Alle Datenströme werden während des ersten <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.Render%2A>-Aufrufs erstellt, aber die Ströme werden anfangs nicht zum Client zurückgegeben. Diese Methode wird für Sekundärströme (wie Bilder in HTML-Rendering) oder zusätzliche Seiten einer mehrseitigen Renderingerweiterung (wie Image/EMF) verwendet.  
  
## <a name="getrenderingresource-method"></a>GetRenderingResource-Methode  
 Die <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A>-Methode ruft die Informationen ab, ohne den kompletten Renderingvorgang für den Bericht auszuführen. Manchmal benötigt ein Bericht Informationen, die es nicht erfordern, dass der Bericht selbst gerendert wird. Wenn Sie die Renderingerweiterung gehörige Symbol benötigen, z. B. Verwenden der *DeviceInfo* Parameter, der das einzeltag enthält  **\<Symbol ">**. In diesen Fällen können Sie die <xref:Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension.GetRenderingResource%2A>-Methode verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Renderingerweiterungen](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Übersicht über Renderingerweiterungen](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
  
  
