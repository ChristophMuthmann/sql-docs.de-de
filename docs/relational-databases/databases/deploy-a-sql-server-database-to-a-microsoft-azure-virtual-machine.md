---
title: Bereitstellen einer SQL Server-Datenbank auf einem virtuellen Microsoft Azure-Computer | Microsoft-Dokumentation
ms.date: 07/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.deploymentwizard.deploymentsettings.f1
- sql13.swb.deploymentwizard.sourcesettings.f1
- sql13.swb.deploymentwizard.summary.f1
- sql13.swb.agdashboard.agp9virtualnw.issues.f1
- sql13.swb.deploymentwizard.f1
- sql13.swb.deploymentwizard.progress.f1
- sql13.swb.usevmdialog.f1
- sql13.swb.newvmdialog.f1
- sql13.swb.sqlvmdialog.f1
- sql13.swb.deploymentwizard.results.f1
- sql13.swb.deploymentwizard.azuresignin.f1
helpviewer_keywords:
- Deploy a database
- Deploy to Azure VM
- Migrate to Azure
- Windows Azure virtual machine
- Migrate to Azure VM
- Migrate to the cloud
- SQL Server Management Studio
- SSMS
- Deploy database wizard
- Deploy a SQL Server database to Azure
- Azure VM
ms.assetid: 5e82e66a-262e-4d4f-aa89-39cb62696d06
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2aca87c0050dd501c73bb4da8953a93bf40c0c8e
ms.lasthandoff: 04/11/2017

---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>Bereitstellen einer SQL Server-Datenbank auf einem virtuellen Microsoft Azure-Computer
  Verwenden Sie den Assistenten **Datenbank auf Microsoft Azure-VM bereitstellen** , um eine Datenbank von einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem virtuellen Microsoft Azure-Computer (VM) bereitzustellen. Der Assistent führt eine vollständige Datenbanksicherung durch und kopiert somit immer das vollständige Datenbankschema und alle Daten einer SQL Server-Benutzerdatenbank. Der Assistent übernimmt außerdem die gesamte Azure-VM-Konfiguration, sodass keine Vorkonfiguration der VM erforderlich ist.  
  
 Sie können den Assistenten nicht für differenzielle Sicherungen verwenden. Der Assistent überschreibt keine vorhandene Datenbank, die denselben Datenbanknamen hat. Um eine vorhandene Datenbank auf der VM zu ersetzen, müssen Sie zuerst die vorhandene Datenbank löschen oder den Datenbanknamen ändern. Falls ein Namenskonflikt zwischen dem Datenbanknamen eines aktiven Bereitstellungsvorgangs und dem einer vorhandenen Datenbank auf der VM auftritt, schlägt der Assistent ein Namenssuffix für den Namen der bereitzustellenden Datenbank vor, sodass der Vorgang erfolgreich abgeschlossen werden kann.  
  
