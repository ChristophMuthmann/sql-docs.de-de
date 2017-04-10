---
title: "Funktion zur Reporting Services-Websitesammlung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
caps.latest.revision: 8
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Funktion zur Reporting Services-Websitesammlung
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Modus umfasst drei SharePoint-Websitesammlung-Funktionen. Die Funktionen unterstützen Folgendes: die allgemeine Berichterstellungsumgebung des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Modus, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], eine Funktion des [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-Ins für [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition und Verwaltungsvorgänge für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der SharePoint-Zentraladministration.  
  
## Websitesammlung-Funktionen  
 In der folgenden Tabelle sind die Websitesammlung-Funktionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] beschrieben.  
  
|Funktion|Description|  
|-------------|-----------------|  
|**Funktion für die Berichtsserver-Zentraladministration**|Aktiviert Funktionen zum Verwalten der Integration in einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver. Diese Funktion ist nur unter der Websitesammlung-Funktion der SharePoint-Zentraladministration installiert und wird auch nur darunter verwendet.<br /><br /> Die Berichtsserver-Integrationsfunktion wird für die Websitesammlung in der SharePoint-Zentraladministration automatisch aktiviert, nachdem Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]-Add-In für SharePoint-Produkte installiert haben. In einigen Situationen müssen Sie die Funktion manuell aktivieren. Um die Berichtsserverfunktion zu aktivieren, verwenden Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Seiten auf der Seite Siteeinstellungen der SharePoint-Zentraladministration.<br /><br /> Durch die [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Version und höhere Versionen des Add-Ins für SharePoint-Produkte wird die Berichtsserver-Integrationsfunktion bei der Installation des Add-Ins für alle vorhandenen Websitesammlungen aktiviert. Darüber hinaus ist die Funktion für neue Websitesammlungen automatisch aktiv.|  
|**Funktion für die Berichtsserverintegration**|Ermöglicht die umfassende Berichterstellung mithilfe von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]<br /><br /> Diese Funktion ist standardmäßig aktiv.|  
|**Power View-Integrationsfunktion**|Aktiviert das interaktive Durchsuchen von Daten und deren visuelle Präsentation für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen und tabellarische Analysis Services-Datenbanken.<br /><br /> Auf das Feature kann über die Kontextmenüs der folgenden Datenquellen zugegriffen werden:<br /><br /> **RDLX**<br /><br /> **RSDS**<br /><br /> **BISM** -Verbindungsdatei<br /><br /> <br /><br /> Wenn [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] nicht in den Kontextmenüs angezeigt wird, sollten Sie überprüfen, ob die **Power View-Integrationsfunktion** aktiviert ist.<br /><br /> Diese Funktion ist standardmäßig deaktiviert.|  
  
## Siehe auch  
 [Aktivieren der Berichtsserver- und Power View-Integrationsfunktionen in SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Einstellungen und Funktionen für Reporting Services-Websites &#40;SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/reporting-services-site-settings-and-site-features-sharepoint-mode.md)   
 [Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien in der SharePoint-Zentraladministration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  
  
  