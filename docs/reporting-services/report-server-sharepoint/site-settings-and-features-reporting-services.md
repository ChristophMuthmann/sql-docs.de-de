---
title: Reporting Services siteeinstellungen und site-Funktionen (SharePoint-Modus) | Microsoft Docs
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
ms.openlocfilehash: ea81c248f302e322d981b90147d42cb83a4804cc
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="reporting-services-site-settings-and-site-features-sharepoint-mode"></a>Reporting Services-Site-Einstellungen und Funktionen (SharePoint-Modus)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Reporting Services-SharePoint-Modus verfügt über mehrere benutzerdefinierte Funktionen auf Websiteebene und Websitefunktionen, die auf der Seite der SharePoint-Websiteeinstellungen verwaltet werden kann. Die Einstellungen gelten Website und betreffen alle Reporting Services-dienstanwendungen. Sie müssen über Inhalts-Manager- und Systemadministratorberechtigungen verfügen, um diese Seite anzuzeigen.  

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

|Siteeinstellung|Description|  
|------------------|-----------------|  
|Die Einstellungen des Reporting Services-Website|Standortweite Einstellungen in diesem Thema beschrieben.|  
|Datenwarnungen verwalten|Verwaltung der Datenwarnungsfunktion.|  
|Berichtsserver-Dateisynchronisierung|Eine Funktion auf Websiteebene, die standardmäßig deaktiviert wird.<br /><br /> Synchronisiert Berichtsserverdateien (.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) einer SharePoint-Dokumentbibliothek mit dem Berichtsserver, wenn Dateien direkt in der Dokumentbibliothek hinzugefügt oder aktualisiert werden.<br /><br /> Weitere Informationen finden Sie unter [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md).|  
  
## <a name="open-the-reporting-services-site-settings-page"></a>Öffnen Sie die Reporting Services-Site-Einstellungsseite
  
1.  Von der SharePoint-Website **Websiteaktionen** klicken Sie im Menü **Standorteinstellungen**.  
  
2.  In der **Reporting Services** Abschnitt **Einstellungen für Reporting Services-Website**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Optionen für die Einstellungen der Reporting Services-Website
  
|Option|Description|  
|------------|-----------------|  
|**Download des RSClientPrint-ActiveX-Steuerelements aktivieren**|Vom Steuerelement wird ein benutzerdefiniertes Dialogfeld zum Drucken angezeigt, das die in Dialogfeldern zum Drucken üblichen Funktionen enthält. Dazu zählen Druckvorschau, Seitenauswahl zum Angeben bestimmter Seiten und Bereiche, Seitenränder und Ausrichtung. Weitere Informationen zum Steuerelement finden Sie unter [Using the RSClientPrint Control in Custom Applications](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Remotefehler im lokalen Modus aktivieren**|Zeigen Sie bei der Ausführung im lokalen Modus ausführliche Fehlermeldungen auf Remotecomputern an, oder blenden Sie sie aus. Wenn ungefähr folgende Fehlermeldung angezeigt wird, ist die Aktivierung von Remotefehlern möglicherweise nützlich:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Barrierefreiheit-Metadaten für Berichte aktivieren**|Barrierefreiheit-Metadaten in der HTML-Ausgabe für Berichte aktivieren|  
|**Genaue Größenanpassung der Datenvisualisierung für Berichte aktivieren**|Konfigurieren Sie das Verhalten für die Datenvisualisierungsanpassung in einem Tablix, damit sie genau passt. Dies schließt Diagramm, Messgerät und Karte ein. Ist die Funktion deaktiviert, bewirkt das Verhalten für Datenvisualisierungen die ungefähre Anpassung, wodurch möglicherweise Leerzeichen auftreten. Diese Einstellung gilt nur für das Rendern im Berichts-Viewer-Webpart. Um dieses Verhaltens für serverseitiges Rendering zu verwalten, müssen Sie ändern die **"rsreportserver.config"** Datei. Weitere Informationen finden Sie unter den folgenden Links:<br /><br /> [Konfigurationsdatei „RsReportServer.config“](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Customize Rendering Extension Parameters in RSReportServer.Config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [HTML Device Information Settings](../../reporting-services/html-device-information-settings.md).<br /><br /> Die Aktivierung der genauen Anpassung hat möglicherweise Auswirkungen auf die Leistung, da die Verarbeitung zur Ermittlung der genauen Größe möglicherweise länger als eine ungefähre Anpassung dauert.|  
  
## <a name="see-also"></a>Siehe auch

 [Manage a Reporting Services SharePoint Service Application (Verwalten einer Reporting Services-SharePoint-Dienstanwendung)](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  

