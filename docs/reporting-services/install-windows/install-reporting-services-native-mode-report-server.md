---
title: Installieren des Reporting Services-Berichtsservers im einheitlichen Modus | Microsoft-Dokumentation
ms.custom: SQL2016_New_Updated
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- default configuration [Reporting Services]
- report servers [Reporting Services], default configurations
- installation options [Reporting Services]
ms.assetid: 8f25e6dc-b753-400e-9e9a-50f4f35bf6c4
caps.latest.revision: "68"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: 15a6372f34d1490499880d89e32ac8f0804b0fb8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="install-reporting-services-native-mode-report-server"></a>Installieren des Reporting Services-Berichtsservers im einheitlichen Modus

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Erhalten Sie Informationen zum Installieren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus. Dies ermöglicht den Zugriff auf ein [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] , über das Sie Berichte und andere Elemente verwalten können.

> [!NOTE]
> Interessieren Sie sich für Power BI-Berichtsserver? Weitere Informationen finden Sie unter [Install Power BI Report Server (Installieren von Power BI-Berichtsserver)](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).

Ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver im einheitlichen Modus ist der Standard- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Servermodus und kann mit dem Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder über die Befehlszeile installiert werden. Im Setup-Assistenten können Sie wahlweise Dateien installieren und den Server anhand der Standardeinstellungen konfigurieren oder nur die Dateien installieren. In diesem Thema wird die *Standardkonfiguration für den einheitlichen Modus* beschrieben, in der eine Berichtsserverinstanz von Setup installiert und konfiguriert wird. Nachdem das Setup abgeschlossen ist, wird der Berichtsserver ausgeführt und kann zum Anzeigen einfacher Berichte und für die Berichtsverwaltung verwendet werden.  Zusätzliche Features, wie die [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] -Integration und die E-Mail-Übermittlung mit Abonnementverarbeitung, erfordern eine zusätzliche Konfiguration.  
  
##  <a name="bkmk_whatisdefaultconfiguration"></a> Was ist die Standardkonfiguration?  
 Beim Setup werden die folgenden [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen installiert, wenn Sie die Standardkonfiguration für den einheitlichen Modus auswählen:  
  
-   Berichtsserverdienst (einschließlich des Berichtsserver-Webdiensts, der Hintergrundverarbeitungsanwendung und des [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] s zum Anzeigen und Verwalten von Berichten sowie Berechtigungen).  
  
-   Der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager  
  
-   Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Befehlszeilen-Hilfsprogramme „rsconfig.exe“, „rskeymgmt.exe“ und „rs.exe“  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sind nun getrennte Downloads.  
  
 Setup konfiguriert für die Installation eines Berichtsservers im einheitlichen Modus folgende Elemente:  
  
-   Dienstkonto für den Berichtsserverdienst.  
  
-   URL des Report Server-Webdiensts  
  
-   Die URL des [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] s.  
  
-   Berichtsserver-Datenbank  
  
-   Dienstkontozugriff auf die Berichtsserver-Datenbanken  
  
-   Verbindungsinformationen, auch als Datenquellenname (Data Source Name, DSN) bezeichnet, für die Berichtsserver-Datenbanken.  
  
 Setup konfiguriert weder das unbeaufsichtigte Ausführungskonto noch Berichtsserver-E-Mail, Sicherung der Verschlüsselungsschlüssel noch die Bereitstellung für horizontales Skalieren. Sie können diese Eigenschaften mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager konfigurieren. Weitere Informationen finden Sie unter [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).
  
##  <a name="bkmk_whentoinstalldefaultconfig"></a> Sinnvoller Einsatz für die Installation der Standardkonfiguration im einheitlichen Modus  
 Bei der Standardkonfiguration wird [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im Betriebszustand installiert, sodass Sie den Berichtsserver sofort nach Ende des Setups verwenden können. Geben Sie diesen Modus an, wenn Sie nicht alle Schritte ausführen möchten und alle erforderlichen Konfigurationsaufgaben weglassen, die Sie ansonsten im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool ausführen müssten.  
  
 Die Installation der Standardkonfiguration garantiert nicht, dass der Berichtsserver funktioniert, wenn das Setup beendet ist. Es kann sein, dass die Standard-URLs nicht registriert werden, wenn der Dienst gestartet wird. Testen Sie Ihre Installation immer, um zu überprüfen, ob der Dienst erwartungsgemäß gestartet und ausgeführt wird.  Weitere Informationen finden Sie unter [Überprüfen einer Installation von Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).
  
##  <a name="bkmk_requirements"></a> Anforderungen  
 Bei der Standardkonfigurationsoption werden die Haupteinstellungen, die für den Betrieb eines Berichtsservers erforderlich sind, mithilfe von Standardwerten konfiguriert. Es bestehen folgende Anforderungen:  
  
-   Informieren Sie sich unter [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) .  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] müssen zusammen in derselben Instanz installiert werden. Die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] hostet die Berichtsserver-Datenbank, die vom Setup erstellt und konfiguriert wurde.  
  
