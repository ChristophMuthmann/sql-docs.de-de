---
title: Berichts-Generator in SQL Server 2016 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
caps.latest.revision: 35
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 5009b0c7ebe8fae67fe51a885dd9f5bf92dc69f9
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="report-builder-in-sql-server-2016"></a>Berichts-Generator in SQL Server 2016
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] ist ein Tool zum Erstellen von paginierten Berichten, für Geschäftsbenutzer, die es bevorzugen, in einer eigenständigen Umgebung zu arbeiten, statt den Berichts-Designer in Visual Studio zu verwenden.  Wenn Sie einen paginierten Bericht erstellen, erstellen Sie Berichtsdefinitionen, die angeben, von woher die Daten abgerufen werden sollen, welche Daten abgerufen werden sollen und wie die Daten dargestellt werden sollen. Wenn Sie den Bericht ausführen lassen, nimmt der Berichtsprozessor die von Ihnen angegebene Berichtsdefinition, ruft die Daten ab und kombiniert sie mit dem Berichtslayout, um den Bericht zu erstellen. Sie können eine Vorschau Ihres Berichts in [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] anzeigen und Ihren Bericht auf einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver im einheitlichen Modus oder im integrierten SharePoint-Modus veröffentlichen. Dort können andere ihn ausführen.  
  
 ![rs_Erste Schritte mit einem Bericht](../../reporting-services/report-builder/media/rs-gettingstartedreport.png "rs_GettingStartedReport")  
  
 Dieser paginierte Bericht enthält eine Matrix mit Zeilen- und Spaltengruppen, Sparklines, Indikatoren und einem Zusammenfassungskreisdiagramm in der Eckzelle sowie eine Karte mit zwei Sätzen geografischer Daten, die durch Farbe und Kreisgröße dargestellt werden.  
  
##  <a name="JumpStartReptCreation"></a> Beschleunigte Berichtserstellung  
  
-   **Beginnen Sie mit einem freigegebenen Dataset**. Freigegebene Datasets sind Abfragen, die auf einer freigegebenen Datenquelle basieren und auf einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtserver im einheitlichen Modus oder im integrieren SharePoint-Modus gespeichert sind.  
  
-   **Beginnen Sie mit dem Tabellen-, Matrix- oder Diagramm-Assistenten**. Wählen Sie eine Datenquellenverbindung aus, verschieben Sie Felder per Drag &amp; Drop, um eine Datasetabfrage zu erstellen, wählen Sie das Layout und Format aus, und passen Sie den Bericht an.  
  
