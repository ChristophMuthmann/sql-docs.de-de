---
title: Remove-PowerPivotServiceApplication-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2742b2a3-927c-4e7c-bd7d-43c072fa01ab
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7078a7733c7764b77667628071c66c8313aae85a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="remove-powerpivotserviceapplication-cmdlet"></a>Remove-PowerPivotServiceApplication-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Löscht eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -dienstanwendung.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
Remove-PowerPivotServiceApplication [-Identity <SPGeminiServiceApplicationPipeBind>] [-DeleteAll <switch>] [-RemoveData <switch>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Das Remove-PowerPivotServiceApplication-Cmdlet löscht eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung aus der Farm. Verwenden Sie DeleteAll, um alle Dienstanwendungen auf einmal zu löschen, oder verwenden Sie den Identity-Parameter, um eine einzelne Instanz zu entfernen. Führen Sie zum Abrufen von Instanzinformationen Get-PowerPivotServiceApplication aus, um alle Instanzen der Farm zurückzugeben.  
  
 Verwenden Sie den RemoveData-Parameter, um Dienstanwendungsdatenbanken und zwischengespeicherte Dateien optional zu entfernen. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Arbeitsmappen verbleiben in Inhaltsbibliotheken, funktionieren jedoch nicht mehr, nachdem die Dienstanwendung entfernt wurde.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>-Identity \<SPGeminiServiceApplicationPipeBind >  
 Gibt die GUID einer einzelnen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung in der Farm an. Sie müssen die GUID angeben, wenn Sie nur eine Anwendung entfernen und die anderen Dienstanwendungen unverändert lassen möchten.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
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
  
### <a name="-deleteall-switch"></a>DeleteAll - \<wechseln >  
 Löscht alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen, aber löscht weder die Datenbank der Dienstanwendung noch die Dienstinstanzobjekte in der Farm. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service- und [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Moduldienstobjekte bleiben nach dem Entfernen der Dienstanwendungen instanziiert, sind jedoch nicht mehr verwendbar.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-removedata-switch"></a>-RemoveData \<wechseln >  
 Entfernt die Dienstanwendungs-Datenbank, in der Zeitpläne zur Datenaktualisierung, Daten zur Arbeitsmappenverwendung, Instanzzuordnungen, die zum Verfolgen der geladenen Datenbanken verwendet werden, und andere interne Daten enthalten sind.  
  
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
C:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop  
```  
  
 In diesem Beispiel wird eine einzelne [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung gelöscht, wobei jedoch nicht die dazugehörige Datenbank oder der Cache entfernt wird. Wenn Sie keine Identität angeben, werden Sie zur Eingabe aufgefordert.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
C:\PS>Remove-PowerPivotServiceApplication -DeleteAll  
```  
  
 In diesem Beispiel werden alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen der Farm gelöscht. Datenbanken und der Cache werden nicht gelöscht.  
  
## <a name="example-3"></a>Beispiel 3  
  
```  
CC:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop -RemoveData  
```  
  
 In diesem Beispiel wird eine einzelne [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung zusammen mit der dazugehörigen Datenbank und den Cachedateien gelöscht.  
  
  
