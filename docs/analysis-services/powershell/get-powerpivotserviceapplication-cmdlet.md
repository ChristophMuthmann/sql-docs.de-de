---
title: Get-PowerPivotServiceApplication-Cmdlet | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71fb05a62dab5ec224744df9425e06cf23c16397
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="get-powerpivotserviceapplication-cmdlet"></a>Get-PowerPivotServiceApplication-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ruft mindestens eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung ab.  

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
  
### <a name="commonparameters"></a>\<CommonParameters>  
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
  
  
