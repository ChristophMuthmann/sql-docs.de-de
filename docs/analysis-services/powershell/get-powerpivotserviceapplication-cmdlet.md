---
title: Get-PowerPivotServiceApplication-Cmdlet | Microsoft Docs
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
ms.assetid: 99e4faa1-2f87-43c6-b7ec-a97d4112c5ac
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: df1c2c4108ad29164ab096fde95bc760a0c7ccb0
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="get-powerpivotserviceapplication-cmdlet"></a>Get-PowerPivotServiceApplication-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Gibt einen oder mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -dienstanwendungen.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
Get-PowerPivotServiceApplication [[-Identity] <SPGeminiServiceApplicationPipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Das Get-PowerPivotServiceApplication-Cmdlet gibt die vom Identity-Parameter angegebene Dienstanwendung zurück. Wenn kein Parameter angegeben wird, gibt das Cmdlet alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen der Farm zurück. Jede Anwendung wird über ihren Anzeigenamen, den Anwendungstyp und die GUID identifiziert. Fügen Sie dem Cmdlet die Option format-list hinzu, um zusätzliche Eigenschaften einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung anzuzeigen.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>-Identity \<SPGeminiServiceApplicationPipeBind >  
 Gibt die abzurufende Dienstanwendung an. Der Wert muss eine gültige GUID sein, die das Objekt in der Farm eindeutig identifiziert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
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
C:\PS>Get-PowerPivotServiceApplication  
```  
  
 In diesem Beispiel wird mindestens eine Dienstanwendung in der Farm zurückgegeben.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
C:\PS>Get-PowerPivotServiceApplication | format-list  
```  
  
 In diesem Beispiel werden alle Eigenschaften einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung zurückgegeben.  
  
## <a name="example-3"></a>Beispiel 3  
  
```  
C:\PS>get-PowerPivotServiceApplication -Identity 1234567-890a-bcde-fghijklm  
```  
  
 In diesem Beispiel wird eine einzelne Dienstanwendung zurückgegeben und der Anzeigename, Anwendungstyp und die GUID der Anwendung angezeigt. Falls der Anzeigename sehr lang ist, wird er abgeschnitten. Verwenden Sie die Option format-list, um den vollständigen Namen anzuzeigen.  
  
  
