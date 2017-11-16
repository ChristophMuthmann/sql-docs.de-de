---
title: Invoke-ProcessPartition-Cmdlet | Microsoft Docs
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
ms.assetid: 516fab44-734e-425b-9bd0-b4aee1fd338f
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b29970facb251e859e1e845c00d4c12587ca33c4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="invoke-processpartition-cmdlet"></a>Invoke-ProcessPartition-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Verarbeiten Sie eine Partition mit einer bestimmten Verarbeitungstypvariable.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="syntax"></a>Syntax  
 `Invoke-ProcessPartition [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [-CubeName] <System.String> [-MeasureGroupName] <System.String> [<CommonParameters>]`  
  
 `Invoke-ProcessPartition –DatabasePartition <Microsoft.AnalysisServices.Partition> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Das Invoke-ProcessParitions-Cmdlet verarbeitet eine bestimmte Partition einer Analysis Services-Datenbank für einen angegebenen Cube und eine Measuregruppe. Der ProcessType-Wert bestimmt den Bereich des Verarbeitungsvorgangs. Bei der Verarbeitung einer Partition muss der Verarbeitungstyp angegeben werden. Weitere Informationen finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-name-string"></a>-Namen \<Zeichenfolge >  
 Gibt die Partition an, die verarbeitet werden soll.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-database-string"></a>-Datenbank \<Zeichenfolge >  
 Gibt die Datenbank an, zu der der Cube gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-cubename-string"></a>CubeName - \<Zeichenfolge >  
 Gibt den Cube an, zu dem die Measuregruppe gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-measuregroupname-string"></a>MeasureGroupName - \<Zeichenfolge >  
 Gibt die Measuregruppe an, zu der die Partition gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-databasepartition-microsoftanalysisservicespartition"></a>-DatabasePartition \<das Microsoft.AnalysisServices.Partition >  
 Gibt die Partition an, die verarbeitet werden soll.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>Der ProcessType - \<Microsoft.AnalysisServices.ProcessType >  
 Gibt den Prozesstyp an: ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|InclusionThresholdSetting|  
|Ausgaben|InclusionThresholdSetting|  
  
## <a name="example-1"></a>Beispiel 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\Sales Orders\Partitions\Total_Orders_2004 > Get-Item .| Invoke-ProcessPartition –ProcessType:ProcessDefault`  
  
 Dieser Befehl wird bis in die Identität der Partition weitergereicht, die verarbeitet werden soll.  
  
## <a name="example-2"></a>Beispiel 2  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups> Invoke-ProcessPartition –Name “Total_Orders_2003” –MeasureGroupname “Sales Order” –CubeName “Adventure Works” –database “AWTEST” –ProcessType “ProcessFull”`  
  
 Dieser Befehl verarbeitet die Partition Total_Orders_2003 in der Measuregruppe Verkaufsaufträge der Datenbank AWTEST.  
  
  
  

