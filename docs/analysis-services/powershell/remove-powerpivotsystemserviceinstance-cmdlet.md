---
title: Remove-PowerPivotSystemServiceInstance-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e44d28106db0c14c293c463d91125b262190350d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="remove-powerpivotsystemserviceinstance-cmdlet"></a>Remove-PowerPivotSystemServiceInstance-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Entfernt eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz aus der Farm.  

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
  
  

