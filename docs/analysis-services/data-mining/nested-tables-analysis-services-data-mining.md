---
title: "Geschachtelte Tabellen (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], nested tables
- tables [Analysis Services], nested
- nested tables
ms.assetid: cb192aa2-597e-4d4f-ac34-3556d037fed4
caps.latest.revision: 52
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ad436f2cfa5da5381ad683a1fc804468c5a40d3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="nested-tables-analysis-services---data-mining"></a>Geschachtelte Tabellen (Analysis Services - Data Mining)
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]müssen einem Data Mining-Algorithmus Daten in Form einer Reihe von Fällen zugeführt werden, die in einer Falltabelle enthalten sind. Nicht alle Fälle lassen sich jedoch durch eine einzelne Datenzeile beschreiben. So kann sich ein Fall z.&nbsp;B. aus zwei Tabellen ableiten: einer Tabelle mit Kundeninformationen und einer anderen Tabelle mit den von Kunden getätigten Käufen. Ein einzelner Kunde in der Kundeninformationstabelle könnte über mehrere Elemente in der Kundenkäufe-Tabelle verfügen, weshalb es schwierig ist, die Daten in einer einzelnen Zeile zu beschreiben. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt eine eindeutige Methode zum Verarbeiten dieser Fälle bereit, indem *geschachtelte Tabellen*verwendet werden. Das Konzept von geschachtelten Tabellen wird in der folgenden Abbildung veranschaulicht.  
  
 ![Zwei Tabellen mit einer geschachtelten Tabelle kombiniert](../../analysis-services/data-mining/media/nested-tables.gif "zwei Tabellen mit einer geschachtelten Tabelle kombiniert")  
  
 In diesem Diagramm enthält die erste Tabelle, bei der es sich um die übergeordnete Tabelle handelt, Kundeninformationen und ordnet jedem Kunden einen eindeutigen Bezeichner zu. Die zweite (untergeordnete) Tabelle enthält die von jedem Kunden getätigten Käufe. Die Käufe in der untergeordneten Tabelle werden durch den eindeutigen Bezeichner, die **CustomerKey** -Spalte, mit der übergeordneten Tabelle verknüpft. Die dritte Tabelle zeigt, wie die beiden Tabellen kombiniert werden.  
  
 Eine geschachtelte Tabelle wird in der Falltabelle als eine spezielle Spalte dargestellt, die dem **TABLE**-Datentyp zugehört. Für jede Fallzeile sind in dieser Art von Spalte ausgewählte Zeilen der untergeordneten Tabelle enthalten, die die übergeordnete Tabelle betreffen.  
  
 Die Daten in einer geschachtelten Tabelle können für die Vorhersage oder die Eingabe verwendet werden, oder aber für beides. Wenn beispielsweise ein Modell zwei Spalten einer geschachtelten Tabelle enthält, kann eine Spalte der geschachtelten Tabelle eine Liste mit den Produkten enthalten, die von einem Kunden bislang gekauft wurden, während die andere Spalte der geschachtelten Tabelle Informationen zu den Hobbys und Interessen des Kunden enthält, die möglicherweise in einer Umfrage erfasst wurden. In diesem Szenario können Sie die Hobbys und Interessen des Kunden als Eingabedaten für die Analyse des Kaufverhaltens verwenden und so wahrscheinliche Käufe vorhersagen.  
  
## <a name="joining-case-tables-and-nested-tables"></a>Verknüpfen von Falltabellen und geschachtelten Tabellen  
 Um eine geschachtelte Tabelle zu erstellen, müssen die beiden Quelltabellen eine definierte Beziehung enthalten, sodass die Elemente in der einen Tabelle der anderen Tabelle zugeordnet werden können. In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]können Sie diese Beziehung in der Datenquellensicht definieren.  
  
> [!NOTE]  
>  Das Feld **CustomerKey** ist ein relationaler Schlüssel, mit dem die Falltabelle und die geschachtelte Tabelle in der Datenquellensicht-Definition miteinander verknüpft werden und mit der die Beziehung zwischen den Spalten in der Miningstruktur festgelegt wird. In der Regel sollte dieser relationale Schlüssel aber nicht in auf dieser Struktur basierenden Miningmodellen verwendet werden. In der Regel empfiehlt es sich, die relationale Schlüsselspalte nicht in das Miningmodell aufzunehmen, wenn sie nur zum Verknüpfen der Tabellen dient und keine für die Analyse relevanten Informationen bereitstellt.  
  
 Geschachtelte Tabellen können entweder programmgesteuert mithilfe von DMX (Data Mining Extensions) oder AMO (Analysis Management Objects) erstellt werden, Sie können aber auch den Data Mining-Assistenten und den Data Mining-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]hierfür verwenden.  
  
