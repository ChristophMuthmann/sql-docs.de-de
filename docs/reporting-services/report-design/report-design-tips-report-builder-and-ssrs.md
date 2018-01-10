---
title: Berichtsentwurfstipps (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1490ff0-5b8a-43c1-8d22-e459395db4f6
caps.latest.revision: "12"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6310daa382072ae5125f0f3cff1913548a0801fb
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="report-design-tips-report-builder-and-ssrs"></a>Berichtsentwurfstipps (Berichts-Generator und SSRS)
  Nutzen Sie die folgenden Tipps zum Entwerfen paginierter [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichte.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DesigningReports"></a> Entwerfen von Berichten  
  
-   Ein sorgfältig geplanter Bericht vermittelt Informationen, die als Grundlage für Aktionen dienen können. Identifizieren Sie die Fragen, die der Bericht beantworten soll. Behalten Sie diese Fragen im Kopf, wenn Sie den Bericht entwerfen.  
  
-   Um effektive Datenvisualisierungen zu entwerfen, überlegen Sie sich, wie dem Berichtsbenutzer Informationen einfach vermittelt werden können. Wählen Sie einen Datenbereich aus, der für die visuell darzustellenden Daten geeignet ist. Zum Beispiel vermittelt ein Diagramm zusammenfassende und aggregierte Informationen besser als eine Tabelle, die viele Seiten mit detaillierten Informationen umfasst. Sie können Daten aus einem Dataset in jedem Datenbereich visuell darstellen, einschließlich Diagrammen, Karten, Indikatoren, Sparklines, Datenbalken und Tabellendaten in verschiedenen Gitternetzlayouts auf Grundlage einer Tablix.  
  
-   Wenn Sie planen, den Bericht in einem bestimmten Exportformat zu übermitteln, testen Sie rechtzeitig das Exportformat im Entwurf. Die Funktionsunterstützung ändert sich abhängig vom ausgewählten Renderer.  
  
-   Wenn Sie planen, den Bericht als Abonnement zu übermitteln, testen Sie rechtzeitig das Abonnement im Entwurf. Die Parameterunterstützung ändert sich abhängig vom erstellten Abonnement.  
  
-   Wenn Sie komplexe Layouts erstellen, können Sie das Layout in Phasen entwerfen. Sie können Rechtecke als Container verwenden, um Berichtselemente zu organisieren. Sie können Datenbereiche direkt auf der Entwurfsoberfläche erstellen, um den Arbeitsbereich zu maximieren, und dann jeweils beim Abschließen in den Rechteckcontainer ziehen. Mit Rechtecken als Container können Sie den gesamten Inhalt in einem Schritt positionieren. Rechtecke helfen auch, das Rendern von Berichtselementen auf jeder Seite zu steuern.  
  
-   Wenn Sie einen Bericht übersichtlicher gestalten möchten, können Sie die bedingte Sichtbarkeit verwenden und den Benutzer entscheiden lassen, ob die Elemente angezeigt werden. Sie können die Sichtbarkeit auf Grundlage eines Parameters oder einer Textfeldumschaltfläche festlegen. Sie können ausgeblendete Textfelder bedingt hinzufügen, um Zwischenausdrucksergebnisse anzuzeigen. Wenn ein Bericht unerwartete Daten anzeigt, können Sie diese Zwischenergebnisse zum Debuggen von Ausdrücken anzeigen.  
  
-   Wenn Sie mit geschachtelten Elementen in Tablix-Zellen oder Rechtecken arbeiten, können Sie andere Hintergrundfarben für den Container und enthaltene Elemente festlegen. Standardmäßig wird als Hintergrundfarbe **Keine Farbe**verwendet. Elemente mit einer bestimmten Hintergrundfarbe scheinen durch Elemente mit einer auf **Keine Farbe**festgelegten Hintergrundfarbe hindurch. Diese Methode kann Ihnen helfen, das richtige Element auszuwählen, um Anzeigeeigenschaften festzulegen, z. B. die Rahmensichtbarkeit in Tablix-Zellen.  
  
 Weitere Informationen zu Aspekten, die Sie beim Entwerfen von Berichten berücksichtigen sollten, finden Sie unter [Planen eines Berichts &#40;Berichts-Generator&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md).  
  
##  <a name="NamingConventions"></a> Benennungskonventionen für Berichte, Datenquellen und Datasets  
  
-   Verwenden Sie Benennungskonventionen für Datenquellen und Datasets, die die Quelle der Daten dokumentieren.  
  
    1.  **Datenquellen.** Wenn Sie aus Sicherheitsgründen keinen echten Server oder eine Datenbank verwenden möchten, verwenden Sie ein Alias, das dem Benutzer die Datenquelle angibt.  
  
    2.  **Datasets.** Verwenden Sie einen Namen, der angibt, auf welcher Datenquelle der Dataset basiert.  
  
    3.  **Datenbereiche.** Geben Sie den Typ des Datenbereichs und die darin angezeigten Daten an. Datenbereichsnamen sind in den folgenden Szenarien nützlich:  
  
        1.  **Datenbereich als Berichtsteil.** Wenn Berichtsautoren den Berichtsteilkatalog durchsuchen, ermöglicht ein aussagekräftiger Name das einfachere Auffinden der gesuchten Berichtsteile.  
  
        2.  **Datenbereich als Datenfeed.** Mit entsprechenden Berechtigungen kann ein Berichtsleser einen ATOM-Datenfeed aus einem Datenbereich erstellen.  
  
-   Verwenden Sie Unterstriche statt Leerzeichen in Berichtsnamen. Wenn Sie einen Bericht aus dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportal herunterladen, werden Leerzeichen durch Unterstriche ersetzt. Wenn Sie die Downloadfunktion verwenden, um Berichte lokal zu speichern, und sie dann in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]einschließen, werden mit Unterstrichen Berichtsabhängigkeiten für Unterberichte und Drillthroughlinks genau beibehalten.  
  
##  <a name="Data"></a> Arbeiten mit Daten  
  
-   Rufen Sie im ersten Schritt alle Daten ab, mit denen Sie arbeiten möchten, um sie im Berichtsdatenbereich anzuzeigen. Während Sie die Fragen verfeinern, die der Bericht beantworten soll, überlegen Sie sich, wie Sie die Daten in den Berichtsdatasets auf das Notwendige beschränken können.  
  
-   Schließen Sie im Allgemeinen nur die Daten ein, die in einem Bericht angezeigt werden. Verwenden Sie Abfragevariablen in den Datasetabfragen, um Benutzern die Auswahl der im Bericht anzuzeigenden Daten zu ermöglichen. Stellen Sie beim Erstellen freigegebener Datasets Filter auf Grundlage von Berichtsparametern bereit, um dieselbe Funktionalität bereitzustellen.  
  
-   Wenn Sie schon Erfahrungen beim Erstellen von Abfragen haben, beachten Sie, dass Sie für Zwischendatenmengen die Daten im Bericht und nicht in der Abfrage gruppieren sollten. Wenn Sie die ganze Gruppierung in der Abfrage ausführen, dann tendiert der Bericht dazu, eine Darstellung des Abfrageresultsets zu sein. Andererseits müssen zum Anzeigen von aggregierten Werten für große Datenmengen in einem Diagramm oder einer Matrix keine Detaildaten einbezogen werden.  
  
-   Abhängig von den Anforderungen können Sie Namen und Orte von Berichtsdatenquellen, Datasetabfrage-Befehlstext und Parameterwerte im Bericht anzeigen. Die erste Frage, die viele neue Benutzer haben, richtet sich nach dem Ursprung der Daten. Wenn Sie den Bericht übersichtlicher gestalten möchten, können Sie Textfelder mit diesem Informationstyp bedingt ausblenden und Benutzer entscheiden lassen, ob sie die Informationen anzeigen möchten. Versuchen Sie, diese Informationen auf der letzten Seite des Berichts hinzuzufügen. Legen Sie die Textfeldsichtbarkeit auf Grundlage eines Parameters fest, den der Benutzer ändern kann.  
  
##  <a name="DesignSurface"></a> Interagieren mit der Berichtsentwurfsoberfläche  
 Die Berichtsentwurfsoberfläche ist nicht WYSIWIG. Wenn Sie Berichtselemente auf der Entwurfsoberfläche platzieren, wirkt sich ihr relativer Speicherort darauf aus, wie die Elemente auf der gerenderten Berichtsseite angezeigt werden. Leerraum wird beibehalten.  
  
-   Verwenden Sie Ausrichtungslinien und die Layoutschaltflächen, um Elemente auf der Berichtsentwurfsoberfläche auszurichten und anzuordnen. Beispielsweise können Sie die oberen Bereiche oder die Ränder ausgewählter Elemente ausrichten, ein Element an die Größe eines anderen Elements angleichen oder den Abstand zwischen Elementen anpassen.  
  
-   Passen Sie die Position und Größe von ausgewählten Elementen auf der Entwurfsoberfläche mithilfe der Pfeiltasten an. Die folgenden Tastenkombinationen sind z. B. sehr nützlich:  
  
    -   **Pfeiltasten** Ausgewähltes Berichtselement verschieben  
  
    -   **STRG+Pfeiltasten** Ausgewähltes Berichtselement bewegen  
  
    -   **STRG+UMSCHALT+Pfeiltasten** Ausgewähltes Berichtselement vergrößern oder verkleinern  
  
-   Um einem Rechteck ein Element hinzuzufügen, verwenden Sie die linke obere Spitze der Maus, um auf die ursprüngliche Position des Elements im Rechteckcontainer zu zeigen. Verwenden Sie die Tastenkombinationen, um ausgewählte Objekte zu positionieren. Das Rechteck wird automatisch auf die Größe der enthaltenen Elemente erweitert.  
  
-   Fügen Sie zuerst ein Rechteck und dann die Elemente hinzu, um einer Tablix-Eckzelle mehrere Elemente hinzuzufügen.  
  
     Standardmäßig enthält jede Tablix-Zelle ein Textfeld. Wenn Sie einer Zelle ein Rechteck hinzufügen, ersetzt das Rechteck das Textfeld. Fügen Sie beispielsweise geschachtelte Indikatoren in einem Rechteck in einer Tablix-Zelle ein, um das Erweitern der Größe eines Diagramms oder Indikators zu steuern, wenn die Höhe der Zeile mit der Zelle geändert wird.  
  
-   Verwenden Sie das **Zoom** -Steuerelement, um die Sicht der Entwurfsoberfläche anzupassen. Sie können mit der ganzen Seite oder kleineren Abschnitten der Seite arbeiten.  
  
-   Um Felder aus dem Berichtsdatenbereich in den Gruppierungsbereich zu ziehen, vermeiden Sie das Ziehen des Felds über andere Berichtselemente auf der Entwurfsoberfläche, da dabei die anderen Objekte ausgewählt werden und die Auswahl des Tablix-Datenbereichs aufgehoben wird. Ziehen Sie das Feld im Berichtsdatenbereich nach unten und dann zum Gruppierungsbereich.  
  
###  <a name="Selecting"></a> Auswählen von Elementen  
 Um das gewünschte Objekt auf der Berichtsentwurfsoberfläche auszuwählen, verwenden Sie die ESC-Taste, das Rechtsklick-Kontextmenü, den Bereich Eigenschaften, den Gruppierungsbereich.  
  
-   -   Drücken Sie die ESC-Taste, um den Stapel von Berichtselementen durchzugehen, die den gleichen Platz auf der Entwurfsoberfläche einnehmen.  
  
    -   Bei einigen Berichtselementen können Sie das Rechtsklick-Kontextmenü verwenden, um das Berichtselement oder den gewünschten Teil des Berichtselements auszuwählen.  
  
    -   Die Eigenschaften für die aktuelle Auswahl werden im Eigenschaftenbereich angezeigt.  
  
    -   Um mit Zeilengruppen und Spaltengruppen in einem Tablix-Datenbereich zu arbeiten, wählen Sie die Gruppe im Gruppierungsbereich aus.  
  
 In Berichts-Designer in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]können Sie aus der Dropdownliste von Objekten auf der Eigenschaftenbereichs-Symbolleiste oder in der hierarchischen Sicht von Berichtselementen im Fenster Dokumentgliederung auswählen. Sie können Elemente in diesem Bereich auswählen und sehen, welches Element auf der Entwurfsoberfläche ausgewählt wird. Zum Öffnen des Fensters **Dokumentgliederung** zeigen Sie im Menü **Ansicht**auf **Weitere Fenster**, und klicken Sie dann auf Dokumentgliederung.  
  
##  <a name="ReportItems"></a> Arbeiten mit bestimmten Arten von Berichtselementen  
  
###  <a name="Parameters"></a> Verwenden von Parametern  
  
-   Der primäre Zweck von Berichtsparametern besteht im Filtern von Daten in der Datenquelle und Abrufen nur der für den Zweck des Berichts benötigten Daten.  
  
-   Suchen Sie für Berichtsparameter ein Gleichgewicht zwischen möglicher Interaktivität und Unterstützung des Benutzers dabei, die gewünschten Ergebnisse zu erhalten. Sie können z. B. Standardwerte für einen Parameter auf gängige Werte festlegen.  
  
###  <a name="Text"></a> Arbeiten mit Text  
  
-   Wenn Sie mehrere Zeilen in ein Textfeld einfügen, wird der Text als Lauftext hinzugefügt. Jede Textausführung kann nur als Einheit formatiert werden. Um jede Zeile separat zu formatieren, fügen Sie eine neue Zeile ein, indem Sie nach Bedarf die EINGABETASTE in der Textausführung drücken. Sie können dann die Formatierung und Formate auf jede unabhängige Textzeile im Textfeld anwenden.  
  
-   Sie können Formateigenschaften und Aktionen in einem Textfeld oder einem Platzhaltertext im Textfeld festlegen. Wenn es nur eine Textzeile gibt, ist es effizienter, die Eigenschaften für das Textfeld statt für den Text festzulegen.  
  
###  <a name="Expressions"></a> Arbeiten mit Ausdrücken  
  
-   Machen Sie sich mit einfachen und komplexen Ausdrucksformaten vertraut. Sie können ein einfaches Ausdrucksformat direkt in Textfelder, Eigenschaften im Eigenschaftenbereich oder an Positionen in Dialogfeldern, die einen Ausdruck akzeptieren, eingeben. Weitere Informationen finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
-   Wenn Sie einen Ausdruck erstellen, hilft es, jeden Teil unabhängig zu erstellen und seinen Wert zu überprüfen. Sie können dann alle Teile in einen abschließenden Ausdruck kombinieren. Eine nützliche Technik ist, ein Textfeld in einer Matrixzelle hinzuzufügen, jeden Teil des Ausdrucks anzuzeigen und bedingte Sichtbarkeit im Textfeld festzulegen. Um die Rahmenart und die Farbe zu steuern, wenn das Textfeld ausgeblendet wird, platzieren Sie zuerst das Textfeld in einem Rechteck, und legen Sie dann die Rahmenart und die Farbe des Rechtecks entsprechend der Matrix fest.  
  
###  <a name="Indicators"></a> Arbeiten mit Indikatoren  
  
-   Standardmäßig zeigt ein Indikator mindestens drei Status an. Nachdem Sie einem Bericht einen Indikator hinzugefügt haben, können Sie ihn durch Hinzufügen oder Entfernen des Status konfigurieren. Wählen Sie zur einfacheren Anzeige durch die Benutzer einen Indikator aus, der sich sowohl hinsichtlich der Farbe als auch der Form verändert.  
  
##  <a name="Rendering"></a> Steuern des Renderns von Berichtselementen auf der Berichtsseite  
  
-   Auf der Berichtsentwurfsoberfläche wachsen Berichtselemente, um den Inhalt aus dem verknüpften Dataset, Ausdruck, Unterbericht oder Text aufzunehmen.  
  
    -   Wenn Sie ein Element auf der Berichtsseite positionieren, wird der Abstand zwischen dem Element und allen Elementen, die rechts davon beginnen, der Mindestabstand, der beim horizontalen Wachsen eines Berichtselements beibehalten werden muss. Entsprechend wird der Abstand zwischen einem Element und dem Element darüber der Mindestabstand, der beim vertikalen Wachsen des obersten Elements beibehalten werden muss.  
  
    -   Ein Element in einem Bericht wächst, um die Daten aufzunehmen, und drängt Peer-Elemente (Elemente innerhalb desselben übergeordneten Containers) mithilfe der folgenden Regeln zur Seite:  
  
    -   Jedes Element wird nach unten verschoben, um den Mindestabstand zu Elementen beizubehalten, die über ihm enden.  
  
    -   Jedes Element wird nach rechts verschoben, um den Mindestabstand zu Elementen beizubehalten, die links von ihm enden. Bei Systemen mit Layouts mit Leserichtung von rechts nach links wird jedes Element nach links verschoben, um den Mindestabstand zu Elementen beizubehalten, die rechts von ihm enden.  
  
    -   Container werden erweitert, um den Wachstum von untergeordneten Elementen aufzunehmen. Für ein ausgewähltes Element im Eigenschaftenbereich bezeichnet die Parent-Eigenschaft den Container für das Element. Sie können auch den Bereich "Dokumentgliederung" verwenden, um die Kapselungshierarchie von Berichtselementen anzuzeigen.  
  
    -   Die Symbolleiste **Layout** stellt mehrere Schaltflächen zum Ausrichten von Rändern, Zentrierungen und Abstand für Berichtselemente bereit. Um die Symbolleiste **Layout** zu aktivieren, zeigen Sie im Menü **Ansicht** auf **Symbolleisten**, und klicken Sie dann auf **Layout**.  
  
-   Wenn Sie planen, den Bericht als PDF-Datei zu speichern, muss die Breite des Berichts explizit auf einen Wert eingestellt werden, mit dem Sie die im Exportdateiformat gewünschten Ergebnisse erhalten. Legen Sie z. B. die Breite der Berichtsseite genau auf 7,9375 Zoll und den linken und rechten Rand auf 0,5 Zoll fest.  
  
-   Verwenden Sie **Seitenlayout** und **Seite einrichten** auf der Berichts-Viewer-Symbolleiste, um einen Bericht in einer druckkompatiblen Sicht zu rendern. Gehen Sie zum Entfernen unerwünschter horizontaler Seiten wie folgt vor:  
  
    1.  Entfernen Sie sämtlichen zusätzlichen Leerraum zwischen Datenbereichen und an den Rändern des Berichts.  
  
    2.  Reduzieren Sie Seitenränder im Dialogfeld **Berichtseigenschaften** .  
  
    3.  Verwenden Sie **Rechtecke** als Container, um das Rendern von Berichtselementen zu steuern.  
  
    4.  Ändern Sie in Spaltenüberschriften die Textfeldeigenschaft „WritingMode“, um vertikalen Text zu verwenden.  
  
 Die Kombination dieses Verhaltens, die Breiten- und Höheneigenschaften von Berichtselementen, die Größe des Hauptteils des Berichts, die Seitenhöhe und die Seitenbreitendefinition, die Seitenrandeinstellungen des übergeordneten Berichts und die rendererspezifische Unterstützung für Auslagerungen bestimmen gemeinsam, welche Berichtselemente sich auf einer gerenderten Seite zusammenfügen. Weitere Informationen finden Sie unter [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Berichts-Generator in SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Reporting Services-Tutorials (SSRS)](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Lernprogramme für den Berichts-Generator](../../reporting-services/report-builder-tutorials.md)  
  
  
