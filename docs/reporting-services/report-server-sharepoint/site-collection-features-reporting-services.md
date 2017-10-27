---
title: Reporting Services-Websitesammlung-Funktionen | Microsoft Docs
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
ms.openlocfilehash: 7c86f9ecdbbf4955ba224e40c245fc412742fc30
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="reporting-services-site-collection-features"></a>Reporting Services-Websitesammlung-Funktionen

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Reporting Services-SharePoint-Modus umfasst drei SharePoint Websitesammlung-Funktionen. Die Funktionen unterstützen die allgemeine berichterstellungsumgebung, Reporting Services in SharePoint-Modus [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], ein Feature der SQL Server 2016 Reporting Services Add-in und Verwaltungsvorgänge für Reporting Services im SharePoint-Zentraladministration.

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.
  
## <a name="site-collection-features"></a>Websitesammlung-Funktionen

 Die folgende Tabelle beschreibt die Reporting Services Websitesammlung-Funktionen.  
  
|Funktion|Description|  
|-------------|-----------------|  
|**Funktion für die Berichtsserver-Zentraladministration**|Aktiviert Funktionen zum Verwalten der Integration mit einem Reporting Services-Berichtsserver an. Diese Funktion ist nur unter der Websitesammlung-Funktion der SharePoint-Zentraladministration installiert und wird auch nur darunter verwendet.<br /><br /> Die Berichtsserver-Integrationsfunktion wird für die Websitesammlung in der SharePoint-Zentraladministration automatisch aktiviert, nachdem Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Add-In für SharePoint-Produkte installiert haben. In einigen Situationen müssen Sie die Funktion manuell aktivieren. Um die berichtsserverfunktion zu aktivieren, verwenden Sie die Reporting Services-Seiten in SharePoint Central Administration-Seite "Siteeinstellungen" ein.<br /><br /> Die [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Reporting Services-Version und später für das Add-in für SharePoint-Produkte Aktivieren der Berichtsserver-Integrationsfunktion für alle vorhandenen Websitesammlungen, wenn das Add-In installiert ist. Darüber hinaus ist die Funktion für neue Websitesammlungen automatisch aktiv.|  
|**Funktion für die Berichtsserverintegration**|Ermöglicht umfassende berichterstellung mithilfe von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Reporting Services<br /><br /> Diese Funktion ist standardmäßig aktiv.|  
|**Power View-Integrationsfunktion**|Aktiviert das interaktive Durchsuchen von Daten und deren visuelle Präsentation für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen und tabellarische Analysis Services-Datenbanken.<br /><br /> Auf das Feature kann über die Kontextmenüs der folgenden Datenquellen zugegriffen werden:<br /><br /> **RDLX**<br /><br /> **RSDS**<br /><br /> **BISM** -Verbindungsdatei<br /><br /> <br /><br /> Wenn [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] nicht in den Kontextmenüs angezeigt wird, sollten Sie überprüfen, ob die **Power View-Integrationsfunktion** aktiviert ist.<br /><br /> Diese Funktion ist standardmäßig deaktiviert.|  

## <a name="next-steps"></a>Nächste Schritte

[Aktivieren der Berichtsserver- und Power View-Integrationsfunktionen in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Einstellungen und Funktionen für Reporting Services-Websites &#40;SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien in der SharePoint-Zentraladministration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