-   **Beginnen Sie mit dem Karten-Assistenten** , um Berichte zu erstellen, die aggregierte Daten vor einem geografischen oder geometrischen Hintergrund anzeigen. Kartendaten können räumliche Daten aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage oder einer ESRI-Shape-Datei (Environmental Systems Research Institute, Inc.) sein. Sie können auch einen [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Bing Map-Kachelhintergrund hinzufügen.  
  
-   **Beginnen Sie Ihren Bericht mit Berichtsteilen**. Berichtsteile sind Berichtselemente, die separat auf einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver im einheitlichen Modus oder im integrierten SharePoint-Modus veröffentlicht wurden. Berichtsteile können in anderen Berichten wiederverwendet werden. Berichtselemente wie Tabellen, Matrizen, Diagramme und Bilder können als Berichtsteile veröffentlicht werden.  
  
##  <a name="DesignRept"></a> Entwerfen des Berichts  
  
-   **Erstellen Sie paginierte Berichte mit Tabellen-, Matrix-, Diagramm- und Freiformberichtslayouts.** Erstellen Sie Tabellenberichte für spaltenbasierte Daten, Matrixberichte für zusammengefasste Daten (wie Kreuztabellenberichten oder PivotTable-Berichten), Diagrammberichte für grafische Daten und Freiformberichte für alle anderen Daten. In Berichte können andere Berichte und Diagramme sowie Listen, Grafiken und Steuerelemente für dynamische webbasierte Anwendungen eingebettet werden.  
  
-   **Erstellen Sie Berichte aus unterschiedlichen Datenquellen.** Erstellen Sie Berichte mit Daten aus beliebigen Datenquellentypen mit einem verwalteten [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Datenanbieter, einem OLE DB-Anbieter oder einer ODBC-Datenquelle. Sie können Berichte erstellen, die relationale und mehrdimensionale Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbanken, Oracle-Hyperion- sowie anderen Datenbanken enthalten. Sie können eine XML-Datenverarbeitungserweiterung verwenden, um Daten von jeder XML-Datenquelle abzurufen. Mit Tabellenwertfunktionen können Sie benutzerdefinierte Datenquellen entwerfen.  
  
-   **Ändern Sie vorhandene Berichte.** Mit [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]können Sie im [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]-Berichts-Designer erstellte Berichte benutzerdefiniert anpassen und aktualisieren.  
  
-   **Ändern Sie die Daten** durch Filtern, Gruppieren und Sortieren oder Hinzufügen von Formeln oder Ausdrücken.  
  
-   **Fügen Sie Diagramme, Messgeräte, Sparklines und Indikatoren hinzu** , um Daten in einem visuellen Format zusammenzufassen und große Mengen aggregierter Informationen auf einen Blick darzustellen.  
  
-   **Fügen Sie interaktive Funktionen hinzu** , z.B. Dokumentstrukturen, Ein-/Ausblendeschaltflächen und Drillthroughlinks zu Unterberichten und Drillthroughberichten. Verwenden Sie Parameter und Filter, um Daten für benutzerdefinierte Sichten zu filtern.  
  
-   **Betten Sie Bilder und andere Ressourcen ein** , oder verweisen Sie auf diese Ressourcen (auch externe Inhalte).  
  
##  <a name="ManageRpt"></a> Verwalten des Berichts  
  
-   **Speichern Sie die Definition des Berichts** auf Ihrem Computer oder dem Berichtsserver speichern, wo Sie ihn verwalten und für andere Benutzer freigeben können.  
  
-   **Wählen Sie ein Darstellungsformat aus** , wenn Sie den Bericht öffnen, oder nachdem Sie den Bericht geöffnet haben. Sie können weborientierte, seitenorientierte und Desktopanwendungsformate auswählen. Zu den Formaten gehören HTML, MHTML, PDF, XML, CSV, TIFF, Word und Excel.  
  
-   **Richten Sie Abonnements ein.** Nachdem Sie den Bericht auf dem Berichtsserver oder einem Berichtsserver im integrierten SharePoint-Modus veröffentlicht haben, können Sie ihn so konfigurieren, dass er zu einer bestimmten Zeit ausgeführt wird. Sie können auch einen Berichtsverlauf erstellen und E-Mail-Abonnements einrichten.  
  
-   **Generieren Sie Datenfeeds** aus dem Bericht, indem Sie die Reporting Services Atom-Renderingerweiterung verwenden.  
  
> [!NOTE]  
>  Veröffentlichte Berichte werden auf einem Berichtsserver oder einem Berichtsserver im integrierten SharePoint-Modus von einem Berichtsserveradministrator verwaltet. Berichtsserveradministratoren können die Sicherheit definieren, Eigenschaften festlegen und Vorgänge planen, wie Berichtsverlauf und E-Mail-Übermittlung von Berichten. Sie können freigegebene Zeitpläne und freigegebene Datenquellen erstellen und zur allgemeinen Verwendung zur Verfügung stellen. Administratoren verwalten auch alle Berichtsserverordner. Welche Verwaltungsaufgaben ausgeführt werden können, hängt von den Berechtigungen des Benutzers ab.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
  [Start Report Builder (Starten des Berichts-Generators.)](../../reporting-services/report-builder/start-report-builder.md)  
  
  [Install Report Builder (Installieren des Berichts-Generators)](../../reporting-services/install-windows/install-report-builder.md)

  [Neues in Reporting Services und beim Berichts-Generator für SQL Server 2016](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)  
  Beschreibt die neuen Funktionen in dieser Version von [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] und [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)], einschließlich Karten.   
  [Lernprogramm: Erstellen eines Quick-Diagrammberichts offline](../../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 Bietet eine Einführung für [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] und die Assistenten, die zur Verfügung stehen, um Ihnen bei der Erstellung von Berichten zu helfen. Das Lernprogramm enthält eine Reihe von Daten, mit denen Sie arbeiten können, ohne eine Verbindung mit einer Datenquelle herstellen zu müssen.  
  
 [Planen eines Berichts &#40;Berichts-Generator&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md)  
 Enthält Informationen zu den Punkten, die Sie vor dem Erstellen des Berichts beachten sollten.  
  
 [Berichtserstellungskonzepte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
 Definiert Schlüsselkonzepte, die in der gesamten [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] -Dokumentation verwendet werden.  
  
 [Berichtsentwurfsansicht &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
 Erläutert die unterschiedlichen Bereiche und Abschnitte der Berichtsentwurfsansicht.  
  
 [Freigegebene Dataset-Entwurfsansicht &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)  
 Erläutert die unterschiedliche Bereiche und Abschnitte der Entwurfsansicht für freigegebene Datasets.  
  
 [Tastenkombinationen &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
 Bietet eine Übersicht über die verfügbaren Tastenkombinationen für die Navigation und das Entwerfen von Berichten im [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)].  
  

