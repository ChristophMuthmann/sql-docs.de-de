---
title: "Meine Einstellungen für die Power BI-Integration (Webportal) | Microsoft Docs"
ms.date: 05/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- pbi
- power bi
- power bi integration
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 91be669329ea6d822dcc489584d649e5a01ce018
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="my-settings-for-power-bi-integration-web-portal"></a>Meine Einstellungen für die Power BI-Integration (Webportal)

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)]

Die Seite **Meine Einstellungen** im [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] wird von einzelnen Benutzern verwendet, um ihre Anmeldung bei [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]zu verwalten. Wenn Sie die Schritte zum Anheften eines Berichtselements ausführen, werden Sie automatisch aufgefordert, sich anzumelden.  Sie können sich jedoch auf der Seite **Meine Einstellungen** manuell an- und abmelden.  Wenn die Menüoption **Meine Einstellungen** nicht angezeigt wird, ist der Berichtsserver nicht in  [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]integriert.  Weitere Informationen finden Sie unter [Berichtsserverintegration für Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)zu verwalten.  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## <a name="why-sign-in"></a>Warum anmelden  
 Wenn Sie sich anmelden, erstellen Sie eine Beziehung zwischen Ihrem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Benutzerkonto und Ihrem [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] -Konto.  Die Anmeldung erstellt ein Sicherheitstoken, das 90 Tage gültig ist. Wenn das Token abläuft und Sie Elemente an Power BI angeheftet haben, erhalten Sie eine Benachrichtigung.  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
Kacheln innerhalb von [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] -Dashboards werden erst aktualisiert, nachdem Sie sich über **MySettings**angemeldet haben.  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
Nachdem Sie sich angemeldet haben, wird ein neues Sicherheitstoken erstellt.  Ihre Dashboardkacheln werden entsprechend den zuvor konfigurierten Zeitplänen aktualisiert.  

## <a name="next-steps"></a>Nächste Schritte

[Berichtsserverintegration für Power BI](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
[Anheften von Reporting Services-Elementen an Power BI-Dashboards](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
[Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
[Webportal](../reporting-services/web-portal-ssrs-native-mode.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
