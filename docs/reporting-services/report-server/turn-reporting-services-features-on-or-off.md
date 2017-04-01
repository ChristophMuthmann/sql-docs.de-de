---
title: "Aktivieren und Deaktivieren der Reporting Services-Funktionen | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Reporting Services, Konfiguration"
  - "Sicherheit [Reporting Services], Strategien"
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
caps.latest.revision: 10
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 9
---
# Aktivieren und Deaktivieren der Reporting Services-Funktionen
  Sie können Berichtsserver-Funktionen, die Sie nicht als Teil einer Sicherheitsstrategie verwenden, deaktivieren, um die Angriffsfläche eines Produktionsberichtsservers zu verkleinern. In den meisten Fällen sollten Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Features gleichzeitig ausführen, damit Sie alle Funktionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]verwenden können. Sie können jedoch je nach Bereitstellungsmodell die Funktionen deaktivieren, die Sie nicht benötigen. Beispielweise können Sie nur die Hintergrundverarbeitung aktivieren, wenn die gesamte Berichtsverarbeitung in Form von geplanten Vorgängen konfiguriert ist. Entsprechend können Sie nur den Report Server-Webdienst ausführen, wenn Sie ausschließlich interaktive, bedarfsgesteuerte Berichte wünschen.  
  
 Die Prozeduren in diesem Thema erläutern, wie Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen des einheitlichen Modus deaktivieren. Sie können die Funktionen auf verschiedene Arten konfigurieren, z.B. indem Sie die Datei `RsReportServer.config` direkt bearbeiten oder indem Sie das Facet **Oberflächenkonfiguration für Reporting Services** der richtlinienbasierten Verwaltung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] bearbeiten. Verwenden Sie die Links, um auf die Prozeduren zuzugreifen, in denen das Aktivieren und Deaktivieren einer Funktion erläutert wird:  
  
