---
title: "Seitenkopf-und Seitenfußzeilen (Berichts-Generator und SSRS) | Microsoft Docs"
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
f1_keywords:
- "10125"
- sql13.rtp.rptdesigner.pagefooter.border.f1
- "10121"
- "10120"
- "10122"
- sql13.rtp.rptdesigner.pageheader.general.f1
- "10123"
- sql13.rtp.rptdesigner.pageheader.fill.f1
- sql13.rtp.rptdesigner.pageheader.border.f1
- sql13.rtp.rptdesigner.pagefooter.fill.f1
- sql13.rtp.rptdesigner.pagefooter.general.f1
- "10124"
ms.assetid: 4fb9faac-511e-404a-b8d7-1f2e3cb47b11
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f89d2e283daf9b9ac107c098d38db4feab17a736
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="page-headers-and-footers-report-builder-and-ssrs"></a>Seitenkopf- und Seitenfußzeilen (Berichts-Generator und SSRS)
  Ein Bericht kann eine Kopf- und Fußzeile enthalten, die am oberen bzw. unteren Rand jeder Seite verläuft. Kopf- und Fußzeilen können statischen Text, Bilder, Linien, Rechtecke, Rahmen, Hintergrundfarbe, Hintergrundbilder und Ausdrücke enthalten. Ausdrücke enthalten Verweise auf Datasetfelder für Berichte mit genau einem Dataset und Aggregatfunktionsaufrufen mit dem Dataset als Bereich.  
  