-   Das zur Ausführung des Setups verwendete Benutzerkonto muss Mitglied der lokalen Administratorgruppe sein und die Berechtigung zum Datenbankzugriff sowie zur Datenbankerstellung mithilfe der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz besitzen, die die Berichtsserver-Datenbanken hostet.  
  
-   Setup muss die Standardwerte verwenden können, um die URLs zu reservieren, über die auf den Berichtsserver und das [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]zugegriffen werden kann. Zu diesen Werten gehören Port 80, ein starker Platzhalter und die Namen der virtuellen Verzeichnisse im Format **ReportServer_\<***Instanzname***>** und **Reports_\<***Instanzname***>**.  
  
-   Setup muss die Standardwerte für die Erstellung der Berichtsserver-Datenbanken verwenden können. Diese Werte lauten **ReportServer** und **ReportServerTempDB**. Wenn Sie über bestehende Datenbanken aus einer früheren Installation verfügen, wird das Setup blockiert, weil es den Berichtsserver nicht in der Standardkonfiguration für den einheitlichen Modus konfigurieren kann. Sie müssen die Datenbanken umbenennen, verschieben oder löschen, um die Blockierung des Setups aufzuheben.  
  
 Wenn Ihr Computer nicht alle Anforderungen für eine Standardinstallation erfüllt, müssen Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im Dateimodus installieren und dann den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationsmanager verwenden, um nach dem Setup die Konfiguration durchzuführen.
 
 > [!IMPORTANT]
 > Reporting Services kann zwar in einer Umgebung installiert werden, die über einen schreibgeschützten Domänencontroller (Read-Only Domain Controller, RODC) verfügt, benötigt jedoch Zugriff auf einen Domänencontroller mit Lese-/Schreibzugriff, um ordnungsgemäß zu funktionieren. Wenn Reporting Services nur Zugriff auf einen schreibgeschützten Domänencontroller hat, können beim Verwalten des Diensts Fehler auftreten.
  
##  <a name="bkmk_defaultURLreservations"></a> Standard-URL-Reservierungen  
 URL-Reservierungen bestehen aus Präfix, Hostname, Port und virtuellem Verzeichnis:  
  
