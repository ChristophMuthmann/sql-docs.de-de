---
title: "WMI-Anbieterbibliotheksreferenz für Reporting Services (SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname: Reporting Services WMI Provider Library
apilocation: reportingservices.mof
helpviewer_keywords: WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
caps.latest.revision: "42"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b936f5bed142afdf3aa2b93161339e8180fb0ef5
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Reporting Services-WMI-Anbieterbibliotheksreferenz (SSRS)
  Der Anbieter der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) unterstützt WMI-Vorgänge, die es Ihnen ermöglichen, Skripts und Code zum Ändern der Einstellungen des Berichtsservers und des Berichts-Managers zu erstellen.  
  
 Wenn Sie zum Beispiel ändern möchten, ob die integrierte Sicherheit verwendet wird, wenn der Berichtsserver eine Verbindung zur Berichtsserver-Datenbank herstellt, erstellen Sie eine Instanz der MSReportServer_ConfigurationSetting-Klasse, und verwenden Sie die DatabaseIntegratedSecurity-Eigenschaft der Berichtsserverinstanz. Die in der folgenden Tabelle angezeigten Klassen stellen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Komponenten dar. Die Klassen werden entweder im [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] -Namespace oder im [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] -Namespace definiert. Jede der Klassen unterstützt Lese- und Schreibvorgänge. Erstellvorgänge werden nicht unterstützt.  
  
## <a name="classes"></a>Klassen  
 [MSReportServer_Instance-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-class.md)  
 Stellt grundlegende Informationen bereit, die ein Client benötigt, um eine Verbindung mit einem installierten Berichtsserver herzustellen.  
  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
 Stellt die Installationsparameter und die Laufzeitparameter einer Berichtsserverinstanz dar. Diese Parameter werden in der Konfigurationsdatei für den Berichtsserver gespeichert.  
  
 Weitere Informationen zu WMI-Vorgängen finden Sie in der WMI SDK-Dokumentation, die mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK geliefert wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Zugreifen auf den Reporting Services-WMI-Anbieter](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [Technische Referenz (SSRS)](../../reporting-services/technical-reference-ssrs.md)  
  
  
