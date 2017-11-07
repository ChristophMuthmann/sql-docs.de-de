---
title: "Konfigurieren von PowerPivot und Bereitstellen von Lösungen (SharePoint 2013) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- power-view
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6401fd92-f43b-450e-8298-12db644c25bc
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 901098e2a656d178932b9b706b70d559bef4f215
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="configure-power-pivot-and-deploy-solutions-sharepoint-2013"></a>Konfigurieren von PowerPivot und Bereitstellen von Lösungen (SharePoint 2013)
  In diesen Themen wird beschrieben, wie Erweiterungen der mittleren Ebene für die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Funktionen in [!INCLUDE[SPS2013](../../../includes/sps2013-md.md)] bereitgestellt und konfiguriert werden, z. B. [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Katalog, planmäßige Datenaktualisierung, Management-Dashboard und Datenanbieter. Führen Sie das **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2013-Konfigurationstool** aus, um folgende Aufgaben auszuführen:  
  
-   Bereitstellen von SharePoint-Lösungsdateien  
  
-   Erstellen einer [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Dienstanwendung  
  
-   Konfigurieren einer Excel Services-Anwendung für die Verwendung eines [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Servers im SharePoint-Modus Informationen zu Back-End-Diensten und zum Installieren eines [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Servers im SharePoint-Modus finden Sie unter [Installieren von Analysis Services im PowerPivot-Modus](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 Weitere Informationen zur Installation des [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2013-Konfigurationstools finden Sie unter [Installieren oder Deinstallieren des Power Pivot für SharePoint-Add-In &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Ausführen der Konfiguration von PowerPivot für SharePoint 2013](#bkmk_run_configuration_tool)  
  
 [Überprüfen der PowerPivot-Konfiguration](#bkmk_verify_powerpivot)  
  
 [Problembehandlung](#bkmk_troubleshoot_issues)  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013|  
  
##  <a name="bkmk_run_configuration_tool"></a> Ausführen der Konfiguration von PowerPivot für SharePoint 2013  
 **Hinweis:** Vom Setup-Assistenten für [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] werden zwei unterschiedliche Konfigurationstools für [!INCLUDE[ssGeminiLong](../../../includes/ssgeminilong-md.md)]installiert. Jedes Tool unterstützt eine andere SharePoint-Version.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2013-Konfigurationstool|SharePoint 2013|  
|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Konfigurationstool|SharePoint 2010 mit SharePoint 2010 Service Pack 1 (SP1)|  
  
 **Hinweis:** Die folgenden Schritte können nur von einem Farmadministrator ausgeführt werden. Angenommen, eine Fehlermeldung mit etwa folgendem Wortlaut wird ausgegeben:  
  
-   "Der Benutzer ist kein Farmadministrator. Beheben Sie die Überprüfungsfehler, und wiederholen Sie den Vorgang."  
  
 Melden Sie sich entweder mit dem Konto an, unter dem SharePoint installiert wurde, oder konfigurieren Sie das Setupkonto als primären Administrator der Website für die SharePoint-Zentraladministration.  
  
1.  Klicken Sie im Menü **Start** auf **Alle Programme**, und klicken Sie dann auf [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Konfigurationstools**und auf **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Konfiguration von**für SharePoint 2013. Das Tool wird nur aufgeführt, wenn [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint auf dem lokalen Server installiert ist.  
  
2.  Klicken Sie auf **Konfigurieren oder reparieren[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint**, und klicken Sie dann auf **OK**.  
  
3.  Mithilfe des Tools wird der aktuelle Status von [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] überprüft und ermittelt, welche Schritte zum Abschließen der Konfiguration erforderlich sind. Erweitern Sie das Fenster auf Vollbildgröße. Am unteren Rand des Fensters wird eine Schaltflächenleiste angezeigt, die die Befehle **Überprüfen**, **Ausführen**und **Beenden** enthält.  
  
4.  Registerkarte **Parameter** :  
  
    1.  **Benutzername für Standardkonto**: Geben Sie ein Domänenbenutzerkonto für das Standardkonto ein. Dieses Konto wird verwendet, um Dienste bereitzustellen, einschließlich des [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Dienstanwendungspools. Geben Sie kein integriertes Konto wie Network Service oder Local System an. Das Tool blockiert Konfigurationen, bei denen integrierte Konten angegeben werden.  
  
    2.  **Datenbankserver**: Sie können das für die SharePoint-Farm unterstützte SQL Server-Datenbankmodul verwenden.  
  
    3.  **Passphrase**. Geben Sie eine Passphrase ein. Wenn Sie eine neue SharePoint-Farm erstellen, wird die Passphrase immer dann verwendet, wenn Sie der SharePoint-Farm einen Server oder eine Anwendung hinzufügen. Wenn die Farm bereits vorhanden ist, geben Sie die Passphrase ein, die Ihnen ermöglicht, der Farm eine Serveranwendung hinzuzufügen.  
  
    4.  **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Server für Excel Services**: Geben Sie den Namen eines [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Servers im SharePoint-Modus ein. Bei einer Bereitstellung auf einem einzelnen Server entspricht dieser dem Datenbankserver. `[ServerName]\powerpivot`  
  
    5.  Klicken Sie im linken Fenster auf **Websitesammlung erstellen** . Notieren Sie sich die **Website-URL** , damit Sie sie später zur Hand haben. Wenn der SharePoint-Server noch nicht konfiguriert ist, verwendet der Konfigurations-Assistent für die URL der Webanwendung und Websitesammlung standardmäßig den Stamm von `http://[ServerName]`. Um die Standardeinstellungen zu ändern, überprüfen Sie die folgenden Seiten im linken Fenster: **Standardwebanwendung erstellen** und **Webanwendungslösung bereitstellen**  
  
5.  Überprüfen Sie optional die verbleibenden Eingabewerte, die zum Abschließen der jeweiligen Aktion verwendet werden. Klicken Sie im linken Fenster auf die einzelnen Aktionen, um die Details zur Aktion anzuzeigen und zu überprüfen. Weitere Informationen über die einzelnen Aktionen finden Sie im Abschnitt „Eingabewerte für die Serverkonfiguration“ im Artikel [Konfigurieren oder Reparieren von PowerPivot für SharePoint 2010 (PowerPivot-Konfigurationstool)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046) in diesem Thema.  
  
6.  Entfernen Sie optional alle Aktionen, die Sie zu dieser Zeit nicht verarbeiten wollen. Wenn Sie z. B. Secure Store Service später konfigurieren möchten, klicken Sie auf **Secure Store Service konfigurieren**, und deaktivieren Sie dann das Kontrollkästchen **Diese Aktion in Taskliste einschließen**.  
  
7.  Klicken Sie auf **Überprüfen** , um zu überprüfen, ob das Tool genügend Informationen hat, um die Aktionen in der Liste zu verarbeiten. Wenn Überprüfungsfehler auftreten, klicken Sie auf die Warnungen im linken Bereich, um Details zum Überprüfungsfehler anzuzeigen. Korrigieren Sie alle Überprüfungsfehler, und klicken Sie dann erneut auf **Überprüfen** .  
  
8.  Klicken Sie auf **Ausführen** , um alle Aktionen in der Aufgabenliste zu verarbeiten. Beachten Sie, dass **Ausführen** verfügbar wird, nachdem Sie die Aktionen überprüft haben. Wenn **Ausführen** nicht aktiviert ist, klicken Sie zuerst auf **Überprüfen** .  
  
 Weitere Informationen finden Sie unter [Konfigurieren oder Reparieren von Power Pivot für SharePoint 2010 (Power Pivot-Konfigurationstool)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
##  <a name="bkmk_verify_powerpivot"></a> Überprüfen der PowerPivot-Konfiguration  
 **Dienste:**  
  
1.  Klicken Sie in der Zentraladministration unter Systemeinstellungen auf **Dienste auf dem Server verwalten**.  
  
2.  Überprüfen Sie, ob **SQL Server Analysis Services** und **SQL Server [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] System Service** gestartet wurden.  
  
 **Farmfunktion:**  
  
1.  Klicken Sie in der Zentraladministration unter Systemeinstellungen auf **Farmfunktionen verwalten**.  
  
2.  Überprüfen Sie, ob die **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Integrationsfunktion** auf **Aktiv**festgelegt ist.  
  
 **Websitesammlungsfunktion:**  
  
1.  Navigieren Sie zu der vom Konfigurationstool erstellten Website-URL.  
  
     Klicken Sie auf **Einstellungen**![SharePoint Einstellungen](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Einstellungen"), und klicken Sie dann auf **Standorteinstellungen**.  
  
     Klicken Sie auf **Websitesammlungs-Features**.  
  
2.  Stellen Sie sicher, dass die **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Integration für Websitesammlungen** auf **Aktiv**festgelegt ist.  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Dienstanwendung:**  
  
1.  Klicken Sie in der Zentraladministration unter **Anwendungsverwaltung**auf **Dienstanwendungen verwalten**.  
  
2.  Vergewissern Sie sich, dass der Status der Dienstanwendung **Gestartet**lautet. Der Standardname lautet **Standard-[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Dienstanwendung**.  
  
     Klicken Sie auf den Namen der Dienstanwendung, um das [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Management-Dashboard für die Dienstanwendung zu öffnen. Bei seiner ersten Verwendung dauert das Laden des Dashboards einige Minuten.  
  
 Weitere Informationen finden Sie unter [Überprüfen einer Power Pivot für SharePoint-Installation](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_troubleshoot_issues"></a> Problembehandlung  
 Um Unterstützung bei der Problembehandlung zu erhalten, empfiehlt es sich, die Diagnoseprotokollierung zu aktivieren.  
  
1.  Klicken Sie in der SharePoint-Zentraladministration auf **Überwachung** und dann auf **Verwendungs- und Integritätsdatenerfassung konfigurieren**.  
  
2.  Achten Sie darauf, dass **Verwendungsdatenerfassung aktivieren** ausgewählt ist.  
  
3.  Überprüfen Sie, ob die folgenden Ereignisse ausgewählt sind:  
  
    -   Definition der Verwendungsfelder für Schulungstelemetrie  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Verbindungen  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Verwendung von Datenladevorgängen  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Verwendung von -Abfragen  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Verwendung von -Datenentladevorgängen  
  
4.  Achten Sie darauf, dass **Integritätsdatenerfassung aktivieren** ausgewählt ist.  
  
5.  Klicken Sie auf **OK**.  
  
 Weitere Informationen zur Problembehandlung bei der Datenaktualisierung finden Sie unter [Problembehandlung bei der Power Pivot-Datenaktualisierung](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 Weitere Informationen zum Konfigurationstool finden Sie unter [PowerPivot-Konfigurationstools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  

