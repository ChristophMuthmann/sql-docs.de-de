---
title: "Invoke-ProcessCube-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: b10ba7c1-8f10-4e72-9626-f9285e4341fd
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Invoke-ProcessCube-Cmdlet
  Verarbeitet einen Cube mit einer bestimmten Verarbeitungstypvariable.  
  
## Syntax  
 `Invoke-ProcessCube [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
 `Invoke-ProcessCube –DatabaseCube <Microsoft.AnalysisServices.Cube> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## Description  
 Das Invoke-ProcessCube-Cmdlet verarbeitet einen Cube auf der Ebene, die Sie angeben. ProcessFull überschreibt z. B. vorhandene Daten mit allen neuen Daten. Bei der Verarbeitung eines Cubes muss der Verarbeitungstyp angegeben werden. Weitere Informationen finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## Parameter  
  
### -Name \<string>  
 Gibt den Cube an, der verarbeitet werden soll.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Database \<string>  
 Gibt die Datenbank an, zu der der Cube gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -ProcessType \<Microsoft.AnalysisServices.ProcessType>  
 Gibt den Prozesstyp an: ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -DatabaseCube \<Microsoft.AnalysisSevices.Cube>  
 Gibt ein Microsoft.AnalysisServices.Cube-Objekt an, das verarbeitet werden soll. Verwenden Sie diesen Parameter, wenn Sie den Cubenamen über die Pipeline übergeben möchten.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|True (ByPropertyName)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### \<CommonParameters>  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|InclusionThresholdSetting|  
|Ausgaben|InclusionThresholdSetting|  
  
## Beispiel 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works > Get-Item .| Invoke-ProcessCube–ProcessType:ProcessDefault`  
  
 Dieser Befehl wird bis in die Identität des Cubes weitergereicht, der verarbeitet werden soll.  
  
## Beispiel 2  
 `PS SQL SERVER:\sqlas\locahost\default > Invoke-ProcessCube “Adventure Works” –database AWTEST –ProcessType:ProcessDefault`  
  
 Mit diesem Befehl wird der Adventure Works-Cube in der AWTEST-Datenbank verarbeitet.  
  
## Siehe auch  
 [PowerShell-Skripts in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Verwalten von tabellarischen Modellen mit PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  