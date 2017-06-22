---
title: Renderingverhalten (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f873ef9-27a3-40e5-b58b-6774f8027a58
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 518b74abc3238fcebee1e8b5356315e49f35db01
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="rendering-behaviors-report-builder--and-ssrs"></a>Renderingverhalten (Berichts-Generator und SSRS)
  Abhängig vom ausgewählten Renderer werden beim Rendern eines Berichts bestimmte Regeln auf den Hauptteil des Berichts und seinen Inhalt angewendet. Wie sich Berichtselemente auf einer Seite zusammenfügen, wird durch die Kombination folgender Faktoren bestimmt:  
  
-   Renderingregeln.  
  
-   Die Breite und die Höhe von Berichtselementen.  
  
-   Die Größe des Berichtshauptteils.  
  
-   Die Breite und die Höhe der Seite.  
  
-   Rendererspezifische Unterstützung für Auslagerungen.  
  
 Die allgemeinen Regeln, die von Reporting Services angewendet werden, werden in diesem Thema erläutert. Weitere Informationen finden Sie unter [Rendern von Berichtselementen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md), [Rendern von Datenbereichen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-data-regions-report-builder-and-ssrs.md) und [Rendern von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-data-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="general-behaviors-for-html-mhtml-word-and-excel-soft-page-break-renderers"></a>Allgemeine Verhaltensweisen für HTML, MHTML, Word und Excel (Renderer mit weichem Seitenumbruch)  
 Im HTML- und MHTML-Format exportierte Berichte sind für die Anzeige am Computerbildschirm optimiert, bei der Seiten unterschiedlich lang sein können. Seitenumbrüche werden vertikal nur an ungefähren Positionen im Berichtshauptteil eingefügt. Diese ungefähren Positionen werden durch die interaktive Höheneinstellung im Bereich Eigenschaften bestimmt. Angenommen, die interaktive Höhe ist auf 5 Zoll festgelegt. Wenn der Bericht gerendert wird, beträgt die Seitenhöhe etwa 5 Zoll. Word und Excel paginieren auf Grundlage logischer Seitenumbrüche und ignorieren die interaktive Höheneinstellung.  
  
> [!NOTE]  
>  Um zu bestimmen, wie ein Bericht in einem Renderer mit weichem Seitenumbruch angezeigt wird, verwenden Sie die Berichtsvorschau. Der Bericht wird so angezeigt, wie dies im HTML-, MHTML-, Word- bzw. Excel-Format der Fall wäre.  
  
 Wenn Sie einen Bericht in HTML, MHTML, Word oder Excel exportieren, werden folgende allgemeine Regeln befolgt:  
  
-   Logische Seitenumbrüche, die Seitenumbrüche, die Sie explizit einfügen, werden für Berichtselemente übernommen. Wenn Sie beispielsweise zwischen den einzelnen Gruppen jeweils einen Seitenumbruch einfügen, werden sie beim Rendern des Berichts angewendet.  
  
-   Es wird ein ungefähres Layout erstellt, und zwar anhand der Seitenhöhe und der Anzahl der Vorkommnisse des Berichtselements. Wenn beispielsweise ein Textfeld eine Höhe von 0,5 Zoll aufweist und fünfmal in dem Bericht vorkommt, werden 2,5 Zoll reserviert.  
  
-   Mehrere weiche Seitenumbrüche werden auf Grundlage der interaktiven Höheneinstellung eingefügt. Wenn die Unterdrückung in HTML und den ReportViewer-Steuerelementen erfolgen und die Paginierung lediglich mit expliziten Seitenumbrüchen gesteuert werden soll, stellen Sie den Wert für die **interactive height** auf 0 oder eine extrem hohe Zahl ein.  
  
    > [!NOTE]  
    >  Die interaktive Breiteneinstellung wird in den Renderern mit weichem Seitenumbruch nicht verwendet.  
  
-   Berichtsseiten können größer werden, um allein stehende Absatzzeilen, Waisen und Berichtselemente aufzunehmen, die zusammenbleiben müssen. Der Bericht kann also über die Bildschirmbreite hinaus erweitert werden; zur Anzeige werden dann Schieberegler verwendet.  
  
-   Die Paginierung wird nur vertikal für Berichte übernommen.  
  
-   Seitenränder werden nicht übernommen.  
  
## <a name="general-behaviors-for-pdf-image-and-print-hard-page-break-renderers"></a>Allgemeine Verhaltensweisen für PDF, Bild und Drucken (Renderer mit hartem Seitenumbruch)  
 Berichte, die im PDF- und Bild-Format exportiert werden, sind für den buch- oder dokumentationsähnlichen Druck optimiert, bei dem Seiten eine konsistente Größe aufweisen. Seitenumbrüche werden vertikal und horizontal an bestimmten Positionen im Berichtshauptteil eingefügt. Diese bestimmten Positionen werden durch die Einstellungen für Seitenbreite und -höhe bestimmt.  
  
> [!NOTE]  
>  Um zu bestimmen, wie ein Bericht in einem Renderer mit hartem Seitenumbruch angezeigt wird, verwenden Sie die Seitenansicht. Der Bericht wird so angezeigt, wie dies im PDF- oder Bild-Format der Fall wäre.  
  
-   Seiten werden sequenziell von links nach rechts nummeriert, dann von oben nach unten.  
  
-   Logische Seitenumbrüche, die Seitenumbrüche, die Sie explizit einfügen, werden für Berichtselemente übernommen. Diese Seitenumbrüche können bewirken, dass Berichtselemente andere Elemente auf die nächste Seite schieben.  
  
-   Wenn ein physischer Seitenumbruch Berichtselemente trennt, die zusammenbleiben müssen, werden die Elemente, die zusammenbleiben müssen, auf die nächste Seite verschoben.  
  
-   Aufgrund der Seitengrößenbeschränkungen ist es unter Umständen nicht möglich, dass alle Elemente zusammenbleiben bzw. dass Elemente wiederholt werden. In diesem Fall ignoriert der Renderer bei einem anderen Element möglicherweise bestimmte Wiederholungsregeln, damit das Berichtselement auf die Seite passt.  
  
-   Wenn ein Element nicht zusammenbleiben kann, beispielsweise ein Textfeld, das zu groß für den vertikalen nutzbaren Seitenbereich wird, wird das Element an der physischen Seitengrenze abgeschnitten und auf der nächsten Seite fortgesetzt.  
  
-   Die Paginierung wird vertikal und horizontal für Berichte übernommen.  
  
    > [!NOTE]  
    >  Die interaktive Breiteneinstellung wird in den Renderern mit hartem Seitenumbruch nicht verwendet.  
  
## <a name="minimum-spacing-between-report-items"></a>Minimaler Abstand zwischen Berichtselementen  
 Berichtselemente wachsen innerhalb des Hauptteils des Berichts, um ihren Inhalt aufzunehmen. So wird beispielsweise ein Matrixdatenbereich beim Rendern des Berichts normalerweise zur Seite und nach unten erweitert, und die Höhe eines Textfelds ändert sich abhängig von den Daten, die von einem Ausdruck zurückgegeben wurden.  
  
 Renderer behalten den minimalen Abstand zwischen Berichtselementen bei, die Sie im Berichtslayout definieren. Wenn Sie ein Berichtselement im Berichtslayout neben einem anderen platzieren, wird der Abstand zwischen den Berichtselementen zum Mindestabstand, der bei der horizontalen bzw. vertikalen Erweiterung des Berichts beibehalten werden muss. Wenn Sie beispielsweise einen Matrixdatenbereich einem Bericht hinzufügen und dann ein Rechteck 0,25 Zoll rechts von der Matrix hinzufügen, wird dieser Abstand beibehalten, wenn die Matrix größer wird. Jedes Element wird nach rechts verschoben, um den Mindestabstand zu Elementen beizubehalten, die links von ihm enden.  
  
## <a name="page-headers-and-footers"></a>Seitenkopfzeilen und -fußzeilen  
 Seitenkopf- und -fußzeilen werden am oberen und unteren Rand der einzelnen gerenderten Seiten angezeigt. Sie können für den Seitenkopf und die Seitenfußzeile eine Rahmenfarbe, Rahmenart und Rahmenbreite formatieren. Sie können auch eine Hintergrundfarbe oder ein Hintergrundbild hinzufügen. Diese Formatierungsoptionen werden alle gerendert, abhängig von dem Format, das Sie auswählen.  
  
 Folgende Regeln gelten für Seitenköpfe und -füße, die im HTML- oder MHTML-Rendering-Format gerendert werden:  
  
> [!NOTE]  
>  Informationen zum Rendern von Kopf- und Fußzeilen in Excel finden Sie unter [Exporting to Microsoft Excel &#40;Report Builder and SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md) (Exportieren nach Microsoft Excel [Berichts-Generator und SSRS]). Informationen zum Rendern von Kopf- und Fußzeilen in Word finden Sie unter [Exporting to Microsoft Word &#40;Report Builder and SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md) (Exportieren nach Microsoft Word [Berichts-Generator und SSRS]).  
  
-   Sind Kopf- und Fußzeilen vorhanden, werden sie am oberen und unteren Rand der einzelnen Seiten innerhalb des nutzbaren Seitenbereichs gerendert.  
  
-   Auf Seiten, auf denen die Kopf- bzw. Fußzeile ausgeblendet ist, bleibt die Höhe der Kopf- bzw. Fußzeile im nutzbaren Seitenbereich weiterhin reserviert, obwohl die Kopf- bzw. Fußzeile nicht gerendert wird.  
  
-   Wenn der Inhalt des Headers bzw. der Fußzeile über die Grenzen der Kopf- bzw. Fußzeile hinausgeht, wird die Größe der Kopf- bzw. Fußzeile angepasst, um den Inhalt aufzunehmen.  
  
 Folgende Regeln gelten für Seitenköpfe und -füße, die im PDF- oder Bild-Rendering-Format gerendert werden:  
  
-   Die Kopf- bzw. Fußzeile wird am oberen und unteren Rand der einzelnen Seiten innerhalb des nutzbaren Seitenbereichs gerendert.  
  
-   Auf Seiten, auf denen die Kopf- bzw. Fußzeile ausgeblendet ist, bleibt die Höhe der Kopf- bzw. Fußzeile im nutzbaren Seitenbereich weiterhin reserviert, obwohl die Kopf- bzw. Fußzeile nicht gerendert wird.  
  
-   Der Header und die Fußzeile werden weder größer noch kleiner. Sie werden auf jeder Seite in der Höhe gerendert, die bei der Erstellung der Kopf- bzw. Fußzeile angegeben wurde.  
  
-   Ungeachtet der Anzahl an Spalten im Bericht gibt es nur eine Kopf- und eine Fußzeile pro Seite.  
  
-   Wenn der Inhalt der Kopf- bzw. Fußzeile über die Grenzen der Kopf- bzw. Fußzeile hinausgeht, wird der Inhalt abgeschnitten.  
  
-   Kopf- und Fußzeilen, die in der ursprünglichen RDL-Datei definiert wurden, werden nicht gerendert, wenn der Bericht als Unterbericht gerendert wird.  
  
## <a name="logical-page-breaks"></a>Logische Seitenumbrüche  
 Logische Seitenumbrüche sind Seitenumbrüche, die vor oder nach Berichtselementen oder -gruppen eingefügt werden. Mithilfe von Seitenumbrüchen können Sie festlegen, wie beim Rendern oder Exportieren des Berichts Inhalt für die optimale Anzeige auf einer Berichtsseite angeordnet wird.  
  
 Folgende Regeln gelten beim Rendern logischer Seitenumbrüche:  
  
-   Logische Seitenumbrüche werden bei Berichtselementen ignoriert, die dauerhaft ausgeblendet sind, und bei Berichtselementen, deren Sichtbarkeit durch Klicken auf ein anderes Berichtselement gesteuert wird.  
  
-   Logische Seitenumbrüche werden auf bedingt sichtbare Elemente angewendet, wenn Sie zum Renderzeitpunkt des Berichts sichtbar waren.  
  
-   Der Abstand zwischen dem Berichtselement mit dem logischen Seitenumbruch und seinen Peer-Berichtselementen wird beibehalten.  
  
-   Logische Seitenumbrüche, die vor einem Berichtselement eingefügt werden, bewirken, dass das Berichtselement auf die nächste Seite verschoben wird. Das Berichtselement wird am Anfang der nächsten Seite gerendert.  
  
-   Logische Seitenumbrüche, die für Elemente in einer Tabellen- oder Matrixzelle definiert wurden, werden nicht beibehalten. Dies gilt nicht für Listenelemente.  
  
## <a name="see-also"></a>Siehe auch  
 [Interaktive Funktionalität für verschiedene Berichtsrenderingerweiterungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendern in das HTML-Format &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)   
 [Seitenlayout und Rendering &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  
