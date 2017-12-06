---
title: "Webdienstmethoden aufrufen – Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Web service [Reporting Services], calls
- calling Web service
- Report Server Web service, SOAP
- XML Web service [Reporting Services], calls
- Report Server Web service, calls
- XML Web service [Reporting Services], SOAP
- SOAP [Reporting Services], calls
ms.assetid: f6f0c6e3-8bb5-4c44-9d19-1872edc72746
caps.latest.revision: "38"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1556a9b4dd8dcb5aab2d002d2903185c5872ba47
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="calling-web-service-methods"></a>Aufrufen von Webdienstmethoden
  Wenn Sie eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Proxyklasse verwenden, um Webdienstvorgänge aufzurufen, verwenden Sie die Methoden dieser Klasse. Diese Methoden verhalten sich wie jede andere Methode einer Klasse in der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Klassenbibliothek. Alle Webdienstmethoden verfügen über öffentlichen Zugriff, und es ist erforderlich, dass Sie die geeignete Anzahl von Argumenten und Argumenttypen angeben. Nachdem Sie eine Instanz der Proxyklasse im Projekt erstellt haben, können Sie die Methoden zum Ausführen von Berichterstellungsvorgängen über den Berichtsserver aufrufen. Im folgenden C#-Code wird die Verwendung der <xref:ReportService2010.ReportingService2010.ListChildren%2A>-Methode der <xref:ReportService2010.ReportingService2010>-Proxyklasse veranschaulicht. Der Code wird dazu verwendet, einen rekursiven Aufruf an den Webdienst auszuführen, der ein Array von <xref:ReportService2010.CatalogItem>-Objekten zurückgibt, das eine Liste aller Elemente in der Berichtsserver-Datenbank enthält:  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
Dim items As CatalogItem() = rs.ListChildren("/", True)  
```  
  
```csharp  
ReportingService2010 rs = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
CatalogItem[] items = rs.ListChildren("/", true);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Technische Referenz (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  
