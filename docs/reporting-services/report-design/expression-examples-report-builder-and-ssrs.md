---
title: "Beispiele f&#252;r Ausdr&#252;cke (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "09/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Seitenumbrüche [Reporting Services], Ausdrücke"
  - "Berichte mit grün-weißem Zebrastreifeneffekt [Reporting Services]"
  - "Visual Basic [Reporting Services]"
  - "Funktionen [Reporting Services], Beispiele"
  - "Benutzerdefinierter Code [Reporting Services]"
  - "Darstellung von Berichten"
  - "Formatieren von Berichten [Reporting Services], Ausdrücke"
  - "Ein-/Ausblenden [Reporting Services]"
  - "Parameter [Reporting Services], Ausdrücke"
  - "Sichtbarkeit [Reporting Services], Ausdrücke"
  - "Seitenkopfzeilen [Reporting Services]"
  - "Seitenfußzeilen [Reporting Services]"
  - "Datumsangaben [Reporting Services], Ausdrücke"
  - "Ausdrücke [Reporting Services], Beispiele"
ms.assetid: 87ddb651-a1d0-4a42-8ea9-04dea3f6afa4
caps.latest.revision: 101
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 101
---
# Beispiele f&#252;r Ausdr&#252;cke (Berichts-Generator und SSRS)
Ausdrücke werden in paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichten häufig zum Steuern des Inhalts und der Darstellung des Berichts verwendet. Ausdrücke werden in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] geschrieben und können integrierte Funktionen, benutzerdefinierten Code, Berichts- und Gruppenvariablen sowie benutzerdefinierte Variablen verwenden. Ausdrücke beginnen immer mit einem Gleichheitszeichen (=). Weitere Informationen zum Ausdrucks-Editor und den Verweistypen, die Sie einfügen können, finden Sie unter [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md) und [Hinzufügen eines Ausdrucks &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md).  
  
> [!IMPORTANT]  
>  Bei aktiviertem RDL-Sandkasten können nur bestimmte Typen und Elemente zum Veröffentlichungszeitpunkt des Berichts im Ausdruckstext verwendet werden. Weitere Informationen finden Sie unter [Enable and Disable RDL Sandboxing](../../reporting-services/report-server-sharepoint/enable-and-disable-rdl-sandboxing.md).  
  
 In diesem Thema sind Beispiele für Ausdrücke enthalten, die in einem Bericht für allgemeine Aufgaben verwendet werden können.  
  
