---
title: "DAX in tabellarischen Modellen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 10/21/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2693985-1bea-4861-a100-cea4761ba809
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: a95f7acdcf05c003521a4471f07036b5f458b65e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="dax-in-tabular-models-ssas-tabular"></a>DAX in tabellarischen Modellen (SSAS – tabellarisch)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Data Analysis Expressions (DAX) ist eine Formelsprache, die zum Erstellen von benutzerdefinierter Berechnungen in Analysis Services, Power BI Desktop und Power Pivot in Excel verwendet. DAX-Formeln beinhalten Funktionen, Operatoren und Werte zum Ausführen erweiterter Berechnungen für Daten in Tabellen und Spalten.  
  
 Obwohl DAX in Analysis Services, Power BI Desktop und Power Pivot in Excel verwendet wird, gilt das in diesem Thema mehr Analysis Services-tabellenmodellprojekte in SQL Server Data Tools (SSDT) erstellt.  
  
##  <a name="bkmk_DAX"></a> DAX-Formeln in berechneten Spalten, Measures und Zeilenfiltern  
 Für tabellarische Modelle in SSDT erstellt werden DAX-Formeln in berechneten Spalten, Measures und Zeilenfiltern verwendet.  
  
### <a name="calculated-columns"></a>Berechnete Spalten  
 Eine berechnete Spalte ist eine Spalte, die Sie einer vorhandenen Tabelle (im Modell-Designer) hinzu, und erstellen Sie eine DAX-Formel, die Werte der Spalte definiert. 
  
> [!NOTE]  
>  Berechnete Spalten werden nicht für Modelle unterstützt, die Daten mit dem DirectQuery-Modus aus einer relationalen Datenquelle abrufen.  
  
 Wenn eine berechnete Spalte eine gültige DAX-Formel enthält, werden Werte für jede Zeile berechnet, sobald die Formel eingegeben wird. Werte werden dann in der Datenbank gespeichert. Wenn in einer Date-Tabelle beispielsweise die Formel `=[Calendar Year] & " Q" & [Calendar Quarter]` in die Bearbeitungsleiste eingegeben wird, wird ein Wert für jede Zeile in der Tabelle berechnet, indem Werten aus der Calendar Year-Spalte (in der gleichen Date-Tabelle) ein Leerzeichen und der Großbuchstabe Q hinzugefügt wird und anschließend die Werte aus der Calendar Quarter-Spalte (in der gleichen Date-Tabelle) hinzugefügt werden. Das Ergebnis wird für jede Zeile in der berechneten Spalte sofort berechnet und beispielsweise in der Form **2010 Q1**angezeigt. Spaltenwerte werden nur neu berechnet, wenn die Daten erneut verarbeitet werden.  
  
 Weitere Informationen finden Sie unter [Berechnete Spalten](../../analysis-services/tabular-models/ssas-calculated-columns.md)erstellte tabellarische Modellprojekte.  
  
### <a name="measures"></a>Measures  
 Measures sind dynamische Formeln, deren Ergebnisse sich abhängig vom Kontext ändern. Measures werden in Berichtsformaten, die unterstützen kombinieren und Filtern von Modelldaten anhand mehrerer Attribute wie z. B. einer Power BI-Bericht oder Excel-PivotTable oder PivotChart verwendet. Measures werden vom Modellentwickler mit dem measureraster (und der Bearbeitungsleiste) im Modell-Designer in SSDT definiert.  
  
 Die Formeln in Measures können automatische mithilfe der AutoSumme-Funktion erstellte Standardaggregationsfunktionen verwenden, z. B. COUNT oder SUM, oder Sie können mit DAX eigene Formeln definieren. Wenn Sie in der Bearbeitungsleiste eine Formel für ein Measure definieren, wird über die QuickInfo eine Vorschau der Ergebnisse für den Gesamtwert im aktuellen Kontext angezeigt. Die Ergebnisse werden jedoch noch nicht ausgegeben. Andere Measuredetails werden auch im Bereich **Eigenschaften** angezeigt.  
  
 Der Grund dafür, dass Sie die (gefilterten) Ergebnisse der Berechnung nicht sofort einsehen können, ist, dass das Ergebnis eines Measures ohne einen Kontext nicht bestimmt werden kann. Das Auswerten eines Measures erfordert eine Clientanwendung zur Berichtserstellung, die in der Lage ist, den erforderlichen Kontext bereitzustellen, um die relevanten Daten für jede Zelle abrufen und anschließend den Ausdruck für jede Zelle auswerten zu können. Dieser Client kann eine Excel-PivotTable oder PivotChart, ein Power BI-Bericht oder eine MDX-Abfrage sein. Unabhängig vom Berichterstellungsclient wird tatsächlich für jede Zelle in den Ergebnissen eine separate Abfrage ausgeführt. Das heißt, generiert jede Kombination von Zeilen- und Spaltenüberschriften in einer PivotTable und jede Auswahl von Slicern und Filtern in einem Power BI-Bericht auf eine andere Teilmenge der Daten, die für die das Measure berechnet wird. Z. B. in einem Measure mit der Formel `Total Sales:=SUM([Sales Amount])`, wenn ein Benutzer das TotalSales-Measure im Fenster Werte in einer PivotTable platziert, und klicken Sie dann stellen die DimProductCategory-Spalte aus einer DimProduct-Tabelle im Fenster Zeilenfilter, die Summe von Sales Amount berechnet und für jede Produktkategorie angezeigt.  
  
 Anders als bei berechneten Spalten und Zeilenfiltern enthält die Syntax für ein Measure den Namen des Measures vor der Formel. Im obigen Beispiel wird der Name **Total Sales:** vor der Formel angezeigt. Nachdem Sie ein Measure erstellt haben, werden der Name und die Definition in der Feldliste der Clientanwendung zur Berichtserstellung angezeigt, und das Measure steht, abhängig von Perspektiven und Rollen, allen Benutzern des Modells zur Verfügung.  
  
 Weitere Informationen finden Sie unter [Measures](../../analysis-services/tabular-models/measures-ssas-tabular.md)erstellte tabellarische Modellprojekte.  
  
