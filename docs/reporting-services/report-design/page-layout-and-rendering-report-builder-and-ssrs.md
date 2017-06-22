---
title: Seitenlayout und Rendering (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2358653-35bc-4496-810a-d3ccf02f229f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d688ed124a419017e97d405d7f5bd80e6e3bf530
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="page-layout-and-rendering-report-builder-and-ssrs"></a>Seitenlayout und Rendering (Berichts-Generator und SSRS)
Erfahren Sie mehr über [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Renderingerweiterungen für paginierte Berichte, damit der Bericht genau so aussieht, wie Sie es möchten – einschließlich Seitenlayout, Seitenumbrüchen und Papierformat. 

 Wenn Sie Berichte auf einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver oder im Vorschaufenster von Berichts-Generator oder Berichts-Designer anzeigen, wird der Bericht zuerst vom HTML-Renderer gerendert. Sie können dann den Bericht in andere Formate, z.B. Excel oder durch Trennzeichen getrennte Dateien (CSV) exportieren. Der exportierte Bericht kann dann in Excel oder als Datenquelle für Anwendungen verwendet werden, die CSV-Dateien importieren und verwenden können.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] schließt zum Exportieren von Berichten in andere Formate einen Satz von Renderern ein. Jeder Renderer wendet beim Rendern von Berichten Regeln an. Wenn Sie einen Bericht in ein anderes Dateiformat exportieren, insbesondere für Renderer wie z. B. den Adobe Acrobat (PDF)-Renderer, der Paginierung auf Grundlage der physischen Seitengröße verwendet, müssen Sie möglicherweise das Layout des Berichts ändern, damit der exportierte Bericht nach der Anwendung der Renderingregeln korrekt aussieht und gedruckt wird.  
  
 Die besten Ergebnisse für exportierte Berichte zu erhalten, ist oft ein iterativer Prozess; Sie erstellen und zeigen den Bericht im Berichts-Generator oder Berichts-Designer in der Vorschau an, exportieren den Bericht in das bevorzugte Format, überprüfen den exportierten Bericht und nehmen dann Änderungen am Bericht vor.  
    
##  <a name="PageLayout"></a> Berichtselemente  
 Berichtselemente sind Layoutelemente, die verschiedenen Typen von Berichtsdaten zugeordnet werden. 
 
* Tabelle, Matrix, Liste, Diagramm und Messgerät sind Datenbereichsberichtselemente, die jeweils mit einem Berichtsdataset verknüpft sind. Wenn der Bericht verarbeitet wird, wird der Datenbereich auf der Berichtsseite zur Seite und nach unten erweitert, um Daten anzuzeigen. 

Andere Berichtselemente sind mit einem einzelnen Element verknüpft und zeigen dieses an. 
* Ein **Bildberichtselement** ist mit einem Bild verknüpft. 
* Ein **Textfeld** -Berichtselement enthält entweder einfachen Text wie einen Titel oder einen Ausdruck, der Verweise auf integrierte Felder, Berichtsparameter oder Datasetfelder enthalten kann. 
* Die Berichtselemente **Zeile** und **Rechteck** stellen einfache grafische Elemente auf der Berichtsseite bereit. Das **Rechteck** kann auch als Container für andere Berichtselemente verwendet werden. 

Ein Bericht kann auch Unterberichte enthalten.  
  
## <a name="page-layout"></a>Seitenlayout

 Mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]können Sie Berichtselemente an einer beliebigen Stelle auf der Entwurfsoberfläche platzieren. Sie können die ursprüngliche Form des Berichtselements mithilfe von Ausrichtungslinien und Ziehpunkten zum Ändern der Größe interaktiv positionieren, erweitern und verkleinern. Sie können Datenbereiche mit unterschiedlichen Datasets oder den gleichen Daten in unterschiedlichen Formaten nebeneinander platzieren. Wenn Sie ein Berichtselement auf der Entwicklungsoberfläche platzieren, weist es eine Standardgröße und -form sowie eine ursprüngliche Beziehung mit allen anderen Berichtselementen auf. 
 
 Sie können Berichtselemente in anderen Berichtselementen platzieren, um komplexere Berichtsentwürfe zu erstellen. Zum Beispiel Diagramme oder Bilder in Tabellenzellen, Tabellen in Tabellenzellen und mehrere Bilder in einem Rechteck. Neben der gewünschten Organisation und Gestaltung des Berichts ermöglicht das Platzieren von Berichtselementen in Formen wie Rechtecken die Anzeige von Berichtselementen auf der Berichtsseite zu steuern.  
  
 Ein Bericht kann mehrere Seiten umfassen, wobei Kopf- und Fußzeile auf jeder Seite wiederholt werden. Ein Bericht kann grafische Elemente wie Bilder und Linien sowie eine Reihe von Schriftarten, Farben und Formaten enthalten, die auf Ausdrücken basieren können.  
  
