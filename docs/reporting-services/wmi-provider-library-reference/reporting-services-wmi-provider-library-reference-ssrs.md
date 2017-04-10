---
title: "Reporting Services-WMI-Anbieterbibliotheksreferenz (SSRS) | Microsoft Docs"
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
apiname: 
  - "Reporting Services WMI Provider Library"
apilocation: 
  - "reportingservices.mof"
helpviewer_keywords: 
  - "WMI-Anbieter [Reporting Services], Bibliothek"
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# Reporting Services-WMI-Anbieterbibliotheksreferenz (SSRS)
  Der Anbieter der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) unterstützt WMI-Vorgänge, die es Ihnen ermöglichen, Skripts und Code zum Ändern der Einstellungen des Berichtsservers und des Berichts-Managers zu erstellen.  
  
 Wenn Sie zum Beispiel ändern möchten, ob die integrierte Sicherheit verwendet wird, wenn der Berichtsserver eine Verbindung zur Berichtsserver-Datenbank herstellt, erstellen Sie eine Instanz der MSReportServer_ConfigurationSetting-Klasse, und verwenden Sie die DatabaseIntegratedSecurity-Eigenschaft der Berichtsserverinstanz. Die in der folgenden Tabelle angezeigten Klassen stellen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Komponenten dar. Die Klassen werden entweder im [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] -Namespace oder im [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] -Namespace definiert. Jede der Klassen unterstützt Lese- und Schreibvorgänge. Erstellvorgänge werden nicht unterstützt.  
  
## Klassen  
 [MSReportServer_Instance-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-class.md)  
 Stellt grundlegende Informationen bereit, die ein Client benötigt, um eine Verbindung mit einem installierten Berichtsserver herzustellen.  
  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
 Stellt die Installationsparameter und die Laufzeitparameter einer Berichtsserverinstanz dar. Diese Parameter werden in der Konfigurationsdatei für den Berichtsserver gespeichert.  
  
 Weitere Informationen zu WMI-Vorgängen finden Sie in der WMI SDK-Dokumentation, die mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK geliefert wird.  
  
## Siehe auch  
 [Zugreifen auf den Reporting Services-WMI-Anbieter](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [Technische Referenz &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  