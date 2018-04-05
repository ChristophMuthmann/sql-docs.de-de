---
title: Ausdrucksverwendungen in Berichten (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- expressions [Reporting Services], about expressions
ms.assetid: 76b9ed31-5aec-40fc-bb88-a1c1b0ab3fc3
caps.latest.revision: 59
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: bc3cfbff325d163ca9ddde120ecc17db97e91c03
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="expression-uses-in-reports-report-builder-and-ssrs"></a>Ausdrucksverwendungen in Berichten (Berichts-Generator und SSRS)
In paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichten werden Ausdrücke innerhalb der gesamten Berichtsdefinition verwendet, um Werte für folgende Elemente anzugeben oder zu berechnen: Parameter, Abfragen, Filter, Berichtselementeigenschaften, Gruppierungs- und Sortierdefinitionen, Textfeldeigenschaften, Lesezeichen, Dokumentstrukturen, dynamischer Inhalt von Seitenkopf- und Seitenfußzeilen, Bilder und dynamische Datenquellendefinitionen. Dieses Hilfethema enthält Beispiele für die vielen Anwendungsmöglichkeiten, die Ausdrücke bieten, um den Inhalt oder die Darstellung eines Berichts zu variieren. Es handelt sich dabei aber nicht um eine vollständige Liste. Sie können für jede beliebige Eigenschaft einen Ausdruck in einem Dialogfeld festlegen, in dem die Ausdrucksschaltfläche (**fx**) angezeigt wird, oder in einer Dropdownliste, in der **\<Ausdruck...>** angezeigt wird.  
  
 Ausdrücke können einfach oder komplex sein. *Einfache Ausdrücke* enthalten einen Verweis auf ein einzelnes Datasetfeld, einen Parameter oder ein integriertes Feld. Komplexe Ausdrücke können mehrere integrierte Verweise, Operatoren und Funktionsaufrufe enthalten. Beispiel: Ein komplexer Ausdruck könnte die auf dem Feld Vertrieb angewendete Sum-Funktion einschließen.  
  
 Ausdrücke werden in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]geschrieben. Ein Ausdruck beginnt mit einem Gleichheitszeichen (=) gefolgt von einer Kombination aus Verweisen auf integrierte Auflistungen wie Datasetfelder und Parameter, Konstanten, Funktionen und Operatoren.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Simple"></a> Verwenden von einfachen Ausdrücken  
 Auf der Entwurfsoberfläche und in Dialogfeldern werden einfache Ausdrücke in Klammern angezeigt. Ein Datasetfeld wird z. B. als `[ProductID]`angezeigt. Einfache Ausdrücke werden automatisch für Sie erstellt, wenn Sie ein Feld aus einem Dataset auf ein Textfeld ziehen. Es wird ein Platzhalter erstellt, und der Ausdruck definiert den zugrunde liegenden Wert. Sie können Ausdrücke auch direkt in eine Datenbereichszelle oder in ein Textfeld eingeben. Dies ist sowohl auf der Entwurfsoberfläche als auch in einem Dialogfeld möglich (Beispiel: `[ProductID]`).  
  
 In der folgenden Tabelle sind Beispiele dafür aufgeführt, wie Sie einfache Ausdrücke verwenden können. In der Tabelle sind die Funktionen, die festzulegende Eigenschaft, das normalerweise zum Festlegen verwendete Dialogfeld und der Wert der Eigenschaft beschrieben. Sie können den einfachen Ausdruck direkt auf der Entwurfsoberfläche, in einem Dialogfeld oder im Bereich Eigenschaften eingeben. Alternativ dazu können Sie den Ausdruck im Dialogfeld Ausdruck bearbeiten, wie Sie dies auch mit anderen Ausdrücken tun.  
  
