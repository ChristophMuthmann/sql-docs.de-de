---
title: "Remove-PowerPivotServiceApplication-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 2742b2a3-927c-4e7c-bd7d-43c072fa01ab
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 11
---
# Remove-PowerPivotServiceApplication-Cmdlet
  Löscht eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung.  
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## Syntax  
  
```  
Remove-PowerPivotServiceApplication [-Identity <SPGeminiServiceApplicationPipeBind>] [-DeleteAll <switch>] [-RemoveData <switch>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## Description  
 Das Remove-PowerPivotServiceApplication-Cmdlet löscht eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung aus der Farm. Verwenden Sie DeleteAll, um alle Dienstanwendungen auf einmal zu löschen, oder verwenden Sie den Identity-Parameter, um eine einzelne Instanz zu entfernen. Führen Sie zum Abrufen von Instanzinformationen Get-PowerPivotServiceApplication aus, um alle Instanzen der Farm zurückzugeben.  
  
 Verwenden Sie den RemoveData-Parameter, um Dienstanwendungsdatenbanken und zwischengespeicherte Dateien optional zu entfernen. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Arbeitsmappen verbleiben in Inhaltsbibliotheken, funktionieren jedoch nicht mehr, nachdem die Dienstanwendung entfernt wurde.  
  
## Parameter  
  
### -Identity \<SPGeminiServiceApplicationPipeBind>  
 Gibt die GUID einer einzelnen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung in der Farm an. Sie müssen die GUID angeben, wenn Sie nur eine Anwendung entfernen und die anderen Dienstanwendungen unverändert lassen möchten.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Confirm \<switch>  
 Fordert eine Bestätigung an, bevor der Befehl ausgeführt wird. Dieser Wert ist standardmäßig aktiviert. Geben Sie Confirm:$false für einen Befehl an, um die Bestätigungsantwort in einem Befehl zu umgehen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -DeleteAll \<switch>  
 Löscht alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendungen, aber löscht weder die Datenbank der Dienstanwendung noch die Dienstinstanzobjekte in der Farm. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service- und [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Moduldienstobjekte bleiben nach dem Entfernen der Dienstanwendungen instanziiert, sind jedoch nicht mehr verwendbar.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -RemoveData \<switch>  
 Entfernt die Dienstanwendungs-Datenbank, in der Zeitpläne zur Datenaktualisierung, Daten zur Arbeitsmappenverwendung, Instanzzuordnungen, die zum Verfolgen der geladenen Datenbanken verwendet werden, und andere interne Daten enthalten sind.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
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
C:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop  
```  
  
 In diesem Beispiel wird eine einzelne [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung gelöscht, wobei jedoch nicht die dazugehörige Datenbank oder der Cache entfernt wird. Wenn Sie keine Identität angeben, werden Sie zur Eingabe aufgefordert.  
  
## Beispiel 2  
  
```  
C:\PS>Remove-PowerPivotServiceApplication -DeleteAll  
```  
  
 In diesem Beispiel werden alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendungen der Farm gelöscht. Datenbanken und der Cache werden nicht gelöscht.  
  
## Beispiel 3  
  
```  
CC:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop -RemoveData  
```  
  
 In diesem Beispiel wird eine einzelne [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung zusammen mit der dazugehörigen Datenbank und den Cachedateien gelöscht.  
  
  