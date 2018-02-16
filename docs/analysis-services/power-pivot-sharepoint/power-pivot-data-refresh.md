---
title: Power Pivot-Datenaktualisierung | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: ac8358a3-ee71-44c7-8ee6-ac7afe3ebaa4
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 22a4a92f63616664ff5018d8a440e437879c7225
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="power-pivot-data-refresh"></a>PowerPivot-Datenaktualisierung
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Nachdem Sie eine Arbeitsmappe mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten erstellt haben, können Sie die Daten in regelmäßigen Abständen aktualisieren, indem Sie eine Abfrage oder einen Befehl wiederholt ausführen, um aktualisierte Informationen aus den Quellen abzurufen, die ursprünglich zum Erstellen der Arbeitsmappe verwendet wurden. Dieses Verfahren wird als **Datenaktualisierung**bezeichnet. Sie können Daten bedarfsgesteuert in [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]oder in einem geplanten Vorgang aktualisieren, der als [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Prozess auf einem Anwendungsserver in einer SharePoint-Farm ausgeführt wird. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [PowerPivot-Datenaktualisierung mit SharePoint 2010](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)  
  
-   [Konfigurieren des PowerPivot-Kontos für die unbeaufsichtigte Datenaktualisierung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
-   [Konfigurieren gespeicherter Anmeldeinformationen für die PowerPivot-Datenaktualisierung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75)  
  
-   [Planen einer Datenaktualisierung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/8571208f-6aae-4058-83c6-9f916f5e2f9b)  
  
-   [Anzeigen des Verlaufs von Datenaktualisierungen &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und Excel Services von SharePoint Server 2013 verwenden eine andere Architektur für die Datenaktualisierung bei [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Datenmodellen. In der von SharePoint 2013 unterstützten Architektur wird Excel Services als Hauptkomponente zum Laden von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenmodellen genutzt. In der vorherigen Datenaktualisierungsarchitektur wurden Datenmodelle mithilfe eines Servers geladen, auf dem der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] im SharePoint-Modus ausgeführt wurden. Weitere Informationen finden Sie unter den folgenden Links:  
>   
>  -   [Power Pivot-Datenaktualisierung mit SharePoint 2013](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [Aktualisieren von Arbeitsmappen und planmäßige Datenaktualisierungen &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
