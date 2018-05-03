---
title: Bereitstellen von PowerPivot-Lösungen in SharePoint | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7fec467c0823d7c2b4649dab307169f0d41de80b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-power-pivot-solutions-to-sharepoint"></a>Bereitstellen von Power Pivot-Lösungen in SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Verwenden Sie die folgenden Anweisungen, um zwei Lösungspakete manuell bereitzustellen, die einer SharePoint Server 2010-Umgebung [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Funktionen hinzufügen. Das Bereitstellen der Lösungen ist ein erforderlicher Schritt für die Konfiguration von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint auf einem SharePoint 2010-Server. Die vollständige Liste der erforderlichen Schritte finden Sie unter [PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
 Sie können die Lösungen auch mithilfe des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstools bereitstellen. Die Verwendung des Konfigurationstools ist für eine einzelne Serverinstallation einfacher und effizienter, aber vielleicht möchten Sie die Zentraladministration und PowerShell verwenden, wenn Sie es vorziehen, mit einem vertrauten Tool zu arbeiten oder wenn Sie mehrere Funktionen gleichzeitig konfigurieren. Weitere Informationen zum Verwenden des Konfigurationstools finden Sie unter [PowerPivot-Konfigurationstools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
 Vor dem Bereitstellen der Lösungen müssen Sie zuerst mithilfe der SQL Server 2012-Installationsmedien [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint installieren. SQL Server-Setup installiert die Lösungspakete, die Sie gleich bereitstellen werden.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Voraussetzung: Überprüfen, ob die Webanwendung den klassischen Authentifizierungsmodus verwendet](#bkmk_classic)  
  
 [Schritt 1: Bereitstellen der Farmlösung](#bkmk_farm)  
  
 [Schritt 2: Bereitstellen der Power Pivot-Webanwendungslösung in der Zentraladministration](#deployCA)  
  
 [Schritt 3: Bereitstellen der Power Pivot-Webanwendungslösung auf anderen Webanwendungen](#deployUI)  
  
 [Erneutes Bereitstellen oder Zurückziehen der Lösung](#retract)  
  
 [Informationen zu den Power Pivot-Lösungen](#intro)  
  
##  <a name="bkmk_classic"></a> Voraussetzung: Überprüfen, ob die Webanwendung den klassischen Authentifizierungsmodus verwendet  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint wird nur für Webanwendungen unterstützt, die den klassischen Authentifizierungsmodus in Windows verwenden. Um zu überprüfen, ob die Anwendung den klassischen Modus verwendet, führen Sie das folgende PowerShell-Cmdlet über die **SharePoint 2010-Verwaltungsshell**, und Ersetzen **http://\<Stammwebsite-Name >** mit der Name der SharePoint-Website:  
  
```  
Get-spwebapplication http://<top-level site name> | format-list UseClaimsAuthentication  
```  
  
 Der Rückgabewert sollte **FALSE**sein. Wenn der Wert **TRUE**ist, kann über diese Webanwendung nicht auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten zugegriffen werden.  
  
##  <a name="bkmk_farm"></a> Schritt 1: Bereitstellen der Farmlösung  
 In diesem Abschnitt erfahren Sie, wie Sie Lösungen mithilfe der PowerShell bereitstellen können. Sie können aber auch das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstool verwenden, um diese Aufgabe abzuschließen. Weitere Informationen finden Sie unter [Konfigurieren oder Reparieren von PowerPivot für SharePoint 2010 (PowerPivot-Konfigurationstool)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Diese Aufgabe muss nur einmal ausgeführt werden, nachdem Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint installiert haben.  
  
1.  Öffnen Sie auf einem Server mit einer Installation von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint mithilfe der Option **Als Administrator ausführen** eine SharePoint 2010-Verwaltungsshell.  
  
2.  Führen Sie das folgende Cmdlet aus, um die Farmlösung hinzuzufügen.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp”  
    ```  
  
     Das Cmdlet gibt den Namen der Lösung, deren Lösungs-ID und "Deployed=False" zurück. Im nächsten Schritt wird die Lösung bereitgestellt.  
  
3.  Führen Sie das nächste Cmdlet aus, um die Farmlösung bereitzustellen:  
  
    ```  
    Install-SPSolution –Identity PowerPivotFarm.wsp –GACDeployment -Force  
    ```  
  
##  <a name="deployCA"></a> Schritt 2: Bereitstellen der Power Pivot-Webanwendungslösung in der Zentraladministration  
 Nach dem Bereitstellen der Farmlösung müssen Sie die Webanwendungslösung in der Zentraladministration bereitstellen. Durch diesen Schritt wird das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard der Zentraladministration hinzugefügt.  
  
1.  Öffnen Sie eine SharePoint 2010-Verwaltungsshell mithilfe der Option **Als Administrator ausführen** .  
  
2.  Führen Sie das nächste Cmdlet aus, um einen Verweis auf die Zentraladministration zu erstellen:  
  
    ```  
    $centralAdmin = $(Get-SPWebApplication -IncludeCentralAdministration | Where { $_.IsAdministrationWebApplication -eq $TRUE})  
    ```  
  
3.  Führen Sie das folgende Cmdlet aus, um die Farmlösung hinzuzufügen.  
  
    ```  
    Add-SPSolution –LiteralPath “C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotWebApp.wsp”  
    ```  
  
     Das Cmdlet gibt den Namen der Lösung, deren Lösungs-ID und "Deployed=False" zurück. Im nächsten Schritt wird die Lösung bereitgestellt.  
  
4.  Führen Sie das nächste Cmdlet aus, um die Webanwendungslösung in der Zentraladministration zu installieren.  
  
    ```  
    Install-SPSolution -Identity PowerPivotWebApp.wsp -GACDeployment -Force -WebApplication $centralAdmin  
    ```  
  
 Da Sie nun die Webanwendungslösung in der Zentraladministration bereitgestellt haben, können Sie mithilfe der Zentraladministration alle verbleibenden Konfigurationsschritte ausführen.  
  
##  <a name="deployUI"></a> Schritt 3: Bereitstellen der Power Pivot-Webanwendungslösung auf anderen Webanwendungen  
 In der vorherigen Aufgabe haben Sie powerpivotwebapp.wsp in der Zentraladministration bereitgestellt. In diesem Abschnitt stellen Sie die Lösung „powerpivotwebapp.wsp“ in jeder vorhandenen Webanwendung bereit, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff unterstützt. Wenn Sie später weitere Webanwendungen hinzufügen, wiederholen Sie unbedingt diesen Schritt für die zusätzlichen Webanwendungen.  
  
1.  Klicken Sie in der Zentraladministration unter Systemeinstellungen auf **Farmlösungen verwalten**.  
  
2.  Klicken Sie auf **powerpivotwebapp.wsp**.  
  
3.  Klicken Sie auf **Lösung bereitstellen**.  
  
4.  Wählen Sie unter **Bereitstellen für**die SharePoint-Webanwendung aus, für die Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Funktionsunterstützung hinzufügen möchten.  
  
5.  Klicken Sie auf **OK**.  
  
6.  Wiederholen Sie die Schritte für andere SharePoint-Webanwendungen, die den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff ebenfalls unterstützen.  
  
##  <a name="retract"></a> Erneutes Bereitstellen oder Zurückziehen der Lösung  
 Obwohl in der SharePoint-Zentraladministration das Zurückziehen der Lösung möglich ist, müssen Sie die Datei powerpivotwebapp.wsp nur entfernen, wenn Sie systematisch ein Installations- oder ein Patchbereitstellungsproblem behandeln.  
  
1.  Klicken Sie in der SharePoint 2010-Zentraladministration in Systemeinstellungen auf **Farmlösungen verwalten**.  
  
2.  Klicken Sie auf **Powerpivotwebapp.wsp**.  
  
3.  Klicken Sie auf **Lösung zurückziehen**.  
  
 Falls Serverbereitstellungsprobleme auftreten, die Sie bis zur Farmlösung zurückverfolgen, können Sie sie über die Option **Reparieren** im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstool erneut bereitstellen. Es empfiehlt sich, Reparaturvorgänge über das Tool auszuführen, da Sie sich dadurch ein paar Schritte ersparen. Weitere Informationen finden Sie unter [Konfigurieren oder Reparieren von PowerPivot für SharePoint 2010 (PowerPivot-Konfigurationstool)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
 Wenn Sie immer noch alle Lösungen erneut bereitstellen möchten, gehen Sie dabei in folgender Reihenfolge vor:  
  
1.  Ziehen Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Webanwendungslösung aus allen SharePoint-Webanwendungen zurück, die sie verwenden.  
  
2.  Ziehen Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aus der Farmlösung zurück.  
  
3.  Stellen Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Farmlösung erneut bereit.  
  
4.  Stellen Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Webanwendungslösung erneut für alle SharePoint-Webanwendungen bereit.  
  
##  <a name="intro"></a> Informationen zu den Power Pivot-Lösungen  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint verwendet zwei Lösungspakete, um Anwendungsseiten und Programmdateien für die Farm und einzelne Webanwendungen bereitzustellen.  
  
-   Die Farmlösung ist global. Sie wird einmal bereitgestellt und ist anschließend für jeden neuen Server mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint automatisch verfügbar, den Sie der Farm später hinzufügen.  
  
-   Die Webanwendungslösung ist anwendungsspezifisch und muss für jede Webanwendung in der Farm bereitgestellt werden, einschließlich der Zentraladministrationswebanwendung.  
  
 Jede Lösung wird unterschiedlich bereitgestellt.  Die Farmlösung wird einmal bereitgestellt, nachdem das erste [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für die SharePoint-Instanz installiert wurde. Verwenden Sie das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstool oder PowerShell-Cmdlets, um die Farmlösung bereitzustellen.  
  
 Die Webanwendungslösung wird anfänglich in der Zentraladministration bereitgestellt. Es folgen weitere Bereitstellungen für alle zusätzlichen Webanwendungen, die Anfragen für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten unterstützen. Sie müssen das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstool oder PowerShell-Cmdlets verwenden, um die Webanwendungslösung in der Zentraladministration bereitzustellen. Für alle anderen Webanwendungen können Sie die Webanwendungslösung manuell bereitstellen, und zwar mithilfe der Zentraladministration oder der PowerShell.  
  
|Lösung|Description|  
|--------------|-----------------|  
|Powerpivotfarm.wsp|Der globalen Assembly wird Microsoft.AnalysisServices.SharePoint.Integration.dll hinzugefügt.<br /><br /> Der globalen Assembly wird Microsoft.AnalysisServices.ChannelTransport.dll hinzugefügt.<br /><br /> Installiert Funktionen sowie Ressourcendateien und registriert Inhaltstypen.<br /><br /> Fügt Bibliotheksvorlagen für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog und Datenfeedbibliotheken hinzu.<br /><br /> Fügt Anwendungsseiten für die Dienstanwendungskonfiguration, das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard, die Datenaktualisierung und den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog hinzu.|  
|powerpivotwebapp.wsp|Fügt dem Ordner für Webservererweiterungen auf dem Web-Front-End Microsoft.AnalysisServices.SharePoint.Integration.dll-Ressourcendateien hinzu.<br /><br /> Fügt dem Web-Front-End den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Webdienst hinzu.<br /><br /> Fügt die Miniaturbildgenerierung für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog hinzu.|  
  
## <a name="see-also"></a>Siehe auch  
 [Upgraden von PowerPivot für SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [PowerPivot-Konfiguration mit Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
  
