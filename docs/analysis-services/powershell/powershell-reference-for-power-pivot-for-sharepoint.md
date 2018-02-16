---
title: "PowerShell-Referenz für PowerPivot für SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2015
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c01735a8-f919-48ad-8d74-35d75a18f821
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae14a52c81407cf4b161d1347d7a769aad168eca
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="powershell-reference-for-power-pivot-for-sharepoint"></a>PowerShell-Referenz für PowerPivot für SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
In diesem Abschnitt sind die zum Konfigurieren oder Verwalten einer [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Installation verwendeten PowerShell-Cmdlets aufgeführt. Weitere Informationen zum Aktivieren der Cmdlets und Anzeigen der integrierten Hilfe finden Sie unter [PowerPivot-Konfiguration mit Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="cmdlet-list"></a>Cmdlet-Liste  
 So zeigen Sie eine Liste der Cmdlets an der PowerShell-Eingabeaufforderung an:  
  
1.  Öffnen Sie die SharePoint-Verwaltungsshell unter Verwendung der Option **Als Administrator ausführen** .  
  
2.  Geben Sie den folgenden Befehl ein: `Get-help *powerpivot*`  
  
|Cmdlet|Unterstützte Versionen|  
|------------|------------------------|  
|[Get-PowerPivotServiceApplication cmdlet (Get-PowerPivotServiceApplication-Cmdlet)](../../analysis-services/powershell/get-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Get-PowerPivotSystemService-Cmdlet](../../analysis-services/powershell/get-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Get-PowerPivotSystemServiceInstance-Cmdlet](../../analysis-services/powershell/get-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[New-PowerPivotServiceApplication-Cmdlet](../../analysis-services/powershell/new-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[New-PowerPivotSystemServiceInstance cmdlet (New-PowerPivotSystemServiceInstance-Cmdlet)](../../analysis-services/powershell/new-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Remove-PowerPivotServiceApplication-Cmdlet](../../analysis-services/powershell/remove-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Remove-PowerPivotSystemServiceInstance-Cmdlet](../../analysis-services/powershell/remove-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Set-PowerPivotServiceApplication cmdlet (Set-PowerPivotServiceApplication-Cmdlet)](../../analysis-services/powershell/set-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Set-PowerPivotSystemService cmdlet (Set-PowerPivotSystemService-Cmdlet)](../../analysis-services/powershell/set-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Update-PowerPivotSystemService-Cmdlet](../../analysis-services/powershell/update-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
  
 Hinweis: Die folgenden Cmdlets haben nur mit SharePoint 2010 funktioniert, das von [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] nicht unterstützt wird.  
  
-   Get-PowerPivotEngineService  
  
-   Get-PowerPivotEngineServiceInstance  
  
-   New-PowerPivotEngineServiceInstance  
  
-   Remove-PowerPivotEngineServiceInstance  
  
-   Set-PowerPivotEngineService  
  
-   Set-PowerPivotEngineServiceInstance  
  
-   Update-PowerPivotEngineService  
  
  