|Teil|Description|  
|----------|-----------------|  
|Präfix|Das Standardpräfix ist http. Wenn Sie zuvor ein SSL-Zertifikat (Secure Sockets Layer) installiert haben, versucht das Setup, die URL-Reservierungen mit dem Präfix HTTPS zu erstellen.|  
|Hostname|Der Standardhostname ist ein Platzhalter (+). Er gibt an, dass der Berichtsserver eine beliebige HTTP-Anforderung an den angegebenen Port für einen beliebigen Hostnamen akzeptiert, der den Computer erreicht, einschließlich `http://<computername>/reportserver`, `http://localhost/reportserver` oder `http://<IPAddress>/reportserver`.|  
|Port|Der Standardport ist 80. Hinweis: Wenn Sie einen anderen Port als Port 80 verwenden, müssen Sie diesen ausdrücklich der URL hinzufügen, wenn Sie eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webanwendung in einem Browserfenster öffnen.|  
|Virtuelles Verzeichnis|Standardmäßig werden virtuelle Verzeichnisse im Format „ReportServer_\<*Instanzname*>“ für den Berichtsserver-Webdienst und „Reports_\<*Instanzname*>“ für das [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] erstellt. Beim Berichtsserver-Webdienst lautet der Standardname für das virtuelle Verzeichnis **reportserver**. Für das [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]ist **reports**das standardmäßige virtuelle Verzeichnis.|  
  
 Ein Beispiel für die vollständige URL-Zeichenfolge könnte folgendermaßen aussehen:  
  
-   `http://+:80/reportserver` bietet Zugriff auf den Berichtsserver.  
  
-   `http://+:80/reports`, bietet Zugriff auf das [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)].
  
##  <a name="bkmk_installwithwizard"></a> Installieren des einheitlichen Modus mit dem SQL Server-Installations-Assistenten  
 Die folgende Liste beschreibt die  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -spezifischen Schritte und Optionen, die Sie im SQL Server-Installations-Assistenten auswählen. Die Liste beschreibt nicht jede im Installations-Assistenten angezeigte Seite. Es werden nur die auf [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bezogenen Seiten beschrieben, die Teil einer Installation im einheitlichen Modus sind.  
  
1.  Führen Sie den Setup-Assistenten für SQL Server (setup.exe) aus, und gehen Sie die folgenden vorläufigen Seiten durch:  
  
    -   Product Key  
  
    -   Lizenzbedingungen  
  
    -   Globale Regeln  
  
    -   Microsoft Update  
  
    -   Produktupdates  
  
    -   Setupinstallationsdateien  
  
    -   Installationsregeln  
  
2.  Wählen Sie auf der Seite **Setuprolle** die Option **SQL Server-Funktionsinstallation**aus.  
  
     ![SQL Server-Funktionsinstallation für Setuprolle](../../reporting-services/install-windows/media/rs-setuprole.png "SQL Server Feature Installation for setup role")  
  
3.  Wählen Sie Folgendes auf der Seite **Funktionsauswahl** aus:  
  
    -   (1) **Datenbankmoduldienste**, sofern nicht eine Instanz des Datenbankmoduls bereits installiert ist.  
  
    -   (2) **Einheitlicher Modus von Reporting Services**.  
  
     ![Auswahl des einheitlichen SSRS-Modus bei der Funktionsauswahl](../../reporting-services/install-windows/media/rs-setupfeatureselection-native-withcircles.png "SSRS Native Mode Select in Feature Selection")  
  
4.  Überprüfen Sie die erfüllten **Funktionsregeln** .  
  
5.  Denken Sie auf der Seite „Instanzkonfiguration“ daran, dass Sie, wenn Sie sich dazu entscheiden, eine **benannte Instanz**zu konfigurieren, den Instanznamen in URLs verwenden müssen, wenn Sie den Berichts-Manager oder den Berichtsserver selbst aufrufen. Wäre der Instanzname THESQLINSTANCE, würden die URLs wie folgt aussehen:  
  
    -   `http://[ServerName]/ReportServer_THESQLINSTANCE`  
  
    -   `http://[ServerName]/Reports_THESQLINSTANCE`  
  
6.  **Serverkonfiguration**: Wenn Sie planen, die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnementfunktion zu verwenden, konfigurieren Sie auf der Seite **Serverkonfiguration** den Starttyp **Automatisch** für den SQL Server-Agent.   Der Standardwert ist „manuell“.  
  
7.  Fügen Sie SQL Server-Administratoren auf der Seite **Datenbankmodulkonfiguration** hinzu.  
  
8.  Wählen Sie auf der Seite **Reporting Services-Konfiguration** die Option zum **Installieren und Konfigurieren**aus.  
  
     ![SSRS-Konfiguration im einheitlichen Modus](../../reporting-services/install-windows/media/rs-setupconfiguration-native-with-circles.png "SSRS Native Mode Configuration")  
  
    > [!NOTE]  
    >  **Installieren und konfigurieren** ist nur verfügbar, wenn auch das Datenbankfeature zur Installation ausgewählt ist.  
  
9. Regeln zur Featurekonfiguration: Überprüfen Sie die erfüllten Regeln. Der Setup-Assistent springt automatisch zu **Installationsbereit** , wenn alle Regeln erfüllt sind.  Spezifisch für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] überprüfen die Regeln, ob noch keine Berichtsserverkatalog- und temporäre Katalogdatenbank vorhanden ist.  
  
