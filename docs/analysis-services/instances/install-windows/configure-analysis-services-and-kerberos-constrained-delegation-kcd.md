---
title: "Konfigurieren von Analysis Services und eingeschränkte Kerberos-Delegierung (KCD) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0006e143-d3ba-4d10-a415-e42c45e2bb0a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9f1a5ab2c98e45d705be57658238077d88daefb5
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="configure-analysis-services-and-kerberos-constrained-delegation-kcd"></a>Konfigurieren von Analysis Services und der eingeschränkten Kerberos-Delegierung
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Die eingeschränkte Kerberos-Delegierung (Kerberos Constrained Delegation, KCD) ist ein Authentifizierungsprotokoll, das Sie mit der Windows-Authentifizierung konfigurieren können, um die Clientanmeldeinformationen in Ihrer gesamten Umgebung von Dienst zu Dienst zu delegieren. Die KCD erfordert zusätzliche Infrastruktur, z. B. einen Domänencontroller, und eine zusätzliche Konfiguration Ihrer Umgebung. Die KCD wird für verschiedene Szenarios vorausgesetzt, bei denen [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] - und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Daten mit SharePoint 2016 verwendet werden. In SharePoint 2016 wurde Excel Services aus der SharePoint-Farm auf einen getrennten, neuen Server, den sog. **Office Online Server**, ausgelagert. Da der Office Online Server getrennt ist, gibt es vermehrt Bedarf an einer Möglichkeit, Clientanmeldeinformationen in den typischen Szenarien mit zwei Hops zu delegieren.  
  
