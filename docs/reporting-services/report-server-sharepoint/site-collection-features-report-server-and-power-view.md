---
title: Aktivieren Sie das Report Server and Power View-Integrationsfunktionen in SharePoint | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f64a54-c555-4d31-bf99-3abe57dc8626
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bca4115307f7bf9dab5ffc9d2ab02ababb209d65
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="site-collection-features---report-server-and-power-view"></a>Websitesammlungs-Features - Report Server and Power View
  Die Websitesammlungsfunktionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] werden in der Regel standardmäßig aktiviert, nachdem Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Add-In für SharePoint-Produkte installiert haben. In einigen Situationen müssen Sie die Funktionen manuell aktivieren.  
  
 Wenn Sie nach der Installation des SharePoint-Produkts das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint 2010-Produkte installieren, werden die Berichtsserverintegrationsfunktion und die Power View-Integrationsfunktion nur für Stammwebsitesammlungen aktiviert. Für andere Websitesammlungen müssen Sie die Funktionen manuell aktivieren. Wenn Sie z. B. eine Websitesammlung von **http://[Mein Servername]/Websites/[Websitesammlungsname]** besitzen, müssen Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Websitesammlungsfunktionen manuell aktivieren.  
  
 Wenn keine Stammwebsitesammlung vorhanden ist, wird vom [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In ungefähr folgende Meldung protokolliert.  
  
 "SharePoint Web App 80 besitzt keine Stammwebsitesammlung"  
  
 Die Meldung befindet sich im Add-In-Installationsprotokoll "RS_SP_#.log", wobei "#" für eine inkrementelle Zahl steht. Die Protokolldatei befindet sich im temporären Ordner des aktuellen Benutzers, z. B. C:\Benutzer\\[Benutzername]\AppData\Local\Temp. Weitere Informationen zu Anmeldeoptionen mit dem Add-In finden Sie unter [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
 In diesem Thema:  
  
-   [So aktivieren Sie die Websitesammlungsfunktion für die Berichtsserver- und Power View-Integration:](#bkmk_features)  
  
-   [So aktivieren oder deaktivieren Sie die Websitesammlungsfunktion für die Berichtsserver-Zentraladministration:](#bkmk_centraladmin)  
  
##  <a name="bkmk_features"></a> So aktivieren Sie die Websitesammlungsfunktion für die Berichtsserver- und Power View-Integration:  
  
1.  Öffnen Sie den Browser für die Website, auf der die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen aktiviert werden sollen.  
  
2.  Klicken Sie auf **Websiteaktionen**.  
  
3.  Klicken Sie auf **Siteeinstellungen**.  
  
4.  Klicken Sie in der Gruppe „Websitesammlungsverwaltung“ auf **Websitesammlungs-Features** .  
  
5.  Suchen Sie in der Liste **Berichtsserver-Integrationsfunktion** oder **Funktion zur Power View-Integration** .  
  
6.  Klicken Sie auf **Aktivieren**.  
  
 Verwenden Sie zum Deaktivieren der Funktionen die gleiche Prozedur, klicken Sie jedoch auf **Deaktivieren** statt auf **Aktivieren**.  
  
##  <a name="bkmk_centraladmin"></a> So aktivieren oder deaktivieren Sie die Websitesammlungsfunktion für die Berichtsserver-Zentraladministration:  
  
1.  Öffnen Sie den Browser für die SharePoint-Zentraladministration.  
  
2.  Klicken Sie auf **Websiteaktionen**.  
  
3.  Klicken Sie auf **Siteeinstellungen**.  
  
4.  Klicken Sie in der Gruppe „Websitesammlungsverwaltung“ auf **Websitesammlungs-Features** .  
  
5.  Suchen Sie in der Liste die Funktion **Berichtsserver-Zentraladministration** .  
  
6.  Klicken Sie auf **Aktivieren**.  
  
 Verwenden Sie zum Deaktivieren der Funktion die gleiche Prozedur, klicken Sie jedoch auf **Deaktivieren** statt **Aktivieren**.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Nachdem die Funktion aktiviert wurde, können Sie die Serverintegration fortsetzen.  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
