---
title: Aktivieren Sie den Berichtsserver und Power View-Integrationsfunktionen in SharePoint | Microsoft Docs
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e97378914a59fab938fc3e4c7926847effcffc94
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="activate-the-report-server-and-power-view-integration-features-in-sharepoint"></a>Aktivieren Sie den Berichtsserver und Power View-Integrationsfunktionen in SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Die Reporting Services Websitesammlung-Funktionen sind standardmäßig aktiviert, nach der Installation der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] Add-in für SharePoint-Produkte. In einigen Situationen müssen Sie die Funktionen manuell aktivieren.  

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

 Wenn Sie das Reporting Services-add-in für SharePoint 2010-Produkte nach der Installation des SharePoint-Produkts installieren, werden anschließend die Berichtsserver-Integrationsfunktion und die Power View-Integrationsfunktion nur für stammwebsitesammlungen aktiviert. Für andere Websitesammlungen müssen Sie die Funktionen manuell aktivieren. Angenommen, Sie haben eine Websitesammlung **http://[my Servername] / Sites / [websitesammlungsname]** müssen Sie die Reporting Services Websitesammlung-Funktionen manuell aktivieren.  
  
 Keine Stammwebsitesammlung liegt, wird das Reporting Services-add-in eine Meldung ähnlich der folgenden protokollieren.  
  
 "SharePoint Web App 80 besitzt keine Stammwebsitesammlung"  
  
 Die Nachricht wurde gefunden, in der Add-in-Installationsprotokoll "RS_SP_ # .log" wobei # eine inkrementelle Zahl steht. Die Protokolldatei befindet sich im aktuellen Temp-Ordner, z. B. C:\Users\\[Benutzername] \AppData\Local\Temp. Weitere Informationen zu Anmeldeoptionen mit dem Add-In finden Sie unter [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  

## <a name="activate-the-report-server-and-power-view-integration-site-collection-features"></a>Aktivieren Sie der Report Server and Power View-Integration Websitesammlungs-features
  
1.  Öffnen Sie den Browser an den Standort der Reporting Services-Funktionen aktiv werden soll.  
  
2.  Klicken Sie auf **Websiteaktionen**.  
  
3.  Klicken Sie auf **Siteeinstellungen**.  
  
4.  Klicken Sie in der Gruppe „Websitesammlungsverwaltung“ auf **Websitesammlungs-Features** .  
  
5.  Suchen Sie in der Liste **Berichtsserver-Integrationsfunktion** oder **Funktion zur Power View-Integration** .  
  
6.  Klicken Sie auf **Aktivieren**.  
  
 Verwenden Sie zum Deaktivieren der Funktionen die gleiche Prozedur, klicken Sie jedoch auf **Deaktivieren** statt auf **Aktivieren**.  
  
## <a name="activate-or-deactivate-reporting-services-central-administration-site-collection-feature"></a>Aktivieren oder deaktivieren Sie Reporting Services-Zentraladministration site Collection-Funktion
  
1.  Öffnen Sie den Browser für die SharePoint-Zentraladministration.  
  
2.  Klicken Sie auf **Websiteaktionen**.  
  
3.  Klicken Sie auf **Siteeinstellungen**.  
  
4.  Klicken Sie in der Gruppe „Websitesammlungsverwaltung“ auf **Websitesammlungs-Features** .  
  
5.  Suchen Sie in der Liste die Funktion **Berichtsserver-Zentraladministration** .  
  
6.  Klicken Sie auf **Aktivieren**.  
  
 Verwenden Sie zum Deaktivieren der Funktion die gleiche Prozedur, klicken Sie jedoch auf **Deaktivieren** statt **Aktivieren**.  
  
## <a name="next-steps"></a>Nächste Schritte

Nachdem die Funktion aktiviert wurde, können Sie die Serverintegration fortsetzen.

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