## <a name="overview"></a>Übersicht  
 Die KCD ermöglicht einem Konto, zum Zweck des Zugriffs auf Ressourcen die Identität eines anderen Kontos anzunehmen. Das Konto, das die Identität annimmt, ist ein einer Webanwendung zugewiesenes Dienstkonto oder das Computerkonto eines Webservers. Das Konto, dessen Identität angenommen wird, ist ein Benutzerkonto, das Zugriff auf Ressourcen benötigt. Die KCD arbeitet auf Dienstebene, sodass ausgewählten Diensten auf einem Server der Zugriff vom Konto, das die Identität annimmt, gewährt wird. Zugleich wird anderen Diensten auf demselben Server bzw. Diensten auf anderen Servern der Zugriff verweigert.  
  
 In den Abschnitten in diesem Thema werden gängige Szenarien mit [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] überprüft, bei denen die KCD erforderlich ist. Außerdem finden Sie ein Beispiel einer Serverbereitstellung samt einer allgemeinen Übersicht über alle Elemente, die Sie installieren und konfigurieren müssen. Im Abschnitt [Weitere Informationen und Community-Inhalte](#bkmk_moreinfo) finden Sie Links zu detaillierten Informationen zu den beteiligten Technologien, wie z.B. Domänencontroller und KCD.  
  
## <a name="scenario-1-workbook-as-data-source-wds"></a>Szenario 1: Arbeitsmappe als Datenquelle  
 ![finden Sie unter 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "finden Sie unter 1") Office Online Server öffnet eine Excel-Arbeitsmappe und ![finden Sie unter 2](../../../analysis-services/instances/install-windows/media/ssas-callout2.png "finden Sie unter 2") erkennt eine Datenverbindung mit einer anderen Arbeitsmappe. Office Online Server sendet eine Anforderung an die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Redirectordienst ![finden Sie unter 3](../../../analysis-services/instances/install-windows/media/ssas-callout3.png "finden Sie unter 3") zum Öffnen der zweiten Arbeitsmappe und die Daten ![finden Sie in 4](../../../analysis-services/instances/install-windows/media/ssas-callout4.png "finden Sie in 4 ").  
  
 In diesem Szenario müssen Anmeldeinformationen des Benutzers von Office Online Server an den SharePoint [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Redirectordienst in SharePoint delegiert werden.  
  
 ![die Arbeitsmappe als Datenquelle](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-wds.png "Arbeitsmappe als Datenquelle")  
  
## <a name="scenario-2-an-analysis-services-tabular-model-links-to-an-excel-workbook"></a>Szenario 2: Tabellarisches Analysis Services-Modell mit Verbindung mit Excel-Arbeitsmappe  
 Ein tabellarisches Analysis Services-Modell ![finden Sie unter 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "finden Sie unter 1") Links zu einer Excel-Arbeitsmappe, die ein Power Pivot-Modell enthält. Wenn [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in diesem Szenario das tabellarische Modell lädt, erkennt [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] die Verbindung mit der Arbeitsmappe. Bei Verarbeitung des Modells sendet [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] eine Abfrageanforderung an SharePoint, um die Arbeitsmappe zu laden. In diesem Szenario müssen Clientanmeldeinformationen **nicht** von Analysis Services an SharePoint delegiert werden. Eine Clientanwendung kann jedoch die Datenquelleninformationen in einer Out-of-Line-Bindung überschreiben. Wenn die Out-of-Line-Bindungsanforderung angibt, dass die Identität des aktuellen Benutzers angenommen werden soll, müssen die Anmeldeinformationen des Benutzers delegiert werden, wofür die KCD zwischen [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] und SharePoint konfiguriert werden muss.  
  
 ![office online server](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-oos.png "office online server")  
  
## <a name="example-deployment-of-kcd-with-office-online-server-and-analysis-services"></a>Beispielbereitstellung von KCD mit Office Online Server und Analysis Services  
 In diesem Abschnitt wird eine Beispielbereitstellung mit vier Computern beschrieben. In den folgenden Abschnitten werden die wesentlichen Schritte für die Installation und Konfiguration der einzelnen Computer vorgestellt. Bevor Sie mit der Bereitstellung beginnen, sollten Sie die Computer mit den neuesten Patches versehen und die Computernamen kennen, da diese bei einigen Konfigurationsschritten benötigt werden.  
  
-   Domänencontroller  
  
-   SQL Server-Datenbankmodul und Analysis Services im Power Pivot-Modus. Die Instanz des Datenbankmoduls wird für die SharePoint-Inhaltsdatenbank verwendet.  
  
-   SharePoint Server 2016  
  
-   Office Online Server  
  
 ![domain controller](../../../analysis-services/instances/install-windows/media/ssas-kcd-domainserver-icon.png "domain controller")  
  
### <a name="domain-controller"></a>Domänencontroller  
 Es folgt eine Übersicht der Elemente, die für den Domänen installiert werden müssen:  
  
-   **Rolle:** Active Directory-Domänendienste. Eine Übersicht finden Sie unter [Configuring Active Directory (AD DS) in Windows Server 2012](http://sharepointgeorge.com/2012/configuring-active-directory-ad-ds-in-windows-server-2012/)(Konfigurieren von Active Directory-Domänendiensten unter Windows Server 2012).  
  
-   **Rolle:** DNS-Server  
  
-   **Feature:** .NET Framework 3.5-Funktionen /.NET Framework 3.5  
  
-   **Feature:** Remoteserver-Verwaltungstools/Rollenverwaltungstools  
  
-   Konfigurieren Sie Active Directory so, dass eine neue Gesamtstruktur erstellt wird und die Computer der Domäne beitreten. Bevor Sie versuchen, weitere Computer der privaten Domäne hinzuzufügen, müssen Sie das DNS der Clientcomputer mit der IP-Adresse des Domänencontrollers konfigurieren. Führen Sie auf dem Domänencontroller `ipconfig /all` aus, um die IPv4- und IPv6-Adressen für den nächsten Schritt abzurufen.  
  
-   Es wird empfohlen, sowohl IPv4- als auch IPv6-Adressen zu konfigurieren. Dies kann in der Windows-Systemsteuerung erfolgen:  
  
    1.  Klicken Sie auf **Netzwerk- und Freigabecenter**.  
  
    2.  Klicken Sie auf Ihre Ethernet-Verbindung.  
  
    3.  Klicken Sie auf **Eigenschaften**.  
  
    4.  Klicken Sie auf **Internet Protocol Version 6 (TCP/IPv6)**.  
  
    5.  Klicken Sie auf **Eigenschaften**.  
  
    6.  Klicken Sie auf **Die folgenden DNS-Serveradressen verwenden**.  
  
    7.  Geben Sie die mit dem Befehl „ipconfig“ abgerufene IP-Adresse ein.  
  
    8.  Klicken Sie auf die Schaltfläche **Erweitert** , anschließend auf die Registerkarte **DNS** , und überprüfen Sie, ob die DNS-Suffixe ordnungsgemäß sind.  
  
    9. Klicken Sie auf **Diese DNS-Suffixe anhängen**.  
  
    10. Wiederholen Sie die Schritte für IPv4.  
  
-   **Hinweis:** Sie können Computer über die Windows-Systemsteuerung über die Einstellung unter „System“ der Domäne hinzufügen. Weitere Informationen finden Sie unter [How To Join Windows Server 2012 to a Domain](http://social.technet.microsoft.com/wiki/contents/articles/20260.how-to-join-windows-server-2012-to-a-domain.aspx)(Hinzufügen von Windows Server 2012 zu einer Domäne).  
  
 ![SSAS-Server im Powerpivot-Modus](../../../analysis-services/instances/install-windows/media/ssas-kcd-powerpivotserver-icon.png "Ssas-Server im Powerpivot-Modus")  
  
### <a name="2016-sql-server-database-engine-and-analysis-services-in-power-pivot-mode"></a>SQL Server 2016-Datenbankmodul und Analysis Services im Power Pivot-Modus  
 Es folgt eine Übersicht der auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Computer zu installierenden Elemente.  
  
 ![Hinweis](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Hinweis") In der [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Setup-Assistenten [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] in Power Pivot-Modus als Teil des Feature Selection Workflows installiert ist.  
  
1.  Führen Sie den Setup-Assistenten von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] aus, und klicken Sie auf der Seite zur Auswahl von Funktionen auf das Datenbankmodul ( [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]) und die Verwaltungstools. Bei einem späteren Setup können Sie für den Setup-Assistenten den [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Modus für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]angeben.  
  
2.  Konfigurieren Sie für die Instanzkonfiguration eine benannte Instanz von „POWERPIVOT“.  
  
3.  Konfigurieren Sie auf der Seite „Analysis Services-Konfiguration“ den Analysis Services-Server für den **Power Pivot** -Modus, und fügen Sie den **Computernamen** von Office Online Server zur Liste der Analysis Services-Serveradministratoren hinzu. Weitere Informationen finden Sie unter [Install Analysis Services in Power Pivot Mode](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
4.  Beachten Sie, dass der Objekttyp „Computer“ nicht standardmäßig in der Suche enthalten ist. Klicken Sie auf ![klicken Sie auf die Objekte zum Hinzufügen von Konto "Computer"](../../../analysis-services/instances/install-windows/media/ss-objects-button.png "klicken Sie auf die Objekte zum Hinzufügen von Konto "Computer"") zum Hinzufügen der Computer-Objekts.  
  
     ![Hinzufügen von Computerkonten als Administratoren von Ssas](../../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "Hinzufügen von Computerkonten als Administratoren von Ssas")  
  
5.  Erstellen Sie die Dienstprinzipalnamen (Service Principal Names, SPNs) für die Analysis Services-Instanz.  
  
     Es folgen nützliche SPN-Befehle:  
  
    -   Listet den SPN für einen bestimmten Kontonamen auf, unter dem der Dienst von Interesse ausgeführt wird: `SetSPN -l <account-name>`  
  
    -   Legt einen SPN für einen Kontonamen fest, unter dem der Dienst von Interesse ausgeführt wird: `SetSPN -a <SPN> <account-name>`  
  
    -   Löscht einen SPN aus einen bestimmten Kontonamen, unter dem der Dienst von Interesse ausgeführt wird: `SetSPN -D <SPN> <account-name>`  
  
    -   Sucht nach doppelten SPNs: `SetSPN -X`  
  
     Der SPN für die Power Pivot-Instanz hat die folgende Form:  
  
    ```  
    MSSQLSvc.3/\<Fully Qualified Domain Name (FQDN)>:POWERPIVOT  
    MSSQLSvc.3/<NetBIOS Name>:POWERPIVOT  
    ```  
  
     Der vollqualifizierte Domänenname (FQDN) und NetBIOS-Name sind der Name des Computers, auf dem sich die Instanz befindet. Diese SPNs werden für das Domänenkonto angegeben, das als Dienstkonto verwendet wird.  Wenn Sie Netzwerkdienst, „Lokales System“ oder die Dienst-ID verwenden, müssen Sie den SPN für das Domänenkonto des Computers angeben.  Wenn Sie ein Domänenbenutzerkonto verwenden, geben Sie den SPN für dieses Konto an.  
  
6.  Erstellen Sie den SPN für den SQL-Browserdienst auf dem Analysis Services-Computer.  
  
     [Weitere Informationen](https://support.microsoft.com/en-us/kb/950599)  
  
7.  **Konfigurieren Sie Einstellungen für die eingeschränkte Delegierung** für das Analysis Services-Dienstkonto für jede externe Datenquelle, die Sie aktualisieren, z.B. SQL Server oder Excel-Dateien. Für das Analysis Services-Dienstkonto sollte Folgendes festgelegt sein.  
  
     **Hinweis:** Wenn die Registerkarte „Delegierung“ in Active Directory-Benutzer und-Computer nicht für das Konto angezeigt wird, liegt das daran, dass für dieses Konto kein SPN vorhanden ist.  Sie können einen gefälschten SPN wie z.B. `my/spn`hinzufügen, damit sie angezeigt wird.  
  
     **Benutzer bei Delegierungen angegebener Dienste vertrauen** und **Beliebiges Authentifizierungsprotokoll verwenden**.  
  
     Dies wird als eingeschränkte Delegierung bezeichnet und ist erforderlich, da das Windows-Token aus dem C2WTS (Claims to Windows Token Service) stammt, wofür die eingeschränkte Delegierung mit Protokollübergang erforderlich ist.  
  
     ![Analysis Services – eingeschränkte Delegierung](../../../analysis-services/instances/install-windows/media/analysis-services-constrained-delegation.png "Analysis Services – eingeschränkte Delegierung")  
  
     Sie müssen auch die Dienste hinzufügen, an die die Delegierung erfolgt. Dies variiert je nach Ihrer Umgebung.  
  
### <a name="office-online-server"></a>Office Online Server  
  
1.  Installieren von Office Online Server  
  
2.  **Konfigurieren Sie Office Online Server so** , dass eine Verbindung mit dem [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Server hergestellt wird. Beachten Sie, dass das Office Online Server-Computerkonto ein Administratorkonto auf dem [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Server sein muss. Dies ist in einem früheren Abschnitt dieses Themas (Installieren des [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Servers) erfolgt.  
  
    1.  Öffnen Sie auf dem Office Online Server ein PowerShell-Fenster mit Administratorrechten, und führen Sie den folgenden Befehl aus:  
  
    2.  `New-OfficeWebAppsExcelBIServer –ServerId <AS instance name>`  
  
    3.  Beispiel: `New-OfficeWebAppsExcelBIServer –ServerId "MTGQLSERVER-13\POWERPIVOT"`  
  
3.  **Konfigurieren Sie Active Directory so** , dass das Office Online Server-Computerkonto die Identität von Benutzern für das SharePoint-Dienstkonto annehmen kann. Legen Sie daher die Delegierungseigenschaft für den Prinzipal, der den Anwendungspool für SharePoint-Webdienste ausführt, auf den Office Online Server fest. Die PowerShell-Befehle in diesem Abschnitt erfordern die Active Directory PowerShell-Objekte.  
  
    1.  Abrufen der Active Directory-Identität von Office Online Server  
  
        ```  
        $computer1 = Get-ADComputer -Identity [ComputerName]  
        ```  
  
         Bestimmen Sie diesen Prinzipalnamen, indem Sie im Task-Manager unter „Details > Benutzername von W3wp.exe“ nachsehen. Beispiel: SvcSharePoint  
  
        ```  
        Set-ADUser svcSharePoint -PrincipalsAllowedToDelegateToAccount $computer1  
  
        ```  
  
    2.  So überprüfen Sie, ob die Eigenschaft ordnungsgemäß festgelegt wurde  
  
    3.  ```  
        Get-ADUser svcSharePoint –Properties PrincipalsAllowedToDelegateToAccount  
        ```  
  
4.  **Konfigurieren Sie die Einstellungen für die eingeschränkte Delegierung** für das Office Online Server-Konto für die Analysis Services-Power Pivot-Instanz. Dies sollte das Computerkonto sein, unter dem Office Online Server ausgeführt wird. Für das Office Online Server-Dienstkonto sollte Folgendes festgelegt sein.  
  
     **Hinweis:** Wenn die Registerkarte „Delegierung“ in Active Directory-Benutzer und-Computer nicht für das Konto angezeigt wird, liegt das daran, dass für dieses Konto kein SPN vorhanden ist.  Sie können einen gefälschten SPN wie z.B. `my/spn`hinzufügen, damit sie angezeigt wird.  
  
     **Benutzer bei Delegierungen angegebener Dienste vertrauen** und **Beliebiges Authentifizierungsprotokoll verwenden**.  
  
     Dies wird als eingeschränkte Delegierung bezeichnet und ist erforderlich, da das Windows-Token aus dem C2WTS (Claims to Windows Token Service) stammt, wofür die eingeschränkte Delegierung mit Protokollübergang erforderlich ist.  Lassen Sie anschließend die Delegierung für die SPNs „MSOLAPSvc.3“ und „MSOLAPDisco.3“ zu, die wir zuvor erstellt haben.  
  
5.  Einrichten des C2WTS (Claims to Windows Token Service) **Dies ist für Szenario 1 erforderlich**. Weitere Informationen finden Sie unter [Übersicht über Claims to Windows Token Service (C2WTS)](https://msdn.microsoft.com/library/ee517278.aspx).  
  
6.  **Konfigurieren Sie die Einstellungen für die eingeschränkte Delegierung** für das C2WTS-Dienstkonto.  Die Einstellungen müssen mit denen in Schritt 4 übereinstimmen.  
  
 ![SharePoint-Server](../../../analysis-services/instances/install-windows/media/ssas-kcd-sharepointserver-icon.png "Sharepoint-Server")  
  
### <a name="sharepoint-server-2016"></a>SharePoint Server 2016  
 Es folgt eine Übersicht über die SharePoint Server-Installation.  
  
1.  Ausführen des SharePoint-Installationsprogramms  
  
2.  Führen Sie die SharePoint-Installation aus, und wählen Sie die Setuprolle **Einzelne Serverfarm** .  
  
3.  Führen Sie das Power Pivot für SharePoint-Add-In (spPowerPivot16.msi) aus. Weitere Informationen finden Sie unter [installieren oder Deinstallieren des PowerPivot für SharePoint-Add-in (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
4.  Führen Sie den Power Pivot-Konfigurations-Assistenten aus. Weitere Informationen finden Sie unter [PowerPivot-Konfigurationstools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
5.  Verbinden Sie SharePoint mit Office Online Server.    ?? Configure_xlwac_on_SPO.ps1?  
  
6.  Konfigurieren Sie SharePoint-Authentifizierungsanbieter für Kerberos. **Dies ist für Szenario 1 erforderlich**. Weitere Informationen finden Sie unter [Planen der Kerberos-Authentifizierung in SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).  
  
##  <a name="bkmk_moreinfo"></a> Weitere Informationen und Community-Inhalte  
 [Kerberos for the Busy Admin (Kerberos für ausgelastete Administratoren)](http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx)  
  
 [Understanding Kerberos Double Hop (Grundlegendes zum Kerberos-Doppel-Hop)](http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx)  
  
 [ALL things .Net and SharePoint (Alles Wissenswerte zu .NET und SharePoint)](http://sbrickey.com/Tech/Blog/Post/Kerberos_Primer)  
  
 [Resource Based Kerberos Constrained Delegation (Ressourcenbasierte eingeschränkte Kerberos-Delegierung)](http://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)  
  
 [KERBEROS-Grundlagen – Videos](http://blog.martinlund.it/kerberos-primer/)  
  
 [Microsoft Kerberos-Konfigurations-Manager für Microsoft SQL Server](http://www.microsoft.com/en-us/download/details.aspx?id=39046)  
  
  
