---
title: "Invoke-ProcessDimension-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 9506938e-7f9f-4595-ad6d-98c8b0ce8395
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Invoke-ProcessDimension-Cmdlet
  Verarbeitet eine Dimension mit einer bestimmten Verarbeitungstypvariable.  
  
## Syntax  
 `Invoke-ProcessDimension [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
 `Invoke-ProcessDimension –DatabaseDimension <Microsoft.AnalysisServices.Dimension> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## Description  
 Die angegebene Dimension wird vom Invoke-ProcessDimension-Cmdlet verarbeitet. Sie müssen den Verarbeitungstyp angeben. Weitere Informationen zur Verarbeitung von Typen für eine Dimension finden Sie unter [Verarbeiten von Optionen und Einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## Parameter  
  
### -Name \<Zeichenfolge>  
 Gibt die Dimension an, die verarbeitet werden soll.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Database \<Zeichenfolge>  
 Gibt die Datenbank an, zu der die Dimension gehört.  
  
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
  
### -DatabaseDimension \<Microsoft.AnalysisSevices.Dimension>  
 Gibt ein Microsoft.AnalysisServices.Dimension-Objekt an, das verarbeitet werden soll. Verwenden Sie diesen Parameter, wenn Sie den Dimensionsnamen über die Pipeline übergeben möchten.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|True (ByPropertyName)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### \<CommonParameters>  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Microsoft.AnalysisSevices.Dimension|  
|Ausgaben|InclusionThresholdSetting|  
  
## Beispiel 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Dimensions\Account> Get-Item .| Invoke-ProcessDimension –ProcessType:ProcessDefault`  
  
 Mit diesem Befehl wird das angegebene Dimensionsobjekt über die Pipeline abgerufen und verarbeitet.  
  
## Beispiel 2  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Dimensions > Invoke-ProcessDimension –Name “Customer” –Database “AWTEST” –ProcessType “ProcessDefault”`  
  
 Mit diesem Befehl wird eine bestimmte Dimension identifiziert, die verarbeitet wird.  
  
> [!NOTE]  
>  Manchmal wird eine erfolgreich verarbeitete Dimension als 'nicht verarbeitet' angezeigt, wenn Sie den Dimensionen-Ordner im PowerShell-Fenster auflisten. Um zu überprüfen, ob eine Dimension tatsächlich verarbeitet wurde, überprüfen Sie die Dimensionseigenschaften in SQL Server Management Studio.  
  
## Siehe auch  
 [PowerShell-Skripts in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Verwalten von tabellarischen Modellen mit PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  