---
title: "Die Web-Portal, um die Übergabe von benutzerdefinierten Authentifizierungscookies konfigurieren | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0f1131c191fa64c6dc6f2a074a9cd5db7a8b0e1b
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>Konfigurieren des Webportals für die Übergabe von benutzerdefinierten Authentifizierungscookies

Wenn Sie eine benutzerdefinierte authentifizierungserweiterung verwenden, sollten Sie die Web-Portal für die Übertragung von benutzerdefinierten Authentifizierungscookies konfigurieren. Andernfalls überträgt der Web-Portal nur Cookies über HTTP-Anforderungen mit dem Berichtsserver her. Sollen zusätzliche Cookies übertragen werden, müssen Sie Änderungen an der Datei RSReportServer.Config vornehmen.

## <a name="modifying-the-rsreportserverconfig-file"></a>Ändern der Datei RSReportServer.Config

Sie können die [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] durch Hinzufügen zusätzlicher Cookies über den Berichtsserver übertragen einer \< **"passthroughcookies"**> Element an den Einstellungen des Web-Portal-Konfiguration in der Datei "rsreportserver.config". Die Übertragung zusätzlicher Cookies ist vor allem bei Verwendung einer Authentifizierungslösung mit einmaliger Anmeldung nützlich, die nicht nur die Authentifizierungscookies des Berichtsservers, sondern auch Cookies der Authentifizierungssysteme von Drittanbietern benötigt.

Um zusätzliche Cookies zu über HTTP-Anforderungen übertragen werden sollen, bei Verwendung von Web-Portal zu aktivieren, legen Sie die folgenden Elemente in der Datei "rsreportserver.config" ein:
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## <a name="see-also"></a>Siehe auch

[Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md)   
[RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Übersicht über Sicherheitserweiterungen](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Konfigurieren Sie und verwalten Sie eines Berichtsservers &#40; SSRS im einheitlichen Modus &#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
Weiteren Fragen wenden? [Wiederholen Sie den Reporting Services-forum](http://go.microsoft.com/fwlink/?LinkId=620231)
