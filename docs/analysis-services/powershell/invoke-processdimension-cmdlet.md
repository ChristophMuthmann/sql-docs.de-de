---
title: Invoke-ProcessDimension-Cmdlet | Microsoft Docs
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
ms.assetid: 9506938e-7f9f-4595-ad6d-98c8b0ce8395
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8a24a4b19f20e28346456e3c0c53f39eaeb200b9
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="invoke-processdimension-cmdlet"></a>Invoke-ProcessDimension-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Verarbeitet eine Dimension mit einer bestimmten Verarbeitungstypvariable.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="syntax"></a>Syntax  
 `Invoke-ProcessDimension [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
 `Invoke-ProcessDimension –DatabaseDimension <Microsoft.AnalysisServices.Dimension> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Die angegebene Dimension wird vom Invoke-ProcessDimension-Cmdlet verarbeitet. Sie müssen den Verarbeitungstyp angeben. Weitere Informationen zur Verarbeitung von Typen für eine Dimension finden Sie unter [Verarbeiten von Optionen und Einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-name-string"></a>-Namen \<Zeichenfolge >  
 Gibt die Dimension an, die verarbeitet werden soll.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-database-string"></a>-Datenbank \<Zeichenfolge >  
 Gibt die Datenbank an, zu der die Dimension gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>Der ProcessType - \<Microsoft.AnalysisServices.ProcessType >  
 Gibt den Prozesstyp an: ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-databasedimension-microsoftanalysissevicesdimension"></a>-DatabaseDimension \<Microsoft.AnalysisSevices.Dimension >  
 Gibt ein Microsoft.AnalysisServices.Dimension-Objekt an, das verarbeitet werden soll. Verwenden Sie diesen Parameter, wenn Sie den Dimensionsnamen über die Pipeline übergeben möchten.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|True (ByPropertyName)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters>  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Microsoft.AnalysisSevices.Dimension|  
|Ausgaben|Keine|  
  
## <a name="example-1"></a>Beispiel 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Dimensions\Account> Get-Item .| Invoke-ProcessDimension –ProcessType:ProcessDefault`  
  
 Mit diesem Befehl wird das angegebene Dimensionsobjekt über die Pipeline abgerufen und verarbeitet.  
  
## <a name="example-2"></a>Beispiel 2  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Dimensions > Invoke-ProcessDimension –Name “Customer” –Database “AWTEST” –ProcessType “ProcessDefault”`  
  
 Mit diesem Befehl wird eine bestimmte Dimension identifiziert, die verarbeitet wird.  
  
> [!NOTE]  
>  Manchmal wird eine erfolgreich verarbeitete Dimension als 'nicht verarbeitet' angezeigt, wenn Sie den Dimensionen-Ordner im PowerShell-Fenster auflisten. Um zu überprüfen, ob eine Dimension tatsächlich verarbeitet wurde, überprüfen Sie die Dimensionseigenschaften in SQL Server Management Studio.  
  
  
  