-   [Report Server-Webdienst](#RSWebSvc)  
  
-   [Geplante Ereignisse und Verarbeitung](#Sched)  
  
-   [Berichts-Manager](#ReportManager)  
  
-   [Berichts-Generator](#ReportBuilder)  
  
-   [Integrierte Sicherheit von Windows für Berichtsdatenquellen](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> Berichtsserver-Webdienst  
  
#### So aktivieren bzw. deaktivieren Sie den Berichtsserver-Webdienst, indem Sie die Konfiguration bearbeiten  
  
1.  Öffnen Sie die Datei `RsReportServer.config` in einem Texteditor. Weitere Informationen finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
2.  Um den Berichtsserver-Webdienst zu aktivieren, setzen Sie **IsWebServiceEnabled** auf **true**:  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  Um den Berichtsserver-Webdienst zu deaktivieren, setzen Sie **IsWebServiceEnabled** auf **false**:  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  Speichern Sie die Änderungen, und schließen Sie dann die Datei.  
  
#### So aktivieren bzw. deaktivieren Sie den Berichtsserver-Webdienst mithilfe von SQL Server Management Studio  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung zu der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz her, die Sie konfigurieren möchten.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Knoten, zeigen Sie auf **Richtlinien**, und klicken Sie auf **Facets**.  
  
3.  Wählen Sie in der Liste **Facet** den Eintrag **Oberflächenkonfiguration für Reporting Services**aus.  
  
4.  Führen Sie unter **Facet-Eigenschaften**Folgendes durch:  
  
    -   Um den Report Server-Webdienst zu aktivieren, setzen Sie **WebServiceAndHTTPAccessEnabled** auf **True**.  
  
    -   Um den Report Server-Webdienst zu deaktivieren, setzen Sie **WebServiceAndHTTPAccessEnabled** auf **False**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> Geplante Ereignisse und Übermittlung  
  
#### So aktivieren bzw. deaktivieren Sie geplante Ereignisse und die Übermittlung, indem Sie die Konfiguration bearbeiten  
  
1.  Öffnen Sie die Datei RSReportServer.config in einem Text-Editor. Weitere Informationen finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
2.  Um die geplante Berichtsverarbeitung und -übermittlung zu aktivieren, setzen Sie **IsSchedulingService**, **IsNotificationService**und **IsEventService** auf **true**:  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  Um die geplante Berichtsverarbeitung und -übermittlung zu deaktivieren, setzen Sie **IsSchedulingService**, **IsNotificationService**und **IsEventService** auf **false**:  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  Speichern Sie die Änderungen, und schließen Sie dann die Datei.  
  
> [!NOTE]  
>  Die Hintergrundverarbeitung kann nicht vollständig deaktiviert werden, da sie Datenbankverwaltungsfunktionen enthält, die für den Serverbetrieb benötigt werden.  
  
#### So aktivieren bzw. deaktivieren Sie geplante Ereignisse und die Übermittlung mithilfe von SQL Server Management Studio  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung zu der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz her, die Sie konfigurieren möchten.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Knoten, zeigen Sie auf **Richtlinien**, und klicken Sie auf **Facets**.  
  
3.  Wählen Sie in der Liste **Facet** den Eintrag **Oberflächenkonfiguration für Reporting Services**aus.  
  
4.  Führen Sie unter **Facet-Eigenschaften**Folgendes durch:  
  
    -   Um geplante Ereignisse und die Übermittlung zu aktivieren, setzen Sie **ScheduleEventsAndReportDeliveryEnabled** auf **True**.  
  
    -   Um geplante Ereignisse und die Übermittlung zu deaktivieren, setzen Sie **ScheduleEventsAndReportDeliveryEnabled** auf **False**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Die Hintergrundverarbeitung kann nicht vollständig deaktiviert werden, da sie Datenbankverwaltungsfunktionen enthält, die für den Serverbetrieb benötigt werden.  
  
##  <a name="ReportManager"></a> Berichts-Manager  
  
#### So aktivieren bzw. deaktivieren Sie den Berichts-Manager, indem Sie die Konfiguration bearbeiten  
  
1.  Öffnen Sie die Datei RSReportServer.config in einem Text-Editor. Anweisungen finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
2.  Um den Berichts-Manager zu aktivieren, setzen Sie **IsReportManagerEnabled** auf **true**:  
  
    ```  
    <IsReportManagerEnabled>true</IsReportManagerEnabled>  
    ```  
  
3.  Um den Berichts-Manager zu deaktivieren, setzen Sie **IsReportManagerEnabled** auf **false**:  
  
    ```  
    <IsReportManagerEnabled>false</IsReportManagerEnabled>  
    ```  
  
4.  Speichern Sie die Änderungen, und schließen Sie dann die Datei.  
  
#### So aktivieren bzw. deaktivieren Sie den Berichts-Manager mithilfe von SQL Server Management Studio  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung zu der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz her, die Sie konfigurieren möchten.  
  
2.  Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Knoten, zeigen Sie auf **Richtlinien**, und klicken Sie auf **Facets**.  
  
3.  Wählen Sie in der Liste **Facet** den Eintrag **Oberflächenkonfiguration für Reporting Services**aus.  
  
4.  Führen Sie unter **Facet-Eigenschaften**Folgendes durch:  
  
    -   Um den Berichts-Manager zu aktivieren, setzen Sie **ReportManagerEnabled** auf **True**.  
  
    -   Um den Berichts-Manager zu deaktivieren, setzen Sie **ReportManagerEnabled** auf **False**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ReportBuilder"></a> Berichts-Generator  
  
#### So aktivieren bzw. deaktivieren Sie den Berichts-Generator mithilfe von SQL Server Management Studio  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung zu der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz her, die Sie konfigurieren möchten.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Knoten, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Servereigenschaften** unter **Seite auswählen**auf **Sicherheit**.  
  
    -   Um den Berichts-Generator zu aktivieren, wählen Sie die Option **Ad-hoc-Berichtsausführungen aktivieren** .  
  
    -   Um den Berichts-Generator zu deaktivieren, heben Sie die Auswahl der Option **Ad-hoc-Berichtsausführungen aktivieren** auf.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="WinIntSec"></a> Integrierte Sicherheit von Windows  
  
#### So aktivieren bzw. deaktivieren Sie die integrierte Windows-Sicherheit mithilfe von SQL Server Management Studio  
  
1.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung zu der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz her, die Sie konfigurieren möchten.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Knoten, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Servereigenschaften** unter **Seite auswählen**auf **Sicherheit**.  
  
    -   Um die integrierte Sicherheit von Windows zu aktivieren, wählen Sie die Option **Integrierte Sicherheit von Windows für Berichtsdatenquellen aktivieren** .  
  
    -   Um die integrierte Sicherheit von Windows zu deaktivieren, heben Sie die Auswahl der Option **Integrierte Sicherheit von Windows für Berichtsdatenquellen aktivieren** auf.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Reporting Services-Konfigurations-Manager (einheitlicher SSRS-Modus)](http://msdn.microsoft.com/de-de/63519ef4-e68a-42fb-9cf7-31228ea4e434)  
  
  