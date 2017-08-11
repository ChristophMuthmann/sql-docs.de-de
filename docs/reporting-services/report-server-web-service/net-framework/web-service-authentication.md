---
title: Web Dienstauthentifizierung | Microsoft Docs
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
- Web service [Reporting Services], authentication
- XML Web service [Reporting Services], authentication
- Report Server Web service, authentication
ms.assetid: 852b4947-a090-4e54-8555-5a503945ceab
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: be7e76aa26ca4b94afd2e32b40b9fbfbe92b170d
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="web-service-authentication"></a>Webdienstauthentifizierung
  Sie können entweder die Windows-Authentifizierung oder die Standardauthentifizierung verwenden, um an den Berichtsserver-Webdienst gerichtete Aufrufe zu authentifizieren. Jeder Client, der SOAP-Anforderungen an den Berichtsserver richtet, muss den Clientteil eines der unterstützten Authentifizierungsprotokolle implementieren. Bei Verwendung der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], können Sie den verwalteten Codeklassen HTTP-Authentifizierung implementieren. Mithilfe von APIs können Sie die Authentifizierungsdaten problemlos zusammen mit den SOAP-Anforderungen senden.  
  
 Wenn Sie die entsprechenden Anmeldeinformationen nicht haben, bevor Sie einen Aufruf an den Berichtsserver-Webdienst richten, schlägt der Aufruf fehl. Zur Laufzeit können Sie Anmeldeinformationen an den Webdienst übergeben, durch Festlegen der **Anmeldeinformationen** Eigenschaft des clientseitigen Objekts, das den Webdienst darstellt, bevor Sie seine Methoden aufrufen.  
  
 Die folgenden Abschnitte enthalten Beispielcode, der die Anmeldeinformationen mithilfe von [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] sendet.  
  
## <a name="windows-authentication"></a>Windows-Authentifizierung  
 Folgender Code übergibt die Windows-Anmeldeinformationen an den Webdienst.  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
ReportingService rs = new ReportingService();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
```  
  
## <a name="basic-authentication"></a>Standardauthentifizierung  
 Folgender Code übergibt die Standardanmeldeinformationen an den Webdienst.  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = New System.Net.NetworkCredential("username", "password", "domain")  
```  
  
```csharp  
ReportingService service = new ReportingService();  
service.Credentials = new System.Net.NetworkCredential("username", "password", "domain");  
```  
  
 Die Anmeldeinformationen müssen jedoch festgelegt sein, bevor Sie eine der Methoden des Berichtsserver-Webdiensts aufrufen. Wenn Sie die Anmeldeinformationen nicht festlegen, erhalten Sie den Fehlercode „Fehler HTTP 401 (Zugriff verweigert)“. Sie müssen den Dienst authentifizieren, bevor Sie es verwenden, aber nachdem Sie die Anmeldeinformationen festgelegt haben, müssen Sie nicht diese erneut festlegen, solange Sie weiterhin dieselbe dienstvariable verwenden (z. B. *Rs*).  
  
## <a name="custom-authentication"></a>Benutzerdefinierte Authentifizierung  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] enthält eine Programmierungs-API, mit denen Entwickler benutzerdefinierte Authentifizierungserweiterungen, so genannte Sicherheitserweiterungen, entwerfen und entwickeln können. Weitere Informationen finden Sie unter [Implementing a Security Extension](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
