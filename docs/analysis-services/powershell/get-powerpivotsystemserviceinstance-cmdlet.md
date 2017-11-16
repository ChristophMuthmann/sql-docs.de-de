---
title: Get-PowerPivotSystemServiceInstance-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 56027a8e-1949-4349-b616-68c8b1d2963c
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 569f03f0a1444d610462317a5ee19dc60f314d31
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="get-powerpivotsystemserviceinstance-cmdlet"></a>Get-PowerPivotSystemServiceInstance-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Gibt mindestens eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz zurück, die auf Anwendungsservern in der Farm ausgeführt wird.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
Get-PowerPivotSystemServiceInstance [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Das Get-PowerPivotSystemServiceInstance-Cmdlet gibt die Eigenschaften von einer oder mehreren [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienstinstanzen zurück, die in der Farm ausgeführt werden. Das Cmdlet meldet den Anwendungstyp, den Status (online oder offline) und die Identität. Um zusätzliche Eigenschaften einer bestimmten Instanz anzuzeigen, fügen Sie dem Cmdlet den Identity-Parameter und die Option format-list hinzu.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>-Identity \<PowerPivotMidTierServiceInstancePipeBind >  
 Gibt die abzurufende Dienstinstanz an. Der Wert muss eine gültige GUID sein, die das Objekt in der Farm eindeutig identifiziert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die folgenden allgemeinen Parameter: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer und OutVariable. Weitere Informationen finden Sie unter [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|Keine.|  
  
## <a name="example-1"></a>Beispiel 1  
  
```  
C:\PS>Get-PowerPivotSystemServiceInstance -Identity 1234567-890a-bcde-fghijklm | format-list| format-list  
```  
  
 In diesem Beispiel werden zusätzliche Eigenschaften der angegebenen Instanz zurückgegeben, einschließlich Servername, Version und Upgradestatus.  
  
  

