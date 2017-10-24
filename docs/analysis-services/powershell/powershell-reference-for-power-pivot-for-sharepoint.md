---
title: "PowerShell-Referenz für PowerPivot für SharePoint | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/16/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c01735a8-f919-48ad-8d74-35d75a18f821
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 39567e2b212761ac2dd726a1f8f33893a83f245c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="powershell-reference-for-power-pivot-for-sharepoint"></a>PowerShell-Referenz für PowerPivot für SharePoint

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  In diesem Abschnitt sind die zum Konfigurieren oder Verwalten einer [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Installation verwendeten PowerShell-Cmdlets aufgeführt. Weitere Informationen zum Aktivieren der Cmdlets und Anzeigen der integrierten Hilfe finden Sie unter [PowerPivot-Konfiguration mit Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="cmdlet-list"></a>Cmdlet-Liste  
 So zeigen Sie eine Liste der Cmdlets an der PowerShell-Eingabeaufforderung an:  
  
1.  Öffnen Sie die SharePoint-Verwaltungsshell unter Verwendung der Option **Als Administrator ausführen** .  
  
2.  Geben Sie den folgenden Befehl ein: `Get-help *powerpivot*`  
  
|Cmdlet|Unterstützte Versionen|  
|------------|------------------------|  
|[Get-PowerPivotServiceApplication-Cmdlet](../../analysis-services/powershell/get-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Get-PowerPivotSystemService-Cmdlet](../../analysis-services/powershell/get-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Get-PowerPivotSystemServiceInstance-Cmdlet](../../analysis-services/powershell/get-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[New-PowerPivotServiceApplication-Cmdlet](../../analysis-services/powershell/new-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[New-PowerPivotSystemServiceInstance-Cmdlet](../../analysis-services/powershell/new-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Remove-PowerPivotServiceApplication-Cmdlet](../../analysis-services/powershell/remove-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Remove-PowerPivotSystemServiceInstance-Cmdlet](../../analysis-services/powershell/remove-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Set-PowerPivotServiceApplication-Cmdlet](../../analysis-services/powershell/set-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Set-PowerPivotSystemService-Cmdlet](../../analysis-services/powershell/set-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Update-PowerPivotSystemService-Cmdlet](../../analysis-services/powershell/update-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
  
 Hinweis: Die folgenden Cmdlets haben nur mit SharePoint 2010 funktioniert, das von [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] nicht unterstützt wird.  
  
-   Get-PowerPivotEngineService  
  
-   Get-PowerPivotEngineServiceInstance  
  
-   New-PowerPivotEngineServiceInstance  
  
-   Remove-PowerPivotEngineServiceInstance  
  
-   Set-PowerPivotEngineService  
  
-   Set-PowerPivotEngineServiceInstance  
  
-   Update-PowerPivotEngineService  
  
  