10. Notieren Sie sich auf der Seite **Installationsbereit** den Pfad zur Konfigurationsdatei, da Sie später für eine gute Zusammenfassung der ursprünglichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfiguration, einschließlich der installierten Komponenten, Dienstkonten und Administratoren, darauf verweisen können.  
  
11. Nachdem der SQL Server-Installations-Assistent abgeschlossen ist, überprüfen Sie die standardmäßige Installation im einheitlichen Modus mithilfe der folgenden Schritte.  
  
    -   Öffnen Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager, und bestätigen Sie, dass Sie keine Verbindung zum Berichtsserver herstellen können.  
  
    -   Öffnen Sie den Browser mit **Administratorprivilegien** , und stellen Sie eine Verbindung zum [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]her, beispielsweise `http://localhost/Reports`.  
  
    -   Öffnen Sie den Browser mit Administratorprivilegien, und stellen Sie eine Verbindung zur [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserverseite her. Beispiel:  `http://localhost/ReportServer`  
  
 Weitere Informationen finden Sie im Abschnitt über die einheitlichen Modi in den folgenden zwei Themen:  
  
 [Überprüfen einer Installation von Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)  
  
 [Problembehandlung für eine Reporting Services-Installation](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
  
##  <a name="bkmk_additional_configuration"></a> Zusätzliche Konfiguration  
  
-   Informationen dazu, wie Sie die [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]-Integration konfigurieren, damit Sie Berichtselemente an ein [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]-Dashboard anheften können, finden Sie unter [Power BI Report Server Integration (Integration von Power BI-Berichtsserver)](../../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
-   Informationen dazu, wie Sie E-Mail für die Abonnementverarbeitung konfigurieren, finden Sie unter [E-Mail-Einstellungen: einheitlicher Modus von Reporting Services](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md) und [E-Mail-Übermittlung in Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   Informationen dazu, wie Sie das Webportal konfigurieren, damit Sie über einen Berichtscomputer darauf zugreifen können, um Berichte anzuzeigen und zu verwalten, finden Sie unter [Konfigurieren einer Firewall für den Zugriff auf den Berichtsserver](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) und [Konfigurieren eines Berichtsservers für die Remoteverwaltung](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
## <a name="see-also"></a>Siehe auch

[Problembehandlung für eine Reporting Services-Installation](../../reporting-services/install-windows/troubleshoot-a-reporting-services-installation.md)   
[Überprüfen einer Installation von Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Konfigurieren des Berichtsserver-Dienstkontos](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
[Konfigurieren von Berichtsserver-URLs](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Konfigurieren einer Verbindung mit der Berichtsserver-Datenbank](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Ausschließliche Datei-Installation &#40;Reporting Services&#41;](../../reporting-services/install-windows/files-only-installation-reporting-services.md)   
[Initialisieren eines Berichtsservers](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
[Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
[Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