-   [Visual Basic-Funktionen](#VisualBasicFunctions) : Beispiele für Datum, Zeichenfolge, Konvertierung und bedingte [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Funktionen.  
  
-   [Berichtsfunktionen:](#ReportFunctions) Beispiele für Aggregate und andere integrierte Berichtsfunktionen  
  
-   [Darstellung von Berichtsdaten](#AppearanceofReportData) : Beispiele zur Änderung der Darstellung eines Berichts.  
  
-   [Eigenschaften](#Properties) Beispiele zum Festlegen von Berichtselementeigenschaften, um Format oder Sichtbarkeit zu steuern.  
  
-   [Parameter](#Parameters) : Beispiele für die Verwendung von Parametern in einem Ausdruck.  
  
-   [Benutzerdefinierter Code](#CustomCode) : Beispiele für eingebetteten benutzerdefinierten Code.  
  
 Beispiele für Ausdrücke und die jeweiligen Verwendungsmöglichkeiten finden Sie in den folgenden Themen:  
  
-   [Beispiele für Gruppierungsausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
-   [Beispiele für Filtergleichungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [Häufig verwendete Filter &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)  
  
-   [Verweise auf Berichts- und Gruppenvariablensammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-and-group-variables-collections-references-report-builder-and-ssrs.md)  
  
 Weitere Informationen zu einfachen und komplexen Ausdrücken, zu den Verwendungsmöglichkeiten von Ausdrücken sowie zu den Verweistypen, die Sie in einen Ausdruck einbinden können, finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md). Weitere Informationen zum Kontext, in dem Ausdrücke zum Berechnen von Aggregaten ausgewertet werden, finden Sie unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
 Um das Schreiben von Ausdrücken zu erlernen, die viele der Funktionen und Operatoren verwenden, die auch in den beispielhaften Ausdrücken in diesem Thema zum Schreiben von Berichten verwendet werden, finden Sie weitere Informationen unter [Tutorial: Introducing Expressions](../../reporting-services/tutorial-introducing-expressions.md).  
  
 Wenn Sie mit dem Berichtsmodellabfrage-Designer eine Datasetabfrage entwerfen, in der ein Berichtsmodell als Datenquelle verwendet wird, verwenden Sie anstelle von Ausdrücken Formeln. Mithilfe dieser Formeln können die Berichtsdaten anhand benutzerdefinierter Berechnungen angegeben werden, die in die Abfrage für die aus der Berichtsmodelldatenquelle zurückzugebenden Daten integriert werden. Weitere Informationen finden Sie unter [Formeln in Berichtsmodellabfragen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formulas-in-report-model-queries-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Funktionen  
 Viele Ausdrücke in einem Bericht enthalten Funktionen. Mit diesen Funktionen können Sie Daten formatieren, Code anwenden und auf Berichtsmetadaten zugreifen. Sie können Ausdrücke schreiben, die Funktionen aus der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Laufzeitbibliothek sowie aus den Namespaces<xref:System.Convert> und <xref:System.Math> verwenden. Sie können Verweise auf Funktionen aus anderen Assemblys oder benutzerdefinierten Code hinzufügen. Sie können auch Klassen aus [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] verwenden, einschließlich <xref:System.Text.RegularExpressions>.  
  
###  <a name="VisualBasicFunctions"></a> Visual Basic-Funktionen  
 Mit [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Funktionen können Sie die Daten bearbeiten, die in Textfeldern angezeigt oder für Parameter, Eigenschaften oder sonstige Bereiche des Berichts verwendet werden. In diesem Abschnitt werden Beispiele zur Veranschaulichung einiger dieser Funktionen bereitgestellt. Weitere Informationen finden Sie unter [Member der Visual Basic-Laufzeitbibliothek](http://go.microsoft.com/fwlink/?LinkId=198941) bei MSDN.  
  
 Der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] bietet zahlreiche benutzerdefinierte Formatoptionen, z. B. für bestimmte Datumsformate. Weitere Informationen finden Sie unter [Formatierung von Typen](http://go.microsoft.com/fwlink/?LinkId=112024) auf MSDN.  
  
#### Mathematische Funktionen  
  
-   Die **Round** -Funktion ermöglicht das Runden von Zahlen auf die nächste ganze Zahl. Mit dem folgenden Ausdruck wird der Wert 1,3 auf 1 abgerundet:  
  
    ```  
    = Round(1.3)  
    ```  
  
     Sie können auch einen Ausdruck schreiben, um einen Wert auf ein von Ihnen angegebenes Vielfaches zu runden (vergleichbar mit der **MRound** -Funktion in Excel). Multiplizieren Sie den Wert mit einem Faktor, der eine ganze Zahl erzeugt, runden Sie die Zahl, und dividieren Sie dann durch den gleichen Faktor. Verwenden Sie z. B. den folgenden Ausdruck, um 1,3 auf das nächste Vielfache von 0,2 (1,4) zu runden:  
  
    ```  
    = Round(1.3*5)/5  
    ```  
  
####  <a name="DateFunctions"></a> Datumsfunktionen  
  
-   Die **Today** -Funktion stellt das aktuelle Datum bereit. Mit diesem Ausdruck können Sie in einem Textfeld das Datum im Bericht anzeigen oder aber in einem Parameter Daten basierend auf dem aktuellen Datum filtern.  
  
    ```  
    =Today()  
    ```  
  
-   Mit der **DateAdd** -Funktion wird ein Datumsbereich basierend auf einem einzigen Parameter bereitgestellt. Der folgende Ausdruck liefert das Datum des Tages, der sechs Monate nach dem Datum des *StartDate*-Parameters liegt.  
  
    ```  
    =DateAdd(DateInterval.Month, 6, Parameters!StartDate.Value)  
    ```  
  
-   Die **Year** -Funktion zeigt das Jahr für ein bestimmtes Datum an. Hiermit können Sie Datumsangaben zusammenfassen oder die Jahreszahl für eine Datumsgruppe anzeigen. Dieser Ausdruck liefert das Jahr für eine bestimmte Gruppe von Bestelldaten. Mit der **Month** -Funktion und anderen Funktionen können Datumsangaben auch bearbeitet werden. Weitere Informationen finden Sie in der Dokumentation zu [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .  
  
    ```  
    =Year(Fields!OrderDate.Value)  
    ```  
  
-   Sie können Funktionen in einem Ausdruck kombinieren, um das Format anzupassen. Durch den folgenden Ausdruck wird das Format Monat-Tag-Jahr eines Datums in das Format Monat-Woche-Woche geändert. 12/23/2009 wird z. B. in Dezember Woche 3 geändert:  
  
    ```  
    =Format(Fields!MyDate.Value, "MMMM") & " Week " &   
    (Int(DateDiff("d", DateSerial(Year(Fields!MyDate.Value),   
    Month(Fields!MyDate.Value),1), Fields!FullDateAlternateKey.Value)/7)+1).ToString  
    ```  
  
     Bei Verwendung als berechnetes Feld in einem Dataset können Sie diesen Ausdruck für ein Diagramm verwenden, um Werte nach der Woche in jedem Monat zu aggregieren.  
  
-   Der folgende Ausdruck legt für den SellStartDate-Wert das Format MMM-YY fest. Beim SellStartDate-Feld handelt es sich um einen datetime-Datentyp.  
  
    ```  
    =FORMAT(Fields!SellStartDate.Value, "MMM-yy")  
    ```  
  
-   Der folgende Ausdruck legt für den SellStartDate-Wert das Format dd/MM/yyyy fest. Beim SellStartDate-Feld handelt es sich um einen datetime-Datentyp.  
  
    ```  
    =FORMAT(Fields!SellStartDate.Value, "dd/MM/yyyy")  
    ```  
  
-   Die **CDate** -Funktion konvertiert den Wert in ein Datum. Die **Now** -Funktion gibt einen Datumswert zurück, der das aktuelle Datum und die aktuelle Uhrzeit des Systems enthält. **DateDiff** gibt einen Long-Wert zurück, der die Zahl der Zeitintervalle zwischen zwei Datumswerten angibt.  
  
     Im folgenden Beispiel wird das Anfangsdatum des aktuellen Jahres angezeigt.  
  
    ```  
    =DateAdd(DateInterval.Year,DateDiff(DateInterval.Year,CDate("01/01/1900"),Now()),CDate("01/01/1900"))  
    ```  
  
-   Im folgenden Beispiel wird das Anfangsdatum des vorherigen Monats basierend auf dem aktuellen Monat angezeigt.  
  
    ```  
    =DateAdd(DateInterval.Month,DateDiff(DateInterval.Month,CDate("01/01/1900"),Now())-1,CDate("01/01/1900"))  
    ```  
  
-   Der folgende Ausdruck generiert die Jahre des Intervalls zwischen SellStartDate und LastReceiptDate. Diese Felder sind in zwei unterschiedlichen Datasets enthalten, DataSet1 und DataSet2. Die Aggregatfunktion [First &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/first-function-report-builder-and-ssrs.md) gibt den ersten Wert von SellStartDate in DataSet1 und den ersten Wert von LastReceiptDate in DataSet2 zurück.  
  
    ```  
    =DATEDIFF(“yyyy”, First(Fields!SellStartDate.Value, "DataSet1"), First(Fields!LastReceiptDate.Value, "DataSet2"))  
    ```  
  
-   Die Funktion **DatePart** gibt einen ganzzahligen Wert zurück, der die angegebene Komponente eines bestimmten Date-Werts enthält. Der folgende Ausdruck gibt das Jahr für den ersten Wert von SellStartDate in DataSet1 zurück. Der Datasetbereich ist angegeben, weil mehrere Datasets im Bericht enthalten sind.  
  
    ```  
    =Datepart("yyyy", First(Fields!SellStartDate.Value, "DataSet1"))  
  
    ```  
  
-   Die Funktion **DateSerial** gibt ein Date-Wert zurück, der das angegebene Jahr, den angegebenen Monat und Tag mit der auf Mitternacht festgelegten Zeitinformation darstellt. Im folgenden Beispiel wird das Enddatum des vorherigen Monats basierend auf dem aktuellen Monat angezeigt.  
  
    ```  
    =DateSerial(Year(Now()), Month(Now()), "1").AddDays(-1)  
    ```  
  
-   Mit den folgenden Ausdrücken werden unterschiedliche Datumsangaben basierend auf dem vom Benutzer ausgewählten date-Parameter angezeigt.  
  
|Beispielbeschreibung|Beispiel|  
|-------------------------|-------------|  
|gestern|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value)-1)`|  
|Vor zwei Tagen|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value)-2)`|  
|Vor einem Monat|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value)-1,Day(Parameters!TodaysDate.Value))`|  
|Vor zwei Monaten|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value)-2,Day(Parameters!TodaysDate.Value))`|  
|Vor einem Jahr|`=DateSerial(Year(Parameters!TodaysDate.Value)-1,Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value))`|  
|Vor zwei Jahren|`=DateSerial(Year(Parameters!TodaysDate.Value)-2,Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value))`|  
  
####  <a name="StringFunctions"></a> Zeichenfolgenfunktionen  
  
-   Mithilfe von Verkettungsoperatoren und [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Konstanten können Sie mehrere Felder kombinieren. Der folgende Ausdruck gibt zwei Felder zurück, die sich jeweils in einer eigenen Zeile in demselben Textfeld befinden.  
  
    ```  
    =Fields!FirstName.Value & vbCrLf & Fields!LastName.Value   
    ```  
  
-   Mit der **Format** -Funktion können Sie Datumsangaben und Zahlen in einer Zeichenfolge formatieren. Mit dem folgenden Ausdruck werden Werte des *StartDate* -Parameters und des *EndDate* -Parameters im langen Datumsformat angezeigt.  
  
    ```  
    =Format(Parameters!StartDate.Value, "D") & " through " &  Format(Parameters!EndDate.Value, "D")    
    ```  
  
     Enthält das Textfeld nur ein Datum oder eine Zahl, sollten Sie die Format-Eigenschaft des Textfelds anstelle der **Format**-Funktion im Textfeld verwenden, um eine Formatierung anzuwenden.  
  
-   Mit den Funktionen **Right**, **Len** und **InStr** kann eine Teilzeichenfolge zurückgegeben werden, um z.B.*DOMÄNE*\\*Benutzername* auf den Benutzernamen zu verkürzen. Der folgende Ausdruck gibt den Teil der Zeichenfolge rechts neben einem umgekehrten Schrägstrich (\\) des *User*-Parameters zurück:  
  
    ```  
    =Right(Parameters!User.Value, Len(Parameters!User.Value) - InStr(Parameters!User.Value, "\"))  
    ```  
  
     Der folgende Ausdruck liefert dasselbe Ergebnis, wobei Elemente der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.String>-Klasse anstelle von [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]-Funktionen verwendet werden:  
  
    ```  
    =Parameters!User.Value.Substring(Parameters!User.Value.IndexOf("\")+1, Parameters!User.Value.Length-Parameters!User.Value.IndexOf("\")-1)  
    ```  
  
-   Die ausgewählten Werte aus einem mehrwertigen Parameter können angezeigt werden. Im folgenden Beispiel wird die **Join** -Funktion zum Verketten der ausgewählten Werte des *MySelection* -Parameters zu einer einzelnen Zeichenfolge verwendet, die als Ausdruck für den Wert eines Textfelds in einem Berichtselement festgelegt werden kann:  
  
    ```  
    = Join(Parameters!MySelection.Value)  
    ```  
  
     Das folgende Beispiel hat die gleiche Funktion wie das Beispiel oben und zeigt darüber hinaus vor der Liste der ausgewählten Werte eine Textzeichenfolge an:  
  
    ```  
    =”Report for “ & JOIN(Parameters!MySelection.Value, “ & “)  
  
    ```  
  
-   Die **Regex**-Funktionen von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.Text.RegularExpressions> sind für das Ändern des Formats vorhandener Zeichenfolgen hilfreich, beispielsweise für das Formatieren einer Telefonnummer. Für den folgenden Ausdruck wird die **Replace**-Funktion zum Ändern des Formats einer zehnstelligen Telefonnummer in ein Feld von „*nnn*-*nnn*-*nnnn*“ in „(*nnn*) *nnn*-*nnnn*“ verwendet:  
  
    ```  
    =System.Text.RegularExpressions.Regex.Replace(Fields!Phone.Value, "(\d{3})[ -.]*(\d{3})[ -.]*(\d{4})", "($1) $2-$3")  
    ```  
  
    > [!NOTE]  
    >  Überprüfen Sie, ob der Wert für Fields!Phone.Value unter Umständen zusätzliche Leerzeichen enthält und vom Typ <xref:System.String> ist.  
  
#### Suche  
  
-   Durch Angabe eines Schlüsselfelds können Sie mit der **Lookup**-Funktion einen Wert von einem Dataset für eine 1:1-Beziehung, beispielsweise ein Schlüssel-Wert-Paar, abrufen. Der folgende Ausdruck zeigt den Produktnamen aus einem Dataset ("Product") an, wenn als Grundlage für die Übereinstimmung der Produktbezeichner angegeben ist:  
  
    ```  
    =Lookup(Fields!PID.Value, Fields!ProductID.Value, Fields.ProductName.Value, "Product")  
    ```  
  
#### LookupSet  
  
-   Indem Sie ein Schlüsselfeld angeben, können Sie mithilfe der **LookupSet**-Funktion einen Satz von Werten für eine 1:n-Beziehung aus einem Dataset abrufen. Beispiel: Eine Person kann mehrere Telefonnummern haben. Nehmen Sie im folgenden Beispiel an, dass das Dataset PhoneList in jeder Zeile einen Personenbezeichner und eine Telefonnummer enthält. **LookupSet** gibt ein Array von Werten zurück. Der folgende Ausdruck kombiniert die Rückgabewerte in eine einzelne Zeichenfolge und zeigt die Liste der Telefonnummern für die mit "ContactID" angegebene Person an:  
  
    ```  
    =Join(LookupSet(Fields!ContactID.Value, Fields!PersonID.Value, Fields!PhoneNumber.Value, "PhoneList"),",")  
    ```  
  
####  <a name="ConversionFunctions"></a> Konvertierungsfunktionen  
 Mithilfe der [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Funktionen können Sie einen Wert von einem Datentyp in einen anderen Datentyp konvertieren. Konvertierungsfunktionen können zum Konvertieren des Standarddatentyps für ein Feld in einen Datentyp verwendet werden, der für Berechnungen oder zum Kombinieren von Text erforderlich ist.  
  
-   Mit dem folgenden Ausdruck wird die Konstante 500 in den Typ "Decimal" konvertiert, um sie mit einem [!INCLUDE[tsql](../../includes/tsql-md.md)] money-Datentyp im Feld "Wert" für einen Filterausdruck zu vergleichen.  
  
    ```  
    =CDec(500)  
    ```  
  
-   Mit dem folgenden Ausdruck wird die Anzahl der für den mehrwertigen *MySelection*-Parameter ausgewählten Werte angezeigt.  
  
    ```  
    =CStr(Parameters!MySelection.Count)  
    ```  
  
####  <a name="DecisionFunctions"></a> Entscheidungsfunktionen  
  
-   Die **Iif** -Funktion gibt einen von zwei Werten zurück, und zwar abhängig davon, ob der Ausdruck mit TRUE ausgewertet wird. Im folgenden Ausdruck wird mit der **Iif**-Funktion der boolesche Wert **TRUE** zurückgegeben, falls der Wert von `LineTotal` 100 überschreitet. Andernfalls wird **False**zurückgegeben:  
  
    ```  
    =IIF(Fields!LineTotal.Value > 100, True, False)  
    ```  
  
-   Verwenden Sie mehrere **IIF**-Funktionen (die auch als „geschachtelte Iif-Funktionen“ bezeichnet werden), um einen von drei Werten in Abhängigkeit vom Wert von `PctComplete` zurückzugeben. Der folgende Ausdruck kann in die Füllfarbe eines Textfelds platziert werden, um die Hintergrundfarbe basierend auf dem Wert im Textfeld zu ändern.  
  
    ```  
    =IIF(Fields!PctComplete.Value >= 10, "Green", IIF(Fields!PctComplete.Value >= 1, "Blue", "Red"))  
    ```  
  
     Werte, die größer oder gleich 10 sind, werden mit einem grünen Hintergrund angezeigt. Werte zwischen 1 und 9 erhalten einen blauen Hintergrund, und Werte kleiner als 1 werden mit rotem Hintergrund dargestellt.  
  
-   Eine andere Möglichkeit, die gleiche Funktionalität zu erhalten, bietet die **Switch** -Funktion. Die **Switch** -Funktion ist nützlich, wenn Sie drei oder mehr Bedingungen testen müssen. Die **Switch** -Funktion gibt den Wert zurück, der mit dem ersten Ausdruck in einer Reihe verknüpft ist, die mit TRUE ausgewertet wird:  
  
    ```  
    =Switch(Fields!PctComplete.Value >= 10, "Green", Fields!PctComplete.Value >= 1, "Blue", Fields!PctComplete.Value = 1, "Yellow", Fields!PctComplete.Value <= 0, "Red",)  
    ```  
  
     Werte, die größer oder gleich 10 sind, werden mit einem grünen Hintergrund angezeigt. Werte zwischen 1 und 9 erhalten einen blauen Hintergrund, Werte, die gleich 1 sind, einen gelben Hintergrund, und Werte, die 0 oder kleiner sind, werden mit einem roten Hintergrund dargestellt.  
  
-   Mit dem Ausdruck wird der Wert des Feldes `ImportantDate` geprüft und "Red" zurückgegeben, wenn er älter als eine Woche ist. Andernfalls wird "Blue" zurückgegeben. Mit diesem Ausdruck kann die Color-Eigenschaft eines Textfelds in einem Berichtselement gesteuert werden:  
  
    ```  
    =IIF(DateDiff("d",Fields!ImportantDate.Value, Now())>7,"Red","Blue")  
    ```  
  
-   Mit dem Ausdruck wird der Wert des Felds `PhoneNumber` geprüft und „No Value“ zurückgegeben, wenn er **NULL** (**Nothing** in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) ist. Andernfalls wird der Wert der Telefonnummer zurückgegeben. Mit diesem Ausdruck kann der Wert eines Textfelds in einem Berichtselement gesteuert werden.  
  
    ```  
    =IIF(Fields!PhoneNumber.Value Is Nothing,"No Value",Fields!PhoneNumber.Value)  
    ```  
  
-   Mit dem Ausdruck wird der Wert des Felds `Department` geprüft und entweder ein Unterberichtsname oder **NULL** (**Nothing** in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) zurückgegeben. Dieser Ausdruck kann für bedingte Drillthrough-Unterberichte verwendet werden.  
  
    ```  
    =IIF(Fields!Department.Value = "Development", "EmployeeReport", Nothing)  
    ```  
  
-   Prüft, ob ein Feldwert NULL ist. Dieser Ausdruck kann verwendet werden, um die **Hidden** -Eigenschaft eines Bildberichtselements zu steuern. Im folgenden Beispiel wird das durch das Feld [LargePhoto] angegebene Bild nur angezeigt, wenn der Wert des Felds ungleich NULL ist.  
  
    ```  
    =IIF(IsNothing(Fields!LargePhoto.Value),True,False)  
    ```  
  
-   Die **MonthName** -Funktion gibt einen Zeichenfolgenwert zurück, der den Namen des angegebenen Monats enthält. Im folgenden Beispiel wird NZ im Monatsfeld angezeigt, wenn das Feld den Wert 0 enthält.  
  
    ```  
    IIF(Fields!Month.Value=0,"NA",MonthName(IIF(Fields!Month.Value=0,1,Fields!Month.Value)))  
  
    ```  
  
###  <a name="ReportFunctions"></a> Berichtsfunktionen  
 In einem Ausdruck können Sie einen Verweis auf weitere Berichtsfunktionen hinzufügen, die Daten in einem Bericht bearbeiten. In diesem Abschnitt werden Beispiele für zwei dieser Funktionen behandelt. Weitere Informationen zu Berichtsfunktionen sowie Beispiele finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md).  
  
#####  <a name="Sum"></a> Sum  
  
-   Die **Sum** -Funktion gibt die Summe von Werten in einer Gruppe oder einem Datenbereich zurück. Diese Funktion ist hilfreich für die Kopf- oder Fußzeile einer Gruppe. Der folgende Ausdruck zeigt die Summe von Daten in der Gruppe bzw. im Datenbereich Order an:  
  
    ```  
    =Sum(Fields!LineTotal.Value, "Order")  
    ```  
  
-   Sie können auch die **Sum** -Funktion für bedingte Aggregatberechnungen verwenden. Wenn ein Dataset ein Feld mit dem Namen State und den möglichen Werten Not Started, Started und Finished enthält, wird mit dem folgenden Ausdruck die Aggregatsumme bei Platzierung in einem Gruppenheader nur für den Wert Finished berechnet:  
  
    ```  
    =Sum(IIF(Fields!State.Value = "Finished", 1, 0))  
    ```  
  
#####  <a name="RowNumber"></a> RowNumber  
  
-   Mit der **RowNumber** -Funktion, die in einem Textfeld innerhalb eines Datenbereichs verwendet wird, wird die Zeilennummer für jede Instanz des Textfelds angezeigt, in der der Ausdruck enthalten ist. Diese Funktion eignet sich, um Zeilen in einer Tabelle zu nummerieren. Sie ist auch bei komplizierteren Aufgaben hilfreich, z. B. beim Einfügen von Seitenumbrüchen auf der Grundlage der Zeilenanzahl. Weitere Informationen finden Sie weiter unten unter " [Seitenumbrüche](#PageBreaks) ".  
  
     Der Bereich, den Sie für **RowNumber** -Steuerelemente angeben, wenn die Neunumerierung beginnt. Das **Nothing** -Schlüsselwort gibt an, dass die Funktion die Zählung mit der ersten Zeile im äußersten Datenbereich beginnt. Wenn Sie in geschachtelten Datenbereichen mit dem Zählen beginnen möchten, verwenden Sie den Namen des Datenbereichs. Um mit dem Zählen innerhalb einer Gruppe zu beginnen, verwenden Sie den Namen der Gruppe.  
  
    ```  
    =RowNumber(Nothing)  
    ```  
  
##  <a name="AppearanceofReportData"></a> Darstellung von Berichtsdaten  
 Mit Ausdrücken können Sie die Darstellung von Daten in einem Bericht ändern. Beispielsweise können Sie die Werte von zwei Feldern in einem einzigen Textfeld anzeigen, Informationen zum Bericht anzeigen oder die Methode zum Einfügen von Seitenumbrüchen im Bericht ändern.  
  
###  <a name="PageHeadersandFooters"></a> Seitenkopfzeilen und -fußzeilen  
 Beim Entwerfen eines Berichts soll möglicherweise der Name des Berichts und die Seitenzahl in der Fußzeile des Berichts angezeigt werden. Dazu können Sie die folgenden Ausdrücke verwenden:  
  
-   Der folgende Ausdruck stellt den Namen des Berichts und die Zeit seiner Ausführung bereit. Er kann in einem Textfeld in der Fußzeile oder im Hauptteil des Berichts eingefügt werden. Die Zeit wird mit der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Formatzeichenfolge für ein kurzes Datum formatiert:  
  
    ```  
    =Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")  
    ```  
  
-   Der folgende Ausdruck zeigt in einem Textfeld in der Fußzeile eines Berichts die Seitenzahl und die Gesamtseitenzahl im Bericht an:  
  
    ```  
    =Globals.PageNumber & " of " & Globals.TotalPages  
    ```  
  
 Die folgenden Beispiele veranschaulichen, wie der erste und letzte Wert einer Seite in der Seitenkopfzeile angezeigt wird, ähnlich wie bei einer Verzeichnisauflistung. Bei diesem Beispiel wird von einem Datenbereich ausgegangen, der das `LastName`-Textfeld enthält.  
  
-   Der folgende Ausdruck, der sich in einem Textfeld auf der linken Seite des Seitenkopfes befindet, gibt den ersten Wert des `LastName` -Textfelds auf der Seite an:  
  
    ```  
    =First(ReportItems("LastName").Value)  
    ```  
  
-   Der folgende Ausdruck, der sich in einem Textfeld auf der rechten Seite des Seitenkopfes befindet, gibt den letzten Wert des `LastName` -Textfelds auf der Seite an:  
  
    ```  
    =Last(ReportItems("LastName").Value)  
    ```  
  
 Das folgende Beispiel beschreibt, wie die Summe einer Seite angezeigt wird. Bei diesem Beispiel wird von einem Datenbereich ausgegangen, der das `Cost`-Textfeld enthält.  
  
-   Der folgende Ausdruck, im Seitenkopf oder -fuß platziert, gibt die Summe der Werte im `Cost` -Textfeld für die Seite an:  
  
    ```  
    =Sum(ReportItems("Cost").Value)  
    ```  
  
> [!NOTE]  
>  In einem Seitenkopf oder -fuß kann pro Ausdruck nur auf ein einziges Berichtselement verwiesen werden. In Seitenkopf- und -fußausdrücken können Sie außerdem auf den Textfeldnamen, jedoch nicht auf den tatsächlichen Datenausdruck innerhalb des Textfelds verweisen.  
  
###  <a name="PageBreaks"></a> Seitenumbrüche  
 In manchen Berichten möchten Sie möglicherweise einen Seitenumbruch am Ende einer bestimmten Anzahl von Zeilen einfügen, und zwar anstelle von bzw. zusätzlich zu Gruppen oder Berichtselementen. Erstellen Sie dazu eine Gruppe mit den gewünschten Gruppen- oder Detaildatensätzen, und fügen Sie der Gruppe einen Seitenumbruch hinzu. Fügen Sie anschließend einen Gruppenausdruck hinzu, um eine Gruppierung nach einer bestimmten Anzahl von Zeilen durchzuführen.  
  
-   Der folgende Ausdruck weist im Gruppenausdruck einer Gruppe von jeweils 25 Zeilen eine Zahl zu. Wenn ein Seitenumbruch für die Gruppe definiert ist, ergibt sich aus diesem Ausdruck alle 25 Zeilen ein Seitenumbruch.  
  
    ```  
    =Ceiling(RowNumber(Nothing)/25)  
    ```  
  
     Damit der Benutzer einen Wert für die Anzahl der Zeilen pro Seite festlegen kann, erstellen Sie einen Parameter mit dem Namen `RowsPerPage` und basieren den Gruppenausdruck auf dem Parameter, wie im folgenden Ausdruck gezeigt:  
  
    ```  
    =Ceiling(RowNumber(Nothing)/Parameters!RowsPerPage.Value)  
    ```  
  
     Weitere Informationen zum Festlegen von Seitenumbrüchen für eine Gruppe finden Sie unter [Hinzufügen eines Seitenumbruchs &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md).  
  
##  <a name="Properties"></a> Eigenschaften  
 Mit Ausdrücken werden nicht nur Daten in Textfeldern angezeigt. Sie können mit Ausdrücken auch festlegen, wie Eigenschaften auf Berichtselemente angewendet werden. Sie können Formatinformationen für ein Berichtselement ändern oder festlegen, ob es angezeigt wird.  
  
###  <a name="Formatting"></a> Formatierung  
  
-   Wenn der folgende Ausdruck in der Color-Eigenschaft eines Textfelds verwendet wird, wird die Farbe des Texts basierend auf dem Wert des Felds `Profit` geändert:  
  
    ```  
    =Iif(Fields!Profit.Value < 0, "Red", "Black")  
    ```  
  
     Sie können auch die [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Objektvariable `Me`verwenden. Diese Variable bietet eine andere Möglichkeit, auf den Wert eines Textfeldes zu verweisen.  
  
     `=Iif(Me.Value < 0, "Red", "Black")`  
  
-   Wenn der folgende Ausdruck in der BackgroundColor-Eigenschaft eines Berichtselements in einem Datenbereich verwendet wird, wird die Hintergrundfarbe der Zeilen von hellgrün in weiß geändert:  
  
    ```  
    =Iif(RowNumber(Nothing) Mod 2, "PaleGreen", "White")  
    ```  
  
     Wenn Sie einen Ausdruck für einen angegebenen Bereich verwenden, müssen Sie möglicherweise das Dataset für die Aggregatfunktion angeben:  
  
    ```  
    =Iif(RowNumber("Employees") Mod 2, "PaleGreen", "White")  
    ```  
  
> [!NOTE]  
>  Verfügbare Farben stammen aus der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] KnownColor-Enumeration.  
  
### Diagrammfarben  
 Mit benutzerdefiniertem Code können Sie die Reihenfolge steuern, in der Datenpunktwerten Farben zugeordnet werden, um Farben für ein Formdiagramm anzugeben. Dies hilft bei der Verwendung konsistenter Farben für mehrere Diagramme mit gleichen Kategoriegruppen. Weitere Informationen finden Sie unter [Angeben von Farben, die für mehrere Formdiagramme konsistent sind &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md).  
  
###  <a name="Visibility"></a> Sichtbarkeit  
 Berichtselemente können mithilfe der Sichtbarkeitseigenschaften ein- und ausgeblendet werden. In einem Datenbereich, wie z. B. einer Tabelle, können die Detailzeilen basierend auf dem Wert eines Ausdrucks anfänglich ausgeblendet werden.  
  
-   Wenn der folgende Ausdruck für die ursprüngliche Sichtbarkeit von Detailzeilen in einer Gruppe verwendet wird, werden die Detailzeilen für alle Umsätze angezeigt, die im `PctQuota` -Feld den Wert 90 % übersteigen:  
  
    ```  
    =Iif(Fields!PctQuota.Value>.9, False, True)  
    ```  
  
-   Wenn der folgende Ausdruck in der Hidden-Eigenschaft einer Tabelle festgelegt ist, wird die Tabelle mithilfe des Ausdrucks nur angezeigt, wenn sie mehr als 12 Zeilen enthält:  
  
    ```  
    =IIF(CountRows()>12,false,true)  
    ```  
  
-   Wenn der folgende Ausdruck in der **Hidden** -Eigenschaft einer Spalte festgelegt wird, wird die Spalte nur angezeigt, wenn das Feld im Berichtsdataset vorhanden ist, nachdem die Daten aus der Datenquelle abgerufen wurden:  
  
    ```  
    =IIF(Fields!Column_1.IsMissing, true, false)  
    ```  
  
###  <a name="Hyperlinks"></a> URLs  
 Sie können URLs anpassen, indem Sie die Berichtsdaten verwenden und bedingt steuern, ob URLs als Aktion für ein Textfeld hinzugefügt werden.  
  
-   Wenn der folgende Ausdruck als Aktion für ein Textfeld verwendet wird, wird eine angepasste URL generiert, die das Datasetfeld `EmployeeID` als URL-Parameter angibt.  
  
    ```  
    ="http://adventure-works/MyInfo?ID=" & Fields!EmployeeID.Value  
    ```  
  
     Weitere Informationen finden Sie unter [Hinzufügen eines Links zu einer URL &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-a-hyperlink-to-a-url-report-builder-and-ssrs.md).  
  
-   Der folgende Ausdruck steuert bedingt, ob eine URL in einem Textfeld hinzugefügt wird. Dieser Ausdruck ist von einem Parameter mit dem Namen `IncludeURLs` abhängig, mit dem ein Benutzer entscheiden kann, ob aktive URLs in einen Bericht eingeschlossen werden sollen. Dieser Ausdruck wird als Aktion in einem Textfeld festgelegt. Indem Sie den Parameter auf FALSE festlegen und dann den Bericht anzeigen, können Sie den Bericht ohne Links nach Microsoft Excel exportieren.  
  
    ```  
    =IIF(Parameters!IncludeURLs.Value,"http://adventure-works.com/productcatalog",Nothing)  
    ```  
  
##  <a name="ReportData"></a> Berichtsdaten  
 Mit Ausdrücken können die im Bericht verwendeten Daten bearbeitet werden. Sie können auf Parameter und sonstige Berichtsinformationen verweisen. Es ist sogar möglich, die Abfrage zu ändern, mit der Daten für den Bericht abgerufen werden.  
  
###  <a name="Parameters"></a> Parameter  
 Ausdrücke können in einem Parameter verwendet werden, um den Standardwert für den Parameter zu ändern. Beispielsweise können Sie mithilfe eines Parameters Daten nach einem bestimmten Benutzer basierend auf der Benutzer-ID filtern, mit der der Bericht ausgeführt wird.  
  
-   Wenn der folgende Ausdruck als Standardwert für einen Parameter verwendet wird, wird die Benutzer-ID der Person abgerufen, die den Bericht ausführt:  
  
    ```  
    =User!UserID  
    ```  
  
-   Verwenden Sie die globale **Parameters** -Auflistung, um auf einen Parameter in einem Abfrageparameter, auf einen Filterausdruck, ein Textfeld oder einen anderen Bereich des Berichts zu verweisen. Bei diesem Beispiel wird von einem Parameter namens *Department*ausgegangen:  
  
    ```  
    =Parameters!Department.Value  
    ```  
  
-   Parameter können in einem Bericht erstellt und trotzdem ausgeblendet werden. Wenn der Bericht auf dem Berichtsserver ausgeführt wird, erscheint der Parameter nicht auf der Symbolleiste und der Leser des Berichts kann den Standardwert nicht ändern. Sie können einen ausgeblendeten, auf einen Standardwert festgelegten Parameter als benutzerdefinierte Konstante verwenden. Diesen Wert können Sie in einem beliebigen Ausdruck verwenden, einschließlich eines Feldausdrucks. Der folgende Ausdruck gibt das vom Standardparameterwert für den Parameter mit dem Namen *ParameterField*angegebene Feld an:  
  
    ```  
    =Fields(Parameters!ParameterField.Value).Value  
    ```  
  
##  <a name="CustomCode"></a> Benutzerdefinierter Code  
 In einem Bericht kann benutzerdefinierter Code verwendet werden. Benutzerdefinierter Code ist entweder in einen Bericht eingebettet oder in einer benutzerdefinierten Assembly gespeichert, die im Bericht verwendet wird. Weitere Informationen zu benutzerdefiniertem Code finden Sie unter [Benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
### Verwenden von Gruppenvariablen für benutzerdefinierte Aggregation  
 Sie können den Wert für eine Gruppenvariable initialisieren, die zu einem bestimmten Gruppenbereich lokal ist, und anschließend einen Verweis auf diese Variable in den Ausdrücken einbinden. Eine der Methoden, wie Sie eine Gruppenvariable mit benutzerdefiniertem Code verwenden können, besteht darin, ein benutzerdefiniertes Aggregat zu implementieren. Weitere Informationen finden Sie unter [Gruppevariablen in Reporting Services 2008 für benutzerdefinierte Aggregation verwenden](http://go.microsoft.com/fwlink/?LinkId=128714).  
  
 Weitere Informationen zu Variablen finden Sie unter [Verweise auf Berichts- und Gruppenvariablensammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-and-group-variables-collections-references-report-builder-and-ssrs.md).  
  
## Unterdrücken von NULL oder 0 zur Laufzeit  
 Einige Werte in einem Ausdruck können zur Berichtsverarbeitungszeit mit NULL oder "nicht definiert" ausgewertet werden. Dies kann zu Laufzeitfehlern und zur Anzeige von **#Error** im Textfeld anstelle des ausgewerteten Ausdrucks führen. Die **IIF**-Funktion ist für dieses Verhalten besonders empfindlich, da im Gegensatz zu einer If-Then-Else-Anweisung jeder Teil der **IIF**-Anweisung (einschließlich Funktionsaufrufe) ausgewertet wird, bevor er an die Routine zur Prüfung auf **TRUE** oder **FALSE** übergeben wird. Die Anweisung `=IIF(Fields!Sales.Value is NOTHING, 0, Fields!Sales.Value)` generiert **#Error** im gerenderten Bericht, wenn `Fields!Sales.Value` NOTHING ist.  
  
 Wählen Sie eine der folgenden Strategien aus, um diesen Fehler zu vermeiden:  
  
-   Legen Sie den Zähler auf 0 und den Nenner auf 1 fest, wenn der Wert für das Feld B 0 oder nicht definiert ist. Andernfalls legen Sie den Zähler auf den Wert für Feld A und den Nenner auf den Wert für Feld B fest.  
  
    ```  
    =IIF(Field!B.Value=0, 0, Field!A.Value / IIF(Field!B.Value =0, 1, Field!B.Value))  
    ```  
  
-   Verwenden Sie eine benutzerdefinierte Codefunktion, um den Wert für den Ausdruck zurückzugeben. Im folgenden Beispiel wird der Prozentsatzunterschied zwischen einem aktuellen Wert und einem vorherigen Wert zurückgegeben. Dieser Wert kann zur Berechnung der Differenz zwischen zwei aufeinanderfolgenden Werten verwendet werden und verarbeitet den Grenzfall des ersten Vergleichs (wenn kein vorheriger Wert vorhanden ist) sowie Fälle, in denen entweder der vorherige Wert oder der aktuelle Wert **NULL** (**Nothing** in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) ist.  
  
    ```  
    Public Function GetDeltaPercentage(ByVal PreviousValue, ByVal CurrentValue) As Object  
        If IsNothing(PreviousValue) OR IsNothing(CurrentValue) Then  
            Return Nothing  
        Else if PreviousValue = 0 OR CurrentValue = 0 Then  
            Return Nothing  
        Else   
            Return (CurrentValue - PreviousValue) / CurrentValue  
        End If  
    End Function  
    ```  
  
     Der folgende Ausdruck veranschaulicht, wie dieser benutzerdefinierte Code aus einem Textfeld für den "ColumnGroupByYear"-Container (Gruppe bzw. Datenbereich) aufgerufen wird.  
  
    ```  
    =Code.GetDeltaPercentage(Previous(Sum(Fields!Sales.Value),"ColumnGroupByYear"), Sum(Fields!Sales.Value))  
    ```  
  
     Dadurch wird die Ausführung von Laufzeitausnahmen vermieden. Sie können nun einen Ausdruck wie `=IIF(Me.Value < 0, "red", "black")` in der **Color**-Eigenschaft des Textfelds verwenden, um den Text unter Bedingungen anzuzeigen, nämlich abhängig davon, ob die Werte größer oder kleiner als 0 sind.  
  
## Siehe auch  
 [Beispiele für Filtergleichungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [Beispiele für Gruppierungsausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Häufig verwendete Filter &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)  
  
  