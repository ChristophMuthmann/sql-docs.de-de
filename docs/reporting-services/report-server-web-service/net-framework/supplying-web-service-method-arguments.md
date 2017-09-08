---
title: Angabe von Argumenten | Microsoft Docs
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
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 761571f88c2321c823dc240cfa9bb3ba75d9414b
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="supplying-web-service-method-arguments"></a>Bereitstellen von Argumenten für Webdienstmethoden
  Eine Report Server-Webdienstmethode sendet eine Anforderung an den Dienst unter einer bestimmten URL, wobei SOAP über HTTP verwendet wird. Der Dienst empfängt die Anforderung, verarbeitet sie und gibt dann eine Antwort zurück. Diese Anforderungen und Antworten haben die Form von XML-Dokumenten.  
  
## <a name="optional-parameters"></a>Optionale Parameter  
 In manchen Fällen kann eine Webdienstmethode optionale Eingabeparameter haben. Auch wenn ein Eingabeparameter für eine Webdienstmethode optional ist, müssen Sie weiterhin fügen Sie ihn und legen Sie den Parameterwert auf **null** (**nichts** in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]). Festlegen eines Parameterwerts auf **null** legt den Elementwert für diesen Parameter in der SOAP-Anforderung **null**.  
  
 Im folgenden Beispiel wird die <xref:ReportService2010.ReportingService2010.CreateFolder%2A>-Methode zum Erstellen eines neuen Ordners mit dem Namen Product Sales im Ordner Sales verwendet. Durch Angabe einer **null** Wert für die Ordnereigenschaften keine benutzerspezifischen Eigenschaften für den Ordner angegeben werden:  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>Komplexe Datentypen  
 Die Kernklasse des Report Server-Webdiensts ist <xref:ReportService2010.ReportingService2010>. Sie wird verwendet, um die SOAP-Vorgänge oder Webmethoden der Proxyklasse aufzurufen. Damit diese Klasse und ihre Methoden unterstützt werden, enthält [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] benutzerdefinierte, komplexe Datentypen, die für die Eingabe- und Ausgabeparameter der Webdienstmethoden spezifisch sind. Diese komplexen Datentypen sind Teil der erzeugten Proxyklasse, die Sie, beim Entwickeln verwenden können der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Umgebung.  
  
 Wenn Sie eine Proxyklasse erzeugen, werden die in der WSDL-Datei definierten komplexen Datentypen durch die Klassen des Proxys dargestellt, die Eigenschaften enthalten, welche den verschiedenen SOAP-Elementen der komplexen Datentypen entsprechen. Sequenzen dieser Datentypen werden zu Objektarrays, die Sie im Code durchlaufen können. Dadurch ist es nicht notwendig, direkt mit den in SOAP-Nachrichten gesendeten XML-Strukturen zu arbeiten. [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] behandelt diese Übersetzung für Sie.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Technische Referenz &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