|Funktionalität|Eigenschaft, Kontext und Dialogfeld|Eigenschaftswert|  
|-------------------|---------------------------------------|--------------------|  
|Angeben eines Datasetfelds, das in einem Textfeld angezeigt werden soll.|Value-Eigenschaft für einen Platzhalter in einem Textfeld. Dialogfeld **Platzhaltereigenschaften, Allgemein**.|`[Sales]`|  
|Aggregieren von Werten für eine Gruppe.|Value-Eigenschaft für einen Platzhalter in einer Zeile, die einer Tablix-Gruppe zugeordnet ist. Dialogfeld **Textfeldeigenschaften**.|`[Sum(Sales)]`|  
|Einbinden einer Seitenzahl.|Value-Eigenschaft für einen Platzhalter in einem Textfeld, das in eine Seitenkopfzeile eingefügt wird. Dialogfeld **Textfeldeigenschaften, Allgemein**.|`[&PageNumber]`|  
|Anzeigen eines ausgewählten Parameterwerts.|Value-Eigenschaft für einen Platzhalter in einem Textfeld auf der Entwurfsoberfläche. Dialogfeld **Textfeldeigenschaften, Allgemein**.|`[@SalesThreshold]`|  
|Angeben einer Gruppendefinition für einen Datenbereich.|Gruppierungsausdruck für die Tablix-Gruppe. Dialogfeld **Tablix-Gruppeneigenschaften, Allgemein**.|`[Category]`|  
|Ausschließen eines bestimmten Feldwerts aus einer Tabelle.|Filtergleichung für Tablix. Dialogfeld **Tablix-Eigenschaften, Filter**.|Wählen Sie als Datentyp die Option **Ganze Zahl**.<br /><br /> `[Quantity]`<br /><br /> `>`<br /><br /> `100`|  
|Alleiniges Einbinden eines bestimmten Werts für einen Gruppenfilter.|Filtergleichung für die Tablix-Gruppe. Dialogfeld **Tablix, Gruppeneigenschaften, Filter**.|`[Category]`<br /><br /> `=`<br /><br /> `Clothing`|  
|Ausschließen bestimmter Werte für mehr als ein Feld aus einem Dataset.|Filtergleichung für eine Gruppe in einem Tablix-Element. Dialogfeld **Tablix-Eigenschaften, Filter**.|`=[Color]`<br /><br /> `<>`<br /><br /> `Red`<br /><br /> `=[Color]`<br /><br /> `<>`<br /><br /> `Blue`|  
|Angeben der Sortierreihenfolge basierend auf einem vorhandenen Feld in einer Tabelle.|Sortierausdruck des Tablix-Elements. Dialogfeld **Tablix-Eigenschaften, Sortierung**.|`[SizeSortOrder]`|  
|Verknüpfen eines Abfrageparameters mit einem Berichtsparameter.|Parameterauflistung im Dataset. Dialogfeld **Dataseteigenschaften, Parameter**.|`[@Category]`<br /><br /> `[@Category]`|  
|Übergeben eines Parameters aus einem Hauptbericht an einen Unterbericht.|Parameterauflistung im Unterbericht. Dialogfeld **Eigenschaften des Unterberichts, Parameter**.|`[@Category]`<br /><br /> `[@Category]`|  
  
##  <a name="Complex"></a> Verwenden von komplexen Ausdrücken  
 Komplexe Ausdrücke können mehrere integrierte Verweise, Operatoren und Funktionsaufrufe enthalten und werden auf der Entwurfsoberfläche als `<<Expr>>`angezeigt. Um den Ausdruckstext anzuzeigen oder zu ändern, müssen Sie das Dialogfeld **Ausdruck** öffnen oder direkt im Bereich Eigenschaften eine Eingabe vornehmen. In der folgenden Tabelle ist aufgeführt, auf welche Weise Sie einen komplexen Ausdruck verwenden können, um Daten anzuzeigen oder zu organisieren oder die Darstellung des Berichts zu ändern. Dazu zählen auch die festzulegende Eigenschaft, das normalerweise zum Festlegen verwendete Dialogfeld und der Wert der Eigenschaft. Sie können einen Ausdruck direkt in ein Dialogfeld, auf der Entwurfsoberfläche oder im Bereich Eigenschaften eingeben.  
  