### <a name="row-filters"></a>Zeilenfilter  
 Zeilenfilter definieren, welche Zeilen in einer Tabelle für Mitglieder einer bestimmten Rolle sichtbar sind. Zeilenfilter können für jede Tabelle in einem Modell mithilfe von DAX-Formeln erstellt werden. Zeilenfilter werden für eine bestimmte Rolle mithilfe von SSDT-Rollen-Manager erstellt. Zeilenfilter können auch für ein bereitgestelltes Modell mit Rolleneigenschaften in SQL Server Management Studio (SSMS) definiert werden.  
  
 In einem Zeilenfilter definiert eine DAX-Formel, die den booleschen Wert TRUE oder FALSE ergeben muss, die Zeilen, die von Mitgliedern dieser spezifischen Rolle in Form der Abfrageergebnisse zurückgegeben werden können. Nicht in der DAX-Formel enthaltene Zeilen können nicht zurückgegeben werden. Beispielsweise können Mitglieder der Sales-Rolle in der Customers-Tabelle mit der DAX-Formel `=Customers[Country] = “USA”`nur Daten für Kunden in den USA anzeigen. Außerdem werden Aggregate, z.B. SUM, nur für Kunden in den USA zurückgegeben.  
  
 Wenn Sie mithilfe der DAX-Formel einen Zeilenfilter definieren, erstellen Sie ein zulässiges Rowset. Dadurch wird der Zugriff auf andere Zeilen nicht verweigert, sie werden vielmehr nicht als Teil des zulässigen Rowsets zurückgegeben Andere Rollen können Zugriff auf die von der DAX-Formel ausgeschlossenen Zeilen gewähren. Wenn ein Benutzer einer anderen Rolle angehört und der Zeilenfilter dieser Rolle Zugriff auf dieses bestimmte Rowset gewährt, kann der Benutzer die Daten für diese Zeile anzeigen.  
  
 Zeilenfilter gelten für die angegebenen sowie für verknüpfte Zeilen. Wenn eine Tabelle über mehrere Beziehungen verfügt, wird die Sicherheit für die aktive Beziehung mithilfe von Filtern gewährleistet. Für Zeilenfilter und Zeilenfilter, die für verknüpfte Tabellen definiert wurden, wird eine Schnittmenge gebildet.  
  
 Weitere Informationen finden Sie unter [Rollen](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
##  <a name="bkmk_DAX_datatypes"></a> DAX-Datentypen  
 Daten können in ein Modell aus vielen unterschiedlichen Datenquellen importiert werden, die unterschiedliche Datentypen unterstützen. Beim Importieren von Daten in ein Modell werden die Daten in einen der tabellarischen Modelldatentypen umgewandelt. Wenn die Modelldaten in einer Berechnung verwendet werden, werden die Daten für die Dauer und die Ausgabe der Berechnung dann in einen DAX-Datentyp konvertiert. Wenn Sie eine DAX-Formel erstellen, bestimmen die in der Formel verwendeten Begriffe automatisch den zurückgegebenen Wertdatentyp.  
  
 Tabellarische Modelle und DAX unterstützen die folgenden Datentypen:  
  
|Datentyp im Modell|Datentyp in DAX|Description|  
|------------------------|----------------------|-----------------|  
|Ganze Zahl|Ein ganzzahliger 64-Bit-Wert (acht Byte) <sup>1, 2</sup>|Zahlen ohne Dezimalstellen. Ganze Zahlen können positiv oder negativ sein, aber müssen ganze Zahlen zwischen -9 223 372 036 854 775 808 (-2^63) und 9 223 372 036 854 775 807 (2^63-1) sein.|  
|Decimal Number|Eine reelle 64-Bit-Zahl (acht Byte) <sup>1, 2</sup>|Reelle Zahlen sind Zahlen, die Dezimalstellen aufweisen können. Reelle Zahlen decken viele Werte ab:<br /><br /> Negative Werte von -1,79E +308 bis -2,23E -308<br /><br /> Null (0)<br /><br /> Positive Werte von 2,23E -308 bis -1,79E +308<br /><br /> Die Anzahl der relevanten Stellen wird jedoch auf siebzehn Dezimalstellen beschränkt.|  
|Boolean|Boolean|Entweder ein True oder ein False-Wert.|  
|Textmodus|Zeichenfolge|Eine Unicodezeichen-Datenzeichenfolge. Dies können Zeichenfolgen, Zahlen oder Datumsangaben im Textformat sein.|  
|date|Date/Time|Datumsangaben und Uhrzeiten in einer akzeptierten Form für die Darstellung von Datum und Uhrzeit.<br /><br /> Gültig sind alle Datumsangaben nach dem 1. März 1900.|  
|Währung|Währung|Der Währungsdatentyp lässt Werte zwischen -922 337 203 685 477,5808 und 922 337 203 685 477,5807 mit vier Dezimalstellen unveränderlicher Genauigkeit zu.|  
|–|Leer|Ein leerer Datentyp in DAX, der SQL-NULLEN darstellt und ersetzt. Sie können mit der BLANK-Funktion ein Leerzeichen erstellen und mit der logischen ISBLANK-Funktion nach Leerzeichen suchen.|  
  
 Tabellarische Modelle beinhalten auch den Table-Datentyp als Eingabe oder Ausgabe für viele DAX-Funktionen. Beispielsweise nimmt die FILTER-Funktion eine Tabelle als Eingabe an und gibt eine neue Tabelle aus, die nur die Zeilen enthält, die die Filterbedingungen erfüllen. Die Kombination von Tabellen- und Aggregationsfunktionen ermöglicht Ihnen die Ausführung komplexer Berechnungen für dynamisch definierte Datasets.  
  
 Obwohl Datentypen in der Regel automatisch festgelegt werden, ist es wichtig, ihre Funktion und Gültigkeit zu verstehen. Dies gilt insbesondere für DAX-Formeln. Fehler in Formeln oder unerwartete Ergebnisse werden z. B. oft von einem bestimmten Operator verursacht, der nicht mit einem in einem Argument angegebenen Datentyp verwendet werden kann. Die Formel `= 1 & 2`gibt z.B. ein Zeichenfolgenergebnis von 12 zurück, die Formel `= “1” + “2”`dagegen die ganze Zahl 3.  
  
 Ausführliche Informationen zu Datentypen in tabellarischen Modellen und expliziten und impliziten Konvertierungen von Datentypen in DAX, finden Sie unter [unterstützte Datentypen](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
##  <a name="bkmk_DAX_opertors"></a> DAX-Operatoren  
 In der DAX-Sprache werden vier verschiedene Berechnungsoperatortypen in Formeln verwendet:  
  
-   Vergleichsoperatoren, um Werte zu vergleichen und einen logischen TRUE\FALSE-Wert zurückzugeben  
  
-   Arithmetische Operatoren, um arithmetische Berechnungen auszuführen, die numerische Werte zurückgeben  
  
-   Textverkettungsoperatoren, die zwei oder mehr Textzeichenfolgen verknüpfen  
  
-   Logische Operatoren, die zwei oder mehr Ausdrücke kombinieren, um ein einzelnes Ergebnis zurückzugeben  
  
 Weitere Informationen zu den in DAX-Formeln verwendeten Operatoren finden Sie unter [DAX-Operator (Referenz)](http://msdn.microsoft.com/en-us/1befbddc-6178-472c-8bc4-05dafd62207e).  
  
##  <a name="bkmk_DAX_Formulas"></a> DAX-Formeln  
 DAX-Formeln sind für das Erstellen von Berechnungen in berechneten Spalten und Measures sowie das Schützen der Daten mit Zeilenebenenfiltern maßgeblich. Um Formeln für berechnete Spalten und Measures erstellen, verwenden Sie die Bearbeitungsleiste entlang des oberen Randes der Modell-Designer-Fenster oder der DAX-Editor. Um Formeln für Zeilenfilter zu erstellen, verwenden Sie das Dialogfeld Rollen-Manager. Die Informationen in diesem Abschnitt sollen Ihnen den Einstieg in die Grundlagen von DAX-Formeln erleichtern.  
  
###  <a name="basics"></a> Formelgrundlagen  
 Mit DAX können Entwickler von tabellarischen Modellen eigene Berechnungen in beiden Modelltabellen als Teil berechneter Spalten oder als Measures definieren, die Tabellen zugeordnet sind, in diesen aber nicht direkt erscheinen. DAX ermöglicht es Modellentwicklern auch, Daten zu schützen, indem sie Berechnungen erstellen, die einen booleschen Wert zurückgeben, der definiert, welche Zeilen in einer bestimmten oder einer verknüpften Tabelle von Mitgliedern der zugehörigen Rolle abgefragt werden können.  
  
 DAX-Formeln können sehr einfach oder sehr komplex sein. In der folgenden Tabelle werden einige Beispiele für einfache Formeln aufgeführt, die in einer berechneten Spalte verwendet werden können.  
  
|||  
|-|-|  
|Formel|Description|  
|`=TODAY()`|Fügt das aktuelle Datum in jede Zeile der Spalte ein.|  
|`=3`|Fügt den Wert 3 in jede Zeile der Spalte ein.|  
|`=[Column1] + [Column2]`|Fügt die Werte in der gleichen Zeile von [Column1] und [Column2] hinzu und fügt die Ergebnisse in die gleiche Zeile der berechneten Spalte ein.|  
  
 Unabhängig davon, ob die von Ihnen erstellte Formel einfach oder komplex ist, können Sie beim Erstellen einer Formel die folgenden Schritte befolgen:  
  
1.  Alle Formeln müssen mit einem Gleichheitszeichen beginnen.  
  
2.  Sie können einen Funktionsnamen eingeben oder auswählen oder einen Ausdruck eingeben.  
  
3.  Geben Sie die ersten Buchstaben der gewünschten Funktion oder des Namens ein. Mithilfe von AutoVervollständigen wird eine Liste der verfügbaren Funktionen, Tabellen und Spalten angezeigt. Drücken Sie TAB-TASTE, um ein Element aus der AutoVervollständigen-Liste zur Formel hinzuzufügen.  
  
     Sie können auch auf die Schaltfläche **Fx** klicken, um eine Liste der verfügbaren Funktionen anzuzeigen. Um in der Dropdownliste eine Funktion auszuwählen, markieren Sie diese mit den Pfeiltasten, und klicken Sie auf **OK** , um die Formel der Funktion hinzuzufügen.  
  
4.  Geben Sie die Argumente für die Funktion an, indem Sie sie aus einer Dropdownliste möglicher Tabellen und Spalten auswählen oder manuell eingeben.  
  
5.  Überprüfen Sie die Syntax auf Fehler: Stellen Sie sicher, dass alle Klammern geschlossen sind und dass alle Verweise auf Spalten, Tabellen und Werte gültig sind.  
  
6.  Drücken Sie die EINGABETASTE, um die Formel zu übernehmen.  
  
> [!NOTE]  
>  Sobald Sie die Formel eingeben und die Formel überprüft wurde, wird die Spalte in einer berechneten Spalte mit Werten aufgefüllt. In einem Measure wird durch Drücken der EINGABETASTE die Measuredefinition im Measureraster mit der Tabelle gespeichert. Wenn eine Formel ungültig ist, wird ein Fehler angezeigt.  
  
 In diesem Beispiel untersuchen wir eine komplexere Formel in einem Measure mit dem Namen Days in Current Quarter:  
  
```  
Days in Current Quarter:=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))  
```  
  
 Dieses Measure wird zum Erstellen eines Vergleichsverhältnisses zwischen einem unvollständigen Zeitraum und dem vorherigen Zeitraum verwendet. In der Formel muss der Anteil des verstrichenen Zeitraums berücksichtigt und mit dem gleichen Anteil des vorherigen Zeitraums verglichen werden. In diesem Fall gibt [Days Current Quarter to Date]/[Days in Current Quarter] den verstrichenen Anteil des aktuellen Zeitraums zurück.  
  
 Diese Formel enthält die folgenden Elemente:  
  
|Formelelement|Description|  
|---------------------|-----------------|  
|`Days in Current Quarter:=`|Der Name des Measures.|  
|`=`|Das Gleichheitszeichen (=) kennzeichnet den Beginn der Formel.|  
|`COUNTROWS`|Die [COUNTROWS-Funktion (DAX)](http://msdn.microsoft.com/en-us/830dd659-5405-4e0a-8d26-01ae9d5e5e9a) zählt die Anzahl von Zeilen in der Date-Tabelle.|  
|`()`|Öffnende und schließende Klammern geben Argumente an.|  
|`DATESBETWEEN`|Die DATESBETWEEN-Funktion gibt die Daten zwischen dem letzten Datum für jeden Wert in der Date-Spalte in der Date-Tabelle zurück.|  
|`'Date'`|Gibt die Date-Tabelle an. Tabellen werden in einfachen Anführungszeichen angegeben.|  
|`[Date]`|Gibt die Date-Spalte in der Date-Tabelle an. Spalten werden in eckigen Klammern angegeben.|  
|`,`||  
|`STARTOFQUARTER`|Die STARTOFQUARTER-Funktion gibt das Datum des Quartalsanfangs zurück.|  
|`LASTDATE`|Die LASTDATE-Funktion gibt das letzte Datum des Quartals zurück.|  
|`'Date'`|Gibt die Date-Tabelle an.|  
|`[Date]`|Gibt die Date-Spalte in der Date-Tabelle an.|  
|`,`||  
|`ENDOFQUARTER`|Die ENDOFQUARTER-Funktion.|  
|`'Date'`|Gibt die Date-Tabelle an.|  
|`[Date]`|Gibt die Date-Spalte in der Date-Tabelle an.|  
  
#### <a name="using-formula-autocomplete"></a>Verwenden von AutoVervollständigen für Formeln  
 Sowohl die Bearbeitungsleiste im Modell-Designer als auch das Formelfenster Zeilenfilter im Dialogfeld Rollen-Manager enthalten eine AutoVervollständigen-Funktion. AutoVervollständigen unterstützt Sie bei der Eingabe einer gültigen Formelsyntax, indem für jedes Element in der Formel Optionen angezeigt werden.  
  
-   Sie können AutoVervollständigen für Formeln auch mitten in einer vorhandenen Formel mit geschachtelten Funktionen verwenden. Ausgehend vom Text unmittelbar vor der Einfügemarke werden Werte in der Dropdownliste angezeigt. Der Text nach der Einfügemarke bleibt unverändert.  
  
-   AutoVervollständigen fügt keine schließende Klammer für Funktionen ein und gleicht Klammern nicht automatisch ab. Sie müssen sicherstellen, dass die Syntax aller Funktionen fehlerfrei ist. Andernfalls können Sie die Formel nicht speichern bzw. verwenden.  
  
#### <a name="using-multiple-functions-in-a-formula"></a>Verwenden mehrerer Funktionen in einer Formel  
 Sie können Funktionen schachteln, d. h. das Ergebnis einer Funktion als Argument in einer anderen Funktion verwenden. Berechnete Spalten unterstützen bis zu 64 Schachtelungsebenen. Die Schachtelung kann jedoch die Formelerstellung und die Problembehandlung erschweren.  
  
 Viele Funktionen wurden zur ausschließlichen Verwendung als geschachtelte Funktionen entwickelt. Diese Funktionen geben eine Tabelle zurück, die nicht direkt als Ergebnis gespeichert werden kann, sondern als Eingabe für eine Tabellenfunktion verwendet werden muss. Die Funktionen SUMX, AVERAGEX und MINX erfordern beispielsweise alle eine Tabelle als erstes Argument.  
  
> [!NOTE]  
>  Für die Schachtelung von Funktionen innerhalb von Measures gelten einige Einschränkungen, um sicherzustellen, dass die Leistung durch die vielen Berechnungen, die die Abhängigkeiten zwischen Spalten erforderlich machen, nicht beeinträchtigt wird.  
  
##  <a name="bkmk_DAX_functions"></a> DAX-Funktionen  
 In diesem Abschnitt finden Sie eine Übersicht über die von DAX unterstützten *Funktionstypen* . Weitere Informationen finden Sie in der [DAX-Funktionsreferenz](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
 DAX stellt eine Vielzahl von Funktionen bereit, mit denen Sie Berechnungen mit Datumsangaben und Uhrzeiten durchführen, bedingte Werte erstellen, mit Zeichenfolgen arbeiten, Suchen auf Grundlage von Beziehungen ausführen und eine Tabelle zum Durchführen rekursiver Berechnungen durchlaufen können. Wenn Sie mit Excel-Formeln vertraut sind, werden Sie feststellen, dass viele dieser Funktionen ähnlich erscheinen. DAX-Formeln unterscheiden sich jedoch in den folgenden wichtigen Punkten:  
  
-   Eine DAX-Funktion verweist immer auf eine vollständige Spalte oder eine Tabelle. Wenn Sie nur bestimmte Werte aus einer Tabelle oder Spalte verwenden möchten, können Sie der Formel Filter hinzufügen.  
  
-   Zum Anpassen von Berechnungen auf Zeilenbasis stellt DAX Funktionen bereit, mit denen Sie, ähnlich einem Parameter, den aktuellen Zeilenwert oder einen verknüpften Wert angeben können, um Berechnungen durchzuführen, die sich je nach Kontext unterscheiden. Informationen zur Arbeitsweise dieser Funktionen finden Sie unter [Kontext in DAX-Formeln](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md#bkmk_context) weiter unten.  
  
-   DAX beinhaltet viele Funktionen, die keinen Wert, sondern eine Tabelle zurückgeben. In einem Berichtserstellungsclient wird diese Tabelle nicht angezeigt, sondern als Eingabe für andere Funktionen verwendet. Sie können z. B. eine Tabelle abrufen und dann die unterschiedlichen Werte darin zählen oder dynamische Summen von gefilterten Tabellen oder Spalten berechnen.  
  
-   DAX-Funktionen umfassen eine Vielzahl von *Zeitintelligenz* Funktionen. Mit diesen Funktionen können Sie Datumsbereiche definieren oder auswählen und dynamische Berechnungen auf Grundlage dieser Datumsangaben oder Bereiche durchführen. Sie können z. B. Summen über parallele Zeiträume vergleichen.  
  
### <a name="date-and-time-functions"></a>Datums- und Uhrzeitfunktionen  
 Die Datums- und Uhrzeitfunktionen in DAX funktionieren ebenfalls ähnlich wie in Microsoft Excel. DAX-Funktionen basieren jedoch auf den von Microsoft SQL Server verwendeten **datetime** -Datentypen. Weitere Informationen finden Sie unter [Datums- und Uhrzeitfunktionen (DAX)](http://msdn.microsoft.com/en-us/9fc9214a-fcd6-40c0-bf51-0c95637c6ffb).  
  
### <a name="filter-functions"></a>Filterfunktionen  
 Mit den Filterfunktionen in DAX können Sie bestimmte Datentypen abrufen, Werte in verknüpften Tabellen suchen und nach verknüpften Werten filtern. Die Suchfunktionen funktionieren mit Tabellen und Beziehungen wie bei einer Datenbank. Die Filterfunktionen ermöglichen die Anpassung des Datenkontexts zur Erstellung dynamischer Berechnungen. Weitere Informationen finden Sie unter [Filterfunktionen (DAX)](http://msdn.microsoft.com/en-us/b036fd40-4d3b-426d-a0d2-80258b53d8e5).  
  
### <a name="information-functions"></a>Informationsfunktionen  
 Eine Informationsfunktion prüft die als Argument bereitgestellte Zelle oder Zeile und gibt an, ob der Wert mit dem erwarteten Typ übereinstimmt. Die ISTFEHLER-Funktion gibt z. B. TRUE zurück, wenn der Wert, auf den Sie verweisen, fehlerhaft ist. Weitere Informationen finden Sie unter [Informationsfunktionen (DAX)](http://msdn.microsoft.com/en-us/6d2bee09-0456-4444-b4d2-c231fd788a2e).  
  
### <a name="logical-functions"></a>Logische Funktionen  
 Logische Funktionen werden auf Ausdrücke angewendet, um Informationen zu den Werten in diesem Ausdruck zurückzugeben. So können Sie z. B. mit der TRUE-Funktion ermitteln, ob ein auszuwertender Ausdruck einen TRUE-Wert zurückgibt. Weitere Informationen finden Sie unter [Logische Funktionen (DAX)](http://msdn.microsoft.com/en-us/2eb33add-60b2-44ab-b761-012a473116a2).  
  
### <a name="mathematical-and-trigonometric-functions"></a>Mathematische und trigonometrische Funktionen  
 Die mathematischen Funktionen in DAX sind den mathematischen und trigonometrischen Funktionen in Excel sehr ähnlich. Die von den DAX-Funktionen verwendeten numerischen Datentypen weisen einige kleinere Unterschiede auf. Weitere Informationen finden Sie unter [Mathematische und trigonometrische Funktionen (DAX)](http://msdn.microsoft.com/en-us/1f408ec1-e769-43d6-a68c-567bc30d893f).  
 
### <a name="other-functions"></a>Andere Funktionen  
 Diese Funktionen führen eindeutige Aktionen, die nicht zu den meisten anderen Funktionen gehören durch keine der Kategorien definiert werden. Weitere Informationen finden Sie unter [andere Funktionen (DAX)](https://msdn.microsoft.com/mt150101).
  
### <a name="statistical-functions"></a>Statistische Funktionen  
 DAX stellt statistische Funktionen bereit, die Aggregationen ausführen. Zusätzlich zum Erstellen von Summen und Durchschnittswerten oder dem Ermitteln von Mindest- und Höchstwerten können in DAX Spalten vor dem Aggregieren gefiltert und Aggregationen auf Grundlage verknüpfter Tabellen erstellt werden. Weitere Informationen finden Sie unter [Statistische Funktionen (DAX)](http://msdn.microsoft.com/en-us/ba4c1298-57a0-40fc-b6f6-00e187ace559).  
  
### <a name="text-functions"></a>Textfunktionen  
 Die DAX-Textfunktionen sind den entsprechenden Funktionen in Excel sehr ähnlich. Sie können einen Teil einer Zeichenfolge zurückgeben, innerhalb einer Zeichenfolge nach Text suchen oder Zeichenfolgenwerte verketten. DAX stellt auch Funktionen zum Steuern der Formate für Datums- und Uhrzeitangaben sowie Zahlen bereit. Weitere Informationen finden Sie unter [Textfunktionen (DAX)](http://msdn.microsoft.com/en-us/e4821571-ae55-4df7-ae98-c578200bba5f).  
  
### <a name="time-intelligence-functions"></a>Verwendung von zeitintelligenzfunktionen  
 Die Verwendung von zeitintelligenzfunktionen in DAX bereitgestellten können Sie Berechnungen erstellen, die integriertes wissen zu Kalendern und Datumsangaben verwenden. Wenn Sie die Zeit- und Datumsbereiche gemeinsam mit Aggregationen oder Berechnungen verwenden, können Sie über vergleichbare Zeiträume aussagekräftige Vergleiche für Verkäufe, Bestände usw. erstellen. Weitere Informationen finden Sie unter [Zeitintelligenz Funktionen (DAX)](http://msdn.microsoft.com/en-us/91df278d-4b28-40c1-a572-cdb91f081517).  
  
###  <a name="bkmk_TableFunc"></a> Tabellenwertfunktionen  
 Es gibt DAX-Funktionen, die Tabellen ausgeben und/oder Tabellen als Eingabe akzeptieren. Da eine Tabelle eine einzelne Spalte enthalten kann, erfordern Tabellenwertfunktionen auch einzelne Spalten als Eingaben. Es ist wichtig zu wissen, wie diese Tabellenwertfunktionen verwendet werden, um DAX-Formeln vollständig nutzen zu können. DAX enthält die folgenden Typen von Tabellenwertfunktionen:  
  
  **Filterfunktionen** -eine Spalte, Tabelle oder Werte, die im Zusammenhang mit der aktuellen Zeile zurückgegeben.  
    
  **Aggregationsfunktionen** -aggregieren einen Ausdruck für die Zeilen einer Tabelle.  
    
  **Verwendung von zeitintelligenzfunktionen** : eine Tabelle mit Datumsangaben zurück, oder verwenden Sie eine Tabelle mit Datumsangaben, um eine Aggregation zu berechnen.  
  
##  <a name="bkmk_context"></a> Kontext in DAX-Formeln  
 Beim Erstellen von Formeln mit DAX ist der*Kontext* ein wichtiges Konzept. Mithilfe des Kontexts können Sie dynamische Analysen ausführen, da sich die Ergebnisse einer Formel ändern und die aktuelle Zeilen- oder Zellenauswahl sowie alle verknüpften Daten widerspiegeln. Es ist sehr wichtig, dass Sie den Kontext verstehen und anwenden, um leistungsstarke, dynamische Analysen erstellen und Probleme in Formeln beheben zu können.  
  
 Formeln in tabellarischen Modellen können abhängig von anderen Entwurfselementen in einem anderen Kontext ausgewertet werden:  
  
-   Filter, die auf eine PivotTable oder einen Bericht angewendet werden  
  
-   Innerhalb einer Formel definierte Filter  
  
-   Mit besonderen Funktionen innerhalb einer Formel angegebene Beziehungen  
  
 Es gibt verschiedene Typen von Kontext: *Zeilenkontext*, *Abfragekontext*und *Filterkontext*.  
  
###  <a name="bkmk_row_context"></a> Zeilenkontext  
 Der*Zeilenkontext* kann als „die aktuelle Zeile“ betrachtet werden. Wenn Sie in einer berechneten Spalte eine Formel erstellen, enthält der Zeilenkontext für diese Formel die Werte aller Spalten in der aktuellen Zeile. Wenn die Tabelle mit einer anderen Tabelle verknüpft ist, enthält der Kontext auch alle Werte aus der anderen Tabelle, die mit der aktuellen Zeile verknüpft sind.  
  
 Angenommen, Sie erstellen die berechnete Spalte `=[Freight] + [Tax]`, die Werte aus zwei Spalten (Fracht und Steuer) aus derselben Tabelle addiert. Diese Formel ruft automatisch nur die Werte der aktuellen Zeile in der angegebenen Spalte ab.  
  
 Der Zeilenkontext folgt auch allen Beziehungen, die zwischen Tabellen definiert wurden, einschließlich der innerhalb einer berechneten Spalte mit DAX-Formeln definierten Beziehungen, um zu ermitteln, welche Zeilen in verknüpften Tabellen der aktuellen Zeile zugeordnet sind.  
  
 In der folgenden Formel wird z. B. mit der RELATED-Funktion auf Grundlage des Lands, in das die Bestellung ausgeliefert wurde, ein Steuerwert aus einer verknüpften Tabelle abgerufen. Der Steuerwert wird mit dem Wert für Region in der aktuellen Tabelle ermittelt. Die Region wird in der verknüpften Tabelle nachgeschlagen, und anschließend wird der Steuersatz für diese Region aus der verknüpften Tabelle abgerufen.  
  
```  
= [Freight] + RELATED('Region'[TaxRate])  
```  
  
 Diese Formel ruft den Steuersatz für den aktuellen Bereich von der Tabelle Region ab und fügt es dem Wert der Spalte Fracht hinzu. In DAX-Formeln müssen Sie die bestimmte Beziehung zum Verknüpfen der Tabellen nicht kennen oder angeben.  
  
#### <a name="multiple-row-context"></a>Mehrere Zeilenkontexte  
 DAX umfasst Funktionen, die eine Tabelle durchlaufen, um Berechnungen durchzuführen. Diese Funktionen können über mehrere aktuelle Zeilen mit jeweils einem eigenen Zeilenkontext verfügen.  In Wesentlichen können Sie mit diesen Funktionen Formeln erstellen, die Vorgänge rekursiv über eine innere und eine äußere Schleife ausführen.  
  
 Angenommen, das Modell enthält eine **Products** -Tabelle und eine **Sales** -Tabelle. Sie können z. B. die gesamte Sales-Tabelle durchlaufen, die mit Transaktionen verschiedener Produkte gefüllt ist, um die größte Bestellmenge für jedes Produkt in einer beliebigen Transaktion zu ermitteln.  
  
 Mit DAX können Sie eine einzelne Formel erstellen, die den richtigen Wert zurückgibt, und die Ergebnisse werden automatisch bei jedem Hinzufügen von Daten zu den Tabellen aktualisiert.  
  
```  
=MAXX(FILTER(Sales,[ProdKey]=EARLIER([ProdKey])),Sales[OrderQty])  
```  
  
 Eine ausführliche exemplarische Vorgehensweise zu dieser Formel finden Sie unter [EARLIER-Funktion (DAX)](http://msdn.microsoft.com/en-us/6d126c4d-2315-49ec-899d-cb396eefbae6).  
  
 Zusammengefasst speichert die EARLIER-Funktion den Zeilenkontext des Vorgangs, der dem aktuellen Vorgang vorausging. Die Funktion speichert zu jedem Zeitpunkt zwei Kontextsätze im Arbeitsspeicher: Ein Kontextsatz stellt die aktuelle Zeile für die innere Schleife der Formel dar, und ein weiterer Kontextsatz stellt die aktuelle Zeile für die äußere Schleife der Formel dar. DAX übermittelt automatisch Werte zwischen den zwei Schleifen, sodass komplexe Aggregate erstellt werden können.  
  
####  <a name="bkmk_query_context"></a> Abfragekontext  
 Der*Abfragekontext* ist die Teilmenge von Daten, die implizit für eine Formel abgerufen wird. Wenn ein Benutzer ein Measure oder ein anderes Wertfeld in einer PivotTable oder einem Bericht platziert, die bzw. der auf einem tabellarischen Modell basiert, untersucht das Modul die Zeilen- und Spaltenüberschriften, die Slicer und die Berichtsfilter, um den Kontext zu ermitteln. Anschließend werden die erforderlichen Abfragen für die Datenquelle ausgeführt, um die richtige Teilmenge der Daten abzurufen, die von der Formel definierten Berechnungen auszuführen und dann jede Zelle in der PivotTable oder dem Bericht aufzufüllen. Der Datensatz, der abgerufen wird, ist der Abfragekontext für jede Zelle.  
  
> [!WARNING]  
>  In einem Modell, das den DirectQuery-Modus verwendet, wird der Kontext ausgewertet, und anschließend werden die Set-Vorgänge, mit denen die richtige Teilmenge der Daten abgerufen und die Ergebnisse berechnet werden, in SQL-Anweisungen übersetzt. Diese Anweisungen werden dann direkt auf dem relationalen Datenspeicher ausgeführt. Daher ändert sich der Kontext selbst nicht, obwohl die Methode zum Abrufen der Daten und Berechnen der Ergebnisse anders ist.  
  
 Da sich der Kontext abhängig davon ändert, wo Sie die Formel platzieren, können sich auch die Ergebnisse der Formel ändern.  
  
 Angenommen, Sie erstellen eine Formel, die die Werte in der Spalte **Profit** der **Sales** -Tabelle addiert: `=SUM('Sales'[Profit])`.  Wenn Sie diese Formel in einer berechneten Spalte innerhalb der **Sales** -Tabelle verwenden, sind die Ergebnisse der Formel für die gesamte Tabelle identisch, da der Abfragekontext für die Formel immer dem gesamten Dataset der **Sales** -Tabelle entspricht. Die Ergebnisse enthalten somit den Gewinn für alle Regionen, alle Produkte, alle Jahre usw.  
  
 In der Regel möchten Benutzer jedoch nicht Hunderte Male das gleiche Ergebnis anzeigen, sondern den Gewinn für ein bestimmtes Jahr, ein bestimmtes Land, ein bestimmtes Produkt oder eine Kombination daraus abrufen, um das Gesamtergebnis zu ermitteln.  
  
 In einer PivotTable kann der Kontext durch Hinzufügen oder Entfernen von Spalten- und Zeilenüberschriften oder Slicern geändert werden. Jedes Mal, wenn Benutzer der PivotTable Spalten- oder Zeilenüberschriften hinzufügen, wird der Abfragekontext geändert, in dem das Measure ausgewertet wird. Slice- und Filterungsvorgänge beeinflussen ebenfalls den Kontext. Daher wird dieselbe Formel, wenn sie in einem Measure verwendet wird, für jede Zelle in einem anderen *Abfragekontext* ausgewertet.  
  
####  <a name="bkmk_filter_context"></a> Filterkontext  
 Der*Filterkontext* ist der Satz von Werten, die in jeder Spalte oder in den aus einer verknüpften Tabelle abgerufenen Werten zulässig sind. Filter können im Designer oder in der Darstellungsschicht (Berichte und PivotTables) auf eine Spalte angewendet werden. Filter können auch explizit durch Filterausdrücke innerhalb der Formel definiert werden.  
  
 Der Filterkontext wird hinzugefügt, wenn Sie Filtereinschränkungen für den in einer Spalte oder einer Tabelle zulässigen Satz von Werten angeben, indem Sie in einer Formel Argumente verwenden. Der Filterkontext wird zusätzlich zu anderen Kontexten wie dem Zeilenkontext oder Abfragekontext angewendet.  
  
 In tabellarischen Modellen gibt es verschiedene Möglichkeiten, einen Filterkontext zu erstellen. Innerhalb des Kontexts von Clients, die das Modell verwenden, z. B. Power BI-Berichten können Benutzer Filter bei Bedarf erstellen, indem Sie Slicer oder Berichtsfilter für Zeilen- und Spaltenüberschriften hinzufügen. Sie können Filterausdrücke auch direkt in der Formel verwenden, um verknüpfte Werte anzugeben, Tabellen zu filtern, die als Eingaben verwendet werden, oder dynamisch den Kontext für Werte abzurufen, die in Berechnungen verwendet werden. Darüber hinaus können Sie die Filter für einzelne Spalten vollständig oder selektiv löschen. Beim Erstellen von Formeln, die Gesamtergebnisse berechnen, ist dies sehr nützlich.  
  
 Weitere Informationen zum Erstellen von Filtern in Formeln finden Sie unter [FILTER-Funktion (DAX)](http://msdn.microsoft.com/en-us/f1f6bee4-547b-407c-b70b-9216b2f3d3fd).  
  
 Ein Beispiel dazu, wie Filter gelöscht werden können, um Gesamtergebnisse zu erzeugen, finden Sie unter [ALL-Funktion (DAX)](http://msdn.microsoft.com/en-us/a7e0ab71-d83e-4463-bc77-9eb5dd73c6fc).  
  
 Beispiele zum selektiven Löschen und Anwenden von Filtern innerhalb von Formeln finden Sie unter [ALLEXCEPT-Funktion (DAX)](http://msdn.microsoft.com/en-us/a6f575a1-9803-4bb2-85b3-c95c060f1fb1).  
  
####  <a name="bkmk_determine_context"></a> Bestimmen des Kontexts in Formeln  
 Wenn Sie eine DAX-Formel erstellen, wird die Formel zuerst auf gültige Syntax getestet, und dann wird überprüft, ob die Namen der Spalten und Tabellen innerhalb der Formel im aktuellen Kontext vorhanden sind. Wenn eine Spalte oder Tabelle innerhalb der Formel nicht gefunden wird, wird ein Fehler zurückgegeben.  
  
 Wie in den vorangehenden Abschnitten beschrieben, wird der Kontext während der Validierung (und während Neuberechnungen) anhand der verfügbaren Tabellen im Modell, anhand der Beziehungen zwischen den Tabellen und anhand der angewendeten Filter bestimmt.  
  
 Wenn Sie z.B. gerade einige Daten in eine neue Tabelle importiert haben, die mit keiner anderen Tabelle verknüpft ist (und Sie keine Filter angewendet haben), ist der *aktuelle Kontext* der gesamte Satz von Spalten in der Tabelle. Wenn die Tabelle über Beziehungen mit anderen Tabellen verknüpft ist, beinhaltet der aktuelle Kontext auch die verknüpften Tabellen. Wenn Sie eine Spalte aus der Tabelle einem Bericht hinzufügen, der Slicer und ggf. auch Berichtsfilter verwendet, ist der Kontext für die Formel die Teilmenge der Daten in jeder Zelle des Berichts.  
  
 Der Kontext ist ein leistungsstarkes Konzept, das die Fehlerbehebung in Formeln allerdings auch erschweren kann. Sie sollten daher mit einfachen Formeln und Beziehungen beginnen, um die Funktionsweise des Kontexts zu verstehen. Der folgende Abschnitt enthält einige Beispiele für Formeln, in denen verschiedene Kontexttypen zur dynamischen Rückgabe von Ergebnissen verwendet werden.  
  
##### <a name="examples-of-context-in-formulas"></a>Beispiele für Kontext in Formeln  
  
1.  Die [RELATED-Funktion (DAX)](http://msdn.microsoft.com/en-us/0023fd13-c17a-4243-ab77-3779a4b502b6) erweitert den Kontext der aktuellen Zeile, sodass Werte mit in eine verknüpfte Spalte aufgenommen werden. Auf diese Weise können Sie Suchvorgänge ausführen. Das Beispiel in diesem Thema veranschaulicht die Interaktion des Filter- und Zeilenkontexts.  
  
2.  Mit der [FILTER-Funktion (DAX)](http://msdn.microsoft.com/en-us/f1f6bee4-547b-407c-b70b-9216b2f3d3fd) können Sie die Zeilen angeben, die in den aktuellen Kontext aufgenommen werden sollen. Zudem wird anhand der Beispiele in diesem Thema veranschaulicht, wie Filter in andere Funktionen, die Aggregate ausführen, eingebettet werden.  
  
3.  Die [ALL-Funktion (DAX)](http://msdn.microsoft.com/en-us/a7e0ab71-d83e-4463-bc77-9eb5dd73c6fc) legt den Kontext in einer Formel fest. Sie können Filter, die als Ergebnis des Abfragekontexts angewendet werden, mithilfe der ALL-Funktion überschreiben.  
  
4.  Mit der [ALLEXCEPT-Funktion (DAX)](http://msdn.microsoft.com/en-us/a6f575a1-9803-4bb2-85b3-c95c060f1fb1) können Sie alle Filter bis auf den angegebenen entfernen. Beide Themen enthalten Beispiele, die Sie durch das Erstellen von Formeln führen, um komplexe Kontexte besser verstehen zu können.  
  
5.  Mit der [EARLIER-Funktion (DAX)](http://msdn.microsoft.com/en-us/6d126c4d-2315-49ec-899d-cb396eefbae6) und der [EARLIEST-Funktion (DAX)](http://msdn.microsoft.com/en-us/9befa04d-78db-492e-a463-80b8b77206d6) können Sie Tabellen durchlaufen, indem Berechnungen durchgeführt werden, während von einer inneren Schleife auf einen Wert verwiesen wird. Wenn Sie mit dem Konzept der Rekursion und inneren und äußeren Schleifen vertraut sind, werden Sie die Leistungsfähigkeit zu schätzen wissen, die die Funktionen EARLIER und EARLIEST bereitstellen. Wenn Sie mit diesen Konzepten nicht vertraut sind, sollten Sie die Schritte in dem Beispiel sorgfältig durchführen, um den inneren und äußeren Kontext beim Durchführen von Berechnungen zu verstehen.  
  
##  <a name="bkmk_RelModel"></a> Formeln und das tabellarische Modell  
 Die Modell-Designer in SSDT ist ein Bereich, in dem Sie mit mehreren Datentabellen arbeiten und die Tabellen in einem tabellarischen Modell verbinden können. Innerhalb dieses Modells werden Tabellen über Beziehungen zwischen Spalten mit gemeinsamen Werten (Schlüsseln) verknüpft. Im tabellarischen Modell können Sie Werte mit Spalten in anderen Tabellen verknüpfen und weitere interessante Berechnungen erstellen. Ebenso wie in einer relationalen Datenbank können Sie mehrere Ebenen verknüpfter Tabellen miteinander verbinden und Spalten aus allen Tabellen in den Ergebnissen verwenden.  
  
 Sie können z. B. eine Verkaufstabelle, eine Produkttabelle und eine Tabelle mit Produktkategorien verknüpfen und verschiedene Kombinationen der Spalten in PivotTables und Berichten verwenden. Verwandte Felder können verwendet werden, um verbundene Tabellen zu filtern oder Berechnungen über Teilmengen zu erstellen. (Wenn Sie nicht mit der relationalen Datenbank und Arbeiten mit Tabellen und Joins vertraut sind, finden Sie unter [Beziehungen](../../analysis-services/tabular-models/relationships-ssas-tabular.md).)  
  
 Tabellarische Modelle unterstützen mehrere Beziehungen zwischen Tabellen. Um Verwirrungen oder falsche Ergebnisse zu vermeiden, wird jeweils nur eine Beziehung als aktive Beziehung festgelegt, Sie können jedoch die aktive Beziehung nach Bedarf erstellen und ändern, um in Berechnungen unterschiedliche Verbindungen der Daten zu durchlaufen. Mithilfe der [USERELATIONSHIP-Funktion (DAX)](http://msdn.microsoft.com/en-us/200484ab-9da1-4570-a100-7f9ed20d33af) kann mindestens eine Beziehung angegeben werden, die in einer bestimmten Berechnung verwendet werden soll.  
  
 In einem tabellarischen Modell sollten die folgenden Regeln für den Formelentwurf beachten werden:  
  
-   Wenn Tabellen durch eine Beziehung verbunden sind, muss sichergestellt werden, dass die beiden als Schlüssel verwendeten Spalten übereinstimmende Werte enthalten. Die referenzielle Integrität wird jedoch nicht erzwungen, daher kann auch bei nicht übereinstimmenden Werten in einer Schlüsselspalte eine Beziehung erstellt werden. In so einem Fall müssen Sie beachten, dass leere oder nicht übereinstimmende Werte die Ergebnisse von Formeln beeinflussen können.  
  
-   Wenn Sie Tabellen im Modell mithilfe von Beziehungen verknüpfen, vergrößern Sie den Bereich oder *Kontext*, in dem die Formeln ausgewertet werden. Änderungen im Kontext, die sich aus der Hinzufügung neuer Tabellen, neuen Beziehungen oder aus Änderungen in der aktiven Beziehung ergeben, können zu unerwarteten Änderungen in den Ergebnissen führen. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Kontext in DAX-Formeln](#bkmk_context) .  
  
##  <a name="bkmk_tables"></a> Arbeiten mit Tabellen und Spalten  
 Tabellen in tabellarischen Modellen sind rein äußerlich mit Excel-Tabellen vergleichbar, allerdings werden Daten und Formeln von ihnen anders verarbeitet:  
  
-   Formeln funktionieren nur für Tabellen und Spalten, nicht für einzelne Zellen, Bereichsverweise oder Arrays.  
  
-   Formeln können Beziehungen verwenden, um Werte aus verknüpften Tabellen abzurufen. Die Werte, die abgerufen werden, beziehen sich immer auf den aktuellen Zeilenwert.  
  
-   Sie können keine unregelmäßigen Daten verwenden, so wie dies in einem Excel-Arbeitsblatt möglich ist. Jede Zeile in einer Tabelle muss die gleiche Anzahl von Spalten enthalten. In einigen Spalten können jedoch leere Werte stehen. Excel-Datentabellen und Datentabellen aus tabellarischen Modellen sind nicht austauschbar.  
  
-   Da der Datentyp für jede Spalte festgelegt ist, muss jeder Wert in dieser Spalte vom gleichen Typ sein,  
  
### <a name="referring-to-tables-and-columns-in-formulas"></a>Verweisen auf Tabellen und Spalten in Formeln  
 Sie können auf alle Tabellen und Spalten anhand des Namens verweisen. Die folgende Formel veranschaulicht z.B., wie Sie auf die Spalten aus zwei Tabellen verweisen, indem Sie den *vollqualifizierten* Namen verwenden:  
  
```  
=SUM('New Sales'[Amount]) + SUM('Past Sales'[Amount])  
```  
  
 Wenn eine Formel ausgewertet wird, überprüft der Modell-Designer zuerst die allgemeine Syntax und vergleicht dann die von Ihnen bereitgestellten Namen der Spalten und Tabellen mit möglichen Spalten und Tabellen im aktuellen Kontext. Wenn der Name mehrdeutig ist oder die Spalte oder die Tabelle nicht gefunden werden kann, wird für die Formel (statt eines Datenwerts wird in Zellen, in denen der Fehler auftritt, eine #ERROR-Zeichenfolge angezeigt) ein Fehler ausgegeben. Weitere Informationen zu den Benennungsanforderungen für Tabellen, Spalten und andere Objekte finden Sie unter „Benennungsanforderungen“ in [DAX-Syntaxspezifikation](http://msdn.microsoft.com/en-us/098630f4-7d1d-467e-976c-99b2279430d5).  
  
### <a name="table-relationships"></a>Tabellenbeziehungen  
 Das Erstellen von Beziehungen zwischen Tabellen bietet die Möglichkeit, in einer anderen Tabelle nach Daten zu suchen und verknüpfte Werte zu verwenden, um komplexe Berechnungen vorzunehmen. Sie können z. B. eine berechnete Spalte verwenden, um alle Versanddatensätze für den aktuellen Wiederverkäufer nachzuschlagen und anschließend die jeweiligen Versandkosten zu addieren. In vielen Fällen ist eine Beziehung u. U. nicht notwendig. Sie können die LOOKUPVALUE-Funktion in einer Formel verwenden, um den Wert in *result_columnName* für die Zeile zurückzugeben, die die im *search_column* -Parameter und im *search_value* -Parameter angegebenen Kriterien erfüllt.  
  
 Viele DAX-Funktionen erfordern, dass zwischen zwei Tabellen oder unter mehreren Tabellen eine Beziehung besteht, um die referenzierten Spalten zu finden und sinnvolle Ergebnisse zurückzugeben. Andere Funktionen versuchen, die Beziehung zu ermitteln. Um jedoch die besten Ergebnisse zu erzielen, sollten Sie nach Möglichkeit immer eine Beziehung erstellen. Weitere Informationen finden Sie unter [Formeln und das tabellarische Modell](#bkmk_RelModel) weiter oben in diesem Thema.  
  
##  <a name="bkmk_RefreshRecalc"></a> Aktualisieren der Ergebnisse von Formeln (Prozess)  
 *Datenverarbeitung* und *Neuberechnung* sind zwei separate, aber verwandte Vorgänge. Diese Konzepte sollten Ihnen sehr geläufig sein, wenn Sie ein Modell mit komplexen Formeln, großen Datenmengen oder aus externen Datenquellen abgerufenen Daten entwerfen.  
  
 *Datenverarbeitung* ist der Vorgang, bei dem die Daten in einem Modell mit neuen Daten aus einer externen Datenquelle aktualisiert werden.  
  
 *Neuberechnung* ist der Vorgang, bei dem die Ergebnisse von Formeln aktualisiert werden, um Änderungen an den Formeln sowie an den zugrunde liegenden Daten widerzuspiegeln. Neuberechnung kann die Leistung in folgender Weise beeinträchtigen:  
  
-   Die Werte in einer berechneten Spalte werden berechnet und im Modell gespeichert. Um die Werte in der berechneten Spalte zu aktualisieren, müssen Sie das Modell mit einem von drei Verarbeitungsbefehlen verarbeiten: Vollständig verarbeiten, Daten verarbeiten oder Prozessneuberechnung. Das Ergebnis der Formel muss immer für die ganze Spalte neu berechnet werden, wenn Sie die Formel ändern.  
  
-   Die von Measures berechneten Werte werden dynamisch ausgewertet, sobald ein Benutzer einer PivotTable das Measure hinzufügt oder einen Bericht öffnet. Wenn der Benutzer den Kontext ändert, ändern sich die von dem Measure zurückgegebenen Werte. Die Ergebnisse des Measures spiegeln immer den aktuellen Stand des speicherinternen Caches wider.  
  
 Die Verarbeitung und die Neuberechnung haben nur dann Auswirkungen auf Zeilenfilterformeln, wenn das Ergebnis einer Neuberechnung einen anderen Wert zurückgibt, durch den die Zeile für Rollenmitglieder abfragbar oder nicht abfragbar wird.  
  
 Weitere Informationen finden Sie unter [Verarbeiten von Daten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/process-data-ssas-tabular.md).  
  
##  <a name="bkmk_troubleshoot"></a> Beheben von Fehlern in Formeln  
 Wenn Sie beim Definieren einer Formel einen Fehler erhalten, enthält die Formel eventuell entweder einen *Syntaxfehler*, einen *Semantikfehler*oder einen *Berechnungsfehler*.  
  
 Syntaxfehler sind am einfachsten zu beheben. Meist geht es um eine fehlende Klammer oder ein fehlendes Komma. Hilfe zur Syntax der einzelnen Funktionen finden Sie in der [DAX-Funktionsreferenz](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
 Der andere Fehlertyp tritt auf, wenn die Syntax keinen Fehler aufweist, aber der Wert oder die Spalte, auf den bzw. die verwiesen wird, im Kontext der Formel keinen Sinn ergibt. Semantik- und Berechnungsfehler dieser Art können die folgenden Ursachen haben:  
  
-   Die Formel verweist auf eine nicht vorhandene Spalte, Tabelle oder Funktion.  
  
-   Die Formel scheint korrekt zu sein, aber wenn das Datenmodul die Daten abruft, wird ein Typenkonflikt erkannt und ein Fehler ausgelöst.  
  
-   Die Formel übergibt eine falsche Zahl oder einen falschen Typ von Parametern an eine Funktion.  
  
-   Die Formel verweist auf eine andere Spalte mit einem Fehler, weshalb die Werte ungültig sind.  
  
-   Die Formel verweist auf eine Spalte, die nicht verarbeitet wurde, d. h., es sind Metadaten vorhanden, aber keine tatsächlichen Daten, die für Berechnungen verwendet werden könnten.  
  
 In den ersten vier Fällen kennzeichnet DAX die gesamte Spalte mit der ungültigen Formel. Im letzten Fall blendet DAX die Spalte ab, um anzugeben, dass sich die Spalte in einem nicht verarbeiteten Zustand befindet.  
  
##  <a name="bkmk_addional_resources"></a> Zusätzliche Ressourcen  
 [Tabellenmodellierung &#40;Adventure Works-Tutorial&#41;](../../analysis-services/tabular-modeling-adventure-works-tutorial.md) stellt Schritt-für-Schritt-Anleitungen zum Erstellen eines tabellarischen Modells bereit, das viele Berechnungen in berechneten Spalten, Measures und Zeilenfiltern enthält. Für die meisten Formeln ist eine Beschreibung ihrer Funktion verfügbar.  
  
 Die [Analysis Services-Teamblog](http://go.microsoft.com/fwlink/?LinkID=220949&clcid=0x409) bietet die neuesten Informationen, Tipps, News und Ankündigungen. 
  
 Im [DAX-Ressourcencenter](http://go.microsoft.com/fwlink/?LinkID=220966&clcid=0x409) finden Sie sowohl interne als auch externe Informationen zu DAX, z.B. zahlreiche DAX-Lösungen von führenden Business Intelligence-Experten.  
  
## <a name="see-also"></a>Siehe auch  
 [DAX-Referenz (Data Analysis Expressions)](http://msdn.microsoft.com/en-us/70a82136-0926-4a91-bcb3-e18e82593b0d)   
 [Measures](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Berechnete Spalten](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Rollen](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [KPIs](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Unterstützte Datenquellen](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
