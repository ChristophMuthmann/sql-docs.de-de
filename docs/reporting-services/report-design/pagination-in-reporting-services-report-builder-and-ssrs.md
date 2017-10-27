---
title: Paginierung in Reporting Services (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0894b0d-dc5b-4a75-8142-75092972a034
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b9e295143b577d99732186b0cefda5be908c1c34
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="pagination-in-reporting-services-report-builder--and-ssrs"></a>Paginierung in Reporting Services (Berichts-Generator und SSRS)
  Paginierung bezieht sich auf die Anzahl der Seiten in einem Bericht und wie Berichtselemente auf diesen Seiten angeordnet werden. Paginierung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ändert sich abhängig von der Renderingerweiterung, die Sie zum Anzeigen und Übermitteln des Berichts verwenden. Wenn Sie einen Bericht auf dem Berichtsserver erstellen, verwendet der Bericht den HTML-Renderer. Für HTML gilt ein bestimmter Satz von Paginierungsregeln. Wenn Sie den gleichen Bericht nach PDF exportieren, wird beispielsweise der PDF-Renderer verwendet, und es findet ein anderer Satz von Regeln Anwendung. Daher wird der Bericht unterschiedlich paginiert. Um einen übersichtlichen Bericht für Ihre Benutzer zu entwerfen, der für den Renderer, mit dem Sie den Bericht übermitteln möchten, optimiert ist, müssen Sie die Regeln zur Steuerung der Paginierung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]kennen.  
  
 In diesem Thema wird erörtert, wie sich Seitengröße und Berichtslayout auf das Rendern des Berichts durch Renderer von harten Seitenumbrüchen auswirken. Im Bereich **Berichtseigenschaften** , im Bereich **Eigenschaften** oder im Dialogfeld **Seite einrichten** können Sie Eigenschaften festlegen, mit denen die physische Seitengröße und die Ränder geändert und der Bericht in Spalten aufgeteilt werden können. Sie können auf den Bereich **Berichtseigenschaften** zugreifen, indem Sie auf den blauen Bereich außerhalb des Hauptteils des Berichts klicken. Zum Öffnen des Dialogfelds **Seite einrichten** klicken Sie auf der Registerkarte Start auf **Ausführen** und dann auf der Registerkarte Ausführen auf **Seite einrichten** .  
  
> [!NOTE]  
>  Wenn Sie einen Bericht so entworfen haben, dass er eine Seite breit ist, er aber über mehrere Seiten gerendert wird, stellen Sie sicher, dass die Breite des Hauptteils des Berichts, einschließlich Ränder, nicht größer als die physische Seitenbreite ist. Damit keine leeren Seiten im Bericht eingefügt werden, können Sie die Containergröße durch Ziehen der Containerecke nach links reduzieren.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="the-report-body"></a>Hauptteil des Berichts  
 Der Hauptteil des Berichts ist ein rechteckiger Container, der als Leerraum auf der Entwurfsoberfläche angezeigt wird. Er lässt sich je nach den enthaltenen Berichtselementen vergrößern oder verkleinern. Der Hauptteil des Berichts spiegelt nicht die physische Seitengröße wider. Er kann über die Seitengrenzen hinaus erweitert werden und sich über mehrere Berichtsseiten erstrecken. Einige Renderer, wie [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], Word, HTML und MHTML, rendern Berichte, die je nach Seiteninhalt vergrößert oder verkleinert werden. In diesen Formaten gerenderte Berichte werden für die Bildschirmanzeige, z. B. in einem Webbrowser, optimiert. Diese Renderer fügen vertikale Seitenumbrüche hinzu, sofern erforderlich.  
  
 Sie können den Hauptteil des Berichts mit einer Rahmenfarbe, einer Rahmenart und einer Rahmenbreite formatieren. Sie können auch eine Hintergrundfarbe und ein Hintergrundbild hinzufügen.  
  
