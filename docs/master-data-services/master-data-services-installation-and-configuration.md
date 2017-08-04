---
title: Master Data Services-Installation und Konfiguration | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
caps.latest.revision: 44
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 25e5dc869efd2417c47b72c70ede7ba19ab54b46
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="master-data-services-installation-and-configuration"></a>Master Data Services-Installation und -Konfiguration
  Dieser Artikel behandelt die Installation von [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] auf einem Computer mit Windows Server 2012 R2, die Einrichtung der MDS-Datenbank und -Website und die Bereitstellung der Beispielmodelle und -daten. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) ermöglicht Ihrer Organisation, eine vertrauenswürdige Version der Daten zu verwalten.   
  
> [!NOTE] 
> Sie können [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] auf einem Windows 10-Computer, die bei der Verwendung der Developer Edition, die nun unterstützt [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. 
>>Weitere Informationen zum Betriebssystem-Unterstützung für verschiedene [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] Editionen finden Sie unter [Hardware and Software Requirements for Installing SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). 

Einen Überblick darüber, wie Sie Daten in [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]organisieren, finden Sie unter [Übersicht über Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md).     
  
 Informationen zu den neuen Funktionen in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] finden Sie unter [Neues in Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
 
Links zu Videos und Ressourcen zum Erlernen von [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] finden Sie unter [Erlernen von SQL Master Data Services](../master-data-services/learn-sql-server-master-data-services.md). 
  
> **Download**  
>-   Navigieren Sie zum Herunterladen von [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]zum  **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2017-ctp/)**.  
>-   Haben Sie ein Azure-Konto?  Wechseln Sie anschließend  **[hier](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**  um eine virtuelle Maschine mit bereits installierten SQL Server zu starten.  
 
> **Sie können keine MDS-Website erstellen?**
>>Lesen Sie diesen Microsoft Support-Artikel für Anweisungen zum Lösen dieses Problems.
[Können Sie keine MDS-Website über ein Konto mit geringen Rechten in SQL Server 2016 erstellen?](https://aka.ms/mdssupport) 

## <a name="internet-explorer-and-silverlight"></a>InternetExplorer und Silverlight
- Bei der Installation [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] auf einem Computer mit Windows Server 2012 müssen Sie möglicherweise verstärkte Sicherheitskonfiguration für Internet Explorer zum Zulassen für die Website für die Anwendung zu konfigurieren. Andernfalls schlägt das Durchsuchen der Website auf dem Servercomputer fehl.
- Um in der Webanwendung arbeiten zu können, muss Silverlight 5 auf dem Clientcomputer installiert werden. Wenn Sie nicht über die erforderliche Version von Silverlight verfügen, werden Sie aufgefordert, es zu installieren, wenn Sie zu einem Bereich der Webanwendung navigieren, die dies erfordert. Sie können Silverlight 5 von  **[hier](https://www.microsoft.com/silverlight/)**.

## <a name="includessmdsshortmdincludesssmdsshort-mdmd-on-an-azure-virtual-machine"></a>[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]auf virtuellen Azure-Computer
Wenn Sie ein Azure Virtual Machine mit spin standardmäßig [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] bereits installiert, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] ist ebenfalls installiert. 

Du nächste Schritt besteht darin, (Internet Information Services, IIS) installieren. Finden Sie unter der [installieren und Konfigurieren von IIS](#InstallIIS) Abschnitt. 

Wenn Sie Änderungen vornehmen, um die Installation des gewünschten [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], finden Sie in den Standardspeicherort die Datei setup.exe von `<drive>`: \SQLServer_13.0_Full.
  
## <a name="InstallMDS"></a>Installieren von Master Data Services  
 Zum Installieren von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwenden Sie den Installations-Assistenten von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Setup oder eine Eingabeaufforderung.  
  
 **So installieren Sie [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] mithilfe des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Setups auf einem Computer mit Windows Server 2012 R2**  
  
1.  Doppelklicken Sie auf Setup.exe, und befolgen Sie die Schritte im Installations-Assistenten.  
  
2.  Wählen Sie auf der Seite [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Funktionsauswahl **unter** Freigegebene Funktionen **** aus.  
  
     Dadurch werden [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], Assemblys, das Windows PowerShell-Snap-In sowie Ordner und Dateien für Webanwendungen und Dienste installiert.  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  Schließen Sie den Installations-Assistenten ab.  

## <a name="InstallIIS"></a>Installieren und Konfigurieren von IIS
  
1.  Klicken Sie in [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]auf das Symbol **Server-Manager** auf der Taskleiste auf dem **Desktop**.  
  
     ![Symbol für den Server-Manager in Windows Server 2012-Taskleiste](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "Symbol für den Server-Manager in Windows Server 2012-Taskleiste")  
  
5.  Klicken Sie im **Server-Manager**im Menü **Verwalten** auf **Rollen und Features hinzufügen** .  
   
     ![In Server verwalten, Hinzufügen von Rollen und Features Menübefehl](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "In Server verwalten, Hinzufügen von Rollen und Features Menübefehl")  
  
6.  Akzeptieren Sie auf der Seite **Installationstyp** des **Assistenten zum Hinzufügen von Rollen und Features**den Standardwert (**Rollenbasierte oder featurebasierte Installation**), und klicken sie auf **Weiter**.  
  
7.  Klicken Sie auf **Einen Server aus dem Serverpool auswählen**und anschließend auf den Server, auf dem Sie [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]installiert haben.  
  
     ![mds_AddRolesFeaturesWizard_ServerSelectionPage](../master-data-services/media/mds-addrolesfeatureswizard-serverselectionpage.png) 
  
8. Auf der **Serverrollen** auf **Webserver** , und klicken Sie dann auf **Weiter**. 

   ![mds_AddRolesFeaturesWizard_ServerRolesPage](../master-data-services/media/mds-addrolesfeatureswizard-serverrolespage.png)
   
9. Auf der **Funktionen** Seite, vergewissern Sie sich, dass die folgenden Funktionen ausgewählt sind, und klicken Sie dann auf **Weiter**. Diese Funktionen sind erforderlich, damit [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] auf [!INCLUDE[winblue_server_2_md](../includes/winblue-server-2-md.md)].
  
    |-Funktionen|-Funktionen|  
    |--------------|--------------|  
    |![mds_AddRolesFeaturesWizard_FeaturesPage](../master-data-services/media/mds-addrolesfeatureswizard-featurespage.png)|![mds_AddRolesFeaturesWizard_FeaturesPage_WindowsProcActive](../master-data-services/media/mds-addrolesfeatureswizard-featurespage-windowsprocactive.png)|  

10. Klicken Sie im linken Bereich auf **Webserverrolle (IIS)** , und klicken Sie dann auf **Rollendienste**.
11. Auf der **Rollendienste** Seite, vergewissern Sie sich, dass die folgenden Dienste ausgewählt sind, und klicken Sie dann auf **Weiter**. Diese Dienste sind erforderlich, damit [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] auf [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)].

    > [!WARNING]  
    >  Installieren Sie nicht den Rollendienst WebDAV-Veröffentlichung. Die WebDAV-Veröffentlichung ist nicht mir [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]kompatibel.  
  
     |Rollendienste|Rollendienste|  
    |-----------------------------|-----------------------------|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_PerformSecurity](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-performsecurity.png)|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage_AppDevsection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-appdevsection.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_ManageToolssection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-managetoolssection.png)|  
    |||  
  
     Eine Liste der erforderlichen Features und Rollendienste auf anderen Betriebssystemen, finden Sie unter [Anforderungen für die Webanwendung &#40; Master Data Services &#41; ](../master-data-services/install-windows/web-application-requirements-master-data-services.md) .   
  
 Weitere Informationen über die Installation [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe des Setups finden Sie unter [Installieren von SQL Server 2016 vom Installations-Assistenten aus &#40;Setup&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
 Weitere Informationen zur Installation von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe einer Eingabeaufforderung finden Sie unter [Installieren von SQL Server 2016 von der Eingabeaufforderung](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Wenn Sie eine Eingabeaufforderung verwenden, ist [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] als Funktionsparameter verfügbar.  
  
 Eine kurze Beschreibung mit Links zu weiteren Informationen zur Installationsvorbereitung finden Sie unter [Installieren von Master Data Services](../master-data-services/install-windows/install-master-data-services.md).  
  
##  <a name="SetUpWeb"></a> Einrichten der Datenbank und Website  
 **So richten Sie Datenbank und Website mithilfe von [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]** ein  

 
> [!WARNING]  
    >  Sie müssen [Installieren von IIS](#InstallIIS) vor dem Starten der [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager. Andernfalls den Konfigurations-Manager zeigt einen Fehler Informationen Information Services und nicht erstellen werden die [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Webanwendung.  
    
> **Browser-Anforderung**
>>Die [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Webanwendung funktioniert nur in Internet Explorer (IE) 9 oder höher. Internet Explorer 8 und frühere Versionen, Microsoft Edge und Chrome werden nicht unterstützt.    
  
1.  Starten Sie den [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], und klicken im linken Bereich auf **Datenbankkonfiguration** .  
  
2.  Klicken Sie auf **Datenbank erstellen**und anschließend im **Datenbank erstellen (Assistent)** auf **Weiter**.  
  
3.  Wählen Sie auf der Seite **Datenbankserver** den **Authentifizierungstyp** , und klicken Sie anschließend auf **Verbindung testen** , um zu bestätigen, dass Sie eine Verbindung mit der Datenbank mithilfe der Anmeldeinformationen für den von Ihnen ausgewählten Authentifizierungstyp herstellen können. Klicken Sie auf **Weiter**.
  
    > [!NOTE]  
    >  Wenn Sie als Authentifizierungstyp **Aktueller Benutzer – Integrierte Sicherheit** auswählen, so ist das Feld **Benutzername** schreibgeschützt und zeigt den Namen des Windows-Benutzerkontos an, das am Computer angemeldet ist. Ausgeführtes Betriebssystem [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] auf ein Azure Virtual Machine (VM), die **Benutzername** Feld zeigt die Namen der virtuellen Maschine und den Benutzernamen für das lokale Administratorkonto auf dem virtuellen Computer. 

    ![mds_2016ConfigManager_CreateDatabaseWizard_ServerPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-serverpage.png)  
  
4.  Geben Sie im Feld **Datenbankname** einen Namen ein. Um eine Windows-Sortierung auszuwählen, deaktivieren Sie optional die **SQL Server-standardsortierung** Kontrollkästchen und klicken Sie auf eine oder mehrere der verfügbaren Optionen wie z. B. **Groß-/Kleinschreibung**. Klicken Sie auf **Weiter**.

    ![mds_2016ConfigManager_CreateDatabaseWizard_DatabasePage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-databasepage.png)  
  
     Weitere Informationen zur Windows-Sortierung finden Sie unter [Name der Windows-Sortierung (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).  
  
5.  Geben Sie im Feld **Benutzername** das Windows-Konto des Benutzers an, der der Standardadministrator für Master Data Services sein wird. Ein Administrator verfügt über Zugriff auf alle Funktionsbereiche und kann alle Modelle hinzufügen, löschen oder aktualisieren.  

    ![mds_2016ConfigManager_CreateDatabaseWizard_AdminPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-adminpage.png)  
  
6.  Klicken Sie auf **Weiter** , um eine Zusammenfassung der Einstellungen für die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank anzuzeigen. Klicken Sie anschließend erneut auf **Weiter** , um die Datenbank zu erstellen. Die **Status und Fertig stellen** Seite wird angezeigt.

7. Wenn die Datenbank erstellt und konfiguriert ist, klicken Sie auf **Fertig stellen**.  
  
     Informationen zu den Einstellungen in **Datenbank erstellen (Assistent)** finden Sie unter [Datenbank erstellen &#40;Assistent im Konfigurations-Manager für Master Data Services&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
7.  Auf der **Datenbankkonfiguration** auf der Seite der [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], klicken Sie auf **Datenbank auswählen**.  
  
8.  Klicken Sie auf **verbinden**, wählen die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Datenbank, die Sie in Schritt 7 erstellt, und klicken Sie dann auf **OK**. 

    ![mds_2016ConfigManager_SelectDatabaseButton_ConnectToDatabaseDialog](../master-data-services/media/mds-2016configmanager-selectdatabasebutton-connecttodatabasedialog.png)  
  
     Somit ist die Einrichtung der Datenbank abgeschlossen. Die Seite **Datenbankkonfiguration** zeigt nun die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz an, mit der Sie für [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine Verbindung hergestellt haben, der Datenbank, die Sie erstellt haben sowie die aktuelle Datenbankversion.  

    ![mds_2016ConfigManager_DatabaseConfig_Completed](../master-data-services/media/mds-2016configmanager-databaseconfig-completed.png)   
  
9. Klicken Sie im [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]im linken Bereich auf **Webkonfiguration** .  
  
10. Klicken Sie im Listenfeld **Website** auf **Standardwebsite**und anschließend auf **Erstellen** , um eine Webanwendung zu erstellen.  
  
    > [!NOTE]  
    >  Wenn Sie **Standardwebsite**auswählen, müssen Sie eine Webanwendung erstellen. Wenn Sie die Option **Neue Website erstellen** im Listenfeld auswählen, wird die Anwendung automatisch erstellt.  

     ![mds_2016ConfigManager_WebConfig](../master-data-services/media/mds-2016configmanager-webconfig.png)  
  
11. Führen Sie im Abschnitt **Anwendungspool** einen der folgenden Schritte aus.  
  
    -   Geben Sie denselben Benutzernamen ein, den Sie in Schritt 5 für das **Administratorkonto**der Datenbank eingegeben haben. Geben Sie zudem das Kennwort ein, und klicken Sie auf **OK**.  
  
         **-ODER-**  
  
    -   Geben Sie einen anderen Benutzernamen ein, geben Sie das Kennwort ein, und klicken Sie anschließend auf OK.  
  
         Sie müssen nicht das gleiche Konto verwenden, wenn Sie die Datenbank und die Webanwendung erstellen.  

        ![mds_2016ConfigManager_WebConfig_CreateWebApplication](../master-data-services/media/mds-2016configmanager-webconfig-createwebapplication.png)   
  
     Weitere Informationen zum Dialogfeld **Webanwendung erstellen** finden Sie unter [Webanwendung erstellen (Dialogfeld) &#40;Konfigurations-Manager für Master Data Services&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).  
  
12. Klicken Sie auf der Seite **Webkonfiguration** im Feld **Webanwendung** auf die Anwendung, die Sie erstellt haben, und anschließend im Abschnitt **Zuordnen einer Anwendung zu einer Datenbank** auf **Auswählen**.  
  
13. Klicken Sie auf **Verbinden**, wählen Sie die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank aus, die Sie der Web-Anwendung zuordnen möchten, und klicken Sie anschließend auf **OK**.  
  
     Somit ist die Einrichtung der Website abgeschlossen. Die Seite **Webkonfiguration** zeigt nun die von Ihnen ausgewählte Website an sowie die Webanwendung, die Sie erstellt haben und die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank, die der Anwendung zugeordnet ist.  

     ![mds_2016ConfigManager_WebConfig_Completed](../master-data-services/media/mds-2016configmanager-webconfig-completed.png)  
 
     
15. Klicken Sie auf **Anwenden**. Die **-Konfiguration abschließen** Meldung wird angezeigt. Klicken Sie auf **OK** im Meldungsfeld zum Starten der Webanwendung. Die Adresse der Website lautet http://*Servername*/*Webanwendung*/. 


![mds_2016ConfigurationComplete_MessageBox](../master-data-services/media/mds-2016configurationcomplete-messagebox.png) 
  
     For more information about the settings on the Web Configuration page, see [Web Configuration Page &#40;Master Data Services Configuration Manager&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 Alternativ können Sie [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] verwenden, um andere Einstellungen für die der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank zugeordneten Webanwendungen und -dienste festzulegen. Beispielsweise können Sie festlegen, wie häufig Daten geladen werden oder wie oft Überprüfungs-E-Mails gesendet werden. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
##  <a name="deploySample"></a> Bereitstellen von Beispielmodellen und -daten  
 Die folgenden drei Beispielmodellpakete sind in  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]enthalten.   Diese Beispielmodelle enthalten Daten. **Der Standardspeicherort für die beispielmodellpaketen ist %programfiles%\Microsoft SQL Server\140\Master Data services\samples\packages verwendet.**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 Stellen Sie diese Pakete mit dem MDSModelDeploy-Tool bereit. Der Standardspeicherort für das MDSModelDeploy-Tool ist *Laufwerk*\Programme\Microsoft SQL Server\ 140\Master Data Services\Configuration.  
  
 Informationen zu den Voraussetzungen zur Ausführung dieses Tools finden Sie unter [Bereitstellen eines Modellbereitstellungspakets mit MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
 Informationen zu Updates an, um die Daten zur Unterstützung neuer Features in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], finden Sie unter [SQL Server-Beispiele: Modell Bereitstellung Pakete (MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md).  
  
 **So stellen Sie die Beispielmodelle bereit**  
  
1.  Kopieren Sie die beispielmodellpaketen auf *Laufwerk*\Programme\Microsoft SQL Server\140\Master Data Services\Configuration.  
  
2.  Öffnen Sie eine Administrator-Eingabeaufforderung, und navigieren Sie zu "MDSModelDeploy.exe", indem Sie folgenden Befehl ausführen.  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration  
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
    >
    > [!NOTE]
    > Um die Metadateninformationen der Beispielmodelle mehr zu erfahren, finden Sie in der Infodatei, die an dieser Stelle "c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration" verfügbar
    >
   
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
  
     ![Befehlszeile für die Bereitstellung des Produkts beispielmodells](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "über die Befehlszeile für die Bereitstellung von Produktmodell-Beispiel")  
  
4.  Führen Sie folgende Schritte aus, um die Beispielmodelle anzuzeigen.  
  
    1.  Navigieren Sie zur [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Website, die Sie eingerichtet haben. Weitere Informationen finden Sie im Abschnitt [Einrichten der Datenbank und der Website](#SetUpWeb) .  
  
         Die Adresse der Website lautet http://*Servername*/*Webanwendung*/.  
  
    2.  Wählen Sie ein Modell aus der Liste **Modell** aus, und klicken Sie auf **Explorer**.  
  
         ![MDS-Website auf der Startseite. ] (../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "MDS-Website, auf der Startseite.")  
  
## <a name="next-step"></a>Nächster Schritt  
 Erstellen Sie ein neues Modell und Entitäten für Ihre Daten. Weitere Informationen finden Sie unter [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md) und [Erstellen einer Entität &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
 Einen Überblick darüber, wie Sie ein Modell und Entitäten verwenden, um eine Struktur für Ihre Daten in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] zu erstellen, finden Sie unter [Übersicht über Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md).  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Get%20Started%20with%20Master%20Data%20Services)  
  
## <a name="see-also"></a>Siehe auch  
 [Master Data Services-Datenbank](../master-data-services/master-data-services-database.md)   
 [Master Data Manager-Webanwendung](../master-data-services/master-data-manager-web-application.md)   
 [Datenbankkonfiguration &#40;Seite im Konfigurations-Manager für Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Neues in Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
  

