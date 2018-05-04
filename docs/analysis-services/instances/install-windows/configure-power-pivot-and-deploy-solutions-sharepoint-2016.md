---
title: Konfigurieren von PowerPivot und Bereitstellen von Lösungen (SharePoint 2016) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 384f1fdec5b77dcc980954e72fe5bfa07f617601
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-power-pivot-and-deploy-solutions-sharepoint-2016"></a>Konfigurieren von Power Pivot und Bereitstellen von Lösungen (SharePoint 2016)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  In diesem Thema wird beschrieben, wie Erweiterungen der mittleren Ebene für die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Funktionen in [!INCLUDE[SPS2016](../../../includes/sps2016-md.md)] bereitgestellt und konfiguriert werden, z.B. den [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Katalog, die planmäßige Datenaktualisierung, das Management-Dashboard und Datenanbieter. Führen Sie das **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2016-Konfigurationstool** aus, um folgende Aufgaben auszuführen:  
  
-   Bereitstellen von SharePoint-Lösungsdateien  
  
-   Erstellen einer [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Dienstanwendung  
  
-   Informationen zu Back-End-Diensten und zum Installieren eines [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Servers im [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Modus finden Sie unter [Installieren von Analysis Services im PowerPivot-Modus](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 Informationen zum Installieren der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] SharePoint 2016-Konfigurationstools finden Sie unter [installieren oder Deinstallieren des PowerPivot für SharePoint-Add-in (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md).  
  
##  <a name="bkmk_run_configuration_tool"></a> Ausführen von Power Pivot für die Konfiguration von SharePoint 2016  
 **Hinweis:** Die folgenden Schritte können nur von einem Farmadministrator ausgeführt werden. Angenommen, eine Fehlermeldung mit etwa folgendem Wortlaut wird ausgegeben:  
  
-   "Der Benutzer ist kein Farmadministrator. Beheben Sie die Überprüfungsfehler, und wiederholen Sie den Vorgang."  
  
 Melden Sie sich entweder mit dem Konto an, unter dem SharePoint installiert wurde, oder konfigurieren Sie das Setupkonto als primären Administrator der Website für die SharePoint-Zentraladministration.  
  
1.  Wählen Sie im **Startmenü** **Alle Programme**aus, und wählen Sie anschließend [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]aus. Wählen Sie dann **Konfigurationstools**und anschließend **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2016**aus. Das Tool wird nur aufgeführt, wenn [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint auf dem lokalen Server installiert ist.  
  
2.  Wählen Sie **konfigurieren oder reparieren [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint** und wählen Sie dann **OK**.  
  
3.  Mithilfe des Tools wird der aktuelle Status von [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] überprüft und ermittelt, welche Schritte zum Abschließen der Konfiguration erforderlich sind. Erweitern Sie das Fenster auf Vollbildgröße. Am unteren Rand des Fensters wird eine Schaltflächenleiste angezeigt, die die Befehle **Überprüfen**, **Ausführen**und **Beenden** enthält.  
  
4.  Registerkarte **Parameter** :  
  
    1.  **Benutzername für Standardkonto**: Geben Sie ein Domänenbenutzerkonto für das Standardkonto ein. Dieses Konto wird verwendet, um Dienste bereitzustellen, einschließlich des [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Dienstanwendungspools. Geben Sie kein integriertes Konto wie Network Service oder Local System an. Das Tool blockiert Konfigurationen, bei denen integrierte Konten angegeben werden.  
  
    2.  **Datenbankserver**: Sie können das für die SharePoint-Farm unterstützte SQL Server-Datenbankmodul verwenden.  
  
    3.  **Passphrase**. Geben Sie eine Passphrase ein. Wenn Sie eine neue SharePoint-Farm erstellen, wird die Passphrase immer dann verwendet, wenn Sie der SharePoint-Farm einen Server oder eine Anwendung hinzufügen. Wenn die Farm bereits vorhanden ist, geben Sie die Passphrase ein, die Ihnen ermöglicht, der Farm eine Serveranwendung hinzuzufügen.  
  
    4.  Klicken Sie im linken Fenster auf **Websitesammlung erstellen** . Notieren Sie sich die **Website-URL** , damit Sie sie später zur Hand haben. Wenn der SharePoint-Server noch nicht konfiguriert ist, verwendet der Konfigurations-Assistent für die URL der Webanwendung und Websitesammlung standardmäßig den Stamm von `http://[ServerName]`. Um die Standardeinstellungen zu ändern, überprüfen Sie die folgenden Seiten im linken Fenster: **Standardwebanwendung erstellen** und **Webanwendungslösung bereitstellen**  
  
5.  Überprüfen Sie optional die verbleibenden Eingabewerte, die zum Abschließen der jeweiligen Aktion verwendet werden. Klicken Sie im linken Fenster auf die einzelnen Aktionen, um die Details zur Aktion anzuzeigen und zu überprüfen. Weitere Informationen über die einzelnen Aktionen finden Sie im Abschnitt „Eingabewerte für die Serverkonfiguration“ im Artikel [Konfigurieren oder Reparieren von PowerPivot für SharePoint 2010 (PowerPivot-Konfigurationstool)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046) in diesem Thema.  
  
6.  Entfernen Sie optional alle Aktionen, die Sie zu dieser Zeit nicht verarbeiten wollen. Wenn Sie z.B. das einmalige Anmelden später konfigurieren möchten, wählen Sie **Einmaliges Anmelden konfigurieren**aus, und deaktivieren Sie anschließend das Kontrollkästchen **Diese Aktion in Taskliste einschließen**.  
  
7.  Wählen Sie **Überprüfen** aus, um zu überprüfen, ob das Tool genügend Informationen zum Verarbeiten der Aktionen in der Liste hat. Wenn Überprüfungsfehler auftreten, klicken Sie auf die Warnungen im linken Bereich, um Details zum Überprüfungsfehler anzuzeigen. Korrigieren Sie alle Überprüfungsfehler, und wählen Sie anschließend erneut **Überprüfen** aus.  
  
8.  Wählen Sie **Ausführen** aus, um alle Aktionen in der Aufgabenliste zu verarbeiten. Beachten Sie, dass **Ausführen** verfügbar wird, nachdem Sie die Aktionen überprüft haben. Wenn **Ausführen** nicht aktiviert ist, wählen Sie zuerst **Überprüfen** aus.  
  
 Weitere Informationen finden Sie unter [Konfigurieren oder Reparieren von PowerPivot für SharePoint 2010 (PowerPivot-Konfigurationstool)](http://msdn.microsoft.com/en-us/d61f49c5-efaa-4455-98f2-8c293fa50046).  
  
##  <a name="bkmk_verify_powerpivot"></a> Überprüfen der PowerPivot-Konfiguration  
 **Dienste:**  
  
1.  Wählen Sie in der Zentraladministration unter „Systemeinstellungen“ **Dienste auf dem Server verwalten**aus.  
  
2.  Überprüfen Sie, ob **SQL Server [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Systemdienst** gestartet wird.  
  
 **Farmfunktion:**  
  
1.  Wählen Sie in der Zentraladministration unter „Systemeinstellungen“ **Farmfunktionen verwalten**aus.  
  
2.  Überprüfen Sie, ob die **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Integration** **Aktiv**ist.  
  
 **Websitesammlungsfunktion:**  
  
1.  Navigieren Sie zu der vom Konfigurationstool erstellten Website-URL.  
  
     Wählen Sie **Einstellungen**![SharePoint Einstellungen](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Einstellungen"), und klicken Sie dann auf **Standorteinstellungen**.  
  
     Wählen Sie **Websitesammlungsfeatures**aus.  
  
2.  Stellen Sie sicher, dass die **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Integration für Websitesammlungen** auf **Aktiv**festgelegt ist.  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Dienstanwendung:**  
  
1.  Wählen Sie in der Zentraladministration unter **Anwendungsverwaltung** **Dienstanwendungen verwalten**aus.  
  
2.  Vergewissern Sie sich, dass der Status der Dienstanwendung **Gestartet**lautet. Der Standardname lautet **Standard-[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Dienstanwendung**.  
  
     Wählen Sie den Namen der Dienstanwendung aus, um das [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Management-Dashboard für die Dienstanwendung zu öffnen. Bei seiner ersten Verwendung dauert das Laden des Dashboards einige Minuten.  
  
 Weitere Informationen finden Sie unter [Überprüfen einer Power Pivot für SharePoint-Installation](../../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).  
  
##  <a name="bkmk_troubleshoot_issues"></a> Problembehandlung  
 Um Unterstützung bei der Problembehandlung zu erhalten, empfiehlt es sich, die Diagnoseprotokollierung zu aktivieren.  
  
1.  Klicken Sie in der SharePoint-Zentraladministration auf **Überwachung** , und wählen Sie anschließend **Verwendungs- und Integritätsdatenerfassung konfigurieren**aus.  
  
2.  Achten Sie darauf, dass **Verwendungsdatenerfassung aktivieren** ausgewählt ist.  
  
3.  Überprüfen Sie, ob die folgenden Ereignisse ausgewählt sind:  
  
    -   Definition der Verwendungsfelder für Schulungstelemetrie  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Verbindungen  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Verwendung von -Datenladevorgängen  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Verwendung von -Abfragen  
  
    -   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Verwendung von -Datenentladevorgängen  
  
4.  Achten Sie darauf, dass **Integritätsdatenerfassung aktivieren** ausgewählt ist.  
  
5.  Wählen Sie **OK**.  
  
 Weitere Informationen zu datenaktualisierung, finden Sie unter [Problembehandlung Power Pivot-Datenaktualisierung](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx) (http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 Weitere Informationen zum Konfigurationstool finden Sie unter [PowerPivot-Konfigurationstools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
  