## <a name="the-physical-page"></a>Die physische Seite  
 Die physische Seitengröße entspricht dem Papierformat. Das Papierformat, das Sie für den Bericht angeben, steuert das Rendern des Berichts. Berichte, die in Formaten mit harten Seitenumbrüchen gerendert werden, fügen basierend auf der physischen Seitengröße horizontal und vertikal Seitenumbrüche ein. Damit wird eine optimale Übersichtlichkeit beim Drucken oder Anzeigen des Berichts in einem Dateiformat mit harten Seitenumbrüchen erzielt. In Formaten mit weichen Seitenumbrüchen gerenderte Berichte fügen basierend auf der physischen Seitengröße horizontal Seitenumbrüche ein. Damit wird eine optimale Übersichtlichkeit beim Anzeigen des Berichts in einem Webbrowser erreicht.  
  
 Das Seitenformat beträgt standardmäßig 8,5 x 11 Zoll. Sie können dieses Format jedoch über den Bereich **Berichtseigenschaften** , das Dialogfeld **Seite einrichten** oder über die Eigenschaften PageHeight und PageWidth im Bereich **Eigenschaften** ändern. Das Seitenformat wird nicht dem Inhalt des Hauptteils des Berichts entsprechend vergrößert oder verkleinert. Wenn der Bericht auf einer einzelnen Seite angezeigt werden soll, muss der gesamte Inhalt des Hauptteils des Berichts auf die physische Seite passen. Passt der Inhalt nicht und Sie verwenden ein Format mit harten Seitenumbrüchen, sind für den Bericht zusätzliche Seiten erforderlich. Wenn der Hauptteil des Berichts über den rechten Rand der physischen Seite hinausragt, wird ein horizontaler Seitenumbruch eingefügt. Wenn der Hauptteil des Berichts über den unteren Rand der physischen Seite hinausragt, wird ein vertikaler Seitenumbruch eingefügt.  
  
 Wenn Sie das im Bericht definierte physische Seitenformat überschreiben möchten, können Sie das physische Seitenformat in den Geräteinformationseinstellungen für den entsprechenden Renderer angeben, mit dem Sie den Bericht exportieren. Weitere Informationen finden Sie unter [Geräteinformationseinstellungen in Reporting Services](http://go.microsoft.com/fwlink/?LinkId=102515).  
  
### <a name="margins"></a>Ränder  
 Ränder werden vom Rand der physischen Seitendimensionen nach innen zur angegebenen Seitenrandeinstellung gezogen. Erstreckt sich ein Berichtselement in den Randbereich, wird es abgeschnitten, sodass der überlappende Bereich nicht gerendert wird. Wenn Sie Seitenränder angeben, durch die die horizontale oder vertikale Seitenbreite null ergibt, werden die Seitenrandeinstellungen standardmäßig auf null gesetzt. Seitenränder werden im Bereich **Berichtseigenschaften** , im Dialogfeld **Seite einrichten** oder durch Ändern der Eigenschaften TopMargin, BottomMargin, LeftMargin und RightMargin im Bereich **Eigenschaften** festgelegt. Wenn Sie die im Bericht definierte Seitenrandgröße überschreiben möchten, können Sie die Randgröße in den Geräteinformationseinstellungen für den entsprechenden Renderer angeben, mit dem Sie den Bericht exportieren.  
  
 Der Bereich der physischen Seite, der nach Zuweisen von Raum für Ränder, Spaltenabstände und Seitenkopf- und Seitenfußzeile verbleibt, wird als *verwendbarer Seitenbereich*bezeichnet. Ränder werden nur übernommen, wenn Sie Berichte in Renderingformaten mit harten Seitenumbrüchen rendern und drucken. Das folgende Bild gibt den Rand und verwendbaren Seitenbereich einer physischen Seite an.  
  
 ![Physische Seite mit Rändern und verwendbarem Bereich. ] (../../reporting-services/report-design/media/rspagemargins.gif "Physische Seite mit Rändern und verwendbarem Bereich.")  
  
### <a name="newsletter-style-columns"></a>Spalten im Zeitungsformat  
 Ihr Bericht kann in Spalten, wie Spalten in einer Zeitung, unterteilt werden, die als logische Seiten behandelt und auf derselben physischen Seite gerendert werden. Sie sind von links nach rechts und von oben nach unten angeordnet und werden durch Leerraum zwischen den einzelnen Spalten abgetrennt. Wird der Bericht in mehr als eine Spalte unterteilt, wird jede physische Seite vertikal in Spalten unterteilt. Jede Spalte wird als eine logische Seite behandelt. Angenommen, es sind zwei Spalten auf einer physischen Seite vorhanden. Dann füllt der Inhalt des Berichts zunächst die erste und anschließend die zweite Spalte aus. Wenn der Bericht nicht vollständig in die ersten beiden Spalten passt, füllt der Bericht die erste Spalte und anschließend die zweite Spalte auf der nächsten Seite aus. Die Spalten werden weiter von links nach rechts und oben nach unten ausgefüllt, bis alle Berichtselemente gerendert sind. Wenn Sie Spaltengrößen angeben, durch die die horizontale oder vertikale Breite null ergibt, wird der Spaltenabstand standardmäßig auf null gesetzt.  
  
 Spalten werden im Bereich **Berichtseigenschaften** , im Dialogfeld **Seite einrichten** oder durch Ändern der Eigenschaften TopMargin, BottomMargin, LeftMargin und RightMargin im Bereich **Eigenschaften** festgelegt. Wenn Sie eine nicht definierte Seitenrandgröße verwenden möchten, können Sie die Randgröße in den Geräteinformationseinstellungen für den entsprechenden Renderer angeben, mit dem Sie den Bericht exportieren. Spalten werden nur übernommen, wenn Sie Berichte im PDF- oder in Bildformaten rendern und drucken. Das folgende Bild gibt den verwendbaren Seitenbereich einer Seite mit Spalten an.  
  
 ![Physische Seite mit gezeichneten Spalten. ] (../../reporting-services/report-design/media/rspagecolumns.gif "Physische Seite mit gezeichneten Spalten.")  
  
## <a name="page-breaks-and-page-names"></a>Seitenumbrüche und Seitennamen  
 Durch die Verwendung von Seitennamen ist ein Bericht u. U. besser zu lesen, und die darin enthaltenen Daten sind einfacher zu überwachen und zu exportieren. Reporting Services stellen Eigenschaften für Berichte und Tablix-Datenbereiche (Tabelle, Matrix und Liste), Gruppen und Rechtecke im Bericht bereit, mit denen die Paginierung gesteuert, Seitenzahlen zurückgesetzt und bei Seitenumbrüchen neue Namen für Berichtsseiten angegeben werden können. Mit diesen Funktionen können Berichte unabhängig vom Format optimiert werden, in dem sie gerendert werden, sie sind jedoch insbesondere beim Exportieren von Berichten in Excel-Arbeitsmappen hilfreich.  
  
 Die InitialPageName-Eigenschaft gibt den ursprünglichen Seitennamen des Berichts an. Wenn der Bericht keine Seitennamen für Seitenumbrüche enthält, dann wird der ursprüngliche Seitenname für alle neuen von Seitenumbrüchen erstellten Seiten verwendet. Es ist nicht erforderlich, einen ursprünglichen Seitennamen zu verwenden.  
  
 Ein gerenderter Bericht kann einen neuen Seitennamen für die neue Seite bereitstellen, die durch einen Seitenumbruch verursacht wird. Um den Seitennamen anzugeben, legen Sie die PageName-Eigenschaft einer Tabelle, Matrix, Liste, Gruppe oder eines Rechtecks festgelegt. Es ist nicht erforderlich, dass Sie Seitennamen auf Umbrüchen angeben. Wenn Sie keine Angabe machen, wird stattdessen der Wert für InitialPageName verwendet. Wenn InitialPageName ebenfalls leer ist, hat die neue Seite keinen Namen.  
  
 Tablix-Datenbereiche (Tabelle, Matrix und Liste), Gruppen und Rechtecke unterstützen Seitenumbrüche.  
  
 Der Seitenumbruch schließt die folgenden Eigenschaften ein:  
  
-   BreakLocation gibt die Position des Umbruchs für das Berichtselement an, für das Seitenumbrüche aktiviert sind: am Anfang, am Ende oder am Anfang und am Ende. In Gruppen kann sich BreakLocation zwischen Gruppen befinden.  
  
-   Disabled gibt an, ob ein Seitenumbruch für das Berichtselement übernommen wird. Wenn diese Eigenschaft True ergibt, wird der Seitenumbruch ignoriert. Diese Eigenschaft wird verwendet, um Seitenumbrüche dynamisch auf Grundlage von Ausdrücken zu deaktivieren, wenn der Bericht ausgeführt wird.  
  
-   ResetPageNumberindicates gibt an, ob die Seitenzahl auf 1 zurückgesetzt werden soll, wenn ein Seitenumbruch auftritt. Wenn diese Eigenschaft True ergibt, wird die Seitenzahl zurückgesetzt.  
  
 Sie können die BreakLocation-Eigenschaft in den Dialogfeldern **Tablix-Eigenschaften**, **Rechteckeigenschaften**oder **Gruppeneigenschaften** festlegen, Sie müssen jedoch die Eigenschaften Disabled, ResetPageNumber und PageName im Eigenschaftenbereich von Berichts-Generator festlegen. Wenn die Eigenschaften im Eigenschaftenbereich nach Kategorie organisiert werden, befinden sich die Eigenschaften in der Kategorie **Seitenumbruch** . Für Gruppen befindet sich die Kategorie **Seitenumbruch** in der Kategorie **Gruppe** .  
  
 Sie können den Wert der Eigenschaften Disabled und ResetPageNumber mithilfe von Konstanten und einfachen oder komplexen Ausdrücken festlegen. Für die BreakLocation-Eigenschaft kann jedoch kein Ausdruck verwenden. Weitere Informationen zum Schreiben und Verwenden von Ausdrücken finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 Im Bericht können Sie Ausdrücke schreiben, die anhand der **Globals** -Auflistung auf die aktuellen Seitennamen oder die Seitenzahlen verweisen. Weitere Informationen finden Sie unter [Integrierte globale Werte und Benutzerverweise &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
### <a name="naming-excel-worksheet-tabs"></a>Benennen von Registerkarten in Excel-Arbeitsblättern  
 Diese Eigenschaften sind nützlich, wenn Sie Berichte in Excel-Arbeitsmappen exportieren. Verwenden Sie die InitialPage-Eigenschaft, um einen Standardnamen für den Registerkartennamen des Arbeitsblatts anzugeben, wenn Sie den Bericht exportieren, und verwenden Sie Seitenumbrüche und die PageName-Eigenschaft, um andere Namen für jedes Arbeitsblatt bereitzustellen. Jede neue von einem Seitenumbruch definierte Berichtsseite wird in ein anderes vom Wert der PageName-Eigenschaft benanntes Arbeitsblatt exportiert. Wenn PageName leer ist, der Bericht jedoch einen ursprünglichen Seitennamen enthält, wird in allen Arbeitsblättern in der Excel-Arbeitsmappe der gleiche Name verwendet – der ursprüngliche Seitenname.  
  
 Weitere Informationen zur Funktion dieser Eigenschaften beim Exportieren von Berichten nach Excel finden Sie unter [Exportieren nach Microsoft Excel &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Seitenlayout und Rendering &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  

