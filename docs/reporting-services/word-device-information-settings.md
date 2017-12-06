---
title: "Geräteinformationseinstellungen für Word | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7001097fb8dc92e82254b586f785a79fa193a548
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="word-device-information-settings"></a>Geräteinformationseinstellungen für Word
  In der folgenden Tabelle werden die Geräteinformationseinstellungen zum Rendern in das Format [!INCLUDE[ofprword](../includes/ofprword-md.md)] aufgeführt.  
  
|Einstellung|Wert|  
|-------------|-----------|  
|**AutoFit**|**False**. AutoAnpassen wird in jeder Word-Tabelle auf **false** eingestellt.<br /><br /> **True**. AutoAnpassen wird in jeder Word-Tabelle auf **true** eingestellt.<br /><br /> **Never**. Die Werte für AutoAnpassen sind in keiner Word-Tabelle festgelegt, und der Word-Standardwert wird wiederhergestellt.<br /><br /> **Default**. AutoAnpassen wird in den Tabellen eingestellt, die enger als der physische Zeichenbereich (physische Seitenbreite ohne Ränder) pro logischer Seite sind.|  
|**ExpandToggles**|Gibt an, ob alle Elemente, die aus- und eingeschaltet werden können, in ihrem voll erweiterten Status gerendert werden sollten. Der Standardwert ist **false**.|  
|**FixedPageWidth**|Gibt an, ob die in die DOC-Datei geschriebene Seitenbreite erhöht wird, damit die Breite der größten Seite im Hauptteil des Berichts hineinpasst. Der Standardwert ist **false**.|  
|**OmitHyperlinks**|Gibt an, ob die Linkaktion auf allen Elementen weggelassen werden soll, wo sie festgelegt ist. Der Standardwert ist **false**|  
|**OmitDrillthroughs**|Gibt an, ob die Drillthrough-Aktion auf allen Elementen weggelassen werden soll, wo sie festgelegt ist. Der Standardwert ist **false**|  
  
## <a name="see-also"></a>Siehe auch  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Übergeben von Geräteinformationseinstellungen an Renderingerweiterungen](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Anpassen der Parameter für Renderingerweiterungen in der Datei „RSReportServer.config“](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Technische Referenz (SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  
