---
title: Installieren des ersten Berichtsservers im SharePoint-Modus | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 140c0f085919b504ab2263abbc944b80897751fe
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="install-the-first-report-server-in-sharepoint-mode"></a>Installieren des ersten Berichtsservers im SharePoint-Modus

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Die Verfahren in diesem Thema führen Sie über eine einzelne Serverinstallation von Reporting Services im SharePoint-Modus. In den Schritten führen Sie u. a. den Installations-Assistenten für SQL Server sowie Konfigurationsaufgaben unter Verwendung der SharePoint-Zentraladministration aus. Das Thema kann auch für einzelne Verfahren zum Aktualisieren einer vorhandenen Installation, z. B. zum Erstellen einer Reporting Services-dienstanwendung verwendet werden.  
  
> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.
  
 Weitere Informationen zum Hinzufügen einer vorhandenen Farm weitere Reporting Services-Server finden Sie hier:  
  
-   [Hinzufügen eines zusätzlichen Berichtsservers zu einer Farm &#40;Horizontales Skalieren für SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [Hinzufügen eines zusätzlichen Reporting Services-Web-Front-Ends zu einer Farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 Die Installation auf einem einzelnen Server ist für Entwicklungs- und Testszenarien geeignet, wird aber für Produktionsumgebungen nicht empfohlen.  
  
##  <a name="bkmk_singleserver"></a>Beispiel-Einzelserver-Bereitstellung

 Die Installation auf einem einzelnen Server ist für Entwicklungs- und Testszenarien geeignet, wird aber für Produktionsumgebungen nicht empfohlen. Die einzelserverumgebung bezieht sich auf einem einzelnen Computer, der SharePoint- und Reporting Services-Komponenten auf demselben Computer installiert ist. Horizontale Skalierung mit mehrere Reporting Services-Server behandelt im Thema nicht.  
  
 Das folgende Diagramm veranschaulicht die Komponenten, die Teil eines einzelnen Servers Reporting Services-Bereitstellung sind.  
 
 > [!NOTE]
 > In SharePoint 2016 wurde Excel Services auf den Office Online Server verschoben und kann nicht in einer Bereitstellung mit einem einzelnen Server verwendet werden. Der Office Online Server muss auf einem anderen Server bereitgestellt werden. Weitere Informationen finden Sie unter [Übersicht über Office Online Server](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx) und [Konfigurieren der Excel Online-Verwaltungseinstellungen](https://technet.microsoft.com/library/jj219698\(v=office.16\).aspx).
  
|||  
|-|-|  
|**(1)**|Mit einer SQL Server-Installation installierter SharePoint-Dienst. Sie können eine oder mehrere Reporting Services-dienstanwendungen erstellen.|  
|**(2)**|Reporting Services-add-in für SharePoint-Produkte stellt der Benutzer Benutzeroberflächenkomponenten auf den SharePoint-Servern bereit.|  
|**(3)**|Die Excel Services-Anwendung wird von Power View und [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]verwendet. Dies ist in einer Einzelserverbereitstellung für SharePoint 2016 nicht verfügbar. Es ist ein [Office Online Server](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx) erforderlich.|  
|**(4)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung zu erstellen.|  
  
 ![SSRS im SharePoint-Modus Einzelserverbereitstellung](../../reporting-services/install-windows/media/rs-sharepoint-1server-deployment.gif "SSRS SharePoint-Modus-Einzelserver-Bereitstellung")  
  
> [!TIP]  
>  Komplexere Bereitstellungsbeispiele finden Sie unter [Bereitstellungstopologien für SQL Server-BI-Funktionen in SharePoint](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26).  
  
##  <a name="bkmk_setupaccounts"></a> Setupkonten

 In diesem Abschnitt wird beschrieben, die Konten und Berechtigungen, die für die wesentlichen Schritte zur Bereitstellung von Reporting Services im SharePoint-Modus verwendet.  
  
 **Installation und Registrierung der Reporting Services-Dienst:**  
  
-   Das aktuelle Konto während der Installation (bezeichnet als das Konto 'Setup') von Reporting Services im SharePoint-Modus muss über Administratorrechte auf dem lokalen Computer verfügen. Wenn Sie nach dem SharePoint installiert ist und das Konto 'Setup' auch ein Mitglied der Administratorgruppe der SharePoint-Farm ist Reporting Services installiert sind, wird die Installation von Reporting Services den Reporting Services-Dienst für Sie registriert. Wenn Sie Reporting Services installieren, bevor SharePoint installiert ist, oder das Konto 'Setup' kein Mitglied der Administratorgruppe der Farm ist ist, registrieren Sie den Dienst manuell. Weitere Informationen finden Sie im Abschnitt [Schritt 2: Registrieren und Starten des SharePoint-Diensts für Reporting Services](#bkmk_install_SSRS_sharedservice).  
  
 **Erstellen von Reporting Services-Dienstanwendungen**  
  
-   Nach der Installation und Registrierung des Diensts für Reporting Services, erstellen Sie eine oder mehrere Reporting Services-dienstanwendungen. Das "Dienstkonto der SharePoint-Farm" muss vorübergehend Mitglied der lokalen Administratorgruppe sein, damit die Reporting Services-Dienstanwendung erstellt werden kann. Weitere Informationen zu SharePoint 2013-Kontoberechtigungen finden Sie unter [Kontoberechtigungen und Sicherheitseinstellungen in SharePoint 2013](http://technet.microsoft.com/library/cc678863.aspx) (http://technet.microsoft.com/library/cc678863.aspx). Für SharePoint 2016 finden Sie weitere Informationen unter [Kontoberechtigungen und Sicherheitseinstellungen in SharePoint 2016](https://technet.microsoft.com/library/cc678863\(v=office.16\).aspx).  
  
     Eine bewährte Sicherheitsmethode besteht darin, die Administratorkonten der SharePoint-Farm nicht gleichzeitig als Administratorkonten des lokalen Betriebssystems festzulegen. Wenn Sie der lokalen Administratorgruppe während der Installation ein Farmadministratorkonto hinzufügen, wird empfohlen, das Konto nach Ende der Installation aus der lokalen Administratorgruppe zu entfernen.  
  
##  <a name="bkmk_install_SSRS"></a> Schritt 1: Installieren eines Reporting Services-Berichtsservers im SharePoint-Modus

 Dieser Schritt wird einen Reporting Services-Berichtsserver im SharePoint-Modus und das Reporting Services-add-in für SharePoint-Produkte installiert. Abhängig von bereits auf dem Computer installierten Komponenten werden einige der in den folgenden Schritten beschriebenen Installationsseiten u. U. nicht angezeigt.  
 
 > [!IMPORTANT]
 > Für SharePoint 2016, die die Reporting Services SharePoint-Server installiert werden soll, auf muss die **benutzerdefinierte** -Serverrolle. Die Bereitstellung von Reporting Services auf einem SharePoint-Server, der nicht erfolgreich die **benutzerdefinierte** Rolle während des nächsten Wartungsfensters SharePoint MinRole den Reporting Services-Dienst beendet, da er festgestellt, dass aber Reporting Services im integrierten SharePoint-Modus gibt keine Unterstützung für eine der anderen SharePoint-Serverrollen. Die Reporting Services-unterstützt nur die **benutzerdefinierte** Rolle.
 
 > [!NOTE]
 > Wenn Sie planen, auch den Power Pivot-Dienst mit SharePoint 2016 zu verwenden, installieren Sie diesen Dienst, bevor Sie Reporting Services installieren. Der Power Pivot-Dienst kann nicht auf einem SharePoint-Server mit der **benutzerdefinierten** Rolle installiert werden. Dadurch wird vermieden, dass die Rollen mehrfach gewechselt werden müssen.
 
 ### <a name="apply-the-custom-server-role-to-a-sharepoint-2016-server"></a>Anwenden der benutzerdefinierten Serverrolle auf einem SharePoint 2016-server
 
 > [!NOTE]
 > Dies gilt nicht für SharePoint 2013.
 
 1. Melden Sie sich bei dem SharePoint-Server an, auf dem Sie [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].
 
 2. Starten Sie die **SharePoint 2016-Verwaltungsshell** als Administrator. 
  
    Sie können mit der rechten Maustaste auf die **SharePoint 2016-Verwaltungsshell** klicken und **Als Administrator ausführen**auswählen.

3. Führen Sie an der PowerShell-Eingabeaufforderung den folgenden Befehl aus.

    > [!NOTE]
    > Stellen Sie sicher, dass Sie den richtigen Namen für den SharePoint-Server angeben.
    
        Set-SPServer SERVERNAME -Role Custom

4. In einer Antwort sollte angezeigt werden, dass ein Zeitgeberauftrag geplant wurde. Sie müssen warten, bis der Auftrag ausgeführt wurde.

5. Verwenden Sie den folgenden Befehl, um die dem Server zugewiesene Rolle zu überprüfen.

        Get-SPServer SERVERNAME 
 
 6. Unter **Rolle** sollte **Benutzerdefiniert**aufgeführt sein.
 
 ### <a name="install-reporting-services"></a>Installieren von Reporting Services
  
1.  Führen Sie den Installations-Assistenten für SQL Server (Setup.exe) aus.  
  
2.  Wählen Sie links im Assistenten die Option **Installation** , und wählen Sie anschließend **Neue eigenständige SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**aus.  

3.  Falls die Seite **Product Key** angezeigt wird, geben Sie Ihren Product Key ein, oder übernehmen Sie den Standardwert der Enterprise Evaluation Edition.  
  
     Wählen Sie **Weiter**aus.  
  
4.  Lesen Sie die Seite mit den Lizenzbedingungen, falls diese angezeigt wird, und akzeptieren Sie die Bedingungen. Microsoft ist Ihnen dankbar, wenn Sie damit einverstanden sind, Daten zur Funktionsverwendung zu senden, damit wir Produktfunktionen und -support verbessern können.  
  
     Wählen Sie **Weiter**aus.  

5.  Es wird empfohlen, die Option **Mit Microsoft Update nach Updates suchen (empfohlen)**auszuwählen. Diese Eingabe ist optional.
  
     Wählen Sie **Weiter**aus.   
  
6.  Je nachdem, welche Komponenten bereits auf dem Computer installiert sind, kann auf der Seite **Setupdateien installieren** folgende Meldung angezeigt werden:  
  
    -   "Für mindestens eine betroffene Datei stehen Vorgänge aus. Sie müssen den Computer nach Abschluss des Setupvorgangs neu starten."  
  
    -   Wählen Sie **Weiter**aus.  
  
7.  Möglicherweise wird die Seite **Installationsregeln** angezeigt. Überprüfen Sie alle Warnungen oder Probleme, die eine Blockierung verursachen. Wählen Sie **Weiter**aus.
 
8. Wählen Sie Folgendes auf der Seite **Funktionsauswahl** aus:  
  
    -   **Reporting Services – SharePoint**  
  
    -   **Reporting Services-Add-In für SharePoint-Produkte**.  
  
    -   Optional können Sie auch **Database Engine Services** auswählen, um eine vollständige Umgebung zu installieren. Sie müssen allerdings über eine SQL Server-Datenbankmodulinstanz verfügen, auf der die SharePoint-Datenbanken gehostet werden.  
  
     Wählen Sie **Weiter**aus.  
  
     ![rs_SetupFeatureSelection_SharePoint_with_circles](../../reporting-services/install-windows/media/rs-setupfeatureselection-sharepoint-with-circles.png)
  
9. Wenn Sie Datenbankmoduldienste ausgewählt haben, akzeptieren Sie die Standardinstanz von **MSSQLSERVER** auf der Seite **Instanzkonfiguration** , und klicken Sie auf **Weiter**.  
  
     ![Hinweis](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Hinweis")der Reporting Services-SharePoint-Dienstarchitektur basiert nicht auf einer SQL Server-"Instanz" wie die vorherige Reporting Services-Architektur war.  
  
10. Wenn die Seite **Serverkonfiguration** angezeigt wird, geben Sie die entsprechenden Anmeldeinformationen ein. Wenn Sie die Reporting Services-Datenfeatures an-datenwarn- oder Abonnementfunktionen verwenden möchten, müssen Sie ändern die **Starttyp** für SQL Server-Agent **automatische**. Abhängig von den bereits auf dem Computer installierten Komponenten wird die Seite **Serverkonfiguration** möglicherweise nicht angezeigt.  
  
     Wählen Sie **Weiter**aus.  
  
11. Wenn Sie die Database Engine Services ausgewählt haben, wird die Seite **Datenbankmodulkonfiguration** angezeigt. Fügen Sie der Liste der SQL-Administratoren entsprechende Konten hinzu, und klicken Sie dann auf **Weiter**.  
  
12. Auf der Seite **Reporting Services-Konfiguration** sollten Sie sehen, dass die Option **Nur Installieren** aktiviert ist. Diese Option installiert die Berichtsserverdateien und die SharePoint-Umgebung wird für Reporting Services nicht konfiguriert.  
  
    > [!NOTE]
    > Nachdem die SQL Server-Installation abgeschlossen wurde, befolgen Sie die Anweisungen in den weiteren Abschnitten dieses Themas, um die SharePoint-Umgebung zu konfigurieren. Dies schließt die gemeinsam genutzte Reporting Services-Dienst installieren und Reporting Services-dienstanwendungen erstellen.  
  
     ![ssRS-2016-setup-configuration](../../reporting-services/install-windows/media/ssrs-2016-setup-configuration.png)
  
13. Überprüfen Sie eventuell angezeigte Warnungen, und klicken Sie dann auf der Seite **Funktionskonfigurationsregeln** auf **Weiter** , wenn Sie die Konfiguration auf diese Seite beenden möchten.  
  
14. Lesen Sie auf der Seite **Installationsbereit** die Installationszusammenfassung. Die Zusammenfassung enthält einen untergeordneten Knoten **SharePoint-Modus für Reporting Services** , für den der Wert **SharePointFilesOnlyMode**angezeigt wird. Wählen Sie **Installieren**aus.  
  
15. Die Installation dauert mehrere Minuten. Die Seite **Abgeschlossen** wird mit einer Liste der Funktionen und dem Status der einzelnen Funktionen angezeigt. Möglicherweise werden Sie in einem Informationsdialogfeld darauf hingewiesen, dass der Computer neu gestartet werden muss.  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a>Schritt 2: Registrieren Sie und starten Sie den Reporting Services-SharePoint-Dienst  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt")  
  
> [!NOTE]
> Wenn Sie in eine vorhandene SharePoint-Farm installieren, müssen Sie die Schritte in diesem Abschnitt nicht ausführen. Die Reporting Services SharePoint-Dienst ist installiert und gestartet, wenn Sie als Teil des im vorherigen Abschnitt dieses Dokuments den Installations-Assistenten von SQL Server ausgeführt wird.  
  
 Es folgen die Hauptgründe, warum Sie den Reporting Services-Dienst manuell zu registrieren müssen.  
  
-   Installation von Reporting Services-SharePoint-Modus wurde vor SharePoint installiert.  
  
-   Das Konto zum Installieren von Reporting Services-SharePoint-Modus war nicht Mitglied der Administratorgruppe der SharePoint-Farm. Weitere Informationen finden Sie im Abschnitt [Setup accounts](#bkmk_setupaccounts).  
  
 Die notwendigen Dateien wurden als Teil des SQL Server-Installations-Assistenten installiert, die Dienste müssen jedoch in der SharePoint-Farm registriert werden.  
  
 Die folgenden Schritte zeigen Ihnen, wie Sie die SharePoint-Verwaltungsshell öffnen und PowerShell-Cmdlets ausführen:  
  
1.  Klicken Sie auf die Schaltfläche **Start** .  
  
2.  Wählen Sie die Gruppe **Microsoft SharePoint 2016-Produkte** oder **Microsoft SharePoint 2013-Produkte** aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf **SharePoint 2016-Verwaltungsshell**bzw. **SharePoint 2013-Verwaltungsshell**, und wählen Sie **Als Administrator ausführen**aus. 

    > [!NOTE]
    > Die SharePoint-Befehle werden im Windows PowerShell-Standardfenster nicht erkannt. Verwenden Sie die **SharePoint-Verwaltungsshell**.  
  
4.  Führen Sie den folgenden PowerShell-Befehl aus, um den Reporting Services SharePoint-Dienst zu installieren. Ein erfolgreicher Abschluss des Befehls zeigt eine neue Zeile in der Verwaltungsshell an. Wurde der Befehl erfolgreich ausgeführt, wird**keine Meldung** an die Verwaltungsshell zurückgegeben:  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  Führen Sie den folgenden PowerShell-Befehl aus, um den Reporting Services-Dienstproxy zu installieren. Ein erfolgreicher Abschluss des Befehls zeigt eine neue Zeile in der Verwaltungsshell an. Wurde der Befehl erfolgreich ausgeführt, wird**keine Meldung** an die Verwaltungsshell zurückgegeben:  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  Führen Sie den folgenden PowerShell-Befehl aus, um den Dienst zu starten, oder starten Sie den Dienst von der SharePoint-Zentraladministration anhand der unten stehenden Anweisungen:  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
    > [!IMPORTANT]
    > Angenommen, eine Fehlermeldung mit etwa folgendem Wortlaut wird ausgegeben:  
    >   
    >     Install-SPRSService: Der Begriff "Install-SPRSService" **wird nicht erkannt** als Namen für ein Cmdlet, Funktion, Skriptdatei oder eines ausführbaren Programms erkannt. Überprüfen Sie die Schreibweise des Namens, oder ob der Pfad enthalten und korrekt ist, und wiederholen Sie den Vorgang.  
    >
    > Entweder Sie befinden sich im Windows Powershell anstatt in der SharePoint-Verwaltungsshell oder Reporting Services-SharePoint-Modus ist nicht installiert. Weitere Informationen zu Reporting Services und PowerShell finden Sie unter [PowerShell-Cmdlets für Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
 Sie können den Dienst auch von der SharePoint-Zentraladministration starten anstatt den dritten PowerShell-Befehl auszuführen. Die folgenden Schritte sind auch nützlich, um sicherzustellen, dass der Dienst gestartet wurde.  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Systemeinstellungen** auf **Dienste auf dem Server verwalten** .  
  
2.  Suchen Sie den **SQL Server Reporting Services-Dienst** , und klicken Sie in der Spalte Aktion auf **Starten** .  
  
3.  Der Status des Reporting Services-Diensts ändert sich von **Beendet** auf **Gestartet**. Installieren Sie den Reporting Services-Dienst mit PowerShell, wenn sich dieser nicht in der Liste befindet.  
  
    > [!NOTE]  
    >  Wenn der Reporting Services-Dienst im Status **Wird gestartet** bleibt und sich nicht in **Gestartet**ändert, stellen Sie sicher, dass der Dienst der SharePoint 2013-Administration im Windows Server-Manager gestartet wurde.  
  
##  <a name="bkmk_create_serrviceapplication"></a>Schritt 3: Erstellen einer Reporting Services-dienstanwendung  
 Dieser Abschnitt enthält die Schritte zum Erstellen einer Dienstanwendung und eine Beschreibung der Eigenschaften, wenn Sie eine vorhandene Dienstanwendung überprüfen.  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie im SharePoint-Menüband auf die Schaltfläche **Neu** .  
  
3.  Klicken Sie im Menü „Neu“ auf **SQL Server Reporting Services-Dienstanwendung**.  
  
    > [!IMPORTANT]  
    >  Wenn die Reporting Services-Option in der Liste nicht angezeigt wird, wird ein **gibt an, dass die freigegebenen von Reporting Services-Dienst ist nicht installiert**. Lesen Sie den vorherigen Abschnitt zur Verwendung von PowerShell-Diensts zum Installieren des Reporting Services-Diensts.  
  
4.  Geben Sie auf der Seite **SQL Server Reporting Services-Dienstanwendung erstellen** einen Namen für die Anwendung ein. Wenn Sie mehrere Reporting Services-Dienstanwendungen erstellen, hilft ein aussagekräftiger Name oder eine Benennungskonvention bei der Organisation von Administrations- und Verwaltungsvorgängen.  
  
5.  Erstellen Sie im Abschnitt **Anwendungspool** einen neuen Anwendungspool für die Anwendung (empfohlen). Die Verwendung des gleichen Namens für den Anwendungspool und die Dienstanwendung kann Ihre laufenden Verwaltungsaufgaben vereinfachen. Die Wahl des Namens kann allerdings auch davon abhängen, wie viele Dienstanwendungen Sie erstellen und ob mehrere Anwendungen in einem einzelnen Anwendungspool verwendet werden müssen. Informieren Sie sich in der SharePoint Server-Dokumentation über Empfehlungen und Best Practices zur Verwaltung von Anwendungspools.  
  
     Wählen Sie ein Sicherheitskonto für den Anwendungspool aus, oder erstellen Sie es. Sie müssen ein Domänenbenutzerkonto angeben. Ein Domänenbenutzerkonto ermöglicht die Verwendung der in SharePoint verfügbaren Funktion "Verwaltetes Konto", mit der Sie Kennwörter und Kontoinformationen zentral aktualisieren können. Domänenkonten sind auch erforderlich, wenn Sie beabsichtigen, die Bereitstellung auf zusätzlichen Dienstinstanzen, die unter der gleichen Identität ausgeführt werden, zu skalieren.  
  
6.  Im **Datenbankserver**können Sie den aktuellen Server verwenden oder einen anderen SQL Server auswählen.  
  
7.  Der Standardwert von **Datenbankname** ist `ReportingService_<guid>`. Dies ist ein eindeutiger Datenbankname. Wenn Sie einen neuen Wert eingeben, geben Sie einen eindeutigen Wert ein. Dies ist die neue Datenbank, die speziell für die Dienstanwendung erstellt werden soll.  
  
8.  Der Standardwert unter **Datenbankauthentifizierung**lautet Windows-Authentifizierung. Wenn Sie **SQL-Authentifizierung**auswählen, finden Sie in der SharePoint-Dokumentation bewährte Methoden zur Verwendung dieses Authentifizierungstyps in einer SharePoint-Bereitstellung.  
  
9. Wählen Sie im Abschnitt **Webanwendungszuordnungen** die Webanwendung aus, die für Zugriff von der aktuellen Reporting Services-Dienstanwendung bereitgestellt werden soll. Sie können einer Webanwendung eine Reporting Services-Dienstanwendung zuordnen. Wenn alle aktuellen Webanwendungen bereits einer Reporting Services-Dienstanwendung zugeordnet sind, wird eine Warnmeldung angezeigt.  
  
10. Wählen Sie **OK**.  
  
11. Der Dienstanwendungserstellungsprozess dauert möglicherweise mehrere Minuten. Wenn es vollständig ist, sehen Sie eine Bestätigungsmeldung und einen Link zu einer Seite **Abonnements und Warnungen bereitstellen** . Führen Sie den Bereitstellungsschritt aus, wenn Sie das Reporting Services-Abonnements-Funktion oder die datenwarnungsfunktion verwenden möchten. Weitere Informationen finden Sie unter [Provision Subscriptions and Alerts for SSRS Service Applications](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell-Inhalt") Informationen zur Verwendung von PowerShell zum Erstellen einer Reporting Services-dienstanwendung finden Sie unter:  
  
-   Weitere Informationen finden Sie im Abschnitt [Windows PowerShell-Skript für die Schritte 1 bis 4](#bkmk_full_script).  
  
-   Thema [So erstellen Sie eine Reporting Services-Dienstanwendung mit PowerShell](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)  

##  <a name="bkmk_powerview"></a>Schritt 4: Aktivieren der Power View-websitesammlungsfunktion.

 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], ein Feature von SQL Server 2016 Reporting Services Add-in für [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint-Produkte und stellt eine websitesammlungsfunktion. Das Feature wird für stammwebsitesammlungen und Websitesammlungen erstellt, nachdem Sie das Reporting Services-add-in installiert ist automatisch aktiviert. Wenn Sie die Verwendung von [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]planen, sollten Sie sicherstellen, dass die Funktion aktiviert ist.  
  
 Wenn Sie das Reporting Services-add-in für SharePoint-Produkte nach der Installation von SharePoint-Server installieren, werden anschließend die Berichtsserver-Integrationsfunktion und die Power View-Integrationsfunktion nur für stammwebsitesammlungen aktiviert. Für andere Websitesammlungen müssen Sie die Funktionen manuell aktivieren.  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>So aktivieren oder überprüfen die Power View-websitesammlungsfunktion  
  
1.  Bei folgenden Schritten wird davon ausgegangen, dass die SharePoint-Website für eine Umgebung mit der **Benutzeroberflächenversion**2013 für SharePoint 2013 konfiguriert ist.  
  
     Öffnen Sie die gewünschte SharePoint-Website in Ihrem Browser. Beispiel: http://\<Servername >/Sites/Bi  
  
2.  Wählen Sie **Einstellungen**![SharePoint Einstellungen](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Einstellungen").  
  
3.  Wählen Sie **Websiteeinstellungen**aus.  
  
4.  Wählen Sie in der Gruppe **Websitesammlungsverwaltung** die Option **Websitesammlungsfeatures**aus.  
  
5.  Suchen Sie **Power View-Integrationsfunktion** in der Liste.  
  
6.  Wählen Sie **Aktivieren**aus. Der Funktionsstatus ändert sich in **Aktiv**.  
  
 Diese Prozedur wird pro Websitesammlung abgeschlossen. Weitere Informationen finden Sie unter [Activate the Report Server and Power View Integration Features in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md).  
  
##  <a name="bkmk_full_script"></a>Windows PowerShell-Skript für die Schritte 1 bis 4  
 Das PowerShell-Skript in diesem Abschnitt entspricht dem Abschluss der Schritte 1 bis 4 in den vorangegangenen Schritten. Das Skript führt folgende Schritte aus:  
  
-   Reporting Services-Dienst und -Dienstproxy installiert und startet den Dienst.  
  
-   Ein neuer Proxy namens Reporting Services wird erstellt.  
  
-   Erstellt eine Reporting Services-dienstanwendung mit dem Namen "Reporting Services Application".  
  
-   Die [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Funktion für eine Websitesammlung wird aktiviert.  
  
 Parameter  
  
-   Aktualisieren Sie den Parameter **-Account** für den Dienstproxy. Dabei muss es sich um ein verwaltetes Dienstkonto in der SharePoint-Farm handeln. Weitere Informationen finden Sie im SharePoint-Thema [Planen von Administrator- und Dienstkonten in SharePoint 2013](http://technet.microsoft.com/library/cc263445.aspx).  
  
-   Aktualisieren Sie den **–DatabaseServer** -Parameter für die Dienstanwendung. Dieser Parameter entspricht der Instanz des Datenbankmoduls.  
  
-   Aktualisieren Sie den **–url** -Parameter der Site, für die die [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Funktion aktiviert werden soll.  
  
 **So verwenden Sie das Skript**  
  
1.  Öffnen Sie Windows PowerShell mit Administratorrechten.  
  
2.  Kopieren Sie folgenden Code in das Skriptfenster.  
  
3.  Aktualisieren Sie die drei im vorherigen Abschnitt beschriebenen Parameter, und führen Sie dann das Skript aus.  
  
```  
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell –EA 0  
  
Write-Host -ForegroundColor Green "Install SSRS Service and Service Proxy, and start the service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
    Write-Host -ForegroundColor Green "Install the Reporting Services Shared Service"  
    Install-SPRSService  
  
    Write-Host -ForegroundColor Green " Install the Reporting Services Service Proxy"  
    Install-SPRSServiceProxy  
  
    # Get the ID of the RS Service Instance and start the service   
    Write-Host -ForegroundColor Green "Start the Reporting Services Service"  
    $RS = Get-SPServiceInstance | Where {$_.TypeName -eq "SQL Server Reporting Services Service"}  
    Start-SPServiceInstance -Identity $RS.Id.ToString()  
  
    # Wait for the Reporting Services Service to start...  
    $Status = Get-SPServiceInstance $RS.Id.ToString()  
    While ($Status.Status -ne "Online")  
    {  
        Write-Host -ForegroundColor Green "SSRS Service Not Online...Current Status = " $Status.Status  
        Start-Sleep -Seconds 2  
        $Status = Get-SPServiceInstance $RS.Id.ToString()  
    }  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Create a new application pool and Reporting Services service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Write-Host -ForegroundColor Green "Create a new application pool"  
#!!!! update "-Account" with an existing Managed Service Account  
New-SPServiceApplicationPool -Name "Reporting Services" -Account "<domain>\User name>"  
$appPool = Get-SPServiceApplicationPool "Reporting Services"  
  
Write-Host -ForegroundColor Green " Create the Reporting Services Service Application"  
#!!!! Update "-DatabaseServer", an instance of the SQL Server database engine   
$rsService = New-SPRSServiceApplication -Name "Reporting Services Application" -ApplicationPool $appPool -DatabaseName "Reporting_Services_Application" -DatabaseServer "<server name>"  
  
Write-Host -ForegroundColor Green "Create the Reporting Services Service Application Proxy"  
$rsServiceProxy = New-SPRSServiceApplicationProxy -Name "Reporting Services Application Proxy" -ServiceApplication $rsService  
  
Write-Host -ForegroundColor Green "Associate service application proxy to default web site and grant web applications rights to SSRS application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"     
# Associate the Reporting Services Service Applicatoin Proxy to the default web site...  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $rsServiceProxy  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url http://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url http://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy  
  
```  
  
##  <a name="bkmk_additional_config"></a>Zusätzliche Konfiguration  
 In diesem Abschnitt werden zusätzliche Konfigurationsschritte beschrieben, die in den meisten SharePoint-Bereitstellungen wichtig sind.  
  
###  <a name="bkmk_configure_ECS"></a> Konfigurieren von Excel Services und PowerPivot  
 Wenn Sie Power View-Berichte von [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] in einer Excel 2016- oder Excel 2013-Arbeitsmappe in SharePoint anzeigen möchten, muss Excel Services für die Verwendung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Servers im Power Pivot-Modus konfiguriert werden. 
 
 Für SharePoint 2016 muss ein [Office Online Server](https://technet.microsoft.com/library/jj219456\(v=office.16\).aspx) konfiguriert werden, um Excel Services verwenden zu können. Weitere Informationen finden Sie in den folgenden Whitepapers.
 
 - [Bereitstellen von SQL Server 2016 PowerPivot und Power View in SharePoint 2016](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
 
 - [Bereitstellen von SQL Server 2016 PowerPivot und Power View in einer Multi-Tier SharePoint 2016-Farm](../../analysis-services/instances/install-windows/deploy-powerpivot-and-power-view-multi-tier-sharepoint-2016-farm.md)
 
 Für SharePoint 2016 müssen Sie eine Excel Services-Anwendung erstellen und konfigurieren. Weitere Informationen finden Sie unter den folgenden Links:  
  
-   Abschnitt „Konfigurieren von Excel Services für die Analysis Services-Integration“ in [Installieren von Analysis Services im Power Pivot-Modus](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
-   [Verwalten von Einstellungen für das Excel Services-Datenmodell (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780.aspx).  

Darüber hinaus muss Sicherheitskonto für den Anwendungspool verwendet wird, von der Reporting Services-dienstanwendung ein Administrator auf dem Analysis Services-Server.
  
###  <a name="bkmk_provision_agent"></a>Bereitstellen von Abonnements und Warnungen  
 Das Reporting Services-Abonnement und-datenwarnungen Daten möglicherweise die Konfiguration von SQL Server-Agent-Berechtigungen. Wenn eine Fehlermeldung darauf hinweist, dass SQL Server-Agent erforderlich ist, Sie jedoch sichergestellt haben, dass SQL Server-Agent gestartet wurde, müssen Sie die Berechtigungen aktualisieren. Sie können auf der Seite mit der Erfolgsmeldung nach der Dienstanwendungserstellung auf den Link **Abonnements und Warnmeldungen bereitstellen** klicken, um eine andere Seite für die SQL Server-Agent-Bereitstellung aufzurufen. Der Bereitstellungsschritt ist erforderlich, wenn die Bereitstellung über mehrere Computer erfolgt (wenn sich z. B. die SQL Server-Datenbankinstanz auf einem anderen Computer befindet). Weitere Informationen finden Sie unter [Bereitstellen von Abonnements und Warnungen für SSRS-Dienstanwendungen](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md).  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>Konfigurieren von E-mail für SSRS-dienstanwendungen  
 Die Reporting Services--datenwarnungsfunktion sendet Warnungen in e-Mail-Nachrichten. Zum Senden von E-mail müssen Sie möglicherweise die Reporting Services-dienstanwendung konfigurieren, und Sie müssen möglicherweise die e-Mail-übermittlungserweiterung für die dienstanwendung zu ändern. Wenn Sie die e-Mail-übermittlungserweiterung für die Reporting Services-Abonnement-Funktion verwenden möchten, müssen die e-Mail-Einstellungen. Weitere Informationen finden Sie unter [Konfigurieren von E-mail für eine Reporting Services-Dienstanwendung &#40; SharePoint 2013 und SharePoint 2016 &#41; ](http://msdn.microsoft.com/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f). 
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>Hinzufügen von Reporting Services-Inhaltstypen zu Inhaltsbibliotheken  
 Reporting Services stellt vordefinierte Inhaltstypen, die zum Verwalten freigegebener Datenquellendateien (rsds), Berichtsmodelle (SMDL) und Berichtsgenerator-Berichtsdefinitionsdateien (RDL) verwendet werden. Wenn einer Bibliothek ein Inhaltstyp ( **Berichts-Generator-Bericht**, **Berichtsmodell**und **Berichtsdatenquelle** ) hinzugefügt wird, wird der Befehl **Neu** aktiviert, sodass Sie neue Dokumente des betreffenden Typs erstellen können. Weitere Informationen finden Sie unter [Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
### <a name="activate-the-report-server-file-sync-feature"></a>Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien  
 Wenn Benutzer häufig veröffentlichte Berichtselemente direkt in SharePoint-Dokumentbibliotheken hochladen, ist die Funktion zur **Synchronisierung der Berichtsserverdateien** auf Websiteebene hilfreich. Die Dateisynchronisierungsfunktion synchronisiert den Berichtsserverkatalog regelmäßiger mit Elementen in Dokumentbibliotheken. Weitere Informationen finden Sie unter [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md).  
  
##  <a name="bkmk_verify_installation"></a> Überprüfen der Installation  
 Im folgenden werden Schritte und Verfahren, um zu überprüfen, ob die Reporting Services SharePoint-Modus-Bereitstellung vorgeschlagen.  
  
-   Weitere Informationen finden Sie im SharePoint-Abschnitt im Thema zur Bereitstellung [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
-   Erstellen Sie in einer SharePoint-Dokumentbibliothek einen grundlegenden Reporting Services-Bericht, der nur ein Textfeld, z. B. einen Titel enthält. Der Bericht enthält keine Datenquellen oder Datasets. Ziel ist es, zu überprüfen, ob Sie den Berichts-Generator öffnen und einen grundlegenden Bericht erstellen und in der Vorschau anzeigen können.  
  
     Speichern Sie den Bericht in der Dokumentbibliothek, und führen Sie den Bericht dann aus der Bibliothek heraus aus. Weitere Informationen zum Erstellen von Berichten mit dem Berichts-Generator finden Sie unter [Starten des Berichts-Generators (Berichts-Generator)](http://technet.microsoft.com/library/ms159221.aspx).  
  
## <a name="next-steps"></a>Nächste Schritte

[PowerShell-Cmdlets für SharePoint-Modus von Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
[Aktualisieren und Migrieren von Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Editionen und unterstützten Funktionen von SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)   
[Reporting Services-SharePoint-Dienst und -Dienstanwendungen](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

