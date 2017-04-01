---
title: "Konfigurieren des Berichts-Managers f&#252;r die &#220;bergabe von benutzerdefinierten Authentifizierungscookies | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Authentifizierung [Reporting Services]"
  - "Erweiterungen [Reporting Services], benutzerdefinierte Sicherheits-"
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 18
---
# Konfigurieren des Berichts-Managers f&#252;r die &#220;bergabe von benutzerdefinierten Authentifizierungscookies
  Falls Sie eine benutzerdefinierte Authentifizierungserweiterung verwenden, sollten Sie das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] für die Übertragung von benutzerdefinierten Authentifizierungscookies konfigurieren. Andernfalls überträgt das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] Cookies nur über HTTP-Anforderungen, die auf den Berichtsserver beschränkt sind. Sollen zusätzliche Cookies übertragen werden, müssen Sie Änderungen an der Datei RSReportServer.Config vornehmen.  
  
## Ändern der Datei RSReportServer.Config  
 Sie können das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] für die Übertragung zusätzlicher Cookies über den Berichtsserver aktivieren, indem Sie den Konfigurationseinstellungen des [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] in der Datei „RSReportServer.config“ ein \<**PassThroughCookies**>-Element hinzufügen. Die Übertragung zusätzlicher Cookies ist vor allem bei Verwendung einer Authentifizierungslösung mit einmaliger Anmeldung nützlich, die nicht nur die Authentifizierungscookies des Berichtsservers, sondern auch Cookies der Authentifizierungssysteme von Drittanbietern benötigt.  
  
 Um zusätzliche Cookies zu aktivieren, die über HTTP-Anforderungen übertragen werden sollen, wenn das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] verwendet wird, legen Sie in der Datei „RSReportServer.config“ die folgenden Elemente fest:  
  
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
  
## Siehe auch  
 [Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md)   
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Übersicht über Sicherheitserweiterungen](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
 [Konfigurieren und Verwalten eines Berichtsservers &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  