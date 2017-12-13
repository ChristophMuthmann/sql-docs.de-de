---
title: Remove-PowerPivotSystemServiceInstance-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 64bb88fb6bc4a86228fef718f1ba8382ef492039
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="remove-powerpivotsystemserviceinstance-cmdlet"></a>Remove-PowerPivotSystemServiceInstance-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Entfernt eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz aus der Farm.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Das Cmdlet „Remove-PowerPivotSystemServiceInstance“ entfernt Instanzinformationen zum [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service aus der Farm. Dabei werden die Programmdateien nicht entfernt. Um die Programmdateien endgültig zu entfernen, müssen Sie sie deinstallieren.  
  
 Wenn Sie den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service entfernen, sollten Sie auch „Remove-PowerPivotEngineServiceInstance“ ausführen, um die zugeordnete Analysis Services-Instanz zu entfernen, gefolgt von „Remove-PowerPivotServiceApplication“, um etwaige PowerPivot-Dienstanwendungen zu löschen. Die Dienstanwendungen werden nicht mehr ausgeführt, nachdem die Dienste entfernt wurden.  
  
 Wenn Sie diese Änderung rückgängig machen möchten, können Sie New-PowerPivotSystemServiceInstance -Provision:$true ausführen, um die Instanzinformationen wieder zu aktivieren.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>-Identity \<PowerPivotMidTierServiceInstancePipeBind >  
 Gibt die GUID der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz an, die Sie entfernen möchten. Auf jedem Anwendungsserver, der über eine Installation von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint verfügt, ist eine Dienstinstanz vorhanden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-deletelocal-switch"></a>-DeleteLocal \<wechseln >  
 Löscht die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz, die auf dem lokalen Computer installiert ist, sodass Sie die Instanz entfernen können, ohne eine Objektidentität angeben zu müssen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-confirm-switch"></a>-Bestätigen Sie \<wechseln >  
 Fordert eine Bestätigung an, bevor der Befehl ausgeführt wird. Dieser Wert ist standardmäßig aktiviert. Geben Sie Confirm:$false für einen Befehl an, um die Bestätigungsantwort in einem Befehl zu umgehen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die folgenden allgemeinen Parameter: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer und OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|Keine.|  
  
## <a name="example-1"></a>Beispiel 1  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 In diesem Beispiel wird gezeigt, wie Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz entfernen, die auf dem lokalen Anwendungsserver ausgeführt wird.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 In diesem Beispiel wird gezeigt, wie ein bestimmter [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service auf Grundlage seiner Identität gelöscht wird.  
  
  
