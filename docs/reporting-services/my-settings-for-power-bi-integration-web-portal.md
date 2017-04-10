---
title: "Meine Einstellungen f&#252;r die Power BI-Integration (Webportal) | Microsoft Docs"
ms.date: "05/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "pbi"
  - "power bi"
  - "power bi integration"
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 15
---
# Meine Einstellungen f&#252;r die Power BI-Integration (Webportal)
  Die Seite **Meine Einstellungen** im [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] wird von einzelnen Benutzern verwendet, um ihre Anmeldung bei [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] zu verwalten. Wenn Sie die Schritte zum Anheften eines Berichtselements ausführen, werden Sie automatisch aufgefordert, sich anzumelden.  Sie können sich jedoch auf der Seite **Meine Einstellungen** manuell an- und abmelden.  Wenn die Menüoption **Meine Einstellungen** nicht angezeigt wird, ist der Berichtsserver nicht in [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] integriert.  Weitere Informationen finden Sie unter [Berichtsserverintegration für Power BI&#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## Warum anmelden  
 Wenn Sie sich anmelden, erstellen Sie eine Beziehung zwischen Ihrem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Benutzerkonto und Ihrem [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]-Konto.  Die Anmeldung erstellt ein Sicherheitstoken, das 90 Tage gültig ist. Wenn das Token abläuft und Sie Elemente an Power BI angeheftet haben, erhalten Sie eine Benachrichtigung.  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
Kacheln innerhalb von [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]-Dashboards werden erst aktualisiert, nachdem Sie sich über **MySettings** angemeldet haben.  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
Nachdem Sie sich angemeldet haben, wird ein neues Sicherheitstoken erstellt.  Ihre Dashboardkacheln werden entsprechend den zuvor konfigurierten Zeitplänen aktualisiert.  
  
## Siehe auch  
 [Berichtsserverintegration für Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [Anheften von Reporting Services-Elementen an Power BI-Dashboards](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
 [Dashboards in Power BI](https://support.powerbi.com/knowledgebase/articles/424868-dashboards-in-power-bi)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]
