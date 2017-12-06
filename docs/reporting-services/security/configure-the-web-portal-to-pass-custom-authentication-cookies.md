---
title: "Konfigurieren des Webportals für die Übergabe von benutzerdefinierten Authentifizierungscookies | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.openlocfilehash: 421c4806ee3a6f5aaf041f8446cbe1c2bf5eed9c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>Konfigurieren des Webportals für die Übergabe von benutzerdefinierten Authentifizierungscookies

Falls Sie eine benutzerdefinierte Authentifizierungserweiterung verwenden, sollten Sie das Webportal für die Übertragung von benutzerdefinierten Authentifizierungscookies konfigurieren. Andernfalls überträgt das Webportal Cookies nur über HTTP-Anforderungen, die auf den Berichtsserver beschränkt sind. Sollen zusätzliche Cookies übertragen werden, müssen Sie Änderungen an der Datei RSReportServer.Config vornehmen.

## <a name="modifying-the-rsreportserverconfig-file"></a>Ändern der Datei RSReportServer.Config

Sie können das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] für die Übertragung zusätzlicher Cookies über den Berichtsserver aktivieren, indem Sie den Konfigurationseinstellungen des Webportals in der Datei „RSReportServer.config“ ein \<**PassThroughCookies**>-Element hinzufügen. Die Übertragung zusätzlicher Cookies ist vor allem bei Verwendung einer Authentifizierungslösung mit einmaliger Anmeldung nützlich, die nicht nur die Authentifizierungscookies des Berichtsservers, sondern auch Cookies der Authentifizierungssysteme von Drittanbietern benötigt.

Legen Sie in der Datei „RSReportServer.config“ die folgenden Elemente fest, um zusätzliche Cookies zu aktivieren, die über HTTP-Anforderungen übertragen werden sollen, wenn das Webportal verwendet wird:
  
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
[Konfigurieren und Verwalten eines Berichtsservers &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
Haben Sie dazu Fragen? [Besuchen Sie das Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
