---
title: Problembehandlung bei einer Installation von Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2536f7f-d90c-4571-9ffd-6bbfe69018d6
caps.latest.revision: 16
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 79d064c7ddb43531fdff086eda71ba1e28d71fd6
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---

# <a name="troubleshoot-a-reporting-services-installation"></a>Problembehandlung für eine Reporting Services-Installation

  Wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aufgrund von Fehlern während der Ausführung von Setup nicht installieren können, können Sie mithilfe der Anweisungen in diesem Thema die häufigsten Ursachen von Installationsfehlern behandeln.  
  
 Informationen zu anderen Fehlern und Problemen, die sich auf [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] beziehen, finden Sie unter [Beheben von SSRS-Problemen und Fehlern](http://social.technet.microsoft.com/wiki/contents/articles/ssrs-troubleshooting-issues-and-errors.aspx)  
  
 Lesen Sie die [Onlinehinweise zu dieser Version](http://go.microsoft.com/fwlink/?linkid=236893) , wenn das aufgetretene Problem in den Versionshinweisen beschrieben wird.  
  
##  <a name="bkmk_setuplogs"></a> Überprüfen von Setupprotokollen  
 Setupfehler werden in Protokolldateien im Ordner **[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Setup Bootstrap\Log** aufgezeichnet. Wenn Sie Setup ausführen, wird ein Unterordner erstellt. Der Name des Unterordners entspricht dem Datum und der Uhrzeit der Ausführung von Setup. Informationen zum Anzeigen der Setupprotokolldateien finden Sie unter [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
-   Die Protokolldateien enthalten eine Auflistung von Dateien.  
  
-   Öffnen Sie die Datei * _summary.txt, um Informationen über Produkt, Komponente und Instanz anzuzeigen.  
  
-   Öffnen Sie die Datei * _errorlog.txt, um Informationen zu Fehlern während der Ausführung von Setup anzuzeigen.  
  
-   Öffnen Sie *_RS\_\*_ComponentUpdateSetup.log, um Setupinformationen für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anzuzeigen.  
  
##  <a name="bkmk_prereq"></a> Überprüfen von Voraussetzungen  
 Die Voraussetzungen werden von Setup automatisch überprüft. Wenn Sie Setupprobleme behandeln möchten, ist es jedoch hilfreich, zu wissen, welche Voraussetzungen von Setup überprüft werden.  
  
-   Zu den Kontoanforderungen für die Ausführung von Setup gehört die Mitgliedschaft in der lokalen Gruppe Administratoren. Setup muss über die Berechtigung zum Hinzufügen von Dateien und Registrierungseinstellungen sowie zum Erstellen von lokalen Sicherheitsgruppen und zum Festlegen von Berechtigungen verfügen. Beim Installieren einer Standardkonfiguration muss das Setup die Berechtigung zum Erstellen einer Berichtsserver-Datenbank auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, auf der die Installation durchgeführt wird, aufweisen.  
  
-   HTTP.SYS 1.1 muss vom Betriebssystem unterstützt werden.  
  
-   Der HTTP-Dienst muss aktiviert sein und ausgeführt werden.  
  
-   Wenn Sie auch den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst installieren, ist eine Ausführung von Distributed Transaction Coordinator (DTC) erforderlich.  
  
-   Der Ordner System32 muss die Datei Authz.dll enthalten.  
  
 Setup führt keine Überprüfung für Internet Information Services (IIS) oder [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]mehr durch. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]erfordert MDAC 2.0 und die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Version 2.0; Setup installiert diese, wenn sie nicht bereits installiert sind.  
  
##  <a name="bkmk_tshoot_sharepoint"></a> Problembehandlung von Installationen im SharePoint-Modus  
  
-   [Reporting Services-Konfigurations-Manager startet nicht.](#bkmk_configmanager_notstart)  
  
-   [Nach der Installation von SQL Server 2016 SSRS im SharePoint-Modus wird der SQL Server Reporting Services-Dienst nicht in der SharePoint-Zentraladministration angezeigt.](#bkmk_no_ssrs_service)  
  
-   [PowerShell-Cmdlets für Reporting Services sind nicht verfügbar, und Befehle werden nicht erkannt.](#bkmk_cmdlets_not_recognized)  
  
-   [Sie sehen eine Fehlermeldung, die angibt, dass die URL nicht konfiguriert ist](#bkmk_URL_not_configured)  
  
-   [Setup erzeugt einen Fehler, wenn SharePoint auf einem Computer zwar installiert, aber nicht konfiguriert ist.](#bkmk_sharepoint_not_confiugred)  
  
-   [Die Seite der SharePoint-Zentraladministration ist leer.](#bkmk_central_admin_blank)  
  
-   [Eine Fehlermeldung wird angezeigt, wenn Sie versuchen, einen neuen Bericht mit dem Berichts-Generator zu erstellen.](#bkmk_reportbuilder_newreport_error)  
  
-   [Eine Fehlermeldung wird angezeigt, die besagt, dass RS_SHP nicht mit PREPAREIMAGE unterstützt wird.](#bkmk_RS_SHP_notsupported)  

### <a name="bkmk_configmanager_notstart"></a> Reporting Services-Konfigurations-Manager startet nicht.

 **Beschreibung:** dieses Problem ist mit Absicht in SQL Server 2012 und höher. Reporting Services ist für die SharePoint-Dienstarchitektur ausgelegt. Zum Konfigurieren und Verwalten des SharePoint-Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wird der Konfigurations-Manager nicht mehr benötigt.  
  
 **Problemumgehung:** Verwenden Sie zum Konfigurieren eines Berichtsservers im SharePoint-Modus die SharePoint-Zentraladministration. Weitere Informationen finden Sie unter [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beheben von Problemen mit Installationen im SharePoint-Modus](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_no_ssrs_service"></a>Sie den SQL Server Reporting Services-Dienst in der SharePoint-Zentraladministration nicht angezeigt, nach der Installation von SQL Server 2016 SSRS im SharePoint-Modus  
 **Beschreibung:** Wenn nach der erfolgreichen Installation von SQL Server 2016 Reporting Services im SharePoint-Modus und das SQL Server 2016 Reporting Services Add-in für SharePoint 2013/2016 ein, nicht "SQL Server Reporting Services" in den folgenden zwei Menüs angezeigt werden und dann die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Dienst wurde nicht registriert:  
  
-   Klicken Sie auf SharePoint 2013/2016-Zentraladministration > „Anwendungsverwaltung“ > Seite „Dienste auf dem Server verwalten“.  
  
-   Klicken Sie auf SharePoint 2013/2016-Zentraladministration > „Anwendungsverwaltung“ > „Dienstanwendungen verwalten“ > Menü „Neu“.  
  
 **Problemumgehung:** Um die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint Services zu registrieren und zu starten, führen Sie folgende Schritte aus:  
  
1.  Auf dem Computer, auf dem SharePoint 2013/2016-Zentraladministration ausgeführt wird  
  
    1.  Öffnen Sie die SharePoint 2013/2016-Verwaltungsshell mit Administratorberechtigungen. Klicken Sie mit der rechten Maustaste auf das Symbol, und wählen Sie "Als Administrator ausführen". Führen Sie die folgenden drei Cmdlets von der Shell aus:  
  
    2.  ```  
        Install-SPRSService  
        ```  
  
    3.  ```  
        Install-SPRSServiceProxy  
        ```  
  
    4.  ```  
        Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
        ```  
  
2.  Vergewissern Sie sich, dass der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dienst auf der folgenden Seite den Status „**Gestartet**“ aufweist: SharePoint 2013/2016-Zentraladministration > „**Anwendungsverwaltung**“ > „**Dienste auf dem Server verwalten**“.  
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beheben von Problemen mit Installationen im SharePoint-Modus](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_cmdlets_not_recognized"></a> PowerShell-Cmdlets für Reporting Services sind nicht verfügbar, und Befehle werden nicht erkannt.  
 **Beschreibung:** Wenn Sie versuchen, ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -PowerShell-Cmdlet auszuführen, wird eine Fehlermeldung mit etwa folgendem Wortlaut angezeigt:  
  
-   Der Begriff „Install-SPRSServiceInstall-SPRSService“ wurde **nicht** als Name eines Cmdlets, einer Funktion, einer Skriptdatei oder eines ausführbaren Programms erkannt. Überprüfen Sie die Schreibweise des Namens, oder ob der Pfad korrekt ist (sofern enthalten), und wiederholen Sie den Vorgang. In Zeile: 1 char:39+ Install-SPRSServiceInstall-SPRSService <<<<    + CategoryInfo          : ObjectNotFound: (Install-SPRSServiceInstall-SPRSService:String) [], CommandNotFoundExcep  
  
 **Problemumgehung:** Führen Sie einen der folgenden Schritte aus:  
  
-   Führen Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint-Produkte aus. **rssharepoint.msi**.  
  
-   Installieren Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus von den SQL Server-Installationsmedien.  
  
 **Hinweis:** Wenn die **SharePoint 2013/2016-Verwaltungsshell** beim Ausführen einer dieser Problemumgehungen geöffnet ist, schließen Sie die Verwaltungsshell, und öffnen Sie sie erneut.  
  
 Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [Verfügbarkeit des Reporting Services-Add-Ins für SharePoint-Produkte](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Installieren des ersten Berichtsservers im SharePoint-Modus](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538)  
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beheben von Problemen mit Installationen im SharePoint-Modus](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_URL_not_configured"></a> Sie sehen eine Fehlermeldung, die angibt, dass die URL nicht konfiguriert ist  
 **Beschreibung:** Die Fehlermeldung lautet wie folgt:  
  
 Diese SQL Server Reporting Services (SSRS)-Funktionalität wird nicht unterstützt. Verwenden Sie Zentraladministration, um eines oder mehrere der folgenden Probleme zu überprüfen und zu korrigieren:
 
 - Eine Berichtsserver-URL ist nicht konfiguriert. Verwenden Sie die SSRS-Integration-Seite zu ihrer Festlegung.
 
 - Der SSRS-Dienstanwendungsproxy ist nicht konfiguriert. Verwenden Sie die SSRS-Dienstanwendungsseiten, um den Proxy zu konfigurieren.
 
 - Die SSRS-Dienstanwendung ist nicht dieser Webanwendung zugeordnet. Verwenden Sie, die SSRS-Dienstanwendungsseiten, um den Proxy der SSRS-Dienstanwendung der Anwendungsproxygruppe dieser Webanwendung zuzuordnen. 
  
 **Problemumgehung:** Die Fehlermeldung enthält drei vorgeschlagene Schritte, um dieses Problem zu beheben. Der erste Vorschlag in der Meldung "Es wurde keine Berichtsserver-URL konfiguriert..." spielt bei der Integration der früheren Version des Berichtsservers in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]eine wichtige Rolle. Die SharePoint-Konfiguration für die vorherigen Berichtsserverversionen wird auf der Seite **Allgemeine Anwendungseinstellungen** abgeschlossen und verwendet **SQL Server Reporting Services (2008 und 2008 R2)**.  
  
 **Weitere Informationen:** Diese Fehlermeldung wird beim Versuch angezeigt, eine der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen zu verwenden, die eine Verbindung zum [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst erfordern. Dies schließt Folgendes ein:  
  
-   Öffnen von SQL Server-Berichts-Generator von einer SharePoint-Dokumentbibliothek.  
  
-   Verwalten von Abonnements.  
  
-   Verwalten einer Dienstanwendung.  
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beheben von Problemen mit Installationen im SharePoint-Modus](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_sharepoint_not_confiugred"></a> Setup erzeugt einen Fehler, wenn SharePoint auf einem Computer zwar installiert, aber nicht konfiguriert ist.  
 **Beschreibung:** Wenn Sie auswählen, Reporting Services SharePoint-Modus auf einem Computer zu installieren, auf dem SharePoint installiert, aber nicht konfiguriert ist, sehen Sie eine Meldung ähnlich der folgenden, und Setup wird angehalten:  
  
 SQL Server-Setup wird nicht mehr ausgeführt.  
  
 **Problemumgehung:** Konfigurieren Sie SharePoint, und führen Sie dann die SQL Server-Installation aus.  
  
 **Weitere Informationen:** Wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in eine vorhandene SharePoint-Installation installieren, versucht Setup, den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -SharePoint-Dienst zu installieren und zu starten. Wenn SharePoint nicht konfiguriert ist, schlägt die Dienstinstallation fehl, sodass Setup fehlschlägt.  
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beheben von Problemen mit Installationen im SharePoint-Modus](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_central_admin_blank"></a> Die Seite der SharePoint-Zentraladministration ist leer.  
 **Beschreibung:** Sie konnten SharePoint 2013/2016 ohne Installationsfehler erfolgreich installieren. Wenn Sie jedoch zur Zentraladministration wechseln, sehen Sie nur eine leere Seite:  
  
 **Problemumgehung:** Dieses Problem ist nicht typisch für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , bezieht sich jedoch auf die Konfiguration von Berechtigungen in der gesamten SharePoint-Installation. Im Folgenden finden Sie eine Liste mit Vorschlägen:  
  
-   Sehen Sie sich das SharePoint-Thema zu Entwicklungsumgebungen an. [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](https://msdn.microsoft.com/library/ee554869)  
  
-   Lesen Sie den Forumsbeitrag: [Die Zentraladministration gibt nach der Installation unter Windows 7 eine leere Seite zurück](http://social.technet.microsoft.com/Forums/en/sharepoint2010setup/thread/a422a3c8-39f6-4b9e-988a-4c4d1e745694)  
  
-   Das Dienstkonto, das Sie für SharePoint-Dienste verwenden, z.B. der SharePoint 2013/2016-Zentraladministrationsdienst, sollte im lokalen Betriebssystem Administratorprivilegien haben.  
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beheben von Problemen mit Installationen im SharePoint-Modus](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_reportbuilder_newreport_error"></a> Eine Fehlermeldung wird angezeigt, wenn Sie versuchen, einen neuen Bericht mit dem Berichts-Generator zu erstellen.  
 **Beschreibung:** Sie sehen eine Fehlermeldung ähnlich der folgenden, wenn Sie versuchen, in einer Dokumentbibliothek einen Bericht mit dem Berichts-Generator zu erstellen:  
  
 Diese Funktionalität wird nicht unterstützt, da eine SQL Server Reporting Services-Dienstanwendung nicht vorhanden ist, oder eine Berichtsserver-URL wurde nicht in der Zentraladministration konfiguriert.  
  
 **Problemumgehung:** Überprüfen Sie, ob eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung vorhanden und ordnungsgemäß konfiguriert ist. Weitere Informationen finden Sie unter [Installieren des ersten Berichtsservers im SharePoint-Modus](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beheben von Problemen mit Installationen im SharePoint-Modus](#bkmk_tshoot_sharepoint)  
  
###  <a name="bkmk_RS_SHP_notsupported"></a> Eine Fehlermeldung wird angezeigt, die besagt, dass RS_SHP nicht mit PREPAREIMAGE unterstützt wird.  
 **Beschreibung:** Wenn Sie versuchen, PREPAREIMAGE für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auszuführen, wird eine Fehlermeldung ähnlich der folgenden angezeigt:  
  
 "Beim Ausführen der PREPAREIMAGE-Aktion wird die angegebene Funktion 'RS_SHP' nicht unterstützt, da sie SysPrep nicht unterstützt." Entfernen Sie die Funktionen, die nicht kompatibel mit SysPrep sind, und führen Sie Setup erneut aus."  
  
 **Problemumgehung:** Es gibt keine Problemumgehung. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt SYSPREP (PREPAREIMAGE) nicht. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt SYSPREP.  
  
 ![Pfeilsymbol mit Back Link zum Anfang verwendet](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit Back Link zum Anfang verwendet") [Beheben von Problemen mit Installationen im SharePoint-Modus](#bkmk_tshoot_sharepoint)  
  
##  <a name="bkmk_tshoot_native"></a> Behandeln von Problemen mit Installationen im einheitlichen Modus  
  
###  <a name="PerfCounters"></a> Nach dem Upgrade auf Windows Vista oder Windows Server 2008 werden keine Leistungsindikatoren angezeigt.  
 Wenn Sie auf einem Computer mit [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] ein Upgrade des Betriebssystems auf [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] oder [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]vornehmen, werden die Leistungsindikatoren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nach dem Upgrade nicht festgelegt.  
  
#### <a name="to-reinstate-reporting-services-performance-counters"></a>So stellen Sie die Leistungsindikatoren von Reporting Services wieder her  
  
1.  Löschen Sie die folgenden Registrierungsschlüssel:  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service**  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service**  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl ein:  
  
    -   **Führen Sie \<**  *.NET 4.0 Framework-Verzeichnis* **> \InstallUtil.exe \< ** *Berichtsserver-Bin-Verzeichnis* **> \ReportingServicesLibrary.dll**  
  
        > [!NOTE]  
        >  Ersetzen Sie \< *.NET 4.0 Framework-Verzeichnis*> durch den physischen Pfad der .NET Framework 4.0-Dateien und \< *Berichtsserver-Bin-Verzeichnis*> durch den physischen Pfad für die Berichtsserver-Binärdateien.  
  
3.  Starten Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst neu.  
  
 Um sicherzustellen, dass die Schritte bearbeitet, öffnen Sie einen Webbrowser, und navigieren Sie zum Webportal-URL oder die Berichtsserver-URL. Öffnen Sie anschließend den Systemmonitor, um sicherzustellen, dass die Indikatoren funktionieren.  
  
#### <a name="to-re-add-the-performance-registry-keys-by-using-registry-editor"></a>So fügen Sie die Leistungsregistrierungsschlüssel mit dem Registrierungs-Editor erneut hinzu  
  
1.  Öffnen Sie den Registrierungs-Editor:  
  
    1.  Klicken Sie auf **Start**und dann auf **Ausführen**.  
  
    2.  Geben Sie im Dialogfeld **Ausführen** im Feld **Öffnen** den Befehl **regedit**ein.  
  
2.  Wählen Sie im Registrierungs-Editor den folgenden Registrierungsschlüssel aus: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance`  
  
3.  Klicken Sie mit der rechten Maustaste auf den Knoten **Performance** , zeigen Sie auf **Neu**, und klicken Sie auf **Wert der mehrteiligen Zeichenfolge**.  
  
4.  Geben Sie **Counter Names** ein, und drücken Sie dann die EINGABETASTE.  
  
5.  Wiederholen Sie den Vorgang, um in diesem Knoten den Registrierungsschlüssel **Counter Types** hinzuzufügen.  
  
6.  Navigieren Sie zu folgendem Registrierungsschlüssel: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance`  
  
7.  Klicken Sie mit der rechten Maustaste auf den Knoten **Performance** , zeigen Sie auf **Neu**, und klicken Sie auf **Wert der mehrteiligen Zeichenfolge**.  
  
8.  Geben Sie **Counter Names** ein, und drücken Sie dann die EINGABETASTE.  
  
9. Wiederholen Sie den Vorgang, um in diesem Knoten den Registrierungsschlüssel **Counter Types** hinzuzufügen.  
  
 Nachdem Sie die 64-Bit-Instanz repariert oder die Registrierungsschlüssel manuell erneut hinzugefügt haben, können Sie mit dem Systemmonitor die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Leistungsobjekte konfigurieren, die Sie überwachen möchten.  
  
###  <a name="ConfigPropsMissing"></a> Nach einem Upgrade von SQL Server 2005 sind die "ReportServerExternalURL"-Konfigurationseigenschaft und die "PassThroughCookies"-Konfigurationseigenschaft nicht konfiguriert.  
 Beim Aktualisieren von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] auf [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], werden die Konfigurationseigenschaften **ReportServerExternalURL** und **PassThroughCookies** nicht durch den Aktualisierungsvorgang konfiguriert. **ReportServerExternalURL** ist eine optionale Eigenschaft und sollte nur dann festgelegt werden, wenn Sie SharePoint 2.0 Webparts verwenden und möchten, dass Benutzer einen Bericht abrufen und in einem neuen Browserfenster öffnen können. Weitere Informationen zu **ReportServerExternalURL** finden Sie unter [URLs in Konfigurationsdateien &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md). **PassThroughCookies** ist nur beim Verwenden der benutzerdefinierten Authentifizierungsmethode erforderlich. Weitere Informationen zu **"passthroughcookies"**, finden Sie unter [konfigurieren Sie das Web-Portal zum Übergeben von benutzerdefinierten Authentifizierungscookies](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).  
  
> [!NOTE]  
>  Wenn Sie benutzerdefinierte Authentifizierung verwenden, wird empfohlen, die Installation zu migrieren, statt ein Upgrade durchzuführen. Weitere Informationen zur Migration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie unter [Migrieren einer Installation von Reporting Services &#40;Einheitlicher Modus&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
 Standardmäßig sind diese Eigenschaften in der [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Konfiguration nicht vorhanden. Wenn Sie diese Eigenschaften in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] konfiguriert haben und die von ihnen bereitgestellte Funktionalität weiterhin benötigen, müssen Sie sie nach dem Upgrade manuell der Datei **RSReportServer.config** hinzufügen. Weitere Informationen finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  

### <a name="WindowsAuthBreaksAfterUpgrade"></a>Fehler 401-nicht autorisiert, bei Verwendung der Windows-Authentifizierung nach einem Upgrade von SQL Server 2005 auf SQL Server 2016

 Wenn Sie ein von Upgrade [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], und Sie NTLM-Authentifizierung mit einem integrierten Konto für die Berichtsserver-Dienstkonto verwenden, treten möglicherweise einen Fehler 401-nicht autorisiert, wenn Sie nach dem Upgrade des Berichtsservers oder der Web-Portal zugreifen.  
  
 Der Grund hierfür ist eine Änderung in der [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Standardkonfiguration für Windows-Authentifizierung. In der Konfiguration ist Aushandeln festgelegt, wenn es sich bei dem Berichtsserver-Dienstkonto um einen Netzwerkdienst oder ein lokales System handelt. In der Konfiguration ist NTLM festgelegt, wenn es sich bei dem Berichtsserver-Dienstkonto um keines dieser integrierten Konten handelt. Um das Problem nach dem Upgrade zu beheben, können Sie die Datei „RSReportServer.config“ bearbeiten und **AuthentificationType** als **RSWindowsNTLM**konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md).  

### <a name="Uninstall32BitBreaks64Bit"></a>Deinstallieren von 32-Bit-Instanz von SQL Server 2016 Reporting Services-Seite-an-Seite-Bereitstellung mit einer Instanz der 64-Bit-Instanz beschädigt. die 64-bit

 Wenn Sie eine 32-Bit-Instanz und eine 64-Bit-Instanz von [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] parallel auf einem Computer installieren und die 32-Bit-Instanz deinstallieren, werden vier [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Registrierungsschlüssel entfernt. Hierdurch wird die 64-Bit-Instanz von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]beschädigt. Beim Deinstallieren der 32-Bit-Instanz werden die folgenden [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Registrierungsschlüssel entfernt:  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Web Service\Performance:Counter Types` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2016 Windows Service\Performance:Counter Types`  
  
 Um dieses Problem zu beheben, können Sie die 64-Bit-Instanz reparieren. Zwar wird empfohlen, die Reparatur auszuführen, Sie können jedoch mithilfe des Registrierungs-Editors die Registrierungsschlüssel manuell erneut hinzufügen.  
  
> [!CAUTION]  
>  Ein fehlerhaftes Bearbeiten der Registrierung kann eine schwerwiegende Beschädigung des Systems zur Folge haben. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie wichtige Daten auf dem Computer sichern.  
  
##  <a name="bkmk_additional"></a> Zusätzliche Ressourcen  
 Folgendes sind zusätzliche Ressourcen, die Sie überprüfen können, um Ihnen beim Behandeln von Problemen zu helfen:  
  
-   TechNet Wiki: Problembehandlungsthemen [Problembehandlung von SQL Server Reporting Services (SSRS) im integrierten SharePoint-Modus](http://social.technet.microsoft.com/wiki/contents/articles/troubleshoot-sql-server-reporting-services-ssrs-in-sharepoint-integrated-mode.aspx)  
  
-   [Forum: SQL Server Reporting Services](http://social.msdn.microsoft.com/Forums/sqlreportingservices/threads)  
  
 ![SharePoint-Einstellungen](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint Einstellungen") [Submit Feedback und Kontaktinformationen Informationen über Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
  

