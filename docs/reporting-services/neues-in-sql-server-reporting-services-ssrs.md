---
title: "Neues in Reporting Services (SSRS) | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Neuigkeiten [Reporting Services]"
  - "Reporting Services, Neuigkeiten"
  - "SQL Server Reporting Services, Neuigkeiten"
  - "SSRS, Neuigkeiten"
ms.assetid: bc909063-6b84-4b3a-80d2-e93fc04b4b9d
caps.latest.revision: 206
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Neues in SQL Server Reporting Services (SSRS)
Erhalten Sie Informationen zu Neuigkeiten in SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Dies umfasst die wesentlichen Features und wird aktualisiert, wenn neue Elemente veröffentlicht werden.
  
  Informationen zu Neuerungen in anderen Bereichen von SQL Server finden Sie unter [Neues in SQL Server vNext](../sql-server/what-s-new-in-sql-server-vnext.md) und [Was ist neu in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).
  
 **Herunterladen** ![download](../analysis-services/media/download.png "download")
 
- Laden Sie die Januar 2017 Technical Preview von Power BI-Berichten in SQL Server Reporting Services, und die Power BI Desktop-Version (SQL Server Reporting Services), aus dem **[Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=839351)** herunter.
  
-   Navigieren Sie zum Herunterladen von [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]zum  **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
  