## <a name="using-nested-table-columns-in-a-mining-model"></a>Verwenden von geschachtelten Tabellenspalten in einem Miningmodell  
 In der Falltabelle ist der Schlüssel oft eine Kundenkennung, ein Produktname oder ein Datum in einer Folge: Daten, die eine Zeile der Tabelle eindeutig identifizieren. verwendet werden. In geschachtelten Tabellen ist der Schlüssel dagegen meist nicht der relationale Schlüssel (oder Fremdschlüssel), sondern die Spalte, die das zu modellierende Attribut enthält.  
  
 Wenn die Falltabelle beispielsweise Bestellungen enthält und die geschachtelte Tabelle enthält die Artikel der Bestellung, wäre es interessant, die Beziehung zwischen den in der geschachtelten Tabelle gespeicherten Artikeln für mehrere der in der Falltabelle gespeicherten Bestellungen zu modellieren. Obwohl die geschachtelte Tabelle **Items** über den relationalen Schlüssel **OrderID** mit der Falltabelle **Orders**verknüpft ist, sollte **OrderID** nicht als Schlüsselspalte für die geschachtelte Tabelle verwendet werden. Stattdessen sollten Sie die Spalte **Items** als Schlüsselspalte für die geschachtelte Tabelle verwenden, weil diese die zu modellierenden Daten enthält. Meist kann die Spalte **OrderID** im Miningmodell gefahrlos ignoriert werden, weil die Beziehung zwischen der Falltabelle und der geschachtelten Tabelle bereits durch die Definition der Datenquellensicht festgelegt wurde.  
  
 Bei der Auswahl einer Spalte als Schlüsselspalte für die geschachtelte Tabelle müssen Sie sicherstellen, dass die Werte dieser Spalte für jeden Fall eindeutig sind. Wenn die Falltabelle beispielsweise Kunden darstellt und die geschachtelte Tabelle die von den Kunden gekauften Artikel darstellt, müssen Sie sicherstellen, dass kein Artikel für einen Kunden mehrmals aufgeführt wird. Wenn ein Kunde den gleichen Artikel mehrmals gekauft hat, sollten Sie eine andere Sicht mit einer Spalte erstellen, die die Anzahl der Käufe für jedes einzelne Produkt aggregiert.  
  
 Wie doppelte Werte in einer geschachtelten Tabelle gehandhabt werden sollen, hängt von dem zu erstellenden Miningmodell und dem zu lösenden Geschäftsproblem ab. In einigen Szenarien ist es möglicherweise gleichgültig, wie oft ein Kunde ein bestimmtes Produkt gekauft hat, weil nur geprüft werden soll, ob mindestens ein Kauf getätigt wurde. In anderen Szenarien ist möglicherweise die Quantität und die Sequenz der Käufe sehr wichtig.  
  
 Wenn die Reihenfolge der Elemente wichtig ist, benötigen Sie unter Umständen eine weitere Spalte, die die Sequenz angibt. Wenn Sie den Sequence Clustering-Algorithmus zum Erstellen eines Modells verwenden, müssen Sie eine zusätzliche *Schlüsselsequenzspalte* auswählen, welche die Reihenfolge der Elemente darstellt. Die Schlüsselsequenzspalte ist eine spezielle Art von geschachtelter Schlüsselspalte, die nur in Sequenzclustermodellen verwendet wird und einen eindeutigen numerischen Datentyp erfordert. Beispielsweise können sowohl ganze Zahlen als auch Datumsangaben als Schlüsselsequenzspalte verwendet werden, jedoch müssen alle Sequenzwerte eindeutig sein. Neben der Schlüsselsequenzspalte verfügt ein Sequenzclustermodell auch über eine geschachtelte Tabellenschlüsselspalte, die das zu modellierende Attribut darstellt, z.&nbsp;B. die gekauften Produkte.  
  
### <a name="using-non-key-nested-columns-from-a-nested-table"></a>Verwenden von geschachtelten Nichtschlüsselspalten einer geschachtelten Tabelle  
 Nachdem Sie den Join zwischen der Falltabelle und der geschachtelten Tabelle definiert und eine Spalte ausgewählt haben, die interessante und eindeutige Attribute enthält und als Schlüsselspalte der geschachtelten Tabelle dienen soll, können Sie andere Spalten der geschachtelten Tabelle als Eingabespalten in das Modell aufnehmen. Alle Spalten der geschachtelten Tabelle können als Eingabe, für Vorhersagen und als Eingabe oder nur für Vorhersagen verwendet werden.  
  
 Wenn die geschachtelte Tabelle beispielsweise die Spalten **Product**, **ProductQuantity**und **ProductPrice**enthält, können Sie **Product** als Schlüsselspalte der geschachtelten Tabelle festlegen und der Miningstruktur **ProductQuantity** als Eingabespalte hinzufügen.  
  
## <a name="filtering-nested-table-data"></a>Filtern von geschachtelten Tabellendaten  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]können Sie Filter für Daten definieren, die zum Trainieren oder Testen eines Data Mining-Modells verwendet werden. Mit einem Filter kann die Zusammensetzung des Modell beeinflusst oder das Modell an einer Teilmenge der Fälle getestet werden. Filter können auch auf geschachtelte Tabellen angewendet werden. Es gibt Einschränkungen bezüglich der Syntax, die für geschachtelte Tabellen verwendet werden kann.  
  
 Wenn Sie einen Filter auf eine geschachtelte Tabelle anwenden, prüfen Sie, ob ein Attribut vorhanden oder nicht vorhanden ist. Sie können beispielsweise einen Filter anwenden, der die im Modell verwendeten Fälle auf diejenigen Fälle beschränkt, die in der geschachtelten Tabelle einen bestimmten Wert aufweisen. Sie könnten die im Modell verwendeten Fälle auch auf die Kunden beschränken, die einen bestimmten Artikel nicht gekauft haben.  
  
 Wenn Sie Filter für eine geschachtelte Tabelle definieren, können Sie auch Operatoren wie "größer als" oder "kleiner als" verwenden. Sie könnten beispielsweise die im Modell verwendeten Fälle auf Kunden beschränken, die mindestens n Einheiten des Zielprodukts gekauft haben. Die Fähigkeit, geschachtelte Tabellenattribute zu filtern, ermöglicht es, Modelle auf verschiedenste Weise anzupassen.  
  
 Weitere Informationen zum Erstellen und Verwenden von Modellfiltern finden Sie unter [Filter für Miningmodelle &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
