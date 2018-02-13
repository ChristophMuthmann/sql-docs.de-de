---
title: Exportieren nach Microsoft Excel (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/09/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74f726fc-2167-47af-9093-1644e03ef01f
caps.latest.revision: 
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 604952211abf63d6dacb111c8170d678acd2d80a
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="exporting-to-microsoft-excel-report-builder-and-ssrs"></a>Exporting to Microsoft Excel (Report Builder and SSRS)
  Die Excel-Renderingerweiterung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] rendert einen paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht im [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Format (XLSX). Mit der Excel-Renderingerweiterung spiegelt die Breite von Spalten in Excel die Breite von Spalten in Berichten genauer wider.  
  
 Das Format ist Office Open XML. Der Inhaltstyp von Dateien, die vom Renderer generiert werden, ist **application/vnd.openxmlformats-officedocument.spreadsheetml.sheet** , und die Dateierweiterung lautet „.xlsx“.  
  
 Sie können einige Standardeinstellungen für diesen Renderer ändern, indem Sie die Geräteinformationseinstellungen ändern. Weitere Informationen finden Sie unter [Excel Device Information Settings](../../reporting-services/excel-device-information-settings.md).  
  
 Weitere Informationen zum Exportieren nach Excel finden Sie unter [Exportieren von Berichten (Berichts-Generator und SSRS)](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
> [!IMPORTANT]  
>  Wenn Sie einen Parameter vom Typ **String**(Zeichenfolge) definieren, wird für den Benutzer ein Textfeld bereitgestellt, das jeden beliebigen Wert annehmen kann. Wenn ein Berichtsparameter nicht an einen Abfrageparameter gebunden ist und die Parameterwerte im Bericht enthalten sind, können Benutzer des Berichts Ausdruckssyntax, ein Skript oder eine URL in den Parameterwert eingeben und den Bericht für Excel rendern. Wenn anschließend ein anderer Benutzer den Bericht anzeigt und auf die gerenderten Parameterinhalte klickt, führt der Benutzer möglicherweise unbeabsichtigt das bösartige Skript bzw. den bösartigen Link aus.  
>   
>  Um das Risiko der versehentlichen Ausführung schädlicher Skripts zu minimieren, sollten gerenderte Berichte nur aus vertrauenswürdigen Quellen geöffnet werden. Weitere Informationen zum Schützen von Berichten finden Sie unter [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md).  
  
##  <a name="ExcelLimitations"></a> Einschränkungen in Excel  
 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] Einschränkungen für exportierte Berichte. Die wichtigsten Einschränkungen sind folgende:  
  
-   Die maximale Spaltenbreite ist auf 255 Zeichen bzw. 1726,5 Punkte beschränkt. Der Renderer prüft nicht, ob die Spaltenbreite unterhalb der Grenze liegt.  
  
-   Die maximale Anzahl an Zeichen in einer Zeile ist auf 32.767 Zeichen beschränkt. Wenn diese Einschränkung überschritten wird, zeigt der Renderer eine Fehlermeldung an.  
  
-   Die maximale Zeilenhöhe beträgt 409 Punkte. Wenn die Inhalte der Zeile dazu führen, dass die Zeilenhöhe 409 Punkte überschreitet, zeigt die Excel-Zelle eine Teilmenge des Texts bis zu 409 Punkten. Der Rest der Zelleninhalte liegt weiterhin innerhalb der Zelle (bis zur maximalen Anzahl von 32.767 Zeichen in Excel).

-  Da die maximale Zeilenhöhe 409 Punkte beträgt, teilt Excel die Zelleninhalte in mehrere Zeilen auf, wenn die definierte Höhe der Zelle im Bericht größer als 409 Punkte ist.
  
-   Die maximale Anzahl an Arbeitsblättern wird nicht in Excel definiert. Stattdessen können externe Faktoren wie der Arbeitsspeicher und der Speicherplatz dazu führen, dass Einschränkungen auftreten.  
  
-   In Gliederungen ermöglicht Excel maximal sieben geschachtelte Ebenen.  
  
-   Falls sich das Berichtselement, das steuert, ob ein anderes Element ein- oder ausgeschaltet wird, nicht in der vorherigen bzw. nächsten Zeile oder Spalte des Elements befindet, das ein- oder ausgeschaltet wird, wird die Gliederung ebenfalls deaktiviert.  
  
 Weitere Informationen zu Excel-Beschränkungen finden Sie unter [Spezifikationen und Beschränkungen in Excel](https://support.office.com/article/Excel-specifications-and-limits-CA36E2DC-1F09-4620-B726-67C00B05040F).  
  
### <a name="sizes-of-excel-2003-xls-files"></a>Größen von Excel 2003-Dateien (XLS)  
  
> [!IMPORTANT]  
>  Die [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003-Renderingerweiterung ist veraltet. Weitere Informationen finden Sie unter [Als veraltet markierte Funktionen in SQL Server Reporting Services in SQL Server 2016](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 Wenn Berichte erstmalig in Excel 2003 exportiert und gespeichert werden, profitieren sie nicht von der Dateioptimierung, die von Excel automatisch für die XLS-Arbeitsmappendateien ausgeführt wird. Die höhere Dateigröße kann Probleme für E-Mail-Abonnements und -Anlagen verursachen. Um die Größe der \*.xls-Datei für exportierte Berichte zu verringern, öffnen Sie die \*.xls-Datei, und speichern Sie die Arbeitsmappen anschließend neu. Durch erneutes Speichern der Arbeitsmappen wird die Dateigröße in der Regel um ca. 40 bis 50 Prozent verringert.  
  
> [!NOTE]  
>  In Excel 2003 werden im Arbeitsblatt in einer Excel-Zelle ungefähr 1000 Zeichen angezeigt. Es können jedoch Zeichen bis zur maximalen Anzahl in der Bearbeitungsleiste bearbeitet werden. Diese Einschränkung gilt nicht für aktuelle Excel-Dateien (XLSX).  
  
### <a name="text-boxes-and-text"></a>Textfelder und Text  
 Die folgenden Einschränkungen gelten für Textfelder und Text:  
  
-   Textfeldwerte, die Ausdrücke sind, werden nicht in Excel-Formeln konvertiert. Der Wert jedes Textfelds wird während der Berichtsverarbeitung ausgewertet. Der ausgewertete Ausdruck wird als Inhalt jeder Excel-Zelle exportiert.  
  
-   Textfelder werden innerhalb einer Excel-Zelle gerendert. Schriftgrad, Schriftart, Schriftdekoration und Schriftschnitt sind die einzigen Formatierungen, die für einzelne Textabschnitte innerhalb einer Excel-Zelle unterstützt werden.  
  
-   Der Texteffekt "Überlagernde Linie" wird in Excel nicht unterstützt.  
  
-   Excel fügt eine Standardauffüllung von ungefähr 3,75 Punkten links und rechts von den Zellen hinzu. Falls die Auffüllungseinstellungen eines Textfelds unter 3,75 Punkten liegen und der Text kaum aufgenommen werden kann, wird dieser in Excel unter Umständen umbrochen.  
  
    > [!NOTE]  
    >  Verbreitern Sie das Textfeld im Bericht, um dieses Problem zu umgehen.  
  
### <a name="images"></a>Bilder  
 Für Bilder gelten die folgenden Einschränkungen:  
  
-   Hintergrundbilder für Berichtselemente werden ignoriert, da Excel keine Hintergrundbilder für einzelne Zellen unterstützt.  
  
-   Die Excel-Renderingerweiterung unterstützt nur das Hintergrundbild des Hauptteils des Berichts. Falls das Hintergrundbild des Hauptteils eines Berichts im Bericht angezeigt wird, wird das Bild als Arbeitsblatt-Hintergrundbild gerendert.  
  
### <a name="rectangles"></a>Rechtecke  
 Für Rechtecke gilt die folgende Einschränkung.  
  
-   Rechtecke in Berichtsfußzeilen werden nicht in Excel exportiert. Allerdings werden Rechtecke im Berichtstext, in Tablix-Zellen usw. als Bereich von Excel-Zellen gerendert.  
  
### <a name="report-headers-and-footers"></a>Berichtskopfzeilen und -fußzeilen  
 Für Berichtsköpfe und Fußzeilen gelten die folgenden Einschränkungen:  
  
-   Für Kopf- und -Fußzeilen in Excel werden einschließlich Markup maximal 256 Zeichen unterstützt. Die Renderingerweiterung schneidet die Zeichenfolge bei 256 Zeichen ab.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt keine Ränder in Berichtsköpfen und Fußzeilen. Wenn die Randwerte in Excel exportiert werden, werden sie auf 0 (null) festgelegt, und abhängig von den Druckereinstellungen werden unter Umständen von allen Kopf- oder Fußzeilen, die mehrere Datenzeilen enthalten, nicht mehrere Zeilen gedruckt.  
  
-   Textfelder in einer Kopf- oder Fußzeile behalten beim Export in Excel ihre Formatierung, jedoch nicht ihre Ausrichtung bei. Dies liegt daran, dass führende und nachfolgende Leerzeichen abgeschnitten werden, wenn der Bericht in Excel gerendert wird.  
  
### <a name="merging-cells"></a>Verbinden von Zellen  
 Für das Verbinden von Zellen gelten die folgenden Einschränkungen:  
  
-   Wenn Zellen verbunden werden, funktioniert der Zeilenumbruch nicht ordnungsgemäß. Falls verbundene Zellen in einer Zeile vorhanden sind, in der ein Textfeld mit der AutoSize-Eigenschaft gerendert wird, funktioniert AutoSize nicht.  
  
 Der Excel-Renderer ist hauptsächlich ein Layoutrenderer. Das Ziel besteht darin, das Layout des gerenderten Berichts in einem Excel-Arbeitsblatt so weit wie möglich zu replizieren. Infolgedessen werden Zellen im Arbeitsblatt möglicherweise verbunden, um das Berichtslayout beizubehalten. Verbundene Zellen können Probleme verursachen, da die Sortierfunktion in Excel erfordert, dass Zellen auf eine ganz bestimmte Art verbunden werden, damit die Sortierung ordnungsgemäß funktioniert. Excel erfordert z. B., dass die Bereiche von verbundenen Zellen die gleiche Größe aufweisen, damit sie sortiert werden.  
  
 Wenn es von Bedeutung ist, dass in Excel-Arbeitsblatter exportierte Berichte sortiert werden können, kann die Anzahl der verbundenen Zellen in den Excel-Arbeitsblattern, die die häufigste Ursache für Schwierigkeiten mit der Sortierfunktion in Excel darstellt, folgendermaßen reduziert werden.  
  
-   Die fehlende Ausrichtung von Elementen nach links und rechts ist die häufigste Ursache verbundener Zellen. Stellen Sie sicher, dass der linke und rechte Rand aller Berichtselemente korrekt zueinander ausgerichtet sind. Die Ausrichtung von Elementen und die Verwendung der gleichen Breite löst das Problem in den meisten Fällen.  
  
-   Obwohl alle Elemente genau ausgerichtet werden, ist in einigen seltenen Fällen festzustellen, dass manche Spalten weiterhin zusammengeführt werden. Dies kann durch eine interne Einheitenkonvertierung und durch Runden beim Rendern des Excel-Arbeitsblatts verursacht werden. In der Berichtsdefinitionssprache (RDL) können Sie die Position und Größe in unterschiedlichen Maßeinheiten wie z. B. Zoll, Pixel, Zentimeter und Punkte angeben. Intern verwendet Excel Punkte. Um den Umrechungsaufwand und die möglichen Rundungsungenauigkeiten bei der Umrechnung der Zoll- und Zentimeterangaben in Punkte zu verringern, geben Sie ggf. alle Maßeinheiten in ganzen Punkten an, um möglichst direkte Ergebnisse zu erhalten. Ein Zoll entspricht 72 Punkten.  
  
### <a name="report-row-groups-and-column-groups"></a>Zeilen- und Spaltengruppen in Berichten  
 Berichte mit Zeilen- oder Spaltengruppen enthalten beim Export in Excel leere Zellen. Angenommen Sie haben einen Bericht, in dem die Zeilen nach der Entfernung zum Geschäft (Commute Distance) sortiert sind. Jede Entfernungskategorie kann mehr als einen Kunden enthalten. Der Bericht ist im folgenden Bild dargestellt.  
  
 ![Bericht im Reporting Services-Webportal](../../reporting-services/report-builder/media/ssrb-excelexportssrs.png "Report in the Reporting Services web portal")  
  
 Wenn der Bericht nach Excel exportiert wird, wird die Entfernung zum Geschäft nur in einer Zelle der Spalte „Entfernung zum Geschäft“ angezeigt. Abhängig von der Ausrichtung des Texts im Bericht (oben, Mitte oder unten) befindet sich der Wert in der ersten, mittleren oder letzten Zelle. Die anderen Zellen sind leer. Die Namensspalte mit den Geschäftsnamen enthält keine leeren Zellen. Das folgende Bild zeigt den Bericht nach dem Export in Excel. Die roten Zellrahmen wurden zur Hervorhebung hinzugefügt. Die grauen Felder sind die leeren Zellen. (Weder die roten Linien noch die grauen Felder sind Teil des exportierten Berichts.)  
  
 ![Nach Excel exportierter Bericht mit Zeilen](../../reporting-services/report-builder/media/ssrb-exportedexcellines.png "Report exported to Excel, with lines")  
  
 Berichte mit Zeilen- oder Spaltengruppen müssen also nach dem Export in Excel geändert werden, bevor Sie die exportierten Daten als PivotTable anzeigen können. Sie müssen den Gruppenwert in Zellen, in denen er fehlt, hinzufügen, um das Arbeitsblatt zu einer flachen Tabelle mit Werten in allen Zellen zu machen. Die folgende Abbildung zeigt das aktualisierte Arbeitsblatt.  
  
 ![Nach Excel exportierter vereinfachter Bericht](../../reporting-services/report-builder/media/ssrb-excelexportnomatrix.png "Report exported to Excel, with lines")  
  
 Wenn Sie einen Bericht erstellen, um ihn zur weiteren Analyse der Berichtsdaten nach Excel zu exportieren, sollten Sie in Ihrem Bericht nicht nach Zeilen oder Spalten gruppieren.  
  
## <a name="excel-renderer"></a>Excel-Renderer  
  
### <a name="current-xlsx-excel-file-renderer"></a>Aktuelle Excel-Datei-Renderer (XLSX)  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ist der Standard-Excel-Renderer die mit den aktuellen [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Dateien (XLSX) kompatible Version. Dies ist die **Excel** -Option in den Menüs **Exportieren** , die in den Listen des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportals und von SharePoint aufgeführt sind.  
  
 Wenn Sie den standardmäßigen Excel-Renderer statt des früheren Excel 2003-Renderers (XLS) verwenden, können Sie das Microsoft Office Compatibility Pack für Word, Excel und PowerPoint installieren, damit frühere Versionen von Excel die exportierten Dateien öffnen können.  
  
### <a name="excel-2003-xls-renderer"></a>Excel 2003-Renderer (XLS)  
  
> [!IMPORTANT]  
>  Die [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003-Renderingerweiterung ist veraltet. Weitere Informationen finden Sie unter [Als veraltet markierte Funktionen in SQL Server Reporting Services in SQL Server 2016](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 Die frühere, mit Excel 2003 kompatible Version heißt jetzt Excel 2003 und ist in Menüs aufgeführt, die diesen Namen verwenden. Der Inhaltstyp von Dateien, die von diesem Renderer generiert werden, ist **application/vnd.ms-excel** , und die Dateierweiterung der Dateien lautet „.xls“.  
  
 Standardmäßig ist die Menüoption **Excel 2003** nicht sichtbar. Ein Administrator kann sie unter bestimmten Umständen sichtbar machen, indem er die RSReportServer-Konfigurationsdatei aktualisiert. Um Berichte aus [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mit dem Excel 2003-Renderer zu exportieren, aktualisieren Sie die RSReportDesigner-Konfigurationsdatei.  
  
 Die Menüoptionserweiterung **Excel 2003** ist in den folgenden Szenarien nie sichtbar:  
  
-   Berichts-Generator im getrennten Modus, und Sie zeigen einen Bericht im Berichts-Generator in der Vorschau an. Da sich die RSReportServer-Konfigurationsdatei auf dem Berichtsserver befindet, müssen die Tools oder Produkten, aus denen Sie Berichte exportieren, mit einem Berichtsserver verbunden sein, um die Konfigurationsdatei zu lesen.  
  
-   Berichts-Viewer-Webpart im lokalen Modus, und die SharePoint-Farm ist nicht in einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver integriert. Weitere Informationen zum lokalen Modus finden Sie unter [Berichte im lokalen Modus im Vergleich zu Berichten im verbundenen Modus im Berichts-Viewer (Reporting Services im SharePoint-Modus)](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
 Wenn der Renderer der Menüoption **Excel 2003** für Sichtbarkeit konfiguriert ist, sind die Excel-Option und die Excel 2003-Option in den folgenden Szenarien verfügbar:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportal (einheitlicher Modus)  
  
-   SharePoint-Website, wenn Reporting Services im integrierten SharePoint-Modus installiert ist.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , und Sie zeigen Berichte in der Vorschau an.  
  
-   Berichts-Generator, der mit einem Berichtsserver verbunden ist.  
  
-   Das Berichts-Viewer-Webpart im Remotemodus.  
  
 Das folgende XML zeigt die Elemente für die beiden Excel-Renderingerweiterungen in der RSReportServer- und der RSReportDesigner-Konfigurationsdatei an:  
  
 `<Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>`  
  
 `<Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>`  
  
 Die EXCELOPENXML-Erweiterung definiert den Excel-Renderer für aktuelle Excel-Dateien (XLSX). Die EXCEL-Erweiterung definiert die Excel 2003-Version. `Visible = “false”` gibt an, dass der Excel 2003-Renderer ausgeblendet wird. Weitere Informationen finden Sie unter [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) und [RSReportDesigner-Konfigurationsdatei](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).  
  
### <a name="differences-between-the-current-xlsx-excel-and-excel-2003-renderers"></a>Unterschiede zwischen dem aktuellen Excel-Renderer (XLSX) und den Excel 2003-Renderern  
 Mit dem aktuellen Excel-Renderer (XLSX) oder dem Excel 2003-Renderer gerenderte Berichte sind in der Regel identisch, und nur in seltenen Fällen bemerken Sie Unterschiede zwischen den beiden Formaten. In der folgenden Tabelle werden der Excel-Renderer und der Excel 2003-Renderer verglichen.  
  
|Eigenschaft|Excel 2003|Aktuelle Excel-Version|  
|--------------|----------------|-------------------|  
|Die maximale Anzahl an Spalten pro Arbeitsblatt|256|16,384|  
|Maximale Anzahl an Zeilen pro Arbeitsblatt|65,536|1,048,576|  
|Anzahl von in einem Arbeitsblatt zulässigen Farben|56 (Palette)<br /><br /> Falls mehr als 56 Farben im Bericht verwendet werden, gleicht die Renderingerweiterung die erforderliche Farbe mit einer der 56 bereits in der benutzerdefinierten Palette vorhandenen Farben ab.|Ungefähr 16 Millionen (24-Bit-Farbe)|  
|Komprimierte ZIP-Dateien|InclusionThresholdSetting|ZIP-Komprimierung|  
|Standardschriftfamilie|Arial|Calibri|  
|Standardschriftgröße|10pt|11pt|  
|Standardzeilenhöhe|12,75 pt|15 pt|  
  
 Da der Bericht die Zeilenhöhe explizit festlegt, wirkt sich die Standardzeilenhöhe nur auf Zeilen aus, deren Größe beim Export nach Excel automatisch geändert wird.  
  
##  <a name="ReportItemsExcel"></a> Berichtselemente in Excel  
 Rechtecke, Unterberichte, der Hauptteil des Berichts und Datenbereiche werden als Bereich von Excel-Zellen gerendert. Textfelder, Bilder, Diagramme, Datenbalken, Sparklines, Karten, Messgeräte und Indikatoren müssen innerhalb einer Excel-Zelle gerendert werden. Abhängig vom Layout des restlichen Berichts kann diese möglicherweise zusammengeführt werden.  
  
 Bilder, Diagramme, Sparklines, Datenbalken, Karten, Messgeräte, Indikatoren und Zeilen werden innerhalb einer Excel-Zelle positioniert, befinden sich jedoch eine Ebene über dem Zellenraster. Linien werden als Zellrahmen gerendert.  
  
 Diagramme, Sparklines, Datenbalken, Karten, Messgeräte und Indikatoren werden als Bilder exportiert. Die von ihnen dargestellten Daten, z. B. die Wert- und Elementbezeichnungen für ein Diagramm, werden nicht exportiert und sind nur in der Excel-Arbeitsmappe verfügbar, wenn sie in einer Spalte oder Zeile in einem Datenbereich innerhalb eines Berichts enthalten sind.  
  
 Wenn Sie Diagramm-, Sparkline-, Datenbalken-, Karten-, Messgerät- und Indikatordaten verwenden möchten, exportieren Sie den Bericht in eine CSV-Datei oder generieren Atom-kompatible Datenfeeds aus dem Bericht. Weitere Informationen finden Sie unter [Exportieren als CSV-Datei (Berichts-Generator und SSRS)](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md) und [Generieren von Datenfeeds aus Berichten (Berichts-Generator und SSRS)](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
## <a name="page-sizing"></a>Anpassen der Seitengröße  
 Die Excel-Renderingerweiterung verwendet die Einstellungen zur Seitenhöhe und -breite, um zu ermitteln, welche Papiereinstellung im Excel-Arbeitsblatt definiert werden soll. Excel versucht, die Eigenschaftseinstellungen von „PageHeight“ und „PageWidth“ mit einer der gebräuchlichsten Papiergrößen abzugleichen.  
  
 Wenn keine Übereinstimmungen gefunden werden, verwendet Excel die Standardseitengröße für den Drucker. Falls die Papierbreite kleiner als die Papierhöhe ist, wird die Ausrichtung auf "Hochformat" festgelegt, andernfalls auf "Querformat".  
  
##  <a name="WorksheetTabNames"></a> Namen von Registern in Arbeitsblättern  
 Wenn Sie einen Bericht nach Excel exportieren, werden die durch Seitenumbruch erstellten Berichtsseiten in andere Arbeitsblätter exportiert. Wenn Sie einen ursprünglichen Seitennamen für den Bericht bereitgestellt haben, erhält jedes Arbeitsblatt der Excel-Arbeitsmappe standardmäßig diesen Namen. Der Name wird auf der Registerkarte des Arbeitsblattes angezeigt. Da jedoch jedes Arbeitsblatt in einer Arbeitsmappe einen eindeutigen Namen haben muss, wird eine ganze Zahl (beginnend bei 1 und jeweils um 1 erhöht) an den ursprünglichen Seitennamen aller zusätzlichen Arbeitsblätter angefügt. Wenn der ursprüngliche Seitenname z. B. **Verkaufbericht nach Geschäftsjahr**ist, würde das zweite Arbeitsblatt **Verkaufbericht nach Geschäftsjahr1**und das dritte Arbeitsblatt **Verkaufbericht nach Geschäftsjahr2**genannt werden.  
  
 Wenn alle mit Seitenumbrüchen erstellte Berichtsseiten neue Seitennamen angeben, erhält auch jedes Arbeitsblatt den entsprechenden Seitennamen. Diese Seitennamen sind jedoch möglicherweise nicht eindeutig. Wenn Seitennamen nicht eindeutig sind, werden die Arbeitsblätter auf die gleiche Weise wie ursprünglichen Seitennamen benannt. Wenn z. B. der Seitenname von zwei Gruppen **Verkäufe für NW**ist, erhält eine Registerkarte des Arbeitsblattes den Namen **Verkäufe für NW**und die andere den Namen **Verkäufe für NW1**.  
  
 Wenn der Bericht weder einen ursprünglichen Seitennamen noch auf Seitenumbrüche bezogene Seitennamen angibt, erhalten die Registerkarten des Arbeitsblattes die Standardnamen **Tabelle1**, **Tabelle2**usw.  
  
 Reporting Services stellt Eigenschaften bereit, die für Berichte, Datenbereiche, Gruppen und Rechtecke festgelegt werden können. So können Sie Berichte erstellen, die mit Ihren bevorzugten Einstellungen nach Excel exportiert werden können. Weitere Informationen finden Sie unter [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
##  <a name="DocumentProperties"></a> Dokumenteigenschaften  
 Der Excel-Renderer schreibt die folgenden Metadaten in die Excel-Datei.  
  
|Berichtselementeigenschaften|Description|  
|-------------------------------|-----------------|  
|Erstellt|Datum und Zeit der Berichtsausführung als Datums-/Uhrzeitwert im ISO-Format.|  
|Author|Autor des Berichts|  
|Description|Berichtsbeschreibung|  
|LastSaved|Datum und Zeit der Berichtsausführung als Datums-/Uhrzeitwert im ISO-Format.|  
  
##  <a name="PageHeadersFooters"></a> Seitenkopfzeilen und -fußzeilen  
 Abhängig von der Einstellung Geräteinformationen SimplePageHeaders kann der Seitenkopf auf zwei Arten gerendert werden: Er kann entweder oben auf jedem Arbeitsblattzellenraster oder im eigentlichen Excel-Arbeitsblatt-Kopfzeilenabschnitt gerendert werden. Standardmäßig wird der Seitenkopf zum Zellenraster auf dem Excel-Arbeitsblatt gerendert.  
  
 Der Seitenfuß wird unabhängig vom Wert der Einstellung SimplePageHeaders immer auf dem eigentlichen Excel-Arbeitsblatt-Footerabschnitt gerendert.  
  
 Excel-Kopf- und -Fußzeilenabschnitte unterstützen einschließlich Markup ein Maximum von 256 Zeichen. Falls diese Grenze überschritten wird, entfernt der Excel-Renderer vom Ende der Zeichenfolge des Seitenkopfs und/oder Seitenfußes her Markupzeichen, um die Anzahl der Zeichen insgesamt zu verringern. Falls alle Markupzeichen entfernt werden und die Länge noch immer über der maximal zulässigen liegt, wird die Zeichenfolge von rechts her abgeschnitten.  
  
### <a name="simplepageheader-settings"></a>SimplePageHeader-Einstellungen  
 Standardmäßig wird die Einstellung der Geräteinformationen SimplePageHeaders auf **false**festgelegt. Daher werden die Seitenköpfe im Bericht auf der Excel-Arbeitsblattoberfläche als Zeilen gerendert. Die Arbeitsblattzeilen, die die Kopfzeilen enthalten, werden gesperrte Zeilen. Sie können den Bereich in Excel fixieren oder die Fixierung des Bereichs aufheben. Bei ausgewählter Option **Drucktitel** wird automatisch festgelegt, dass diese Kopfzeilen auf jeder Arbeitsblattseite ausgedruckt werden.  
  
 Wenn in Excel die Option **Titel drucken** auf der Registerkarte Seitenlayout ausgewählt ist, wird der Seitenkopf außer auf dem Dokumentstrukturdeckblatt oben auf jedem Arbeitsblatt in der Arbeitsmappe wiederholt. Wenn im Dialogfeld Berichtskopfeigenschaften bzw. Berichtsfußeigenschaften die Option **Auf erster Seite drucken** bzw. **Auf letzter Seite drucken** nicht ausgewählt ist, wird die Kopfzeile nicht zur ersten bzw. letzten Seite hinzugefügt.  
  
 Seitenfüße werden im Excel-Fußzeilenabschnitt gerendert.  
  
 Aufgrund von Einschränkungen in Excel können in Excel-Kopf- und -Fußzeilenabschnitten ausschließlich Textfelder als Berichtselement angezeigt werden.  
  
##  <a name="Interactivity"></a> Interaktivität  
 Einige interaktive Elemente werden in Excel unterstützt. Im Folgenden werden spezifische Funktionsweisen beschrieben.  
  
### <a name="show-and-hide"></a>Einblenden und Ausblenden  
 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] weist Einschränkungen auf, wie ausgeblendete und angezeigte Berichtselemente beim Exportieren verwaltet werden. Gruppen, Zeilen und Spalten, die Berichtselemente enthalten, die ein- und ausgeschaltet werden können, werden als Excel-Gliederungen gerendert. Excel erstellt Gliederungen, die Zeilen und Spalten über die gesamte Zeile oder Spalte hinweg erweitern oder reduzieren. Dadurch können unter Umständen Berichtselemente reduziert werden, die nicht zum Reduzieren vorgesehen sind. Darüber hinaus können die Gliederungssymbole von Excel übermäßig viele sich überschneidende Gliederungen enthalten. Beim Verwenden der Excel-Renderingerweiterung werden daher die folgenden Gliederungsregeln angewendet, um diese Probleme zu vermeiden:  
  
-   Das Berichtselement oben links, das ein- und ausgeschaltet werden kann, kann in Excel weiterhin ein- und ausgeschaltet werden. Berichtselemente, die ein- und ausgeschaltet werden können und einen gemeinsamen horizontalen oder vertikalen Bereich mit dem Berichtselement aufweisen, das oben links ein- und ausgeschaltet werden kann, können in Excel nicht ein- und ausgeschaltet werden.  
  
-   Um zu ermitteln, ob ein Datenbereich zeilen- bzw. spaltenweise reduzierbar ist, wird die Position des Berichtselements ermittelt, das das Ein-/Ausschalten und die Position des Berichtselements steuert, das ein- und ausgeschaltet wird. Falls das Element, das das Ein-/Ausschalten steuert, vor dem ein- bzw. auszublendenden Element auftritt, kann das Element zeilenweise reduziert werden. Andernfalls ist das Element spaltenweise reduzierbar. Falls das Element, das das Ein-/Ausschalten steuert, zu gleichen Teilen neben und über dem ein- bzw. auszublendenden Bereich auftritt, wird das Element mit Zeilen gerendert, die zeilenweise reduziert werden können.  
  
-   Um zu ermitteln, ob die Teilergebnisse im gerenderten Bericht platziert werden, überprüft die Renderingerweiterung die erste Instanz eines dynamischen Elements. Falls direkt darüber ein statisches Peerelement auftritt, wird davon ausgegangen, dass es sich beim dynamischen Element um die Teilergebnisse handelt. Gliederungen werden festgelegt, um anzugeben, dass es sich dabei um Zusammenfassungsdaten handelt. Falls keine statisch gleichgeordneten Elemente eines dynamischen Elements vorhanden sind, ist die erste Instanz der Instanz das Teilergebnis.  
  
-   Aufgrund einer Einschränkung in Excel können geschachtelte Gliederungen nur bis zu 7 Ebenen aufweisen.  
  
### <a name="document-map"></a>Dokumentstruktur  
 Wenn im Bericht Dokumentstrukturbezeichnungen vorhanden sind, wird eine Dokumentstruktur gerendert. Die Dokumentstruktur wird als Excel-Deckarbeitsblatt gerendert, das an der Position der ersten Registerkarte in die Arbeitsmappe eingefügt wird. Das Arbeitsblatt wird **Dokumentstruktur**genannt.  
  
 Der in der Dokumentstruktur angezeigte Text wird von der DocumentMapLabel-Eigenschaft des Berichtselements oder der Gruppe bestimmt. Dokumentstrukturbezeichnungen werden in der Reihenfolge aufgeführt, in der sie, angefangen bei der ersten Zeile, in der ersten Spalte im Bericht auftreten. Jede Dokumentstruktur-Bezeichnungszelle wird um die Anzahl der Ebenen eingerückt, an der sie im Bericht auftritt. Jede Einzugsebene wird dargestellt, indem die Bezeichnung in einer nachfolgenden Spalte einfügt wird. Excel unterstützt bis zu 256 Ebenen der Gliederungsschachtelung.  
  
 Die Dokumentstrukturgliederung wird als reduzierbare Excel-Gliederung gerendert. Die Gliederungsstruktur stimmt mit der geschachtelten Struktur der Dokumentstruktur überein. Die Gliederung kann ab der zweiten Ebene erweitert und reduziert werden.  
  
 Der Stammknoten der Struktur entspricht dem Berichtsnamen (\<*Berichtsname*>.rdl), der nicht interaktiv ist. Die Schriftart des Dokumentstrukturlinks ist Arial, 10pt.  
  
### <a name="drillthrough-links"></a>Drillthroughlinks  
 In Textfeldern enthaltene Drillthroughlinks werden in der Zelle als Excel-Hyperlinks gerendert, in die der Text gerendert wird. Drillthroughlinks für Bilder und Diagramme werden beim Rendern als Excel-Hyperlinks auf dem Bild gerendert. Beim Klicken auf den Drillthroughlink wird der Standardbrowser des Clients geöffnet und zur HTML-Ansicht des Ziels navigiert.  
  
### <a name="hyperlinks"></a>Hyperlinks  
 In Textfeldern enthaltene Hyperlinks werden in der Zelle als Excel-Hyperlinks gerendert, in die der Text gerendert wird. Hyperlinks für Bilder und Diagramme werden beim Rendern als Excel-Hyperlinks auf dem Bild gerendert. Beim Klicken auf den Hyperlink wird der Standardbrowser des Clients geöffnet und zur HTML-Ansicht der Ziel-URL navigiert.  
  
### <a name="interactive-sorting"></a>Interaktives Sortieren  
 Excel unterstützt keine interaktive Sortierung.  
  
### <a name="bookmarks"></a>Lesezeichen  
 Lesezeichenlinks in Textfeldern werden in der Zelle als Excel-Hyperlinks gerendert, in die der Text gerendert wird. Lesezeichenlinks für Bilder und Diagramme werden beim Rendern als Excel-Hyperlinks auf dem Bild gerendert. Durch Klicken auf das Lesezeichen wird zur Excel-Zelle gewechselt, in der das mit Lesezeichen versehene Berichtselement gerendert wird.  
  
##  <a name="ConditionalFormat"></a> Ändern von Berichten zur Laufzeit  
 Wenn ein Bericht in mehrere Formate gerendert werden muss und kein Berichtslayout erstellt werden kann, das in allen erforderlichen Formaten wunschgemäß Rendervorgänge ausführt, verwenden Sie ggf. das integrierte globale Objekt von "RenderFormat", um die Darstellung des Berichts zur Laufzeit bedingt zu ändern. Dadurch können Berichtselemente abhängig vom verwendeten Renderer ausgeblendet oder angezeigt werden, um die besten Ergebnisse in den einzelnen Formaten zu erhalten. Weitere Informationen finden Sie unter [Integrierte globale Werte und Benutzerverweise &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Renderingverhalten (Berichts-Generator und SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Interaktive Funktionalität für verschiedene Berichtsrenderingerweiterungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendern von Berichtselementen (Berichts-Generator und SSRS)](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
