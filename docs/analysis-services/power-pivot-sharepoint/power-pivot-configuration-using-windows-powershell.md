---
title: Power Pivot-Konfiguration mit Windows PowerShell | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ff0decfe7bfe8ba1d93c4b722fecbc50c0d86ed1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="power-pivot-configuration-using-windows-powershell"></a>PowerPivot-Konfiguration mit Windows PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] enthält Windows PowerShell-Cmdlets, mit denen Sie eine Installation von [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]konfigurieren können. Für die vollständige Konfiguration einer Installation mit PowerShell ist die Verwendung von SharePoint-Cmdlets und [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Cmdlets erforderlich. Ein Großteil der Konfiguration kann mithilfe eines der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Tools ausgeführt werden. Weitere Informationen zu den Tools finden Sie unter [Power Pivot-Konfigurationstools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
> [!IMPORTANT]  
>  Für eine SharePoint 2010-Farm muss SharePoint 2010 SP1 installiert sein, bevor Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint oder eine SharePoint-Farm konfigurieren können, die einen [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Datenbankserver verwendet. Wenn Sie das Service Pack noch nicht installiert haben, installieren Sie es, bevor Sie mit der Serverkonfiguration beginnen.  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-powershell"></a>Vorteile der Konfiguration von PowerPivot für SharePoint mithilfe von PowerShell  
 Sie können Windows PowerShell-Skriptdateien (.ps1) erstellen, um Konfigurationstasks zu automatisieren. Dieser Ansatz wird empfohlen, wenn Sie skriptbasierte Installation und Konfigurationsschritte benötigen, die Sie auf jedem Server ausführen können. Sie benötigen ein solches Skript möglicherweise als Teil eines Notfallwiederherstellungsplans zum Neuerstellen eines Servers im Fall eines Hardwarefehlers.  
  
## <a name="view-a-list-of-the-power-pivot-cmdlets-on-a-server"></a>Anzeigen einer Liste der Power Pivot-Cmdlets auf einem Server  
 Inhalte und Beispiele zu den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Cmdlets finden Sie unter [PowerShell-Referenz für PowerPivot für SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md).  
  
 So zeigen Sie mithilfe von PowerShell eine Liste der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Cmdlets an:  
  
1.  Öffnen Sie die SharePoint-Verwaltungsshell unter Verwendung der Option **Als Administrator ausführen** .  
  
2.  Geben Sie den folgenden Befehl ein:  
  
    ```  
    Get-help *powerpivot*  
    ```  
  
     Eine Liste von Cmdlets sollte angezeigt werden, die im Cmdlet-Namen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] enthalten. Beispiel: `Get-PowerPivotServiceApplication`. Wie viele Cmdlets verfügbar sind, hängt von der verwendeten Analysis Services-Version ab.  
  
    -   10 Cmdlets mit SQL Server 2012 SP1 Analysis Services-Server, der im SharePoint-Modus konfiguriert ist, und SharePoint 2013. Die 2012 SP1-Version verwendet eine neue Architektur, die die Ausführung des Analysis-Servers außerhalb der SharePoint-Farm zulässt und weniger Windows PowerShell-Cmdlets für die Verwaltung erfordert.  
  
    -   17 Cmdlets mit SQL Server 2012 Analysis Services-Server, der im SharePoint-Modus konfiguriert ist, und SharePoint 2010.  
  
     Wenn keine Befehle in der Liste zurückgegeben werden oder eine ähnliche Fehlermeldung wie „`get-help could not find *powerpivot* in a help file in this session.`“ angezeigt wird, finden Sie im nächsten Abschnitt dieses Themas Anweisungen dazu, wie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Cmdlets auf dem Server aktiviert werden.  
  
     Alle Cmdlets verfügen über eine Onlinehilfe. Im folgenden Beispiel wird dargestellt, wie die Onlinehilfe für das Cmdlet **New-PowerPivotServiceApplication** angezeigt wird:  
  
    ```  
    Get-help new-powerpivotserviceapplication -full  
    ```  
  
     Oder verwenden Sie die folgende Syntax, um nur die Beispiele anzuzeigen:  
  
    ```  
    Get-help new-powerpivotserviceapplication -example  
    ```  
  
## <a name="enable-power-pivot-cmdlets-on-a-server"></a>Aktivieren von PowerPivot-Cmdlets auf einem Server  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Cmdlets sind verfügbar, nachdem Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint installiert und die Farmlösung bereitgestellt haben. Die Lösungen werden bereitgestellt, wenn Sie das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstool ausführen. Führen Sie folgende Schritte aus, um die Verwendung von Cmdlets zu aktivieren:  
  
1.  Öffnen Sie die SharePoint-Verwaltungsshell unter Verwendung der Option **Als Administrator ausführen** .  
  
2.  Führen Sie das erste Cmdlet aus:  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp”  
    ```  
  
     Das Cmdlet gibt den Namen der Lösung, deren Lösungs-ID und "Deployed=False" zurück. Im nächsten Schritt wird die Lösung bereitgestellt.  
  
3.  Führen Sie das zweite Cmdlet aus, um die Lösung bereitzustellen:  
  
    ```  
    Install-SPSolution –Identity PowerPivotFarm.wsp –GACDeployment -Force  
    ```  
  
4.  Schließen Sie das Fenster. Öffnen Sie es erneut mit der Option **Als Administrator ausführen** .  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Power Pivot-Konfigurationstools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
 [PowerShell-Referenz für PowerPivot für SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)  
  
  
