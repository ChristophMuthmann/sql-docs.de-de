---
title: "Master Data Services-Installation und -Konfiguration | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
caps.latest.revision: 44
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 37
---
# Master Data Services-Installation und -Konfiguration
  Dieser Artikel behandelt die Installation von [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] auf einem Computer mit Windows Server 2012 R2, die Einrichtung der MDS-Datenbank und -Website und die Bereitstellung der Beispielmodelle und -daten. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) ermöglicht Ihrer Organisation, eine vertrauenswürdige Version der Daten zu verwalten.   
   
Einen Überblick darüber, wie Sie Daten in [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]organisieren, finden Sie unter [Übersicht über Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md).     
  
 Informationen zu den neuen Funktionen in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] finden Sie unter [Neues in Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
 
Links zu Videos und Ressourcen zum Erlernen von [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] finden Sie unter [Erlernen von SQL Master Data Services](../master-data-services/learn-sql-server-master-data-services.md). 
  
> **Download**  
>-   Um [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]herunterzuladen, navigieren Sie zum  **[Evaluierungscenter](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
>-   Sie haben ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** , um einen virtuellen Computer zu starten, auf dem bereits [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  installiert ist.  
 
> **Sie können keine MDS-Website erstellen?**
>>Lesen Sie diesen Microsoft Support-Artikel für Anweisungen zum Lösen dieses Problems.
[Können Sie keine MDS-Website über ein Konto mit geringen Rechten in SQL Server 2016 erstellen?](https://aka.ms/mdssupport) 
  
## <a name="installing-master-data-services-and-iis-roles-and-features"></a>Installieren von Master Data Services und IIS-Rollen und -Funktionen  
 Zum Installieren von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwenden Sie den Installations-Assistenten von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Setup oder eine Eingabeaufforderung.  
  
 **So installieren Sie [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] mithilfe des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Setups auf einem Computer mit Windows Server 2012 R2**  
  
1.  Doppelklicken Sie auf Setup.exe, und befolgen Sie die Schritte im Installations-Assistenten.  
  
2.  Wählen Sie auf der Seite [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Funktionsauswahl **unter** Freigegebene Funktionen ** **aus.  
  
     Dadurch werden [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], Assemblys, das Windows PowerShell-Snap-In sowie Ordner und Dateien für Webanwendungen und Dienste installiert.  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  Schließen Sie den Installations-Assistenten ab.  
  
4.  Klicken Sie in [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]auf das Symbol **Server-Manager** auf der Taskleiste auf dem **Desktop**.  
  
     ![Icon for the Server Manager in Windows Server 2012 taskbar](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "Icon for the Server Manager in Windows Server 2012 taskbar")  
  
5.  Klicken Sie im **Server-Manager**im Menü **Verwalten** auf **Rollen und Features hinzufügen** .  
  
     ![In Server Manage, the Add Roles and Features menu command](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "In Server Manage, the Add Roles and Features menu command")  
  
6.  Akzeptieren Sie auf der Seite **Installationstyp** des **Assistenten zum Hinzufügen von Rollen und Features**den Standardwert (**Rollenbasierte oder featurebasierte Installation**), und klicken sie auf **Weiter**.  
  
7.  Klicken Sie auf **Einen Server aus dem Serverpool auswählen**und anschließend auf den Server, auf dem Sie [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]installiert haben.  
  
     ![Server Selection page on the Add Roles and Features Wizard](../master-data-services/media/mds-servermanagerdashboard-addrolesandfeatureswizard-serverselection.png "Server Selection page on the Add Roles and Features Wizard")  
  
8.  Klicken Sie im Feld **Rollen** auf die Rollen und Rollendienste, die für [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] auf [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]benötigt werden. Klicken Sie anschließend auf **Weiter**. Das folgende Bild zeigt die ausgewählten erforderlichen Rollen und Rollendienste.  
  
    > [!WARNING]  
    >  Installieren Sie nicht den Rollendienst WebDAV-Veröffentlichung. Die WebDAV-Veröffentlichung ist nicht mir [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]kompatibel.  
  
    > [!IMPORTANT]  
    > Die **Komprimierung dynamischer Inhalte** ist standardmäßig aktiviert. Dadurch wird die Größe der XML-Antwort erheblich verringert und die Netzwerk-E/A reduziert, obwohl die CPU-Auslastung erhöht wird.  Weitere Klicken Sie informationen finden Sie unter **[CTP 2.0] Verbesserte Leistung** in [What's New in Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
  
    |Rolle und Rollendienste|Rolle und Rollendienste|  
    |-----------------------------|-----------------------------|  
    |![Common HTTP Features](../master-data-services/media/mds-servermanagerdashboard-commonhttpfeaturesroles.png "Common HTTP Features")|![Health Diagnostics Roles](../master-data-services/media/mds-servermanagerdashboard-healthdiagnosticsroles.png "Health Diagnostics Roles")|  
    |![Performance Roles](../master-data-services/media/mds-servermanagerdashboard-performanceroles.png "Performance Roles")|![Security Roles](../master-data-services/media/mds-servermanagerdashboard-securityroles.png "Security Roles")|  
    |![WebServer Application Development Roles](../master-data-services/media/mds-servermanagerdashboard-webserverapplicationdevelopmentroles.png "WebServer Application Development Roles")|![Management Tools](../master-data-services/media/mds-servermanagerdashboard-managementtoolsroles.png "Management Tools")|  
  
     Eine Liste der benötigten Rollen und Rollendienste bei anderen Betriebssystemen finden Sie unter [Anforderungen für die Webanwendung &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md).  
  
9. Klicken Sie im Feld **Funktionen** auf die Funktionen, die für [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] auf [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]benötigt werden. Klicken Sie anschließend auf **Weiter**. Das folgende Bild zeigt die ausgewählten erforderlichen Funktionen.  
  
    |Funktionen|Funktionen|  
    |--------------|--------------|  
    |![Net Framework Features](../master-data-services/media/mds-servermanagerdashboard-netframeworkfeatures.png "Net Framework Features")|![Windows Process Features](../master-data-services/media/mds-servermanagerdashboard-windowsprocessfeatures.png "Windows Process Features")|  
  
     Eine Liste der benötigten Funktionen bei anderen Betriebssystemen finden Sie unter [Anforderungen für die Webanwendung &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md).  
  
 Weitere Informationen über die Installation [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe des Setups finden Sie unter [Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md).  
  
 Weitere Informationen zur Installation von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe einer Eingabeaufforderung finden Sie unter [Installieren von SQL Server 2016 von der Eingabeaufforderung](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Wenn Sie eine Eingabeaufforderung verwenden, ist [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] als Funktionsparameter verfügbar.  
  
 Eine kurze Beschreibung mit Links zu weiteren Informationen zur Installationsvorbereitung finden Sie unter [Installieren von Master Data Services](../master-data-services/install-windows/install-master-data-services.md).  
  
##  <a name="a-namesetupweba-setting-up-the-database-and-website"></a><a name="SetUpWeb"></a> Einrichten der Datenbank und Website  
 **So richten Sie Datenbank und Website mithilfe von [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]** ein  
  
1.  Starten Sie den [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], und klicken im linken Bereich auf **Datenbankkonfiguration** .  
  
2.  Klicken Sie auf **Datenbank erstellen**und anschließend im **Datenbank erstellen (Assistent)** auf **Weiter**.  
  
3.  Wählen Sie auf der Seite **Datenbankserver** den **Authentifizierungstyp** , und klicken Sie anschließend auf **Verbindung testen** , um zu bestätigen, dass Sie eine Verbindung mit der Datenbank mithilfe der Anmeldeinformationen für den von Ihnen ausgewählten Authentifizierungstyp herstellen können.  
  
    > [!NOTE]  
    >  Wenn Sie als Authentifizierungstyp **Aktueller Benutzer – Integrierte Sicherheit** auswählen, so ist das Feld **Benutzername** schreibgeschützt und zeigt den Namen des Windows-Benutzerkontos an, das am Computer angemeldet ist.  
  
     ![The Database server page in the Create Database Wizard](../master-data-services/media/mds-configurationmanager-createdatabasewizard-serverpage.png "The Database server page in the Create Database Wizard")  
  
4.  Geben Sie im Feld **Datenbankname** einen Namen ein. Deaktivieren Sie optional das Kontrollkästchen **SQL Server-Standardsortierung**, um eine Windows-Sortierung auszuwählen und mindestens eine verfügbare Option anzugeben, z.B. **Groß-/Kleinschreibung wird beachtet** .  
  
     ![The Database page in the Create Database Wizard](../master-data-services/media/mds-configurationmanager-createdatabasewizard-databasepage.png "The Database page in the Create Database Wizard")  
  
     Weitere Informationen zur Windows-Sortierung finden Sie unter [Name der Windows-Sortierung (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).  
  
5.  Geben Sie im Feld **Benutzername** das Windows-Konto des Benutzers an, der der Standardadministrator für Master Data Services sein wird. Ein Administrator verfügt über Zugriff auf alle Funktionsbereiche und kann alle Modelle hinzufügen, löschen oder aktualisieren.  
  
     ![The Administrator Account page in the Create Database Wizard.](../master-data-services/media/mds-configurationmanager-createdatabasewizard-adminpage.png "The Administrator Account page in the Create Database Wizard.")  
  
6.  Klicken Sie auf **Weiter**, um eine Zusammenfassung der Einstellungen für die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank anzuzeigen. Klicken Sie anschließend erneut auf **Weiter**, um die Datenbank zu erstellen.  
  
     Informationen zu den Einstellungen in **Datenbank erstellen (Assistent)** finden Sie unter [Datenbank erstellen &#40;Assistent im Konfigurations-Manager für Master Data Services&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
7.  Klicken Sie auf der Seite Datenbankkonfiguration im [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] auf „Datenbank auswählen“.  
  
8.  Klicken Sie auf **Verbinden**, und wählen Sie anschließend die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank, die Sie in Schritt 6 erstellt haben.  
  
     ![Connect to Database dialog box for the Database Configuration page](../master-data-services/media/mds-configurationmanager-selectdatabasebutton-connecttodatabasedialog.png "Connect to Database dialog box for the Database Configuration page")  
  
     Somit ist die Einrichtung der Datenbank abgeschlossen. Die Seite **Datenbankkonfiguration** zeigt nun die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz an, mit der Sie für [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine Verbindung hergestellt haben, der Datenbank, die Sie erstellt haben sowie die aktuelle Datenbankversion.  
  
     ![Database Configuration page in the Configuration Manager shows a completed database setup.](../master-data-services/media/mds-configurationmanager-databaseconfig-completed.png "Database Configuration page in the Configuration Manager shows a completed database setup.")  
  
9. Klicken Sie im [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]im linken Bereich auf **Webkonfiguration** .  
  
10. Klicken Sie im Listenfeld **Website** auf **Standardwebsite**und anschließend auf **Erstellen** , um eine Webanwendung zu erstellen.  
  
    > [!NOTE]  
    >  Wenn Sie **Standardwebsite**auswählen, müssen Sie eine Webanwendung erstellen. Wenn Sie die Option **Neue Website erstellen** im Listenfeld auswählen, wird die Anwendung automatisch erstellt.  
  
     ![Web Configuration page in the Configuration Manager](../master-data-services/media/mds-configurationmanager-webconfig.png "Web Configuration page in the Configuration Manager")  
  
11. Führen Sie im Abschnitt **Anwendungspool** einen der folgenden Schritte aus.  
  
    -   Geben Sie denselben Benutzernamen ein, den Sie in Schritt 5 für das **Administratorkonto**der Datenbank eingegeben haben. Geben Sie zudem das Kennwort ein, und klicken Sie auf **OK**.  
  
         **-ODER-**  
  
    -   Geben Sie einen anderen Benutzernamen ein, geben Sie das Kennwort ein, und klicken Sie anschließend auf OK.  
  
         Sie müssen nicht das gleiche Konto verwenden, wenn Sie die Datenbank und die Webanwendung erstellen.  
  
     ![Create Web Application dialog box, Web Configuration page](../master-data-services/media/mds-configurationmanager-webconfig-createwebapplication.png "Create Web Application dialog box, Web Configuration page")  
  
     Weitere Informationen zum Dialogfeld **Webanwendung erstellen** finden Sie unter [Webanwendung erstellen (Dialogfeld) &#40;Konfigurations-Manager für Master Data Services&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).  
  
12. Klicken Sie auf der Seite **Webkonfiguration** im Feld **Webanwendung** auf die Anwendung, die Sie erstellt haben, und anschließend im Abschnitt **Zuordnen einer Anwendung zu einer Datenbank** auf **Auswählen**.  
  
13. Klicken Sie auf **Verbinden**, wählen Sie die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank aus, die Sie der Web-Anwendung zuordnen möchten, und klicken Sie anschließend auf **OK**.  
  
     Somit ist die Einrichtung der Website abgeschlossen. Die Seite **Webkonfiguration** zeigt nun die von Ihnen ausgewählte Website an sowie die Webanwendung, die Sie erstellt haben und die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank, die der Anwendung zugeordnet ist.  
  
     ![The completed Web site configuration](../master-data-services/media/mds-configurationmanager-webconfig-completed.png "The completed Web site configuration")  
  
     Weitere Informationen zu den Einstellungen auf der Seite „Webkonfiguration“ finden Sie unter [Webkonfiguration &#40;Seite im Konfigurations-Manager für Master Data Sevices&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 Alternativ können Sie [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] verwenden, um andere Einstellungen für die der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank zugeordneten Webanwendungen und -dienste festzulegen. Beispielsweise können Sie festlegen, wie häufig Daten geladen werden oder wie oft Überprüfungs-E-Mails gesendet werden. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
##  <a name="a-namedeploysamplea-deploying-sample-models-and-data"></a><a name="deploySample"></a> Bereitstellen von Beispielmodellen und -daten  
 Die folgenden drei Beispielmodellpakete sind in  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]enthalten.   Diese Beispielmodelle enthalten Daten. **Der Standardspeicherort für die Beispielmodellpakete ist: %programfiles%\Microsoft SQL Server\130\Master Data Services\Samples\Packages**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 Stellen Sie diese Pakete mit dem MDSModelDeploy-Tool bereit. Der Standardspeicherort für das MDSModelDeploy-Tool ist *Laufwerk*\Programme\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
 Informationen zu den Voraussetzungen zur Ausführung dieses Tools finden Sie unter [Bereitstellen eines Modellbereitstellungspakets mit MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
 Informationen zu Updates für die Daten zur Unterstützung neuer Funktionen in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] finden Sie unter [Beispiele: Modellbereitstellungspakete &#40;Master Data Services&#41;](../Topic/Samples:%20Model%20Deployment%20Packages%20\(Master%20Data%20Services\).md).  
  
 **So stellen Sie die Beispielmodelle bereit**  
  
1.  Kopieren Sie die Beispielmodellpakete in *Laufwerk*:\Programme\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
2.  Öffnen Sie eine Administrator-Eingabeaufforderung, und navigieren Sie zu "MDSModelDeploy.exe", indem Sie folgenden Befehl ausführen.  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration  
    ```  
  
3.  Stellen Sie jedes Beispielmodell in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] bereit, indem Sie jeden der folgenden Befehle ausführen.  
  
    > [!IMPORTANT]  
    >  In den folgenden Beispielen wird der `MDS1` -Dienstwert angegeben. Dieser Wert wird verwendet, wenn Sie beim Einrichten der  **-Website** Standardwebsite [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ausgewählt haben.  Weitere Informationen finden Sie im Abschnitt [Einrichten der Datenbank und der Website](#SetUpWeb) .  
    >   
    >  Wenn Sie eine neue Website erstellt haben oder eine vorhandene Website ausgewählt haben, führen Sie zunächst folgenden Befehl aus, um den korrekten Dienstwert zu bestimmen.  
    >   
    >  `MDSModelDeploy listservices`  
    >   
    >  Der erste Dienstwert in der Liste mit den Werten wird zurückgegeben und dies ist der Wert, den Sie angeben, um ein Modell bereitzustellen.  
  
     **So stellen Sie das Beispielmodell „chartofaccounts_en.pkg“ bereit**  
  
    ```  
    MDSModelDeploy deploynew -package chartofaccounts_en.pkg -model ChartofAccounts -service MDS1  
    ```  
  
     **So stellen Sie das Beispielmodell „customer_en.pkg“ bereit**  
  
    ```  
    MDSModelDeploy deploynew -package customer_en.pkg -model Customer -service MDS1  
    ```  
  
     **So stellen Sie das Beispielmodell „product_en.pkg“ bereit**  
  
    ```  
    MDSModelDeploy deploynew -package product_en.pkg -model Product -service MDS1  
  
    ```  
  
     Wenn ein Modell erfolgreich bereitgestellt wurde, wird die Meldung **Der MDSModelDeploy-Vorgang wurde erfolgreich abgeschlossen** angezeigt.  
  
     Die folgende Abbildung zeigt den Befehl zum Bereitstellen des Beispielmodells product_en.pkg.  
  
     ![Command line for deploying the Product sample model](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "Command line for deploying the Product sample model")  
  
4.  Führen Sie folgende Schritte aus, um die Beispielmodelle anzuzeigen.  
  
    1.  Navigieren Sie zur [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Website, die Sie eingerichtet haben. Weitere Informationen finden Sie im Abschnitt [Einrichten der Datenbank und der Website](#SetUpWeb) .  
  
         Die Adresse der Website lautet http://*Servername*/*Webanwendung*/.  
  
    2.  Wählen Sie ein Modell aus der Liste **Modell** aus, und klicken Sie auf **Explorer**.  
  
         ![MDS Web site, home page.](../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "MDS Web site, home page.")  
  
## <a name="next-step"></a>Nächster Schritt  
 Erstellen Sie ein neues Modell und Entitäten für Ihre Daten. Weitere Informationen finden Sie unter [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md) und [Erstellen einer Entität &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
 Einen Überblick darüber, wie Sie ein Modell und Entitäten verwenden, um eine Struktur für Ihre Daten in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] zu erstellen, finden Sie unter [Übersicht über Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md).  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Get%20Started%20with%20Master%20Data%20Services)  
  
## <a name="see-also"></a>Siehe auch  
 [Master Data Services-Datenbank](../master-data-services/master-data-services-database.md)   
 [Master Data Manager-Webanwendung](../master-data-services/master-data-manager-web-application.md)   
 [Datenbankkonfiguration &#40;Seite im Konfigurations-Manager für Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Neues in Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
  