-   [Vorbereitungen](#before_you_begin)  
  
-   [Einschränkungen](#limitations)  
  
-   [Überlegungen zur Bereitstellung einer FILESTREAM-aktivierten Datenbank](#filestream)  
  
-   [Überlegungen zur geografischen Verteilung von Ressourcen](#geography)  
  
-   [Konfigurationseinstellungen des Assistenten](#configuration_settings)  
  
-   [Erforderliche Berechtigungen](#permissions)  
  
-   [Starten des Assistenten](#launch_wizard)  
  
-   [Assistentenseiten](#wizard_pages)  
  
> [!NOTE]  
>  Eine ausführliche exemplarische Schritt-für-Schritt-Vorgehensweise zu diesem Assistenten finden Sie unter [Migrieren einer SQL Server-Datenbank zu SQL Server auf einem virtuellen Azure-Computer](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-migrate-onpremises-database/)  
  
##  <a name="before_you_begin"></a> Vorbereitungen  
 Für diesen Assistenten sind die folgenden Informationen und Konfigurationseinstellungen verfügbar sein:  
  
-   Die Microsoft-Kontodetails, die dem Windows Azure-Abonnement zugeordnet sind.  
  
-   Ihr Windows Azure-Veröffentlichungsprofil.  
  
    > [!CAUTION]  
    >  SQL Server unterstützt derzeit die Version 2.0 des Veröffentlichungsprofils. Weitere Informationen zum Herunterladen der unterstützten Version des Veröffentlichungsprofils finden Sie unter [Herunterladen des Veröffentlichungsprofils 2.0](http://go.microsoft.com/fwlink/?LinkId=396421).  
  
-   Das Verwaltungszertifikat wurde in das Microsoft Azure-Abonnement hochgeladen.  Erstellen Sie das Verwaltungszertifikat mit dem Powershell-Cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/library/hh848633(v=wps.630)).  Laden Sie das Verwaltungszertifikat anschließend in Ihr Microsoft Azure-Abonnement hoch.  Weitere Informationen zum Hochladen von Verwaltungszertifikaten finden Sie unter [Hochladen eines Verwaltungszertifikats für die Azure-Verwaltung-API](https://azure.microsoft.com/en-us/documentation/articles/azure-api-management-certs/).  Beispielsyntax zum Erstellen eines Verwaltungszertifikats aus [Übersicht über Zertifikate für Azure Cloud Services](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-certs-create/): 

    ```powershell  
    $cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
    $password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
    Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
    ```    

    > [!NOTE]  
    > Das MakeCert-Tool kann ebenfalls zum Erstellen eines Verwaltungszertifikats verwendet werden; MakeCert ist allerdings mittlerweile veraltet.  Weitere Informationen finden Sie unter [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968).
   
  -   Das Verwaltungszertifikat wurde im persönlichen Zertifikatspeicher auf dem Computer gespeichert, auf dem der Assistent ausgeführt wird.  
  
-   Ein temporärer Speicherort muss für den Computer verfügbar sein, auf dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank gehostet wird. Der temporäre Speicherort muss zudem auch für den Computer verfügbar sein, auf der der Assistent ausgeführt wird.  
  
-   Wenn Sie die Datenbank auf einer vorhandenen virtuellen Maschine bereitstellen, muss die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für das Abhören eines TCP/IP-Ports konfiguriert werden.  
  
-   Für die Microsoft Azure-VM oder das Katalog-Image, das Sie für die Erstellung der VM verwenden möchten, muss der [Cloud-Adapter für SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877) konfiguriert sein und ausgeführt werden.  
  
-   Sie müssen einen geöffneten Endpunkt für den [Cloud-Adapter für SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877) auf dem Microsoft Azure-Gateway mit privatem Port 11435 festlegen.  
  
 Wenn Sie planen, Ihre Datenbank in einer vorhandenen Windows Azure-VM bereitzustellen, sind zudem die folgenden Informationen erforderlich:  
  
-   Der DNS-Name des Cloud-Diensts, der die VM hostet.  
  
-   Administrator-Anmeldeinformationen für die VM.  
  
-   Anmeldeinformationen mit Sicherungsoperatorprivilegien für die bereitzustellende Datenbank, aus der Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Weitere Informationen zum Ausführen von SQL Server auf virtuellen Microsoft Azure-Computern finden Sie unter [Bereitstellen eines virtuellen Computers mit SQL Server im Azure-Portal](https://msdn.microsoft.com/library/dn133141.aspx) und [Migrieren einer SQL Server-Datenbank zu SQL Server auf einem virtuellen Azure-Computer](http://msdn.microsoft.com/library/dn133142.aspx).  
  
 Auf Computern, auf denen ein Windows Server-Betriebssystem ausgeführt wird, müssen Sie zur Ausführung dieses Assistenten die folgenden Konfigurationseinstellungen vornehmen:  
  
-   Deaktivieren Sie die verstärkte Sicherheitskonfiguration: Wählen Sie „Server-Manager > Lokaler Server“, und geben Sie für „Verstärkte Sicherheitskonfiguration für Internet Explorer“ den Wert **AUS** an.  
  
-   Aktivieren Sie JavaScript: Internet Explorer > Internetoptionen > Sicherheit > Stufe anpassen > Skripting > Active Scripting: **Aktivieren**.  
  
###  <a name="limitations"></a> Einschränkungen  
Dieses Bereitstellungsfeature funktioniert nur mit einem Azure Storage-Konto, das über das Dienstverwaltungs-Bereitstellungsmodell (klassisch) erstellt wurde. Weitere Informationen zu Azure-Bereitstellungsmodellen finden Sie unter [Azure Resource Manager-Bereitstellung im Vergleich zur klassischen Bereitstellung: Grundlegendes zu Bereitstellungsmodellen und zum Status von Ressourcen](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/).

 Die Datenbankgröße für diesen Vorgang ist auf 1 TB beschränkt.  
  
 Dieses Bereitstellungsfeature ist in SQL Server Management Studio für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]verfügbar.  
  
 Diese Bereitstellungsfunktion ist nur für die Verwendung mit Benutzerdatenbanken vorgesehen. Das Bereitstellen von Systemdatenbanken wird nicht unterstützt.  
  
 Die Bereitstellungsfunktion unterstützt keine gehosteten Dienste, die einer Affinitätsgruppe zugeordnet sind. Beispielsweise können Speicherkonten, die einer Affinitätsgruppe zugeordnet sind, nicht auf der Seite **Bereitstellungseinstellungen** dieses Assistenten nicht zur Verwendung ausgewählt werden.  
  
 Die folgenden SQL Server-Datenbank-Versionen können mit diesem Assistenten in einer Windows Azure-VM bereitgestellt werden:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 In einer Windows Azure-VM ausgeführte SQL Server-Datenbankversionen können wie folgt bereitgestellt werden:  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Falls ein Namenskonflikt zwischen dem Datenbanknamen eines aktiven Bereitstellungsvorgangs und dem einer vorhandenen Datenbank auf der VM auftritt, schlägt der Assistent ein Namenssuffix für den Namen der bereitzustellenden Datenbank vor, sodass der Vorgang erfolgreich abgeschlossen werden kann.  
  
###  <a name="filestream"></a> Überlegungen zur Bereitstellung einer FILESTREAM-aktivierten Datenbank in einer Azure-VM  
 Beachten Sie die folgenden Richtlinien und Einschränkungen, wenn Sie Datenbanken bereitstellen, in denen BLOBs in FILESTREAM-Objekten gespeichert sind:  
  
-   Die Bereitstellungsfunktion kann eine FILESTREAM-aktivierte Datenbank nicht in einer neuen VM bereitstellen. Wenn FILESTREAM vor dem Ausführen des Assistenten in der VM nicht aktiviert wurde, schlägt der Vorgang zur Datenbankwiederherstellung fehl, und der Assistentenvorgang kann nicht erfolgreich abgeschlossen werden. Um eine Datenbank, die FILESTREAM verwendet, erfolgreich bereitzustellen, aktivieren Sie FILESTREAM in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf der Host-VM, bevor Sie den Assistenten starten. Weitere Informationen finden Sie unter [FILESTREAM (SQL Server)](http://msdn.microsoft.com/library/gg471497.aspx).  
  
-   Wenn die Datenbank In-Memory OLTP verwendet, können Sie die Datenbank ohne Änderungen an der Datenbank in einer Azure-VM bereitstellen. Weitere Informationen finden Sie unter [In-Memory OLTP (Speicheroptimierung)](http://msdn.microsoft.com/library/dn133186\(SQL.120\).aspx).  
  
###  <a name="geography"></a> Überlegungen zur geografischen Verteilung von Ressourcen  
 Beachten Sie, dass sich die folgenden Ressourcen in der gleichen geografischen Region befinden müssen:  
  
-   Cloud-Dienst  
  
-   VM-Speicherort  
  
-   Datenträgerspeicherdienst  
  
 Wenn sich die oben genannten Ressourcen nicht in derselben Region befinden, kann der Assistent nicht erfolgreich abgeschlossen werden.  
  
###  <a name="configuration_settings"></a> Konfigurationseinstellungen des Assistenten  
 Verwenden Sie die folgenden Konfigurationsdetails, um die Einstellungen für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankbereitstellung in einer Azure-VM zu ändern.  
  
-   **Standardpfad für die Konfigurationsdatei** – %LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM\DeploymentSettings.xml  
  
-   **Struktur der Konfigurationsdatei**  
  
    -   \<DeploymentSettings>  
  
        -   <OtherSettings  
  
            -   TraceLevel="Debug" \<!-- Protokolliergrad -->  
  
            -   BackupPath="\\\\[server name]\\[volume]\\" \<!-- Der zuletzt verwendete Pfad für die Sicherung. Wird als Standard im Assistenten verwendet. -->  
  
            -   CleanupDisabled = False /> \<!-- Der Assistent löscht keine Zwischendateien und Microsoft Azure-Objekte (VM, CS, SA). -->  
  
        -   <PublishProfile \<!-- Die zuletzt verwendeten Veröffentlichungsprofilinformationen. -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- Das Zertifikat für die Verwendung im Assistenten. -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- Das Abonnement für die Verwendung im Assistenten. -->  
  
            -   Name="Mein Abonnement" \<!-- Der Name des Abonnements. -->  
  
            -   Publisher="" />  
  
    -   \</DeploymentSettings>  
  
 **Konfigurationsdateiwerte**  
  
###  <a name="permissions"></a> Berechtigungen  
 Die bereitzustellende Datenbank muss sich in einem normalen Status befinden. Außerdem muss das Benutzerkonto, über das der Assistent ausgeführt wird, Zugriff auf die Datenbank haben und über die Berechtigung verfügen, einen Sicherungsvorgang auszuführen.  
  
##  <a name="launch_wizard"></a> Verwenden des Assistenten zur Datenbankbereitstellung auf Microsoft Azure-VM  
 **Gehen Sie folgendermaßen vor, um den Assistenten zu starten:**  
  
1.  Verbinden Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe von SQL Server Management Studio mit der bereitzustellenden Datenbank.  
  
2.  Erweitern Sie im **Objekt-Explorer**den Instanznamen und dann den Knoten **Datenbanken** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, die Sie bereitstellen möchten, wählen Sie **Tasks**und dann **Datenbank in Microsoft Azure-VM bereitstellen**aus.  
  
##  <a name="wizard_pages"></a> Assistentenseiten  
 Die folgenden Abschnitte enthalten zusätzliche Informationen zur Bereitstellungseinstellungen und Konfigurationsdetails für diesen Vorgang.  
  
-   [Einführung](#Introduction)  
  
-   [Quelleinstellungen](#Source_settings)  
  
-   [Windows Azure-Anmeldung](#Azure_sign-in)  
  
-   [Bereitstellungseinstellungen](#Deployment_settings)  
  
-   [Zusammenfassung](#Summary)  
  
-   [Ergebnisse](#Results)  
  
##  <a name="Introduction"></a> Einführung 
 Auf dieser Seite wird der Assistent **Datenbank auf Microsoft Azure-VM bereitstellen** beschrieben.  
  
-   **Diese Seite nicht mehr anzeigen.**  
  Aktivieren Sie dieses Kontrollkästchen, damit die Einführungsseite in Zukunft nicht mehr angezeigt wird.  
  
-   **Weiter**  
Schreitet zur Seite **Quelleinstellungen** fort.  
  
-   **Abbrechen**  
  Bricht den Vorgang ab und schließt den Assistenten.  
  
-   **Hilfe**  
Startet das MSDN-Hilfethema für den Assistenten.  
  
##  <a name="Source_settings"></a> Quelleinstellungen  
 Auf dieser Seite stellen Sie eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, die die Datenbank hostet, die Sie in der Microsoft Azure-VM bereitstellen möchten. Hier geben Sie zudem einen temporären Speicherort für die Speicherung der Dateien auf dem lokalen Computer, bevor sie mit Microsoft Azure übertragen werden. Dies kann ein freigegebener Netzwerkspeicherort sein.  
 
- **SQL Server**    
Klicken Sie auf **Verbinden** und geben Sie Verbindungsdetails für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, die die bereitzustellende Datenbank hostet.  
  
-   **Datenbank auswählen**  
Wählen Sie in der Dropdownliste die Datenbank aus, die bereitgestellt werden soll.  
  
-   **Weitere Einstellungen**  
Geben Sie in dem Feld einen freigegebenen Ordner an, auf den der Microsoft Azure-VM-Dienst zugreifen kann.  
  
##  <a name="Azure_sign-in"></a> Microsoft Azure-Anmeldung  
 Melden Sie sich bei Microsoft Azure mit Ihrem Microsoft-Konto oder Unternehmenskonto an. Ihr Microsoft- oder Unternehmenskonto hat das Format einer E-Mail-Adresse wie z.B. patc@contoso.com. Weitere Informationen zu Azure-Anmeldeinformationen finden Sie unter [Microsoft-Konto für Organisationen – Häufig gestellte Fragen](http://technet.microsoft.com/jj592903) und [Behandeln von Problemen](https://technet.microsoft.com/dn197220).  
  
##  <a name="Deployment_settings"></a> Bereitstellungseinstellungen
 Auf dieser Seite können Sie den Zielserver angeben sowie Details zur neuen Datenbank bereitstellen.  
  
 **Virtueller Microsoft Azure-Computer**  
  
-   **Name des Clouddiensts**  
Geben Sie den Namen des Diensts an, der die VM hostet. Um einen neuen Clouddienst zu erstellen, geben Sie einen Namen für den neuen Clouddienst an.  
  
-   **Name der virtuellen Machine** Geben Sie den Namen der VM an, die die SQL Server-Datenbank hostet. Um eine neue Microsoft Azure-VM zu erstellen, geben Sie einen Namen für die neue VM an.  
  
-   **Speicherkonto**  
Wählen Sie aus der Dropdownliste das Speicherkonto aus. Um ein neues Speicherkonto zu erstellen, geben Sie einen Namen für das neue Konto an. Beachten Sie, dass Speicherkonten, die einer Affinitätsgruppe zugeordnet sind, nicht in der Dropdownliste verfügbar sind.  

-   **Einstellungen**  
Erstellen Sie über die Schaltfläche „Einstellungen“ eine neue VM, die dann die SQL Server-Datenbank hostet. Wenn Sie eine vorhandene VM verwenden, werden die angegebenen Informationen verwendet, um Ihre Anmeldeinformationen zu authentifizieren.  
  
**Zieldatenbank**
  
-   **Name der SQL-Instanz**  
Verbindungsdetails für den Server.  
  
-   **Datenbankname**  
Bestätigen, oder geben Sie den Namen einer neuen Datenbank an. Wenn der Datenbankname auf der SQL Server-Zielinstanz bereits vorhanden ist, wird empfohlen, einen anderen Datenbanknamen anzugeben.  
  
##  <a name="Summary"></a> Zusammenfassung
 Auf dieser Seite können Sie die für den Vorgang angegebenen Einstellungen überprüfen. Klicken Sie auf **Fertig stellen**, um den Bereitstellungsvorgang mithilfe der angegebenen Einstellungen abzuschließen. Klicken Sie auf **Abbrechen**, um den Bereitstellungsvorgang abzubrechen und den Assistenten zu beenden.  Durch das Klicken auf **Fertig stellen** wird die Seite **Bereitstellungsstatus** geöffnet.  Sie können den Status auch aus der Protokolldatei unter `"%LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM"`ersehen.
  
 Möglicherweise sind manuelle Schritte erforderlich, um Datenbankdetails an die SQL Server-Datenbank auf der Windows Azure-VM bereitzustellen. Diese Schritte werden detailliert für Sie beschriebenen.  
  
##  <a name="Results"></a> Ergebnisse 
 Auf dieser Seite wird angegeben, ob der Bereitstellungsvorgang erfolgreich war oder ob dabei Fehler auftraten, dabei werden die Ergebnisse jeder Aktion angezeigt. Für alle Aktionen, die fehlerhaft waren, wird dies in der Spalte **Ergebnis** entsprechend angezeigt. Klicken Sie auf den Link, um einen Bericht des für diese Aktion aufgetretenen Fehlers anzuzeigen.  
  
 Klicken Sie auf **Fertig stellen** , um den Assistenten zu schließen.  
  
## <a name="see-also"></a>Siehe auch  
 [Cloud-Adapter für SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877)   
 [Datenbank-Lebenszyklusverwaltung](../../relational-databases/database-lifecycle-management.md)   
 [Exportieren einer Datenebenenanwendung](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)   
 [Importieren einer BACPAC-Datei zum Erstellen einer neuen Benutzerdatenbank](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Sichern und Wiederherstellen von Azure SQL-Datenbanken](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [SQL Server-Bereitstellung in Microsoft Azure Virtual Machines](http://msdn.microsoft.com/library/dn133141.aspx)   
 [Vorbereitung auf die Migration zu SQL Server auf Microsoft Azure Virtual Machines](http://msdn.microsoft.com/library/dn133142.aspx)  
  
  

