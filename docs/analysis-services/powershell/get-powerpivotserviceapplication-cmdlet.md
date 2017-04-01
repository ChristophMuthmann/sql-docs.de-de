---
title: "Get-PowerPivotServiceApplication-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 99e4faa1-2f87-43c6-b7ec-a97d4112c5ac
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Get-PowerPivotServiceApplication-Cmdlet
  Ruft mindestens eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung ab.  
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## Syntax  
  
```  
Get-PowerPivotServiceApplication [[-Identity] <SPGeminiServiceApplicationPipeBind>] [<CommonParameters>]  
```  
  
## Description  
 Das Get-PowerPivotServiceApplication-Cmdlet gibt die vom Identity-Parameter angegebene Dienstanwendung zurück. Wenn kein Parameter angegeben wird, gibt das Cmdlet alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen der Farm zurück. Jede Anwendung wird über ihren Anzeigenamen, den Anwendungstyp und die GUID identifiziert. Fügen Sie dem Cmdlet die Option format-list hinzu, um zusätzliche Eigenschaften einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung anzuzeigen.  
  
## Parameter  
  
### -Identity \<SPGeminiServiceApplicationPipeBind>  
 Gibt die abzurufende Dienstanwendung an. Der Wert muss eine gültige GUID sein, die das Objekt in der Farm eindeutig identifiziert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### \<CommonParameters>  
 Dieses Cmdlet unterstützt die folgenden allgemeinen Parameter: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer und OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|Keine.|  
  
## Beispiel 1  
  
```  
C:\PS>Get-PowerPivotServiceApplication  
```  
  
 In diesem Beispiel wird mindestens eine Dienstanwendung in der Farm zurückgegeben.  
  
## Beispiel 2  
  
```  
C:\PS>Get-PowerPivotServiceApplication | format-list  
```  
  
 In diesem Beispiel werden alle Eigenschaften einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung zurückgegeben.  
  
## Beispiel 3  
  
```  
C:\PS>get-PowerPivotServiceApplication -Identity 1234567-890a-bcde-fghijklm  
```  
  
 In diesem Beispiel wird eine einzelne Dienstanwendung zurückgegeben und der Anzeigename, Anwendungstyp und die GUID der Anwendung angezeigt. Falls der Anzeigename sehr lang ist, wird er abgeschnitten. Verwenden Sie die Option format-list, um den vollständigen Namen anzuzeigen.  
  
  