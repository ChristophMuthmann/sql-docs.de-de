---
title: Entwerfen von Berichten mithilfe des Berichts-Designers (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Designer [Reporting Services], report creation
ms.assetid: 3a26dccc-6ad6-48f5-a882-f96c6c0dd405
caps.latest.revision: 77
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 02e1eb6504ae66ba6e48cedc0c511c4cd9505fb2
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---

# <a name="design-reporting-services-paginated-reports-with-report-designer-ssrs"></a>Erstellen von paginierten Berichten von Reporting Services mit dem Berichts-Designer (SSRS)

Mit dem Berichts-Designer können Sie paginierte [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichte und -Berichtslösungen mit vollem Funktionsumfang erstellen. Die grafische Benutzeroberfläche des Berichts-Designers ermöglicht Ihnen, Datenquellen, Datasets und Abfragen, Berichtslayoutpositionen für Datenbereiche und Felder sowie interaktive Funktionen. z. B. Parameter und zusammenwirkende Berichtssätze, zu definieren.  

Der Berichts-Designer ist ein Feature von  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], einer Microsoft Visual Studio-Umgebung zum Erstellen von Business Intelligence-Lösungen. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ist nicht im Lieferumfang von SQL Server enthalten. Herunterladen von [SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714). 
  
## <a name="benefits-of-report-projects"></a>Vorteile von Berichtsprojekten  
Berichtsprojekte dienen als Container für Berichtsdefinitionen und Ressourcen. Verwenden Sie Projekte für folgende Aufgaben:  
  
-   Organisieren Sie Berichte und verwandten Elemente in einem Container.  
  
-   Testen Sie Berichtslösungen mit Berichten und verwandten Elementen lokal.  
  
-   Stellen Sie verwandte Elemente gemeinsam bereit. Nutzen Sie die Projekteigenschaften und Konfigurationsverwaltung für eine Bereitstellung in mehreren Umgebungen.  
  
-   Behalten Sie einen Satz von Masterkopien für Berichte und verwandte Elemente bei. Nach der Bereitstellung können veröffentlichte Berichte unbeabsichtigt geändert werden.  
  
 Anhand der Informationen in diesem Thema können Sie paginierte Berichte und verwandte Elemente für ein konkretes Berichtsprojekt in einer [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] -Projektmappe entwerfen. Weitere Informationen zu Projektmappen und mehreren Projekten in SQL Server Data Tools finden Sie unter [Reporting Services in SQL Server Data Tools](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).  

  
##  <a name="bkmk_SharedDataSources"></a> Freigegebene Datenquellen  
 Verwenden Sie [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] , um freigegebene Datenquellen für eine Berichtslösung zu definieren und bereitzustellen. Freigegebene Datenquellen können mit den Eigenschaften **OverwriteDataSources** und **TargetDataSourceFolder** unabhängig von anderen Elementen in einem Projekt bereitgestellt werden. Weitere Informationen finden Sie unter [Festlegen von Bereitstellungseigenschaften &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
 Im Berichts-Designer nutzen Sie sowohl den Berichtsdatenbereich als auch den Projektmappen-Explorer, um die in einem Bericht verwendeten Datenquellen zu definieren. Weitere Informationen finden Sie unter [Report Data Pane](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane). Sie können Datenquellen, die auf einem Berichtsserver oder einer SharePoint-Website veröffentlicht, aber nicht in die [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] -Projektmappe eingeschlossen wurden, nicht mit [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] öffnen. Verwenden Sie für diese Funktion die [Berichterstellungsumgebung des Berichts-Generators &#40;SSRS&#41;](../../reporting-services/tools/report-builder-authoring-environment-ssrs.md).  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ist ein Clienttool. Sie können die Berichtslösung lokal auf dem Computer testen, zum Testen der Serverlösung in einer Testumgebung bereitstellen und dann in einer Produktionsumgebung bereitstellen. Überprüfen Sie nach der Bereitstellung, dass die Verarbeitungserweiterungen und Anmeldeinformationen der Datenquelle für die Berichtsserverumgebung konfiguriert wurden. Der Konfigurations-Manager unterstützt Sie beim Verwalten der Eigenschaften für verschiedene Bereitstellungen. Weitere Informationen finden Sie unter [Reporting Services in SQL Server Data Tools &#40;SSDT&#41;](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).  
  
 Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
   
##  <a name="bkmk_SharedDatasets"></a> Freigegebene Datasets  
 Verwenden Sie [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] , um freigegebene Datasets für eine Berichtslösung zu definieren und bereitzustellen. Freigegebene Datasets können mit den Eigenschaften **OverwriteDatasets** und **TargetDatasetFolder** unabhängig von anderen Elementen in einem Projekt bereitgestellt werden. Weitere Informationen finden Sie unter [Festlegen von Bereitstellungseigenschaften &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
 Im Berichts-Designer nutzen Sie sowohl den Berichtsdatenbereich als auch den Projektmappen-Explorer, um die in einem Bericht verwendeten freigegebenen Datasets zu definieren. Weitere Informationen finden Sie unter [Report Data Pane](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane). Sie können veröffentlichte Datasets mithilfe von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] nicht direkt von einem Berichtsserver oder einer SharePoint-Website aus öffnen. Verwenden Sie für diese Funktion die [Berichterstellungsumgebung des Berichts-Generators &#40;SSRS&#41;](../../reporting-services/tools/report-builder-authoring-environment-ssrs.md) im Modus für freigegebene Datasets.  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ist ein Clienttool. Abfrage-Designern unterstützen Sie beim Erstellen und Testen von Abfrageergebnissen lokale in der Vorschau. Nach der Bereitstellung können Sie freigegebene Datasets unabhängig von den freigegebenen Datenquellen und Berichten verwalten, von denen sie abhängen. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md), [Abfrageentwurfstools &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md) und [Verwalten von freigegebenen Datasets](../../reporting-services/report-data/manage-shared-datasets.md).  
  
##  <a name="bkmk_Reports"></a> Paginierte Berichte  
Paginierte Berichte sind Dateien, die in einem Berichtsprojekt gespeichert werden. Berichte können als eigenständige Berichte, als Unterberichte oder als Ziele für Drillthroughaktionen in Hauptberichten verwendet werden. Mit **TargetReportFolder** und anderen Eigenschaften können Berichte unabhängig von anderen Elementen in einem Projekt bereitgestellt werden. Weitere Informationen finden Sie unter [Festlegen von Bereitstellungseigenschaften &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
> [!NOTE]  
>  Bei Veröffentlichung auf einem Berichtsserver im SharePoint-Modus können einige Berichtslösungsfunktionen im Berichts-Designer-Projekt nicht getestet werden. Für Verweise auf Berichte, Unterberichte und Drillthroughberichte müssen vollqualifizierte URLs verwendet werden, die erst nach der Bereitstellung des Berichtsprojekts getestet werden können. Weitere Informationen finden Sie unter [Beispiele für URLs von veröffentlichten Berichtselementen auf einem Berichtsserver im SharePoint-Modus &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
 Sie können einem Projekt Berichte auf folgende Weise hinzufügen:  
  
-   **Fügen Sie ein neues Berichtsprojekt hinzu.** Standardmäßig wird ein leerer Bericht in Berichts-Designer geöffnet. Weitere Informationen finden Sie unter [Hinzufügen eines neuen oder vorhandenen Berichts zu einem Berichtsprojekt &#40;SSRS&#41;](../../reporting-services/tools/add-a-new-or-existing-report-to-a-report-project-ssrs.md).  
  
-   **Fügen Sie ein Berichts-Assistent-Projekt hinzu.** Sie erstellen das Projekt mithilfe einer detaillierten Anleitung. Der Berichts-Assistent vereinfacht die Datendefinition und den Berichtsentwurf, indem er sie in einzelne Schritte aufteilt und am Ende einen fertigen Bericht erstellt. Sie können Formate hinzufügen und den Assistenten so für Ihre Organisation anpassen. Weitere Informationen finden Sie unter [Hinzufügen eines neuen oder vorhandenen Berichts zu einem Berichtsprojekt &#40;SSRS&#41;](../../reporting-services/tools/add-a-new-or-existing-report-to-a-report-project-ssrs.md).  
  
-   **Fügen Sie ein neues Element vom Typ „Bericht“ hinzu.** Ein leerer Bericht wird im Berichts-Designer geöffnet.  
  
-   **Fügen Sie ein vorhandenes Element hinzu.** Eine vorhandene Berichtsdefinition (.rdl) wird im Berichts-Designer geöffnet. Beim Öffnen eines Berichts oder Projekts aus einer früheren Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wird das Projekt ggf. automatisch auf die aktuelle Version bzw. der Bericht auf das aktuelle Schema aktualisiert. Weitere Informationen finden Sie unter [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
-   **Importieren Sie einen [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Zugriffsbericht.** Importieren Sie alle Berichte aus einer Access-Datenbank (.mdb, .accdb) oder einer Projektdatei (.adp). Jeder Bericht in einer Datenbank- oder Projektdatei wird vom Berichts-Designer in Berichtsdefinitionssprache (RDL, Report Definition Language) konvertiert und im Berichtsprojekt gespeichert. Nicht alle Funktionen eines Access-Berichts werden in eine Berichtsdefinitionsdatei (.rdl) übertragen. Weitere Informationen finden Sie unter [Importieren von Berichten aus Microsoft Access (Reporting Services)](http://msdn.microsoft.com/library/4f29d5b8-b77d-4714-a84a-05523df55646) und [Unterstützte Zugriffsberichtsfunktionen (SSRS)](http://msdn.microsoft.com/library/7ffec331-6365-4c13-8e58-b77a48cffb44).  
  
    > [!NOTE]  
    >  Die Verwendung des Importfunktionen setzt voraus, dass auf dem Computer, auf dem auch der Berichts-Designer installiert ist, Access 2002 oder höher installiert ist. Beim Importieren der Berichte muss die Datenquelle für die Access-Berichte verfügbar sein.  
  
-   **Arbeiten Sie direkt in RDL.** Wenn Sie im Berichts-Designer einen Bericht erstellen, wird dieser als RDL-Datei (Report Definition Language, Berichtsdefinitionssprache) im XML-Format gespeichert. Sie können diese Datei mit dem Berichts-Designer, einem Texteditor oder jedem anderen Tool zur Bearbeitung von XML bearbeiten.  
  
     Wenn Sie die Berichtsdefinitionsquelle im Berichts-Designer ändern, bearbeiten Sie das aktuelle RDL-Schema für die Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , von der aus Sie die Entwicklungstools installiert haben. Wenn Sie ein Projekt erstellen, kann sich die Schemaversion abhängig von den Bereitstellungseigenschaften ändern. Weitere Informationen finden Sie unter [Bereitstellung und Versionsunterstützung in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)enthalten.  
  
     Das direkte Bearbeiten von RDL kann zur Folge haben, dass der Bericht nicht auf dem Berichtsserver veröffentlicht oder nicht ausgeführt werden kann. Stellen Sie wie bei jeder XML-Datei sicher, dass in den Elementen verwendete XML-spezifische Zeichen richtig codiert sind. Wenn Sie den Bericht veröffentlichen, wird auf dem Berichtsserver der in der RDL-Datei enthaltene XML-Code anhand des Schemas überprüft.  
  
     Um Elemente einzuschließen, die nicht Teil des RDL-Schemas sind, fügen Sie sie in das Custom-Element ein. Das Custom-Element kann von benutzerdefinierten Renderingerweiterungen gelesen werden, wird aber von den mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]bereitgestellten Renderingerweiterungen ignoriert. Sie können mithilfe des Custom-Elements beispielsweise Kommentare im Bericht speichern.  
  
     Weitere Informationen finden Sie unter [Berichtsdefinitionssprache (Report Definition Language, RDL) &#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md).  
  
##  <a name="bkmk_ReportParts"></a> Berichtsteile  
 Nachdem Sie Tabellen, Diagramme und andere paginierte Berichtselemente in einem Projekt erstellt haben, können Sie sie im Berichts-Designer auf einem Berichtsserver oder einer in einen Berichtsserver integrierten SharePoint-Website als *Berichtsteile* veröffentlichen, damit sie von Ihnen und weiteren Benutzern in anderen Berichten wiederverwendet werden können. Weitere Informationen finden Sie unter [Berichtsteile im Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
 Mit **TargetReportPartFolder** und anderen Eigenschaften können Berichtsteile unabhängig von anderen Elementen in einem Projekt bereitgestellt werden. Weitere Informationen finden Sie unter [Festlegen von Bereitstellungseigenschaften &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
##  <a name="bkmk_Resources"></a> Ressourcen  
 Sie können dem Projekt Dateien hinzufügen, die zwar einen Bezug zu dem Bericht haben, aber nicht vom Berichtsserver verarbeitet werden. Sie können z. B. Grafiken für Bilder oder ESRI-Shape-Dateien für räumliche Daten hinzufügen. Weitere Informationen finden Sie unter [Resources](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md#bkmk_Resources).  
 
##  <a name="bkmk_ReportLayout"></a> Paginiertes Berichtslayout  
 Um das Berichtslayout zu erstellen, ziehen Sie Berichtselemente und Datenbereiche aus der Toolbox auf die Entwurfsoberfläche, und ordnen Sie sie entsprechend an. Ziehen Sie Datasetfelder auf die Elemente in der Entwurfsoberfläche, um dem Bericht Daten hinzuzufügen. Wenn Sie Daten in einem Tablix-Datenbereich in Gruppen organisieren möchten, ziehen Sie Datasetfelder in den Bereich für die Gruppierung. Da Berichterstellungstools primär zum Erstellen von Berichtsdefinitionen dienen, sind die Ansätze für den Berichtsentwurf im Berichts-Generator und Report Designer einander sehr ähnlich.  
   
##  <a name="bkmk_Preview"></a> Anzeigen einer Vorschau eines paginierten Berichts  
 Verwenden Sie die **Vorschau** , um die Berichtsdaten und den Layoutentwurf zu überprüfen. Wenn Sie eine Vorschau eines Berichts anzeigen, überprüft der Berichtsprozessor das Berichtsdefinitionsschema und die Ausdruckssyntax. Probleme werden im Fenster [Output](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) aufgelistet.  
  
> [!NOTE]  
>  Wenn Sie eine Vorschau für einen Bericht anzeigen, werden die Daten für den Bericht auf dem lokalen Computer in einer Datei zwischengespeichert. Wenn Sie für denselben Bericht erneut eine Vorschau anzeigen, indem Sie dieselbe Abfrage und dieselben Parameter und Anmeldeinformationen verwenden, ruft der Berichts-Designer die zwischengespeicherte Kopie ab, anstatt die Abfrage erneut auszuführen. Die Datendatei wird in demselben Verzeichnis wie die Berichtsdefinitionsdatei unter dem Namen „*\<Berichtsname>*.rdl.data“ gespeichert. Die Datei wird nicht gelöscht, wenn Sie den Berichts-Designer schließen.  
  
 Sie können eine Vorschau eines Berichts wie folgt anzeigen:  
  
-   **Vorschauansicht.** Klicken Sie auf die Registerkarte **Vorschau** . Der Bericht wird lokal mit derselben Berichtsverarbeitungs- und Renderingfunktionalität ausgeführt, die auf dem Berichtsserver zur Verfügung steht. Der Bericht wird als interaktives Bild angezeigt, in dem Sie Parameter auswählen, auf Links klicken, die Dokumentstruktur anzeigen und ausgeblendete Bereiche des Berichts erweitern bzw. reduzieren können. Darüber hinaus können Sie den Bericht in jedes installierte Renderingformat exportieren.  
  
-   **Eigenständige Vorschau.** Führen Sie den lokalen Bericht in einem Browser aus. Mit einer Debugkonfiguration können Sie diesen Modus auch verwenden, um von Ihnen geschriebene benutzerdefinierte Assemblys zu debuggen. Es gibt drei Möglichkeiten, ein Projekt im Debugmodus auszuführen:  
  
    -   Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
    -   Klicken Sie auf der [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] -Standardsymbolleiste auf die Schaltfläche **Start** .  
  
    -   Drücken Sie F5.  
  
     Falls Sie eine Projektkonfiguration verwenden, die zwar den Bericht erstellt, aber nicht bereitstellt, wird der in der **StartItem** -Eigenschaft angegebene Bericht der aktuellen Konfiguration in einem separaten Vorschaufenster geöffnet.  
  
    > [!NOTE]  
    >  Um den Debugmodus verwenden zu können, müssen Sie ein Startelement festlegen. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Berichtsprojekt, klicken Sie auf **Eigenschaften**, und wählen Sie unter **StartItem**den Namen des anzuzeigenden Berichts aus.  
  
     Wenn Sie einen bestimmten Bericht in der Vorschau anzeigen möchten, der nicht als Startelement für das Projekt festgelegt ist, wählen Sie eine Konfiguration aus, die den Bericht zwar erstellt, jedoch nicht bereitstellt (z.B. die DebugLocal-Konfiguration). Klicken Sie anschließend mit der rechten Maustaste auf den Bericht, und klicken Sie anschließend auf **Ausführen**. Sie müssen eine Konfiguration auswählen, die den Bericht nicht bereitstellt. Andernfalls wird der Bericht auf dem Berichtsserver veröffentlicht und nicht lokal in einem Vorschaufenster angezeigt.  
  
-   **Seitenansicht.**  
  
     Wenn Sie einen Bericht zum ersten Mal im Vorschaumodus oder im Vorschaufenster anzeigen, gleicht die Anzeige des Berichts einem per HTML-Renderingerweiterung erstellten Bericht. Die Vorschau ist kein HTML-Code, das Layout und die Paginierung des Berichts gleichen jedoch der HTML-Ausgabe.  
  
     Sie können die Ansicht ändern und einen gedruckten Bericht darstellen, indem Sie zur Seitenansicht wechseln. Klicken Sie auf der Vorschausymbolleiste auf die Schaltfläche **Seitenansicht** . Der Bericht wird so angezeigt, wie er auf einer physischen Seite dargestellt werde würde. Diese Ansicht gleicht der Ausgabe durch die Bild- und PDF-Renderingerweiterung. Die Seitenansicht ist keine Bild- oder PDF-Datei, das Layout und die Paginierung des Berichts gleichen jedoch der Ausgabe in diesen Formaten. Sie können die Größe des Berichtsbilds auswählen, z. B. indem Sie die Breite der Seite festlegen.  
  
     Die Seitenansicht hilft Ihnen, zahlreiche Renderingprobleme zu erkennen, die beim Drucken des Berichts auftreten können. Folgende Renderingprobleme können auftreten:  
  
    -   Zusätzliche leere Seiten, da der Bericht zu breit für das Papierformat ist, das für den Bericht angegeben wurde.  
  
    -   Zusätzliche leere Seiten, da der Bericht eine Matrix enthält, die dynamisch erweitert wird, um die angegebene Breite des Papiers zu überschreiten.  
  
    -   Unerwünschte Seitenumbrüche zwischen Gruppen.  
  
    -   falsche Anzeige von Kopf- und Fußzeilen.  
  
    -   Notwendige Änderungen am Berichtslayout für eine bessere Lesbarkeit im gedruckten Format.  
   
##  <a name="bkmk_SaveandDeploy"></a> Speichern und Bereitstellen von paginierten Berichten  
 Sie können Berichte und andere Projektdateien im Berichts-Designer lokal speichern oder auf einem Berichtsserver oder einer SharePoint-Website bereitstellen. Freigegebene Datenquellen, freigegebene Datasets, Berichte, Berichtsressourcen und Berichtsteile können abhängig von den konfigurierten Projektbereitstellungseigenschaften unabhängig oder zusammen bereitgestellt werden. Weitere Informationen finden Sie unter [Configuration and Deployment Properties](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties).  
  
 Beachten Sie, dass Sie Berichte im Berichts-Designer unter Verwendung des Berichtsdefinitionsschemas entwerfen, das von der aktuellen Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]unterstützt wird. Wenn Sie Projektbereitstellungseigenschaften für einen bestimmten Berichtsserver oder eine SharePoint-Website festlegen und den Bericht anschließend speichern, speichert der Berichts-Designer die Berichtsdefinition im Buildverzeichnis in dem Schema, das der Version auf dem Zielberichtsserver entspricht. Um Berichte zu erstellen, die auf einem Berichtsserver einer niedrigeren Version veröffentlicht werden können, löscht der Berichts-Designer Berichtselemente, die im Zielschema nicht vorhanden sind. Dies erfolgt automatisch und ohne Aufforderung. In diesem Fall wird die ursprüngliche Berichtsdefinition im Projektordner beibehalten. Die geänderte Berichtsdefinition, die bereitgestellt wird, befindet sich im Buildordner.  
  
> [!NOTE]  
>  Zum Debuggen von Ausdrücken und Bereitstellungsfehlern müssen Sie die Berichtsdefinition im Buildordner anzeigen. Verwenden Sie nicht **Quelltext anzeigen**. Durch**Quelltext anzeigen** wird die Berichtsdefinitionsquelle aus dem Projektordner angezeigt.  
  
 Weitere Informationen finden Sie unter [Bereitstellung und Versionsunterstützung in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)enthalten.  
  
### <a name="save-a-report-locally"></a>Lokales Speichern eines Berichts  
 Wenn Sie einen Bericht oder andere Projektelemente im Berichts-Designer bearbeiten, werden die Dateien auf dem lokalen Computer oder einer Freigabe auf einem anderen Computer gespeichert, auf den Sie Zugriff haben.  
  
 Wenn Sie Software für die Quellcodeverwaltung verwenden, müssen Sie die Berichte beim Speichern möglicherweise in den Quellcodeverwaltungsserver einchecken. Weitere Informationen finden Sie unter [Source Control](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_SourceControl).  
  
### <a name="deploy-or-publish-paginated-reports"></a>Bereitstellen oder Veröffentlichen von paginierten Berichten  
 Ab [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]können Sie Berichte oder andere Projektelemente in mehreren Versionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsservern bereitstellen. Das Upgrade von Berichtsdefinitionen auf Schemaversionen, die mit den Zielberichtsservern kompatibel sind, steuern Sie mithilfe von Projektkonfigurationen. Zu den mittels Projektkonfigurationen gesteuerten Eigenschaften zählen der Zielberichtsserver, der Ordner, in dem der Buildprozess vorübergehend Berichtsdefinitionen für die Vorschau und Bereitstellung speichert, und die Fehlerebenen. Weitere Informationen finden Sie unter [Konfigurations- und Bereitstellungseigenschaften](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties) und [Festlegen von Bereitstellungseigenschaften &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
### <a name="export-a-paginated-report-to-a-different-file-format"></a>Exportieren eines paginierten Berichts in ein anderes Dateiformat  
 Berichte können in verschiedene Formate exportiert werden. Diese Formate haben Einfluss auf die Funktionsweise einiger Berichtslayouts und interaktiver Funktionen. Weitere Informationen zu Entwurfsüberlegungen zu verschiedenen Ausgabeformaten finden Sie unter [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
   
##  <a name="bkmk_ReportValidationandErrorLevels"></a> Berichtsüberprüfung und Fehlerebenen  
 Berichte werden vor der Vorschau und während der Bereitstellung überprüft. Beim Erstellen von Berichten können verschiedene Erstellungsprobleme auftreten. Berichte können Zeichenfolgen, z. B. Ausdrücke oder Abfragen, enthalten, die mit der von der Projektkonfiguration angegebenen Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nicht kompatibel sind.  
  
 Verwenden Sie die ErrorLevel-Eigenschaft, um die während der Erstellung angezeigten Warnungen und Fehler zu verwalten. Die ErrorLevel-Eigenschaft kann einen Wert von 0 bis einschließlich 4 enthalten. Durch den Wert wird bestimmt, welche Erstellungsprobleme als Fehler und welche als Warnungen gemeldet werden. Der Standardwert ist 2. Die Warnungen und die Fehler werden in das [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)][-Ausgabefenster](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) geschrieben.  
  
 Probleme mit Schweregraden kleiner oder gleich dem Wert von ErrorLevel werden als Fehler gemeldet. Andernfalls werden die Probleme als Warnungen gemeldet.  
  
 In der folgenden Tabelle sind die Fehlerebenen aufgeführt.  
  
|Fehlerebene|Description|  
|-----------------|-----------------|  
|0|Äußerst schwerwiegende und unvermeidliche Erstellungsprobleme, die die Vorschau und Bereitstellung von Berichten verhindern.|  
|1|Schwere Erstellungsprobleme, die das Berichtslayout drastisch ändern.|  
|2|Weniger schwere Erstellungsprobleme, die das Berichtslayout wesentlich ändern.|  
|3|Kleinere Erstellungsprobleme, die das Berichtslayout auf geringfügigere Weise ändern, die möglicherweise nicht auffällt.|  
|4|Wird nur für Veröffentlichungswarnungen verwendet.|  
  
 Wenn Sie versuchen, einen Bericht, der neue Berichtselemente in [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]enthält, in der Vorschau anzuzeigen oder bereitzustellen, können diese Berichtselemente aus dem Bericht entfernt werden. Standardmäßig wird die ErrorLevel-Eigenschaft der Konfiguration auf 2 festgelegt. Dies würde dazu führen, dass der Bericht nicht erstellt wird, sobald die Struktur entfernt wurde. Wenn Sie den Wert der ErrorLevel-Eigenschaft in 0 oder 1 ändern, wird die Struktur jedoch gelöscht, eine Warnung ausgegeben und der Erstellungsvorgang fortgesetzt.  

## <a name="next-steps"></a>Nächste Schritte

[Herunterladen von SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714)  
[Reporting Services in SQL Server Data Tools](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)   
[Abfrageentwurfstools](../../reporting-services/report-data/query-design-tools-ssrs.md)   
[Bereitstellung und Versionsunterstützung in SQL Server Data Tools](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
