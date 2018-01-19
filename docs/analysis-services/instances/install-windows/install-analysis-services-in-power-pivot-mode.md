---
title: Installieren von Analysis Services im PowerPivot-Modus | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- setup-install
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7528721b65101ee32285d57f18f93f98eeec9dae
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="install-analysis-services-in-power-pivot-mode"></a>Installieren von Analysis Services im PowerPivot-Modus
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Die Verfahren in diesem Thema führen Sie durch die Installation eines einzelnen Servers eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Server in [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Modus für eine SharePoint-Bereitstellung. In den Schritten führen Sie u. a. den Installations-Assistenten für SQL Server sowie Konfigurationsaufgaben unter Verwendung der SharePoint-Zentraladministration aus.  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2016 &#124; SharePoint 2013|  
  
 **In diesem Thema:**  
  
 [Hintergrund](#bkmk_background)  
  
 [Erforderliche Komponenten](#bkmk_prereq)  
  
 [Schritt 1: Installieren von PowerPivot für SharePoint](#InstallSQL)  
  
 [Schritt 2: Konfigurieren einer grundlegenden Analysis Services-SharePoint-Integration](#bkmk_config)  
  
 [Schritt 3: Überprüfen der Integration](#bkmk_verify)  
  
 [Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](#bkmk_firewall)  
  
 [Aktualisieren von Arbeitsmappen und geplanter Datenaktualisierung](#bkmk_upgrade_workbook)  
  
 [Über die Installation auf einem einzelnen Server hinausgehend – PowerPivot für Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="bkmk_background"></a> Hintergrund  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint umfasst Dienste der mittleren Ebene sowie Back-End-Dienste, die den [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Datenzugriff in einer SharePoint 2016- oder einer SharePoint 2013-Farm ermöglichen.  
  
-   **Back-End-Dienste:** Falls Sie [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für Excel zum Erstellen von Arbeitsmappen mit analytischen Daten verwenden, benötigen Sie [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint, um in einer Serverumgebung auf diese Daten zuzugreifen. Sie können [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup auf einem Computer ausführen, auf dem SharePoint Server installiert ist, oder auf einem anderen Computer, der über keine SharePoint-Software verfügt. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] und SharePoint bestehen keine Abhängigkeiten.  
  
     **Hinweis:** In diesem Thema wird die Installation des [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Servers und der Back-End-Dienste beschrieben.  
  
-   **Mittlere Ebene:** Erweiterungen zu den [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Erfahrungen in SharePoint, einschließlich des [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Katalogs, der planmäßigen Datenaktualisierung, des Management-Dashboards und Datenanbietern. Weitere Informationen zur Installation und Konfiguration der mittleren Ebene finden Sie unter:  
  
    -   [Installieren oder Deinstallieren des „Power Pivot für SharePoint“-Add-In (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
    -   [Installieren oder Deinstallieren des PowerPivot für SharePoint-Add-Ins &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [Konfigurieren von PowerPivot und Bereitstellen von Lösungen &#40;SharePoint 2016&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2016.md)  
  
    -   [Konfigurieren von PowerPivot und Bereitstellen von Lösungen &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> Erforderliche Komponenten  
  
1.  Sie müssen lokaler Administrator sein, um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup auszuführen.  
  
2.  SharePoint Server Enterprise Edition wird für [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint benötigt. Sie können auch die Evaluation Enterprise Edition verwenden.  
  
3.  Der Computer muss einer Domäne in derselben Active Directory-Gesamtstruktur wie Office Online Server (SharePoint 2016) oder Excel Services (SharePoint 2013) beitreten.  
  
4.  Der Name der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Instanz muss verfügbar sein. Der Computer, auf dem Sie Analysis Services im [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Modus installieren, darf keine benannte [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Instanz enthalten.  
  
     **Hinweis:** Der Instanzname muss POWERPIVOT lauten.  
  
5.  Lesen Sie die [Hardware- und Softwareanforderungen für Analysis Services-Server im SharePoint-Modus](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
6.  Informieren Sie sich über die Anmerkungen zu dieser Version unter [SQL Server 2016 Release Notes](../../../sql-server/sql-server-2016-release-notes.md).  
  
###  <a name="bkmk_sqleditions"></a> Anforderungen für die SQL Server-Edition  
 Nicht alle Business Intelligence-Funktionen sind in allen Editionen von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]verfügbar. Weitere Informationen finden Sie unter [von den SQL Server 2016-Editionen unterstützte Analysis Services Funktionen](../../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) und [Editionen und Komponenten von SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
##  <a name="InstallSQL"></a> Schritt 1: Installieren von PowerPivot für SharePoint  
 In diesem Schritt führen Sie das SQL Server-Setup aus, um einen [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Server im [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Modus zu installieren. In einem anschließenden Schritt konfigurieren Sie Excel Services so, dass dieser Server für Arbeitsmappen-Datenmodelle verwendet wird.  
  
1.  Führen Sie den Installations-Assistenten für SQL Server (Setup.exe) aus.  
  
2.  Wählen Sie im linken Navigationsbereich **Installation** aus.  
  
3.  Wählen Sie **Neue eigenständige SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**aus.  
  
4.  Wenn die Seite **Product Key** angezeigt wird, geben Sie die Evaluation Edition an, oder geben Sie einen Product Key für eine lizenzierte Kopie der Enterprise Edition ein. Wählen Sie **Weiter**aus. Weitere Informationen zu den Editionen finden Sie unter [Editions and Components of SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
5.  Lesen und akzeptieren Sie die Microsoft-Software-Lizenzbedingungen, und klicken Sie dann auf **Weiter**.  
  
6.  Wenn die Seite **Globale Regeln** geöffnet wird, lesen Sie alle Regelinformationen, die vom Setup-Assistenten angezeigt werden.  
  
7.  Auf der Seite **Microsoft Update** sollten Sie mithilfe von Microsoft Update nach Updates suchen und dann **Weiter**auswählen.  
  
8.  Die Seite **Setupdateien installieren** wird mehrere Minuten lang ausgeführt. Überprüfen Sie alle Regelwarnungen oder fehlerhaften Regeln, und wählen Sie dann **Weiter**aus.  
  
9. Wenn erneut die **Setupunterstützungsregeln**angezeigt werden, überprüfen Sie alle Warnungen, und wählen Sie **Weiter**aus.  
  
     **Hinweis:** Da die Windows-Firewall aktiviert ist, werden Sie davor gewarnt, Ports zu öffnen, um den Remotezugriff zu ermöglichen.  
  
10. Wählen Sie auf der Seite **Setuprolle** die Option **SQL Server-Funktionsinstallation**aus.  
  
     Wählen Sie **Weiter**aus.  
  
11. Wählen Sie auf der Seite „Funktionsauswahl“ **Analysis Services**aus. Mit dieser Option können Sie einen der drei [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Modi installieren. Sie wählen den Modus in einem späteren Schritt aus. Wählen Sie **Weiter**aus.  
  
12. Wählen Sie auf der Seite **Instanzkonfiguration** **Benannte Instanz** aus, geben Sie **POWERPIVOT** als Instanznamen ein, und klicken Sie auf **Weiter**.  
  
     ![SQL-Setup - Landing Page Instanzkonfiguration](../../../analysis-services/instances/install-windows/media/sql2016-pp-instance-config-landing-page.png "SQL-Setup - Landing Page Instanzkonfiguration")  
  
13. Legen Sie alle Dienste auf der Seite **Serverkonfiguration** auf den **Starttyp**"Automatisch" fest. Geben Sie das gewünschte Domänenkonto und Kennwort für **SQL Server Analysis Services**an, **(1)** im folgenden Diagramm.  
  
    -   Für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]können Sie ein **Domänenbenutzerkonto** oder ein **NetworkService-Konto** verwenden. Das LocalSystem- oder LocalService-Konto sollte nicht verwendet werden.  
  
    -   Wenn Sie das SQL Server-Datenbankmodul und den SQL Server-Agent hinzugefügt haben, können Sie die Dienste zur Ausführung unter Domänenbenutzerkonten oder unter dem standardmäßigen virtuellen Konto konfigurieren.  
  
    -   Stellen Sie niemals Dienstkonten unter Ihrem eigenen Domänenbenutzerkonto bereit. Dies gewährt dem Server die gleichen Berechtigungen, über die Sie für die Ressourcen im Netzwerk verfügen. Wenn der Server von einem böswilligen Benutzer angegriffen wird, wird dieser Benutzer mit Ihren Domänenanmeldeinformationen angemeldet. Der Benutzer ist dann berechtigt, die gleichen Daten und Anwendungen herunterzuladen und zu verwenden wie Sie.  
  
     Wählen Sie **Weiter**aus.  
  
     ![Setup für SQL - Serverkonfiguration Angebotsseite](../../../analysis-services/instances/install-windows/media/sql2016-pp-server-config-landing-page.png "Setup für SQL - Serverkonfiguration-Angebotsseite")  
  
14. Wenn Sie das [!INCLUDE[ssDE](../../../includes/ssde-md.md)]installieren, wird die Seite **Datenbankmodulkonfiguration** angezeigt. Wählen Sie in der [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Konfiguration **Aktuellen Benutzer hinzufügen** aus, um Ihrem Benutzerkonto Administratorberechtigungen für die Datenbankmodulinstanz zu gewähren.  
  
     Wählen Sie **Weiter**aus.  
  
15. Wählen Sie auf der Seite **Analysis Services-Konfiguration** unter **Servermodus**  **PowerPivot-Modus**aus  
  
     ![SQL-Setup – Analysis Services-Konfiguration Landing Page](../../../analysis-services/instances/install-windows/media/sql2016-pp-as-config-landing-page.png "SQL-Setup - Landing Page Analysis Services-Konfiguration")  
  
16. Wählen Sie auf der Seite **Analysis Services-Konfiguration** **Aktuellen Benutzer hinzufügen** aus, um Ihrem Benutzerkonto Administratorberechtigungen zu gewähren. Sie benötigen die Administratorberechtigung, um den Server nach Abschluss von Setup zu konfigurieren.  
  
    -   Fügen Sie auf der gleichen Seite das Windows-Benutzerkonto einer Person hinzu, die ebenfalls Administratorberechtigungen benötigt. Beispielsweise muss jeder Benutzer, der in [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] eine Verbindung mit der [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] -Instanz herstellen möchte, um Datenbankverbindungsprobleme zu beheben, über Systemadministratorberechtigungen verfügen. Fügen Sie das Benutzerkonto einer Person hinzu, die möglicherweise jetzt die Problembehandlung oder Verwaltung des Servers ausführen möchte.  
  
    -   > [!NOTE]  
        >  Alle Dienstanwendungen, die Zugriff auf die Analysis Services-Serverinstanz erfordern, müssen über Analysis Services-Administratorberechtigungen verfügen. Fügen Sie z. B. die Dienstkonten für Excel Services, Power View und PerformancePoint-Dienste hinzu. Fügen Sie zusätzlich das SharePoint-Farmkonto hinzu, das als Identität der Webanwendung verwendet wird, von der die Zentraladministration gehostet wird.  
  
     Wählen Sie **Weiter**aus.  
  
17. Wählen Sie auf der Seite **Fehlerberichterstellung** **Weiter**aus.  
  
18. Wählen Sie auf der Seite **Installationsbereit** **Installieren**aus.  
  
19. Wenn das Dialogfeld **Computerneustart erforderlich**angezeigt wird, wählen Sie **OK**aus.  
  
20. Wenn die Installation abgeschlossen ist, wählen Sie **Schließen**aus.  
  
21. Starten Sie den Computer neu.  
  
22. Wenn in Ihrer Umgebung eine Firewall verwendet wird, informieren Sie sich im Thema [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)der SQL Server-Onlinedokumentation.  
  
### <a name="verify-the-sql-server-installation"></a>Überprüfen der SQL Server-Installation  
 Vergewissern Sie sich, dass der Analysis Services-Dienst ausgeführt wird.  
  
1.  Klicken Sie in Microsoft Windows auf **Start**, wählen Sie **Alle Programme**und dann die Gruppe **Microsoft SQL Server 2016** aus.  
  
2.  Wählen Sie **SQL Server Management Studio**aus.  
  
3.  Stellen Sie eine Verbindung mit der Analysis Services-Instanz her, beispielsweise **[Servername]\POWERPIVOT**. Wenn Sie eine Verbindung mit der Instanz herstellen können, ist sichergestellt, dass der Dienst ausgeführt wird.  
  
##  <a name="bkmk_config"></a> Schritt 2: Konfigurieren einer grundlegenden Analysis Services-SharePoint-Integration  
 In den folgenden Schritten werden die erforderlichen Konfigurationsänderungen beschrieben, die die Interaktion mit erweiterten Excel-Datenmodellen innerhalb einer SharePoint-Dokumentbibliothek ermöglichen. Führen Sie diese Schritte nach der Installation von SharePoint Server und SQL Server Analysis Services aus.  
  
### <a name="sharepoint-2016"></a>SharePoint 2016  
 Excel Services wurde aus SharePoint 2016 entfernt. Stattdessen wird Office Online Server zum Hosten von Excel verwendet.  
  
#### <a name="grant-office-online-server-machine-account-administration-rights-on-analysis-services"></a>Gewähren von Administratorrechten in Analysis Services für Office Online Server-Computerkonto  
 Die in diesem Abschnitt beschriebenen Schritte müssen nicht ausgeführt werden, wenn Sie das Office Online Server-Computerkonto während der Analysis Services-Installation als Analysis Services-Administrator hinzugefügt haben.  
  
1.  Starten Sie auf dem Analysis Services-Server die Anwendung SQL Server Management Studio, und stellen Sie eine Verbindung mit der Analysis Services-Instanz her, z. B. `[MyServer]\POWERPIVOT`.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Instanznamen, und wählen Sie **Eigenschaften**aus.  
  
     ![Anzeigen der Eigenschaften eines SSAS-Servers](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "Anzeigen der Eigenschaften eines SSAS-Servers")  
  
3.  Wählen Sie im linken Bereich **Sicherheit**aus. Fügen Sie das Computerkonto hinzu, auf dem Office Online Server installiert ist.  
  
     ![Sicherheitseinstellungen eines SSAS-Servers](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "Sicherheitseinstellungen eines SSAS-Servers")  
  
#### <a name="register-analysis-services-server-with-office-online-server"></a>Registrieren des Analysis Services-Servers bei Office Online Server  
 Führen Sie diese Schritte auf Office Online Server aus.  
  
-   Öffnen Sie als Administrator ein PowerShell-Befehlsfenster.  
  
-   Laden Sie das `OfficeWebApps` -PowerShell-Modul.  
  
     `Import-Module OfficeWebApps`  
  
-   Fügen Sie den Analysis Services-Server hinzu, z.B. `[MyServer]\POWERPIVOT`.  
  
     `New-OfficeWebAppsExcelBIServer -ServerId [MyServer]\POWERPIVOT]`  
  
### <a name="sharepoint-2013"></a>SharePoint 2013  
  
#### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>Gewähren von Excel Services-Serveradministratorrechten für Analysis Services  
 Die in diesem Abschnitt beschriebenen Schritte müssen nicht ausgeführt werden, wenn Sie das Dienstkonto für die Excel Services-Anwendung während der Analysis Services-Installation als Analysis Services-Administrator hinzugefügt haben.  
  
1.  Starten Sie auf dem Analysis Services-Server die Anwendung SQL Server Management Studio, und stellen Sie eine Verbindung mit der Analysis Services-Instanz her, z. B. `[MyServer]\POWERPIVOT`.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Instanznamen, und wählen Sie **Eigenschaften**aus.  
  
     ![Anzeigen der Eigenschaften eines SSAS-Servers](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "Anzeigen der Eigenschaften eines SSAS-Servers")  
  
3.  Wählen Sie im linken Bereich **Sicherheit**aus. Fügen Sie die Domänenanmeldung hinzu, die Sie in Schritt 1 für die Excel Services-Anwendung konfiguriert haben.  
  
     ![Sicherheitseinstellungen eines SSAS-Servers](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "Sicherheitseinstellungen eines SSAS-Servers")  
  
#### <a name="configure-excel-services-for-analysis-services-integration"></a>Konfigurieren von Excel Services für die Analysis Services-Integration  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf den Namen der Dienstanwendung; der Standardname lautet **Excel Services-Anwendung**.  
  
3.  Klicken Sie auf der Seite **Excel Services-Anwendung verwalten**auf **Datenmodelleinstellungen**.  
  
4.  Klicken Sie auf **Server hinzufügen**.  
  
5.  Geben Sie unter **Servername**den Namen des Analysis Services-Servers und der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Instanz ein. Beispiel: `MyServer\POWERPIVOT`. Der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Instanzname wird benötigt.  
  
     Geben Sie eine Beschreibung ein.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Die Änderungen werden innerhalb einiger Minuten wirksam. Alternativ können Sie für den Dienst **Dienste für Excel-Berechnungen** auch auf **Beenden** bzw. **Starten**klicken. Aktion  
  
     Eine andere Möglichkeit besteht darin, eine Eingabeaufforderung unter Verwendung von Administratorprivilegien zu öffnen und `iisreset /noforce`einzugeben.  
  
     Anhand der Einträge im ULS-Protokoll können Sie feststellen, ob der Server von Excel Services erkannt wird. Die Einträge lauten etwa wie folgt:  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> Schritt 3: Überprüfen der Integration  
 In den folgenden Schritten erfahren Sie, wie eine neue Arbeitsmappe erstellt und hochgeladen wird, um zu überprüfen, ob die Analysis Services-Integration erfolgreich war. Sie benötigen für diese Schritte eine SQL Server-Datenbank.  
  
1.  **Hinweis:** Wenn Sie bereits über eine erweiterte Arbeitsmappe mit Slicern oder Filtern verfügen, können Sie sie in die SharePoint-Dokumentbibliothek hochladen und überprüfen, ob Sie in der Lage sind, mit den Slicern und Filtern in der Dokumentbibliotheksansicht zu interagieren.  
  
2.  Starten Sie in Excel eine neue Arbeitsmappe.  
  
3.  Wählen Sie auf der Registerkarte „Daten“ im Menüband in **Externe Daten abrufen** **Aus anderen Quellen**aus.  
  
4.  Wählen Sie **Aus SQL Server**.  
  
5.  Geben Sie im **Datenverbindungs-Assistenten** den Namen der SQL Server-Instanz ein, in der die Datenbank enthalten ist, die Sie verwenden möchten.  
  
6.  Stellen Sie sicher, dass unter „Anmeldeinformationen“ **Windows-Authentifizierung verwenden** ausgewählt ist, und klicken Sie dann auf **Weiter**.  
  
7.  Wählen Sie die Datenbank aus, die Sie verwenden möchten.  
  
8.  Achten Sie darauf, dass das Kontrollkästchen **Mit einer ausgewählten Tabelle verbinden** aktiviert ist.  
  
9. Aktivieren Sie das Kontrollkästchen **Auswahl mehrerer Tabellen aktivieren und Tabellen zum Excel-Datenmodell hinzufügen** .  
  
10. Wählen Sie die Tabellen aus, die Sie importieren möchten.  
  
11. Aktivieren Sie das Kontrollkästchen **Beziehungen zwischen ausgewählten Tabellen importieren**, und wählen Sie dann **Weiter**aus. Durch den Import mehrerer Tabellen aus einer relationalen Datenbank können Sie mit Tabellen arbeiten, die bereits verknüpft sind. Sie sparen Arbeitsschritte, da Sie die Beziehungen nicht manuell erstellen müssen.  
  
12. Geben Sie auf der Assistentenseite **Datenverbindungsdatei speichern und fertig stellen** einen Namen für die Verbindung ein, und wählen Sie **Fertig stellen**aus.  
  
13. Das Dialogfeld **Daten importieren** wird angezeigt. Wählen Sie **PivotTable-Bericht**, und wählen Sie dann **OK**aus.  
  
14. In der Arbeitsmappe wird eine PivotTable-Feldliste angezeigt.   
    Wählen Sie in der Feldliste die Registerkarte **Alle** aus.  
  
15. Fügen Sie den Bereichen Zeile, Spalten und Wert in der Feldliste Felder hinzu.  
  
16. Fügen Sie der PivotTable einen Slicer oder Filter hinzu. **Sie sollten diesen Schritt nicht überspringen**. Mithilfe eines Slicers oder Filters können Sie auf einfache Weise die Analysis Services-Installation überprüfen.  
  
17. Speichern Sie die Arbeitsmappe in einer Dokumentbibliothek in Ihrer SharePoint-Farm. Sie können die Arbeitsmappe auch auf einer Dateifreigabe speichern und dann in die SharePoint-Dokumentbibliothek hochladen.  
  
18. Wählen Sie den Namen der Arbeitsmappe aus, um sie in Excel Online anzuzeigen, und klicken Sie auf den Slicer, oder ändern Sie den Filter, den Sie zuvor hinzugefügt haben. Im Fall eines Datenupdates wissen Sie, dass Analysis Services installiert und für Excel verfügbar ist. Wenn Sie die Arbeitsmappe in Excel öffnen, verwenden Sie eine zwischengespeicherte Kopie und nicht den Analysis Services-Server.  
  
##  <a name="bkmk_firewall"></a> Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen  
 Anhand der Informationen im Thema [Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) können Sie feststellen, ob Sie die Blockierung von Ports in einer Firewall aufheben müssen, um den Zugriff auf Analysis Services oder [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint benötigt. Führen Sie die Schritte in diesem Thema aus, um Port- und Firewalleinstellungen zu konfigurieren. In der Praxis sollten Sie diese Schritte zusammen ausführen, um den Zugriff auf Ihren Analysis Services-Server zuzulassen.  
  
##  <a name="bkmk_upgrade_workbook"></a> Aktualisieren von Arbeitsmappen und geplanter Datenaktualisierung  
 Welche Schritte Sie zum Upgraden von Arbeitsmappen ausführen müssen, die in früheren Versionen von [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] erstellt wurden, hängt von der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Version ab, mit der die Arbeitsmappe erstellt wurde. Weitere Informationen finden Sie unter [Aktualisieren von Arbeitsmappen und planmäßige Datenaktualisierungen &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_multiple_servers"></a> Über die Installation auf einem einzelnen Server hinausgehend – PowerPivot für Microsoft SharePoint  
 **Web-Front-End (WFE)** oder **Mittlere Ebene**: Um einen [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Server im SharePoint-Modus in einer größeren SharePoint-Farm zu verwenden und zusätzliche [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Funktionen in der Farm zu installieren, führen Sie das Installationspaket **spPowerPivot16.msi (SharePoint 2016) oder spPowerPivot.msi (SharePoint 2013)** auf jedem einzelnen SharePoint-Server aus. Mithilfe von „spPowerPivot16.msi“ oder „spPowerPivot.msi“ werden die erforderlichen Datenanbieter und das [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2016- oder 2013-Konfigurationstool installiert.  
  
 Weitere Informationen zur Installation und Konfiguration der mittleren Ebene finden Sie unter:  
  
-   [Installieren oder Deinstallieren des PowerPivot für SharePoint-Add-Ins &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   [Installieren oder Deinstallieren des PowerPivot für SharePoint-Add-Ins &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   Informationen zum Herunterladen der MSI-Datei finden Sie unter [Microsoft SQL Server 2016 PowerPivot für Microsoft SharePoint 2016](http://go.microsoft.com/fwlink/?LinkID=324854)  
  
-   [Konfigurieren von PowerPivot und Bereitstellen von Lösungen &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **Redundanz und Serverauslastung:** Das Installieren eines zweiten bzw. weiterer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Server im [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Modus führt zu einer Redundanz der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Serverfunktionalität. Durch Hinzufügen zusätzlicher Server wird die Arbeitsauslastung auf mehrere Server verteilt. Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [Konfigurieren von Analysis Services für die Verarbeitung von Datenmodellen in Excel Services (SharePoint 2013)](http://technet.microsoft.com/library/jj614437(v=office.15)).  
  
-   [Verwalten von Excel Services-datenmodelleinstellungen (SharePoint 2013)](http://technet.microsoft.com/library/jj219780(v=office.15)).  
  
 ![SharePoint-Einstellungen](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Einstellungen") [Submit Feedback und Kontaktinformationen Informationen über SQL Server Feedback](https://feedback.azure.com/forums/908035-sql-server).  
  
## <a name="see-also"></a>Siehe auch  
 [Migrieren von Power Pivot zu SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [Installieren oder Deinstallieren des PowerPivot für SharePoint-Add-In &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Aktualisieren von Arbeitsmappen und planmäßige Datenaktualisierungen &#40; SharePoint 2013 &#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
