---
title: "Remove-PowerPivotSystemServiceInstance-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Remove-PowerPivotSystemServiceInstance-Cmdlet
  Entfernt eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz aus der Farm.  
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## Syntax  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## Description  
 Das Cmdlet „Remove-PowerPivotSystemServiceInstance“ entfernt Instanzinformationen zum [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service aus der Farm. Dabei werden die Programmdateien nicht entfernt. Um die Programmdateien endgültig zu entfernen, müssen Sie sie deinstallieren.  
  
 Wenn Sie den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service entfernen, sollten Sie auch „Remove-PowerPivotEngineServiceInstance“ ausführen, um die zugeordnete Analysis Services-Instanz zu entfernen, gefolgt von „Remove-PowerPivotServiceApplication“, um etwaige PowerPivot-Dienstanwendungen zu löschen. Die Dienstanwendungen werden nicht mehr ausgeführt, nachdem die Dienste entfernt wurden.  
  
 Wenn Sie diese Änderung rückgängig machen möchten, können Sie New-PowerPivotSystemServiceInstance -Provision:$true ausführen, um die Instanzinformationen wieder zu aktivieren.  
  
## Parameter  
  
### -Identity \<PowerPivotMidTierServiceInstancePipeBind>  
 Gibt die GUID der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz an, die Sie entfernen möchten. Auf jedem Anwendungsserver, der über eine Installation von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint verfügt, ist eine Dienstinstanz vorhanden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -DeleteLocal \<switch>  
 Löscht die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz, die auf dem lokalen Computer installiert ist, sodass Sie die Instanz entfernen können, ohne eine Objektidentität angeben zu müssen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
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
  
### \<CommonParameters>  
 Dieses Cmdlet unterstützt die folgenden allgemeinen Parameter: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer und OutVariable. Weitere Informationen finden Sie unter [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|Keine.|  
  
## Beispiel 1  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 In diesem Beispiel wird gezeigt, wie Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Instanz entfernen, die auf dem lokalen Anwendungsserver ausgeführt wird.  
  
## Beispiel 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 In diesem Beispiel wird gezeigt, wie ein bestimmter [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service auf Grundlage seiner Identität gelöscht wird.  
  
  