|Funktionalität|Eigenschaft, Kontext und Dialogfeld|Eigenschaftswert|  
|-------------------|---------------------------------------|--------------------|  
|Berechnen von Aggregatwerten für ein Dataset.|Value-Eigenschaft für einen Platzhalter in einem Textfeld. Dialogfeld **Platzhaltereigenschaften, Allgemein**.|`=First(Fields!Sales.Value,"DataSet1")`|  
|Verketten von Text und Ausdrücken in einem Textfeld.|Wert für einen Platzhalter in einem Textfeld, das in eine Seitenkopf- oder Seitenfußzeile eingefügt wird. Dialogfeld **Platzhaltereigenschaften, Allgemein**.|`="This report began processing at " & Globals!ExecutionTime`|  
|Berechnen eines Aggregatwerts für ein Dataset in einem anderen Bereich.|Wert für einen Platzhalter in einem Textfeld, das in eine Tablix-Gruppe eingefügt wird. Dialogfeld **Platzhaltereigenschaften, Allgemein**.|`=Max(Fields!Total.Value,"DataSet2)`|  
|Formatieren von Daten in einem Textfeld in Abhängigkeit des Werts.|Farbe für einen Platzhalter in einem Textfeld in der Detailzeile eines Tablix-Elements. Dialogfeld **Textfeldeigenschaften, Schriftart**.|`=IIF(Fields!TotalDue.Value < 10000,"Red","Black")`|  
|Einmaliges Berechnen eines Werts, um überall im Bericht darauf verweisen zu können.|Wert für eine Berichtsvariable. Dialogfeld **Berichtseigenschaften, Variablen**.|`=Variables!MyCalculation.Value`|  
|Einschließen bestimmter Werte für mehrere Felder aus einem Dataset.|Filtergleichung für eine Gruppe in einem Tablix-Element. Dialogfeld **Tablix-Eigenschaften, Filter**.|Wählen Sie als Datentyp die Option **Boolesch**.<br /><br /> `=IIF(InStr(Fields!Subcat.Value,"Shorts")=0 AND (Fields!Size.Value="M" OR Fields!Size.Value="S"),TRUE, FALSE)`<br /><br /> `=`<br /><br /> `TRUE`|  
|Ausblenden eines Textfelds auf der Entwurfsoberfläche, das von Benutzern ein- oder ausgeblendet werden kann, indem diese einen booleschen Parameter mit dem Namen *Show*verwenden.|Ausgeblendete Eigenschaft in einem Textfeld. Dialogfeld **Textfeldeigenschaften, Sichtbarkeit**.|`=Not Parameters!` *Anzeigen\<boolescher Parameter>* `.Value`|  
|Angeben des dynamischen Inhalts von Seitenkopf- oder Seitenfußzeilen.|Wert für einen Platzhalter in einem Textfeld, das in die Seitenkopf- oder Seitenfußzeile eingefügt wird.|`="Page " & Globals!PageNumber & " of "  & Globals!TotalPages`|  
|Dynamisches Angeben einer Datenquelle mithilfe eines Parameters.|Verbindungszeichenfolge in der Datenquelle. Dialogfeld **Datenquelleneigenschaften, Allgemein**.|`="Data Source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks2012"`|  
|Identifizieren aller Werte für einen mehrwertigen Parameter, der vom Benutzer ausgewählt wurde.|Wert für einen Platzhalter in einem Textfeld. Dialogfeld **Tablix-Eigenschaften, Filter**.|`=Join(Parameters!MyMultivalueParameter.Value,", ")`|  
|Angeben von Seitenumbrüchen nach jeweils 20 Zeilen in einem Tablix-Element ohne andere Gruppen.|Gruppierungsausdruck für eine Gruppe in einem Tablix-Element. Dialogfeld **Gruppeneigenschaften, Seitenumbrüche**. Wählen Sie Option **Zwischen den einzelnen Instanzen einer Gruppe**aus.|`=Ceiling(RowNumber(Nothing)/20)`|  
|Angeben der bedingten Sichtbarkeit basierend auf einem Parameter.|Ausgeblendete Eigenschaft für ein Tablix-Element. Dialogfeld **Tablix-Eigenschaften, Sichtbarkeit**.|`=Not Parameters!<` *boolescher Parameter* `>.Value`|  
|Angeben eines Datums, das für einen bestimmten Kulturkreis formatiert ist.|Wert für einen Platzhalter in einem Textfeld in einem Datenbereich. Dialogfeld **Textfeldeigenschaften, Allgemein**.|`=Fields!OrderDate.Value.ToString(System.Globalization.CultureInfo.CreateSpecificCulture("de-DE"))`|  
|Verketten einer Zeichenfolge und einer Zahl, die als Prozentsatz mit zwei Dezimalstellen formatiert ist.|Wert für einen Platzhalter in einem Textfeld in einem Datenbereich. Dialogfeld **Textfeldeigenschaften, Allgemein**.|`="Growth Percent: " & Format(Fields!Growth.Value,"p2")`|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Beispiele für Filtergleichungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Seitenkopf- und Seitenfußzeilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Formatieren von Text und Platzhaltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Ausblenden eines Elements (Berichts-Generator und SSRS)](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