> [!NOTE]  
>  Jede Renderingerweiterung verarbeitet Seiten unterschiedlich. Weitere Informationen zur Berichtspaginierung und zu Renderingerweiterungen finden Sie unter [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 Standardmäßig haben Berichte Seitenfußzeilen, jedoch keine Seitenkopfzeilen. Weitere Informationen dazu, wie Sie diese hinzufügen oder entfernen, finden Sie unter [Hinzufügen oder Entfernen einer Seitenkopf- oder Seitenfußzeile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md).  
  
 Kopf- und Fußzeilen enthalten im Allgemeinen Seitennummern, Berichtstitel und andere Berichtseigenschaften. Weitere Informationen dazu, wie Sie diese Elemente der Kopf- bzw. Fußzeile Ihres Berichts hinzufügen, finden Sie unter [Anzeigen von Seitenzahlen oder anderen Berichtseigenschaften &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md).  
  
 Nachdem Sie eine Seitenkopfzeile oder -fußzeile erstellt haben, wird diese auf jeder Berichtsseite angezeigt. Weitere Informationen zum Unterdrücken von Kopf- und Fußzeilen auf der ersten und letzten Seite finden Sie unter [Ausblenden einer Seitenkopf- oder Seitenfußzeile auf der ersten oder letzten Seite &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-headers-and-footers"></a>Berichtskopfzeilen und -fußzeilen  
 Seitenkopfzeilen und -fußzeilen sind nicht mit Berichtskopfzeilen und -fußzeilen identisch. Berichte weisen keine besondere Berichtskopfzeile oder -fußzeile auf. Eine Berichtskopfzeile besteht aus den Berichtselementen, die auf der Berichtsentwurfsoberfläche über dem Berichtstext angeordnet werden. Diese werden nur einmal als erster Inhalt im Bericht angezeigt. Eine Berichtsfußzeile besteht aus den Berichtselementen, die unter dem Berichtstext angeordnet werden. Diese werden nur einmal als letzter Inhalt im Bericht angezeigt.  
  
## <a name="displaying-variable-data-in-a-page-header-or-footer"></a>Anzeigen von Variablendaten in einem Seitenkopf oder -fuß  
 Seitenkopfzeilen und -fußzeilen können statischen Inhalt enthalten. Meistens werden sie jedoch zur Anzeige von variierendem Inhalt wie Seitenzahlen oder Informationen zum Inhalt einer Seite verwendet. Wenn Sie unterschiedliche Variablendaten auf den einzelnen Seiten anzeigen möchten, müssen Sie einen Ausdruck verwenden.  
  
 Wenn nur ein Dataset im Bericht definiert wurde, können Sie einer Kopf- oder Fußzeile einfache Ausdrücke wie `[FieldName]` hinzufügen. Ziehen Sie das Feld aus der Datasetfeldauflistung im Berichtsdatenbereich oder der integrierten Feldauflistung in die Kopf- oder Fußzeile. Ein Textfeld mit dem entsprechenden Ausdruck wird automatisch hinzugefügt.  
  
 Wenn Sie Gesamtbeträge oder Aggregate für Werte auf der Seite berechnen möchten, können Sie Aggregatausdrücke verwenden, die ReportItems oder den Namen eines Datasets angeben. Die ReportItems-Auflistung entspricht der Auflistung von Textfeldern auf den einzelnen Seite nach dem Berichtsrendering. Der Name des Datasets muss in der Berichtsdefinition enthalten sein. In der folgenden Tabelle werden die Elemente angezeigt, die von den Aggregatausdruckstypen unterstützt werden:  
  
|Unterstützt im Ausdruck|ReportItems-Aggregate|Dataset-Aggregate (Bereich muss Datasetname sein)|  
|-----------------------------|----------------------------|----------------------------------------------------------|  
|Textfelder im Berichtstext|Ja|Nein|  
|&PageNumber|Ja|Nein|  
|&TotalPages|Ja|Nein|  
|Aggregate-Funktion|Ja. Beispiel:<br /><br /> `=First(ReportItems!TXT_LastName.Value)`|Ja. Beispiel:<br /><br /> `=Max(Quantity.Value,"DataSet1")`|  
|Feldauflistung für Elemente auf der Seite|Indirekt. Beispiel:<br /><br /> `=Sum(ReportItems!Textbox1.Value)`|Ja. Beispiel:<br /><br /> `=Sum(Fields!Quantity.Value,"DataSet1")`|  
|Datengebundenes Bild|Indirekt. Beispiel: `=ReportItems!TXT_Photo.Value`|Ja. Beispiel:<br /><br /> `=First(Fields!Photo.Value,"DataSet1")`|  
  
 Die folgenden Abschnitte dieses Themas zeigen sofort verwendbare Ausdrücke, die in Kopf- und Fußzeilen üblicherweise verwendete Variablendaten abrufen. Außerdem ist ein Abschnitt vorhanden, in dem erklärt wird, wie die Excel-Renderingerweiterung Kopf- und Fußzeilen verarbeitet. Weitere Informationen zu Ausdrücken finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
### <a name="adding-calculated-page-totals-to-a-header-or-footer"></a>Hinzufügen berechneter Seitengesamtergebnisse zu Kopf- oder Fußzeilen  
 In einigen Fällen ist es nützlich, einen berechneten Wert in die Kopf- oder Fußzeile jedes Berichts aufzunehmen (beispielsweise eine Gesamtsumme pro Seite, wenn die Seite numerische Werte enthält). Da Sie nicht direkt auf die Felder verweisen können, muss der Ausdruck, den Sie in die Kopf- oder Fußzeile einfügen, nicht auf das Datenfeld, sondern auf den Namen des Berichtselements (z. B. eines Textfelds) verweisen.  
  
 `=Sum(ReportItems!Textbox1.Value)`  
  
 Wenn sich das Textfeld in einer Tabelle oder Liste befindet, die wiederholte Zeilen von Daten enthält, ist der Wert, der zur Laufzeit in der Kopf- oder Fußzeile angezeigt wird, eine Summe aller Werte aller `TextBox1` -Instanzdaten in der Tabelle oder Liste für die aktuelle Seite.  
  
 Beim Berechnen von Seitengesamtergebnissen gibt es erwartungsgemäß Unterschiede bei den Gesamtergebnissen, wenn verschiedene Renderingerweiterungen zum Anzeigen des Berichts verwendet werden. Paginierte Ausgaben werden für jede Renderingerweiterung unterschiedlich berechnet. Eine Seite, die zunächst in HTML angezeigt wird, weist möglicherweise andere Gesamtergebnisse auf, wenn sie in PDF angezeigt wird, wenn die Menge der Daten auf der PDF-Seite unterschiedlich ist. Weitere Informationen finden Sie unter [Renderingverhalten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
### <a name="for-reports-with-multiple-datasets"></a>Berichte mit mehreren Datasets  
 Berichten mit mehreren Datasets können keine Felder oder datengebundenen Bilder unmittelbar in einer Kopf- oder Fußzeile hinzugefügt werden. Sie können jedoch einen Ausdruck schreiben, der indirekt auf ein datengebundenes Feld oder Bild verweist, das Sie in einer Kopf- oder Fußzeile verwenden möchten.  
  
 So fügen Sie Variablendaten in eine Kopf- oder Fußzeile ein  
  
-   Fügen Sie der Kopf- oder Fußzeile ein Textfeld hinzu.  
  
-   Schreiben Sie in dem Textfeld einen Ausdruck, der die Variablendaten erzeugt, die angezeigt werden sollen.  
  
-   Nehmen Sie in den Ausdruck Verweise auf Berichtselemente auf der Seite auf. (Sie können z. B. auf ein Textfeld verweisen, das Daten aus einem bestimmten Feld enthält). Nehmen Sie keinen direkten Verweis auf Felder in einem Dataset auf. Beispielsweise kann der Ausdruck `[LastName]`nicht verwendet werden. Der folgende Ausdruck zeigt den Inhalt der ersten Instanz des Textfelds `TXT_LastName`an:  
  
     `=First(ReportItems!TXT_LastName.Value)`  
  
 Sie können keine Aggregatfunktionen für Felder im Seitenkopf oder -fuß verwenden. Aggregatfunktionen können nur für Berichtselemente im Hauptteil des Berichts verwendet werden. Allgemeine Ausdrücke in Kopf- und Fußzeilen finden Sie unter [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
#### <a name="adding-a-data-bound-image-to-a-header-or-footer"></a>Hinzufügen eines datengebundenen Bilds zu Kopf- oder Fußzeilen  
 Sie können in einer Datenbank gespeicherte Bilddaten in einer Kopf- oder Fußzeile verwenden. Sie können jedoch nicht direkt vom Bildberichtselement aus auf Datenbankfelder verweisen. Sie müssen stattdessen ein Textfeld im Hauptteil des Berichts hinzufügen und das Textfeld dann auf das Datenfeld festlegen, das das Bild enthält (der Wert muss base64-codiert sein). Sie können das Textfeld im Hauptteil des Berichts ausblenden, um die Anzeige des base64-codierten Bilds zu verhindern. Dann können Sie vom Bildberichtselement im Seitenkopf oder -fuß aus auf den Wert des ausgeblendeten Textfelds verweisen.  
  
 Nehmen Sie z. B. an, dass Sie einen Bericht haben, der aus Produktinformationsseiten besteht. In der Kopfzeile jeder Seite soll ein Foto des Produkts angezeigt werden. Wenn Sie ein gespeichertes Bild im Berichtskopf drucken möchten, definieren Sie das ausgeblendete Textfeld `TXT_Photo` im Hauptteil des Berichts, das das Bild aus der Datenbank abruft, und verwenden Sie einen Ausdruck, um ihm einen Wert zuzuweisen:  
  
 `=Convert.ToBase64String(Fields!Photo.Value)`  
  
 Fügen Sie in der Kopfzeile ein Bildberichtselement hinzu, das das zum Anzeigen des Bilds decodierte Textfeld `TXT_Photo` verwendet:  
  
 `=Convert.FromBase64String(ReportItems!TXT_Photo.Value)`  
  
## <a name="using-headers-and-footers-to-position-text"></a>Verwenden von Kopf- und Fußzeilen zum Positionieren von Text  
 Sie können Kopf- und Fußzeilen zum Positionieren von Text auf einer Seite verwenden. Nehmen Sie z. B. an, dass Sie einen Bericht erstellen, den Sie an Kunden versenden möchten. Sie können eine Kopf- oder Fußzeile verwenden, um die Kundenadresse so zu positionieren, dass sie nach dem Falten im Umschlagfenster angezeigt wird.  
  
 Wenn Sie nur das Textfeld verwenden, um eine Kopf- oder Fußzeile aufzufüllen, können Sie das Textfeld im Hauptteil des Berichts ausblenden. Die Platzierung des Textfelds im Hauptteil des Berichts kann Einfluss darauf haben, ob der Wert in der Kopf- oder Fußzeile der ersten oder letzten Seite eines Berichts angezeigt wird. Wenn Sie beispielsweise Tabellen, Matrizen oder Listen haben, die bewirken, dass der Bericht mehrere Seiten umfasst, wird der Wert des ausgeblendeten Textfelds auf der letzten Seite angezeigt. Wenn der Wert auf der ersten Seite angezeigt werden soll, platzieren Sie das ausgeblendete Textfeld am Anfang des Hauptteils des Berichts.  
  
## <a name="designing-reports-with-page-headers-and-footers-for-specific-renderers"></a>Entwerfen von Berichten mit Seitenkopfzeilen und -fußzeilen für bestimmte Renderer  
 Bei der Verarbeitung eines Berichts werden die Berichtsdaten mit den Layoutinformationen kombiniert. Wenn Sie einen Bericht anzeigen, werden die kombinierten Informationen an einen Renderer übergeben, der den Umfang der Berichtsdaten festlegt, die auf den einzelnen Seiten angezeigt werden.  
  
 Wenn Sie einen Bericht auf dem Berichtsserver mithilfe eines Browsers anzeigen, wird der auf den einzelnen Seiten angezeigte Inhalt vom HTML-Renderer gesteuert. Wenn Sie Berichte in einem anderen Format als dem Anzeigeformat übermitteln möchten, oder wenn Sie Berichte in einem spezifischen Format drucken möchten, können Sie das Berichtslayout für den Renderer optimieren, der für das abschließende Berichtsformat verwendet werden soll. Weitere Informationen zur Berichtspaginierung finden Sie unter [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
### <a name="working-with-page-headers-and-footers-in-excel"></a>Arbeiten mit Seitenköpfen und -füßen in Excel  
 Befolgen Sie beim Definieren von Seitenköpfen und -füßen für Berichte, die auf die Excel-Renderingerweiterung abzielen, diese Richtlinien, um optimale Ergebnisse zu erhalten:  
  
-   Verwenden Sie Seitenfüße zum Anzeigen von Seitenzahlen.  
  
-   Verwenden Sie Seitenköpfe zum Anzeigen von Bildern, Titeln oder sonstigem Text. Fügen Sie Seitenzahlen nicht in die Kopfzeile ein.  
  
 In Excel haben Seitenfüße ein eingeschränktes Layout. Wenn Sie einen Bericht definieren, der komplexe Berichtselemente im Seitenfuß enthält, wird der Seitenfuß nicht wie erwartet verarbeitet, wenn der Bericht in Excel angezeigt wird.  
  
 Die Excel-Renderingerweiterung kann Bilder und absolute Positionierung einfacher oder komplexer Berichtselemente in den Seitenkopf aufnehmen. Ein Nebeneffekt der Unterstützung eines vielfältigeren Seitenkopflayouts ist die reduzierte Unterstützung für das Berechnen von Seitenzahlen in der Kopfzeile. Bei der Excel-Renderingerweiterung bewirken Standardeinstellungen, dass Seitenzahlen basierend auf der Anzahl der Arbeitsblätter berechnet werden. Abhängig davon, wie Sie den Bericht definieren, kann dies zu fehlerhaften Seitenzahlen führen. Nehmen Sie z. B. an, dass Sie einen Bericht haben, der als einzelnes großes Arbeitsblatt gerendert wird, das auf vier Seiten gedruckt wird. Wenn Sie Seitenzahlinformationen in die Kopfzeile aufnehmen, zeigt jede gedruckte Seite "Seite 1 von 1" in der Kopfzeile an.  
  
 Eine genauere Seitenanzahl basiert auf logischen Seiten, die mit den Abmessungen einer gedruckten Seite korrelieren. In Excel verwendet der Seitenfuß automatisch logische Seitenzahlen. Um die logische Seitenanzahl in den Seitenkopf einzufügen, müssen Sie die Geräteinformationseinstellungen für die Verwendung einfacher Kopfzeilen konfigurieren. Denken Sie daran, dass durch die Verwendung einfacher Kopfzeilen die Möglichkeit verloren geht, komplexes Berichtslayout im Kopfzeilenbereich zu verwenden.  
  
 Weitere Informationen finden Sie unter [Exporting to Microsoft Excel &#40;Report Builder and SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md) (Exportieren nach Microsoft Excel (Berichts-Generator und SSRS)).  
  
## <a name="see-also"></a>Siehe auch  
 [Einbetten eines Bilds in einen Bericht &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Rechtecke und Linien &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
  
