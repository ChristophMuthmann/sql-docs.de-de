---
title: Set-PowerPivotSystemService-Cmdlet | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00f080d09fd433d22ecf0e5eebeb84e7fc6394d8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="set-powerpivotsystemservice-cmdlet"></a>Set-PowerPivotSystemService-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Legt die globalen Eigenschaften des PowerPivotSystemService-Objekts auf Farmebene fest.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
Set-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [-UpdateAssemblyInformation <switch>] [-WorkbookUpgradeOnDataRefresh <boolean>] [-DirectTCPConnections <boolean>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Das Cmdlet „Set-PowerPivotSystemService“ aktualisiert die Eigenschaften des übergeordneten [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] System Service-Objekts in der Farm.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>-Identity \<PowerPivotMidTierServicePipeBind >  
 Gibt das übergeordnete Objekt an, für das Sie Eigenschaften aktualisieren. Der Wert muss eine gültige GUID sein, die das Objekt in der Farm eindeutig identifiziert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-updateassemblyinformation-switch"></a>' Updateassemblyinformation ' - \<wechseln >  
 Wird nur zu Upgradezwecken verwendet. Wenn sich die in der Farm bereitgestellte Assemblyversion von der Version unterscheidet, die in der SharePoint-Konfigurationsdatenbank gespeichert ist, können Sie dieses Cmdlet ausführen, um die Assemblyinformationen in der Konfigurationsdatenbank zu aktualisieren. Informationen zur Assemblyversion sind in den Dateieigenschaften der Datei Microsoft.AnalysisServices.SharePoint.Integration.dll verfügbar, die in der globalen Assembly gespeichert ist.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-workbookupgradeondatarefresh-boolean"></a>-WorkbookUpgradeOnDataRefresh \<booleschen >  
 Wird verwendet, um eine [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] -Arbeitsmappe beim Starten einer geplanten Datenaktualisierung auf dem Server automatisch zu aktualisieren. Die Datenaktualisierung wird nur für Arbeitsmappen unterstützt, die mit der aktuellen Version des Servers übereinstimmen. Wenn Sie diese Eigenschaft aktivieren, wird eine Arbeitsmappe automatisch aktualisiert, damit die Datenaktualisierung fortgesetzt werden kann. Diese Eigenschaft wird auf Serverinstanzebene festgelegt. Sie können sie nicht für bestimmte Arbeitsmappen, Bibliotheken, Websites oder Benutzer variieren.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|2|  
|Standardwert|false|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-directtcpconnections-boolean"></a>-DirectTCPConnections \<boolean>  
 Gibt an, dass Excel Services alle Abfragen direkt an die Instanz von SQL Server Analysis Services (POWERPIVOT) sendet, für die eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbank geladen wurde. So wird der MSOLAP-Datenanbieter- und Kanaltransport umgangen, der andernfalls für alle Abfrageanforderungen verwendet wird, die an eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbank gesendet werden.  
  
 Das Festlegen dieser Parameter verbessert die Leistung und Skalierbarkeit von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Abfragen, indem die Verbindungen mit geladenen Datenbanken effizienter gemacht werden. Beachten Sie, dass dieser Parameter nicht das Verhalten ändert, wie die anfängliche Ladeanforderung zugeordnet wird. Andere Parameter, z.B. –RoundRobinAllocation und –HealthBasedAllocation, die zum Zuordnen von Datenbankladeanforderungen für mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Instanzen in der Farm verwendet werden, sind nicht betroffen, da –DirectTCPConnections nur für Abfragen gilt, die nach dem Laden der Datenbank ausgegeben werden.  
  
 Bei Farmtopologien, die auf separaten Anwendungsservern ausgeführte Excel Services- und [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Anwendungen enthalten, müssen Sie einen Port in der Firewall öffnen, um sicherzustellen, dass die Anforderungen die SQL Server Analysis Services (POWERPIVOT)-Instanz erreichen. Anweisungen zum Aktivieren von eingehenden Verbindungen für eine benannte Instanz von Analysis Services finden Sie unter [Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|3|  
|Standardwert|false|  
|Pipelineeingabe akzeptieren?|false|  
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
C:\PS>Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true  
```  
  
 Aktiviert das automatische Upgrade von Arbeitsmappen früherer Versionen, damit die geplante Datenaktualisierung fortgesetzt werden kann.  
  
  
