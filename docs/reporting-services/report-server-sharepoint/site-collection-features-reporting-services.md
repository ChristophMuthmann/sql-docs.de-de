---
title: Funktionen zur Reporting Services-Websitesammlung | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4d3a72452ef0383c4d05d1758bab92570db0df51
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="reporting-services-site-collection-features"></a>Funktionen zur Reporting Services-Websitesammlung

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Der SharePoint-Modus von Reporting Services umfasst drei Funktionen für SharePoint-Websitesammlungen. Die Funktionen unterstützen die allgemeine Berichtserstellungsumgebung des SharePoint-Modus von Reporting Services, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], bei dem es sich um eine Funktion des SQL Server 2016 Reporting Services-Add-Ins handelt, sowie Verwaltungsvorgänge für Reporting Services in der SharePoint-Zentraladministration.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.
  
## <a name="site-collection-features"></a>Funktionen der Websitesammlungen

 In der folgenden Tabelle sind die Funktionen der Websitesammlungen von Reporting Services beschrieben.  
  
|Funktion|Description|  
|-------------|-----------------|  
|**Funktion für die Berichtsserver-Zentraladministration**|Aktiviert Funktionen zum Verwalten der Integration in einen Reporting Services-Berichtsserver. Diese Funktion ist nur unter der Websitesammlung-Funktion der SharePoint-Zentraladministration installiert und wird auch nur darunter verwendet.<br /><br /> Die Berichtsserver-Integrationsfunktion wird für die Websitesammlung in der SharePoint-Zentraladministration automatisch aktiviert, nachdem Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Add-In für SharePoint-Produkte installiert haben. In einigen Situationen müssen Sie die Funktion manuell aktivieren. Verwenden Sie die Reporting Services-Seiten auf der Seite „Siteeinstellungen“ der SharePoint-Zentraladministration, um die Berichtsserverfunktion zu aktivieren.<br /><br /> Durch die [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Reporting Services-Version und höhere Versionen des Add-Ins für SharePoint-Produkte wird die Berichtsserver-Integrationsfunktion bei der Installation des Add-Ins für alle vorhandenen Websitesammlungen aktiviert. Darüber hinaus ist die Funktion für neue Websitesammlungen automatisch aktiv.|  
|**Funktion für die Berichtsserverintegration**|Ermöglicht die umfassende Berichterstellung mithilfe von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Reporting Services<br /><br /> Diese Funktion ist standardmäßig aktiv.|  
|**Power View-Integrationsfunktion**|Aktiviert das interaktive Durchsuchen von Daten und deren visuelle Präsentation für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen und tabellarische Analysis Services-Datenbanken.<br /><br /> Auf das Feature kann über die Kontextmenüs der folgenden Datenquellen zugegriffen werden:<br /><br /> **RDLX**<br /><br /> **RSDS**<br /><br /> **BISM** -Verbindungsdatei<br /><br /> <br /><br /> Wenn [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] nicht in den Kontextmenüs angezeigt wird, sollten Sie überprüfen, ob die **Power View-Integrationsfunktion** aktiviert ist.<br /><br /> Diese Funktion ist standardmäßig deaktiviert.|  

## <a name="next-steps"></a>Nächste Schritte

[Aktivieren der Berichtsserver- und Power View-Integrationsfunktionen in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Einstellungen und Funktionen für Reporting Services-Websites &#40;SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien in der SharePoint-Zentraladministration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