##  <a name="ReportSections"></a> Berichtsabschnitte  
 Ein Bericht besteht aus drei Hauptabschnitten: einer optionalen *Kopfzeile* , einer optionalen *Fußzeile* und einem Berichtshauptteil. Die Kopf- und die Fußzeile des *Berichts* stellen keine separaten Abschnitte dar, sondern bestehen aus den Berichtselementen, die am Anfang und am Ende des Berichts stehen. Die Kopf- und die Fußzeile wiederholen denselben Inhalt oben und unten auf jeder Seite des Berichts. Sie können Bilder, Textfelder und Linien in Kopf- und Fußzeilen einfügen. Im Hauptteil des Berichts können Sie alle verfügbaren Typen von Berichtselementen einfügen.  
  
 Sie können Eigenschaften für Berichtselemente festlegen, um sie anfänglich auf der Seite auszublenden oder anzuzeigen. Sie können Sichtbarkeitseigenschaften für Zeilen, Spalten oder Gruppen für Datenbereiche erstellen und Umschaltflächen einrichten, über die die Benutzer interaktiv Berichtsdaten anzeigen und ausblenden können. Sie können Sichtbarkeit oder ursprüngliche Sichtbarkeit mit Ausdrücken festlegen, einschließlich Ausdrücke, die auf Berichtsparametern basieren.  
  
 Wenn ein Bericht verarbeitet wird, werden die Berichtsdaten mit den Berichtslayoutelementen kombiniert, und die kombinierten Daten werden an einen Berichtsrenderer gesendet. Der Renderer folgt vordefinierten Regeln für die Berichtselementerweiterung und bestimmt, wie viele Daten auf jede Seite passen. Um einen übersichtlichen Bericht zu entwerfen, der für den Renderer, den Sie verwenden möchten, optimiert ist, müssen Sie die Regeln zur Steuerung der Paginierung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] kennen. Weitere Informationen finden Sie unter [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
##  <a name="RenderingExtensions"></a> Renderer  
 Reporting Services schließt einen Satz von Renderern ein, die auch als Renderingerweiterungen bezeichnet werden, mit denen Sie Berichte in andere Formate exportieren können. Es stehen drei Arten von Renderern zur Verfügung:  
  
-   **Datenrenderer** : Datenrenderer entfernen alle Formatierungs- und Layoutinformationen aus dem Bericht und zeigen nur die Daten an. Die mithilfe dieser Option erstellte Datei kann zum Importieren der Rohberichtsdaten in einen anderen Dateityp verwendet werden, z. B. Excel, eine andere Datenbank, eine XML-Datennachricht oder eine benutzerdefinierte Anwendung. Die verfügbaren Datenrenderer sind: CSV und XML.  
  
    > [!NOTE]  
    >  Obwohl es keinen direkten Export für ein anderes Format bereitstellt, generiert Atom-Rendering Datendateien aus Berichten.  
  
-   **Renderer mit weichem Seitenumbruch:** Renderer mit weichem Seitenumbruch behalten das Berichtslayout und die Formatierung bei. Die mithilfe dieser Option erstellte Datei wird für die Bildschirmanzeige und -bereitstellung optimiert, beispielsweise auf einer Webseite. Die folgenden Renderer mit weichem Seitenumbruch sind verfügbar: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word, Webarchiv (MHTML) und HTML.  
  
-   **Renderer mit hartem Seitenumbruch:** Renderer mit hartem Seitenumbruch behalten das Berichtslayout und die Formatierung bei. Die mithilfe dieser Option erstellte Datei wird für einen konsistenten Druck oder für die Onlineanzeige in einem Buchformat optimiert. Die folgenden Renderer mit festem Seitenumbruch sind verfügbar: TIFF und PDF.  
  
 Wenn Sie einen Bericht im Berichts-Generator oder Berichts-Designer in der Vorschau anzeigen oder einen Bericht auf einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver ausführen, wird der Bericht immer zuerst in HTML gerendert. Nachdem Sie den Bericht ausgeführt haben, können Sie ihn in andere Dateiformate exportieren. Weitere Informationen finden Sie unter [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)kennen.  
  
##  <a name="RenderingBehaviors"></a> Renderingverhalten  
 Abhängig vom Renderer, den Sie auswählen, werden bestimmte Regeln beim Rendern des Berichts angewendet. Wie sich Berichtselemente auf einer Seite zusammenfügen, wird durch die Kombination folgender Faktoren bestimmt:  
  
-   Renderingregeln.  
-   Die Breite und die Höhe von Berichtselementen.  
-   Die Größe des Berichtshauptteils.  
-   Die Breite und die Höhe der Seite.  
-   Rendererspezifische Unterstützung für Auslagerungen.  
  
 Im HTML- und MHTML-Format exportierte Berichte sind beispielsweise für die Anzeige auf einem Computerbildschirm optimiert, bei der Seiten unterschiedliche Längen aufweisen können.  
  
 Weitere Informationen finden Sie unter [Renderingverhalten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
   
##  <a name="Pagination"></a> Paginierung  
 Paginierung bezieht sich auf die Anzahl der Seiten in einem Bericht und wie Berichtselemente auf diesen Seiten angeordnet werden. Die Paginierung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ändert sich abhängig von der Renderingerweiterung, die Sie zum Anzeigen und Übermitteln des Berichts verwenden, sowie von den Seitenumbruchseinstellungen, die Sie für den Bericht konfiguriert haben.  
  
 Um einen übersichtlichen Bericht für Ihre Benutzer zu entwerfen, der für den Renderer, mit dem Sie den Bericht übermitteln möchten, optimiert ist, müssen Sie die Regeln zur Steuerung der Paginierung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]kennen. Die Paginierung hat typischerweise keine Auswirkungen auf Berichte, die mit den Erweiterungen für **Datenrenderer** und **Renderer mit weichem Seitenumbruch** exportiert werden. Wenn Sie eine Datenrenderingerweiterung verwenden, wird der Bericht als Tabellenrowset in einem XML- oder CSV-Format gerendert. Um sicherzustellen, dass die exportierten Berichtsdaten verwendet werden können, müssen Sie die Regeln für das Rendering eines vereinfachten Tabellenrowsets verstehen.  
  
 Wenn Sie eine Erweiterung für ein **Rendering mit weichem Seitenumbruch** verwenden, z.B. die HTML-Renderingerweiterung, möchten Sie möglicherweise wissen, wie der ausgedruckte Bericht aussieht und wie er aussieht, wenn ein Renderer mit einem harten Seitenumbruch verwendet wird, wie z.B. PDF. Während der Erstellung oder des Updates eines Berichts können Sie ihn in der Vorschau anzeigen und im Berichts-Generator und Berichts-Designer exportieren.  
  
 Die **Renderer mit hartem Seitenumbruch** haben die größten Auswirkungen auf das Berichtslayout und die physische Seitengröße. Weitere Informationen finden Sie unter [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
   
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
 In diesem Abschnitt werden Prozeduren aufgelistet, die Ihnen Schritt für Schritt das Arbeiten mit der Paginierung in Berichten erklären.  
  
-   [Hinzufügen eines Seitenumbruchs &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md)  
  
-   [Anzeigen von Zeilen- und Spaltenüberschriften auf mehreren Seiten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)  
  
-   [Hinzufügen oder Entfernen einer Seitenkopf- oder Seitenfußzeile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)  
  
-   [Sichtbarhalten von Kopfzeilen beim Scrollen durch einen Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
-   [Anzeigen von Seitenzahlen oder anderen Berichtseigenschaften &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)  
  
-   [Ausblenden einer Seitenkopf- oder Seitenfußzeile auf der ersten oder letzten Seite &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)  
  
##  <a name="InThisSection"></a> In diesem Abschnitt  
 Die folgenden Themen enthalten weitere Informationen zu Seitenlayout und Rendering.  
  
 [Seitenkopf- und Seitenfußzeilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
 Stellt Informationen zum Verwenden von Headern und Fußzeilen in Berichten bereit und wie die Paginierung mit ihnen gesteuert wird.  
  
 [Steuern von Seitenumbrüchen, Überschriften, Spalten und Zeilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)  
 Stellt Informationen zum Verwenden von Seitenumbrüchen bereit.  
  
## <a name="see-also"></a>Siehe auch  
 [Interaktive Funktionalität für verschiedene Berichtsrenderingerweiterungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Exportieren von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
