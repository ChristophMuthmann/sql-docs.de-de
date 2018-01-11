---
title: Verweise auf Parameterauflistungen (Berichts-Generator und SSRS) | Microsoft-Dokumentation
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
ms.assetid: edc0c75f-0530-4e6d-85aa-3385301bfd00
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 5a084d3bb236100728b5decab3569c37f46600f8
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="built-in-collections---reportitems-collection-references-report-builder"></a>Integrierte Auflistungen: Verweise auf ReportItems-Auflistungen (Berichts-Generator)
  Die integrierte **ReportItems** -Sammlung besteht aus einem Satz von Textfeldern aus Berichtselementen, wie Zeilen eines Datenbereichs oder Textfelder auf der Berichtsentwurfsoberfläche. Die **ReportItems** -Auflistung umfasst Textfelder, die sich im aktuellen Bereich einer Seitenkopfzeile, einer Seitenfußzeile oder eines Berichtshauptteils befinden. Diese Auflistung wird vom Berichtsprozessor und vom Berichtsrenderer zur Laufzeit bestimmt. Der aktuelle Bereich wird geändert, wenn der Berichtsprozessor Berichtsdaten und die Layoutelemente des Berichtselements erfolgreich kombiniert, während der Benutzer Seiten eines Berichts anzeigt. Sie können die integrierte **ReportItems** -Sammlung verwenden, um Seitenkopfzeilen im Wörterbuchformat zu erstellen, die das erste und das letzte Element auf jeder Seite anzeigen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-reportitems-value-property"></a>Verwenden der ReportItems-Werteigenschaft  
 Elemente in der **ReportItems** -Auflistung verfügen nur über eine Eigenschaft: Wert. Mit dem Wert für ein **ReportItems** -Element können Daten aus einem anderen Feld im Bericht angezeigt oder berechnet werden. Der Zugriff auf den Wert des aktuellen Textfelds kann über den in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] integrierten globalen Me.Value oder einfach über Value erfolgen. In Berichtsfunktionen wie "Erster" und in Aggregatfunktionen müssen Sie jedoch die vollqualifizierte Syntax verwenden.  
  
 Zum Beispiel:  
  
-   Dieser Ausdruck wird in einem Textfeld platziert und zeigt den Wert eines **ReportItem** -Textfelds mit dem Namen `Textbox1`an:  
  
     `=ReportItems!Textbox1.Value`  
  
-   Dieser Ausdruck wird in der Color-Eigenschaft eines **ReportItem**-Textfelds platziert und zeigt den Text in Schwarz an, wenn der Wert > 0 ist. Andernfalls wird der Wert in Rot angezeigt:  
  
     `=IIF(Me.Value > 0,"Black","Red")`  
  
-   Dieser Ausdruck wird in einem Textfeld des Seitenkopfes oder Seitenfußes platziert und zeigt den ersten Wert pro Seite des gerenderten Berichts für ein Textfeld mit dem Namen `LastName`an:  
  
     `=First(ReportItems("LastName").Value)`  
  
## <a name="dictionary-style-page-header-expressions"></a>Seitenkopfausdrücke im Wörterbuchformat  
 Sie können einen Seitenkopf erstellen, der den ersten Kunden auf der Seite und den letzten Kunden auf der Seite anzeigt. Da ein Textfeld im Seitenkopf nur einmal auf die integrierte **ReportItems** -Sammlung verweisen kann, müssen Sie dem Seitenkopf zwei Textfelder hinzufügen: ein Feld für den Namen des ersten Kunden (`=First(ReportItems!textboxLastName.Value`) und ein Feld für den Namen des letzten Kunden (`=Last(ReportItems!textboxLastName.Value`).  
  
 In einem Seitenkopf- oder Seitenfußabschnitt sind nur Textfelder auf der aktuellen Seite als Elemente der **ReportItems** -Auflistung verfügbar. Wenn `ReportItems!textboxLastName.Value` beispielsweise auf ein Textfeld verweist, das nur auf der ersten Seite eines mehrseitigen Datenbereichs angezeigt wird, wird ein Wert für die erste Seite angezeigt. Alle anderen Seiten enthalten jedoch die Meldung **#Error** , die angibt, dass der Ausdruck nicht als geschrieben ausgewertet werden konnte.  
  
## <a name="scope-for-the-reportitems-collection"></a>Bereich der ReportItems-Auflistung  
 Während der Bericht verarbeitet wird, wird jedes Textfeld im Berichtshauptteil oder in einem Datenbereich im Kontext des entsprechenden Datasets, des Datenbereichs und der Gruppenzuordnungen ausgewertet. Der Bereich für einen Verweis auf die **ReportItems** -Auflistung ist der aktuelle Bereich oder jeder Punkt, der höher liegt als der aktuelle Bereich.  
  
 Ein Textfeld in einer Zeile, die sich in einer übergeordneten Gruppe befindet, darf beispielsweise keinen Ausdruck enthalten, der auf den Namen eines Textfelds in einer Zeile einer untergeordneten Gruppe verweist. Ein solcher Ausdruck wird nicht in einen Wert des Berichts aufgelöst, da sich das Textfeld in der untergeordneten Zeile außerhalb des Bereichs befindet. Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integrierte Sammlungen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