-   Haben Sie ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016sp1enterprisewindowsserver2016/)** , um einen virtuellen Computer zu starten, auf dem [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] bereits installiert ist.  
  
 ![Hinweis](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Hinweis") Die aktuellen Versionshinweise finden Sie unter [Technical Preview of Power BI reports in SSRS - Release notes (Technical Preview von Power BI-Berichten in SSRS – Versionshinweise)](../reporting-services/reporting-services-versionshinweise.md) oder unter [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md).  

## <a name="whats-new-in-the-january-2017-technical-preview-of-power-bi-reports-in-sql-server-reporting-services"></a>Neues in der Januar 2017 Technical Preview von Power BI-Berichten in SQL Server Reporting Services

### <a name="reporting-services-has-a-new-setup-experience"></a>Reporting Services bietet einen neuen Setupvorgang

Reporting Services kann nun außerhalb von SQL Server-Setup installiert werden. Der Setupvorgang verfügt über weniger Schritte und ist einfacher. Das Setup installiert die Dateien für Reporting Services. Sie können dann die Datenbank für den Berichtsserver konfigurieren. Dies erfordert, dass Sie Zugriff auf einen SQL Server Datenbankmodul-Server in Ihrer Umgebung haben.

![ssrs-standalone-setup1](../reporting-services/media/ssrs-standalone-setup1.png)

Weitere Informationen finden Sie unter [Install the January 2017 Technical Preview of Power BI reports in SQL Server Reporting Services (Installieren der Januar 2017 Technical Preview von Power BI-Berichten in SQL Server Reporting Services)](Install%20the%20January%202017%20Technical%20Preview%20of%20Power%20BI%20reports%20in%20SQL%20Server%20Reporting%20Services.md).

### <a name="host-power-bi-reports-within-the-web-portal"></a>Hosten von Power BI-Berichten im Webportal

Jetzt können Sie Ihre Power BI Desktop-Dateien in Reporting Services hochladen und Berichte direkt im Webportal ansehen.

![ssrs-powerbi-report-config-render](../reporting-services/media/ssrs-powerbi-report-config-render.png)

Sie müssen die Power BI Desktop-Version (SQL Server Reporting Services) herunterladen. Die Vorschau unterstützt derzeit nur in dieser Version von Power BI Desktop erstellte Berichte. Power BI Desktop (SQL Server Reporting Services) kann parallel mit Power BI Desktop für Power BI-Dienst vorhanden sein. Sie können Power BI Desktop (SQL Server Reporting Services) aus dem Microsoft Download Center herunterladen. 

Sie sind derzeit für das Erstellen eines Power BI-Berichts für aktive Verbindungen mit Analysis Services (tabellarisch oder multidimensional) beschränkt. Wir möchten einen Support für andere Datenquellen hinzufügen und Power Query-Funktionen in einer kommenden Vorschau verwenden.

Weitere Informationen finden Sie unter [Power BI reports in Reporting Services (Power Bl-Berichte in Reporting Services)](../reporting-services/power-bi-reports-in-reporting-services.md).
 
## <a name="whats-new-in-sql-server-2016"></a>Neues in SQL Server 2016
  
### <a name="reporting-services-includessrswebportal-non-markdowntokenssrswebportal-non-markdownmdmd"></a>Reporting Services [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]  
 Ein neues [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] ist verfügbar. Dies ist ein aktualisiertes, modernes Portal, das KPIs, mobile und paginierte Berichte sowie Excel- und Power BI Desktop-Dateien einbezieht. Das [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] ersetzt den Berichts-Manager aus früheren Versionen. Ohne dass ClickOnce-Technologie erforderlich ist, können Sie auch den Publisher für mobile Berichte und Berichts-Generator aus dem [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] herunterladen.
 
 Zum Erstellen mobiler Berichte ist [!INCLUDE[SS_MobileReptPub_Short](../includes/ss-mobilereptpub-short-md.md)] erforderlich.  
  
 Weitere Informationen zum [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] finden Sie unter [Webportal (einheitlicher SSRS-Modus)](../reporting-services/web-portal-ssrs-native-mode.md).  
  
 ![ssRSPortal](../reporting-services/media/ssrsportal.png "ssRSPortal")  
 
 #### <a name="custom-branding-for-the-includessrswebportal-non-markdowntokenssrswebportal-non-markdownmdmd"></a>Benutzerdefiniertes Branding für [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 
  Sie können jetzt das [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] mit dem Logo und den Farben Ihres Unternehmens mithilfe eines Brandingpakets anpassen.  
  
  Weitere Informationen zum benutzerdefinierten Branding finden Sie unter [Branding des Webportals](http://msdn.microsoft.com/de-de/6dac97f7-02a6-4711-81a3-e850a6b40bf1).
 
 #### <a name="key-performance-indicators-kpi-in-the-includessrswebportal-non-markdowntokenssrswebportal-non-markdownmdmd"></a>Key Performance Indicators (KPI) im [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 

Sie können KPIs direkt im [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] erstellen, die im Kontext mit dem Ordner sind, in dem Sie sich befinden. Wenn Sie KPIs erstellen, können Sie Datasetfelder wählen und diese Werte zusammenfassen. Sie können auch verwandte Inhalte auswählen, um per Drillthrough zu weiteren Details zu gelangen.
  
 ![ssrs-webportal-kpi](../reporting-services/media/ssrs-webportal-kpi.png)
 
 Weitere Informationen finden Sie unter [Arbeiten mit KPIs im Webportal](http://msdn.microsoft.com/de-de/a28cf500-6d47-4268-a248-04837e7a09eb).
  
 
 ### <a name="mobile-reports"></a>Mobile Berichte
 
Mobile Reporting Services-Berichte sind dedizierte Berichte, die für eine Vielzahl von Formfaktoren optimiert sind und eine optimale Erfahrung für Benutzer bieten, die auf mobilen Geräten auf Berichte zugreifen. Mobile Berichte stellen eine Reihe von Visualisierungen zur Verfügung – von Zeit-, Kategorie- und Vergleichsdiagrammen über Treemap-Diagramme bis hin zu benutzerdefinierten Karten. Verbinden Sie Ihre mobilen Berichte mit einer Reihe von Datenquellen, einschließlich lokalen mehrdimensionalen und tabellarischen SQL Server Analysis Services-Daten. Gestalten Sie Ihre mobilen Berichte auf einer Entwurfsoberfläche mit anpassbaren Rasterzeilen und -spalten und flexiblen Elementen für mobile Berichte, die sich gut auf jede Bildschirmgröße skalieren lassen. Speichern Sie diese mobilen Berichte anschließend auf einem Reporting Services-Server, und verwenden Sie zum Anzeigen bzw. Interagieren mit diesen einen Browser oder die mobile Power BI-App auf iPads, iPhones, Android-Telefonen und Windows 10-Geräten.
  
#### <a name="mobile-report-publisher"></a>Publisher für mobile Berichte  
 Mit dem [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] können Sie mobile SQL Server-Berichte in Ihrem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] erstellen und veröffentlichen.  
  
 ![SS_MRP_LayoutTabSmall](../reporting-services/media/ss-mrp-layouttabsm.png "SS_MRP_LayoutTabSmall")  
  
 Weitere Informationen finden Sie unter [Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md).  
  
#### <a name="sql-server-mobile-reports-hosted-in-reporting-services-available-in-power-bi-mobile-app"></a>In Reporting Services gehostete mobile SQL Server-Berichte sind in der Power BI Mobile-App verfügbar  
 Die Power BI Mobile-App für iOS auf dem iPad und iPhone kann jetzt auf dem lokalen Berichtsserver gehostete mobile SQL Server-Berichte anzeigen.  
  
 ![SS_MRP_iPad_HomeSm](../reporting-services/media/ss-mrp-ipad-homesm.png "SS_MRP_iPad_HomeSm")  
  
 Sie können keine Standardverbindung herstellen, ohne einige Änderungen an der Konfiguration vorzunehmen. Weitere Informationen zum Herstellen der Verbindung zwischen der Power BI Mobile-App und dem Berichtsserver finden Sie unter [Aktivieren eines Berichtsservers für einen Zugang zu Power BI von Mobilgeräten](../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md).
  
### <a name="support-of-sharepoint-mode-and-sharepoint-2016"></a>Unterstützen des SharePoint-Modus und von SharePoint 2016  
 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] unterstützt die Integration in SharePoint 2013 und SharePoint 2016.
 
Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Unterstützte Kombinationen von SharePoint und Reporting Services-Server und -Add-In &#40;SQL Server 2016&#41;](../reporting-services/install-windows/supported combinations of sharepoint and reporting services server.md)  
  
-   [Verfügbarkeit des Reporting Services-Add-Ins für SharePoint-Produkte](../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Installieren des SharePoint-Modus von Reporting Services](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  

### <a name="microsoft-net-framework-4-support"></a>Microsoft .NET Framework 4-Unterstützung  
 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] unterstützt die aktuellen Versionen von Microsoft .NET Framework 4. Dies umfasst die Versionen 4.0 und 4.5.1. Wenn keine Version von .NET Framework 4.x installiert ist, installiert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Setup .NET 4.0 während der Installation von Features.  

### <a name="report-improvements"></a>Verbesserungen an Berichten

**HTML 5-Renderingmodul**: Es wurde ein neues HTML5-Renderingmodul hinzugefügt, das auf „vollständige“ moderne Webstandardsmodi und moderne Browser ausgerichtet ist.  Das neue Renderingmodul beruht nicht mehr auf dem Quirksmodus, der von einigen älteren Browsern verwendet wird.
  
 Weitere Informationen zur Browserunterstützung von finden Sie unter [Browserunterstützung für Reporting Services und Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md).  

**Moderne paginierte Berichte:** Entwerfen Sie moderne paginierte Berichte mit neuen, modernen Formatvorlagen für Diagramme, Messgeräte, Karten und andere Datenvisualisierungen.
  
**Strukturzuordnung und Sunburst-Diagramme**: Verbessern Sie Ihre Berichte mit der Strukturzuordnung ![ssrs_treemap_icon](../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon") und Sunburst ![ssrs_sunburst_icon](../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")-Diagrammen, die eine hervorragende Möglichkeit zum Anzeigen hierarchischer Daten bieten. Weitere Informationen finden Sie unter [Strukturzuordnung und Sunburst-Diagramme in Reporting Services](../reporting-services/report-design/tree-map-and-sunburst-charts-in-reporting-services.md).  

**Berichtseinbettung:** Sie können jetzt mobile und paginierte Berichte in andere Webseiten und Anwendungen unter Verwendung eines IFRAMEs zusammen mit URL-Parametern einbetten.  

**Anheften von Berichtselementen an ein Power BI-Dashboard**: Bei der Anzeige eines Berichts im [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] können Sie Berichtselemente auswählen und sie an ein [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]-Dashboard heften.   Die Elemente, die angeheftet werden können, sind Diagramme, Messgerätbereiche, Karten und Bilder. **(1)** Wählen Sie die Gruppe aus, die das Dashboard enthält, an das Sie das Element anheften möchten, **(2)** wählen Sie das Dashboard aus, an das Sie das Element anheften möchten, und **(3)** wählen Sie aus, wie oft die Kachel im Dashboard aktualisiert werden soll.   ![Hinweis](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Hinweis") Die Aktualisierung wird durch [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Abonnements verwaltet. Nach dem Anheften des Elements können Sie das Abonnement bearbeiten und einen anderen Aktualisierungszeitplan konfigurieren.  
  
 ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png) 
  
 Weitere Informationen finden Sie unter [Berichtsserverintegration für Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md) und [Anheften von Reporting Services-Elementen an Power BI-Dashboards](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).  
 
 **PowerPoint-Rendering und -Export**: Das Microsoft PowerPoint-Format (PPTX) ist eine neue [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]-Renderingerweiterung. Sie können Berichte im PPTX-Format über die üblichen Anwendungen exportieren: Berichts-Generator, Berichts-Designer (in SSDT) und [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. Für das Beispiel zeigt die folgende Abbildung das Exportmenü des [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]s. 
  
 ![ssrs-export-powerpoint](../reporting-services/media/ssrs-export-powerpoint.png) 
  
 Sie können auch das PPTX-Format für die Abonnementausgabe auswählen und den Zugriff auf die Berichtsserver-URL zum Rendern und Exportieren eines Berichts verwenden. Der folgende URL-Befehl in Ihrem Browser exportiert z. B. einen Bericht von einer benannten Instanz des Berichtsservers.  
  
```  
http://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Weitere Informationen finden Sie unter [Exportieren von Berichten über URL-Zugriff](../reporting-services/export-a-report-using-url-access.md).  
 
 **PDF ersetzt ActiveX für Remotedruckvorgänge**: Die ActiveX-Druckfunktion auf der Symbolleiste des Berichts-Viewers wurde durch eine moderne, PDF-basierte Funktion ersetzt, die von verschiedenen unterstützt wird, einschließlich Microsoft Edge. Es müssen keine ActiveX-Steuerelemente heruntergeladen werden! Je nach verwendetem Browser und den Anwendungen für die Anzeige von PDF-Dateien sowie nach den installierten Diensten, öffnet [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] entweder das Dialogfeld „Drucken“ zum Drucken des Berichts, oder Sie werden aufgefordert, eine PDF-Datei für Ihren Bericht herunterzuladen.  Als Administrator können Sie weiterhin das clientseitige Drucken über [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] deaktivieren. Weitere Informationen finden Sie unter [Aktivieren und Deaktivieren des clientseitigen Drucks für Reporting Services](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).

![ssrs-pdf-printing](../reporting-services/media/ssrs-pdf-printing.png)

### <a name="subscription-improvements"></a>Abonnementverbesserungen  
 
|Funktion|Unterstützter Servermodus|  
|-------------|---------------------------|  
|**Aktivieren und Deaktivieren von Abonnements**. Neue Optionen der Benutzeroberfläche ermöglichen ein schnelles Deaktivieren und Aktivieren von Abonnements. Die deaktivierten Abonnements behalten ihre anderen Konfigurationseigenschaften, z. B. den Zeitplan, bei und können leicht aktiviert werden.<br /><br /> ![ssrs-enable-disable-subscriptions](../reporting-services/media/ssrs-enable-disable-subscriptions.png)<br /><br /> Weitere Informationen finden Sie unter [Deaktivieren oder Anhalten der Berichts- und Abonnementverarbeitung](../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).|Einheitlicher Modus|  
|**Abonnementbeschreibung**. Wenn Sie ein neues Abonnement erstellen, können Sie jetzt eine Beschreibung des Berichts als Teil der Abonnementeigenschaften einbeziehen. Die Beschreibung ist auf der Seite zur Abonnementzusammenfassung enthalten.|SharePoint- und einheitlicher Modus|  
|**Ändern des Abonnementbesitzers**. Verbesserte Benutzeroberfläche zum schnellen Ändern des Besitzers eines Abonnements. Bei früheren Versionen von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] konnten Administratoren die Abonnementbesitzer mithilfe eines Skripts ändern. Ab Version [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] können Sie Abonnementbesitzer über die Benutzeroberfläche oder ein Skript ändern. Das Ändern des Abonnementbesitzers ist eine häufige Verwaltungsaufgabe, wenn Benutzer Ihr Unternehmen verlassen oder eine andere Funktion übernehmen.|SharePoint- und einheitlicher Modus|  
|**Freigegebene Anmeldeinformationen für Dateifreigabeabonnements**. Es gibt jetzt zwei Workflows mit [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Dateifreigabeabonnements:<br /><br /> In diesem Release kann Ihr [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Administrator neuerdings eine einzelne Dateifreigabe konfigurieren, die für ein oder mehrere Abonnements verwendet wird. Das Dateifreigabekonto wird im einheitlichen Modus des [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Configuration Managers konfiguriert. **Geben Sie ein Dateifreigabekonto an**, und auf der Abonnementkonfigurationsseite wählen Benutzer dann **Dateifreigabekonto verwenden** aus.<br /><br /> Sie können einzelne Abonnements mit spezifischen Anmeldeinformationen für die Zieldateifreigabe konfigurieren.<br /><br /> Sie können beide Ansätze auch kombinieren, sodass einige Dateifreigabeabonnements das zentrale Dateifreigabekonto verwenden, während andere Abonnements bestimmte Anmeldeinformationen nutzen.|Einheitlicher Modus|  

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
 Die neue Version von SSDT enthält die Projektvorlagen für [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]: Berichtsserverprojekt-Assistent und Berichtsserverprojekt. Informationen zum Herunterladen von SSDT finden Sie unter [SQL Server Data Tools für Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=827542).  

### <a name="report-builder-improvements"></a>Verbesserungen am Berichts-Generator

**Neue Benutzeroberfläche für den Berichts-Generator**: Die [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)]-Hauptbenutzeroberfläche weist jetzt ein modernes Layout mit optimierten UI-Elementen auf.  
  
|||  
|-|-|  
|Neu|Previous|  
|![ssrs_rbfacelift_new](../reporting-services/media/ssrs-rbfacelift-new.png "ssrs_rbfacelift_new")|![ssrs_rbfacelift_old](../reporting-services/media/ssrs-rbfacelift-old.png "ssrs_rbfacelift_old")|  

**Benutzerdefinierter Parameterbereich**: Sie können jetzt den Parameterbereich anpassen. Mithilfe der Entwurfsoberfläche im Berichts-Generator, können Sie einen Parameter zu einer bestimmten Spalte und Zeile im Parameterbereich ziehen. Sie können Spalten hinzufügen und entfernen, um das Layouts des Bereichs zu ändern.   Weitere Informationen finden Sie unter [Benutzerdefiniertes Anpassen des Parameterbereichs &#40;Berichts-Generator&#41;](../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
 ![Parameter list in Report Data pane and in parameters pane](../reporting-services/media/ssrs-customizeparameter-parameterlist-reportdatapane.png "Parameter list in Report Data pane and in parameters pane")  

  
**Unterstützung hoher DPI-Werte**: [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)] für [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] unterstützt die Skalierung sowie Geräte mit hohen DPI-Werten (Punkte pro Zoll).  Weitere Informationen zu hohen DPI-Werten finden Sie in folgenden Themen:  
  
-   [Windows 8.1 DPI Scaling Enhancements (Erweiterungen für Windows 8.1 DPI-Skalierung)](https://blogs.windows.com/windowsexperience/2013/07/15/windows-8-1-dpi-scaling-enhancements/)  
  
-   [Hohe DPI-Werte und Windows 8.1](http://technet.microsoft.com/library/dn528848.aspx)  
  
## <a name="see-also"></a>Siehe auch  
 [Neuigkeiten in Analysis Services](http://msdn.microsoft.com/de-de/aa69c299-b8f4-4969-86d8-b3292fe13f08)  
 [Technical Preview of Power BI reports in SSRS - Release notes (Technical Preview von Power BI-Berichten in SSRS - Versionshinweise)](../reporting-services/reporting-services-versionshinweise.md)  
 [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)   
 [Abwärtskompatibilität](http://msdn.microsoft.com/de-de/675b0e0e-cfee-4790-9675-80fc3ea6d30f)   
 [Von den SQL Server 2016-Editionen unterstützte Reporting Services-Funktionen](http://msdn.microsoft.com/de-de/39f03d2d-6e48-4b34-a9d3-07f86313b937)   
 [Aktualisieren und Migrieren von Reporting Services](../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-ssrs.md)  
  
  