---
title: Verweise auf Datasetfeldauflistungen (Berichts-Generator und SSRS) | Microsoft-Dokumentation
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
ms.assetid: 006c6bd3-d776-4c20-9092-32e40688ac49
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d9c1c724e1b097e842975de2e8095a34fbbbb2d3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="built-in-collections---dataset-fields-collection-references-report-builder"></a>Integrierte Auflistungen: Verweise auf Datasetfeldauflistungen (Berichts-Generator)
  Jedes Dataset in einem Bericht enthält eine Fields-Sammlung. Bei der Fields-Sammlung handelt es sich um eine Gruppe von Feldern, die von der Datasetabfrage und zusätzlichen berechneten Feldern angegeben werden, die Sie erstellen. Nachdem Sie ein Dataset erstellt haben, wird die Feldauflistung im **Berichtsdatenbereich** angezeigt.  
  
 Ein einfacher Feldverweis in einem Ausdruck wird auf der Entwurfsoberfläche als einfacher Ausdruck angezeigt. Wenn Sie zum Beispiel das Feld `Sales` aus dem Bereich Berichtsdaten in eine Tabellenzelle der Entwurfsoberfläche ziehen, wird `[Sales]` angezeigt. Dies ist der zugrunde liegende Ausdruck `=Fields!Sales.Value` , der in der Value-Eigenschaft des Textfelds festgelegt wird. Wenn der Bericht ausgeführt wird, wertet der Berichtsprozessor diesen Ausdruck aus und zeigt die eigentlichen Daten der Datenquelle in der Tabellenzelle im Textfeld an. Weitere Informationen finden Sie unter [Ausdrücke (Berichts-Generator und SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md) und [Datasetfeldauflistung (Berichts-Generator und SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-the-field-collection-for-a-dataset"></a>Anzeigen der Feldauflistung für ein Dataset  
 Ziehen Sie die Felder einzeln in eine Tabellendetailzeile, um die jeweiligen Werte für eine Feldauflistung anzuzeigen. Die Verweise aus der Detailzeile eines Tabellen- oder Listendatenbereichs zeigen für jede Zeile im Dataset einen Wert an.  
  
 Um zusammengefasste Werte für ein Feld anzuzeigen, ziehen Sie die einzelnen numerischen Felder in den Datenbereich einer Matrix. Die Standardaggregatfunktion für die gesamte Zeile ist Sum, zum Beispiel `=Sum(Fields!Sales.Value)`. Sie können die Standardfunktion ändern, um andere Gesamtbeträge zu berechnen. Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
 Sie müssen den Datasetnamen als Bereich für die Aggregatfunktion angeben, um die zusammengefassten Werte für eine Feldauflistung in einem Textfeld direkt auf der Entwurfsoberfläche anzuzeigen (ist nicht Teil eines Datenbereichs). Für ein Dataset mit dem Namen `SalesData`gibt der folgende Ausdruck den Gesamtbetrag aller Werte für das Feld `Sales`an: `=Sum(Fields!Sales,"SalesData")`.  
  
 Wenn Sie das Dialogfeld **Ausdruck** zum Definieren eines einfachen Feldverweises verwenden, können Sie die Fields-Sammlung im Bereich „Kategorie“ auswählen, um die Liste der verfügbaren Felder im Bereich **Feld** anzuzeigen. Jedes Feld verfügt über mehrere Eigenschaften, zum Beispiel Value und IsMissing. Bei den restlichen Eigenschaften handelt es sich um vordefinierte erweiterte Feldeigenschaften, die je nach Datenquellentyp für das Dataset verfügbar sind.  
  
### <a name="detecting-nulls-for-a-dataset-field"></a>Erkennen von Nullen für ein Datasetfeld  
 Sie können die Funktion**IsNothing** verwenden, um einen Feldwert zu erkennen, der NULL ( [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]Nothing **in**) ist. Wenn der folgende Ausdruck in einem Textfeld in eine Tabellendetailzeile eingefügt wird, prüft dieser das Feld `MiddleName` und ersetzt den Text "No Middle Name", wenn der Wert NULL ist, und den Feldwert selbst, wenn der Wert nicht NULL ist:  
  
 `=IIF(IsNothing(Fields!MiddleName.Value),"No Middle Name",Fields!MiddleName.Value)`  
  
### <a name="detecting-missing-fields-for-dynamic-queries-at-run-time"></a>Erkennen von fehlenden Feldern für dynamische Abfragen zur Laufzeit  
 Elemente in der Fields-Sammlung besitzen in der Standardeinstellung zwei Eigenschaften: Value und IsMissing. Mit der IsMissing-Eigenschaft wird angegeben, ob ein zur Entwurfszeit für ein Dataset definiertes Feld in den Feldern enthalten ist, die zur Laufzeit abgerufen werden. Die Abfrage kann zum Beispiel eine gespeicherte Prozedur aufrufen, bei der das Resultset in Abhängigkeit eines Eingabeparameters variiert, oder die Abfrage kann `SELECT * FROM` *\<Tabelle>* lauten und die Tabellendefinition ändern.  
  
> [!NOTE]  
>  IsMissing erkennt für alle Datenquellentypen Änderungen des Datasetschemas zwischen Entwurfs- und Laufzeit. Sie können IsMissing nicht verwenden, um in einem mehrdimensionalen Cube leere Elemente zu erkennen, und es besteht keine Beziehung zu den Begriffen **EMPTY** und **NON EMPTY**der MDX-Abfragesprache.  
  
 Sie können die IsMissing-Eigenschaft in benutzerdefiniertem Code testen, um zu ermitteln, ob ein Feld im Resultset vorhanden ist. Für diesen Test können Sie keinen Ausdruck mit einem [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Funktionsaufruf verwenden, wie **IIF** oder **SWITCH**, weil [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] alle Parameter im Aufruf basierend auf der Funktion auswertet. Dies führt zu einem Fehler, wenn der Verweis auf das fehlende Feld ausgewertet wird.  
  
#### <a name="example-for-controlling-the-visibility-of-a-dynamic-column-for-a-missing-field"></a>Beispiel für die Steuerung der Sichtbarkeit einer dynamischen Spalte für ein fehlendes Feld  
 Um einen Ausdruck festzulegen, der die Sichtbarkeit einer Spalte steuert, die ein Feld in einem Dataset anzeigt, führen Sie Folgendes durch: Sie müssen zuerst eine benutzerdefinierte Codefunktion definieren, die einen booleschen Wert basierend darauf zurückgibt, ob das Feld fehlt. Beispielsweise gibt die folgende benutzerdefinierte Codefunktion true zurück, wenn das Feld fehlt, und false, wenn das Feld vorhanden ist.  
  
```  
Public Function IsFieldMissing(field as Field) as Boolean  
 If (field.IsMissing) Then  
 Return True  
  Else   
  Return False  
 End If  
End Function  
```  
  
 Legen Sie die Hidden-Eigenschaft der Spalte auf den folgenden Ausdruck fest, um diese Funktion zum Steuern der Sichtbarkeit einer Spalte zu verwenden:  
  
 `=Code.IsFieldMissing(Fields!FieldName)`  
  
 Die Spalte wird ausgeblendet, wenn das Feld nicht vorhanden ist.  
  
#### <a name="example-for-controlling-the-text-box-value-for-a-missing-field"></a>Beispiel für die Steuerung des Textfeldwerts für ein fehlendes Feld  
 Um Text zu ersetzen, den Sie anstelle des Wertes eines fehlenden Felds schreiben, müssen Sie benutzerdefinierten Code schreiben. Der Code muss Text zurückgeben, den Sie anstelle eines Feldwertes verwenden können, wenn das Feld fehlt. Die folgende benutzerdefinierte Codefunktion gibt den Wert des Felds zurück, wenn das Feld vorhanden ist, und die als zweiten Parameter angegebene Meldung, wenn das Feld nicht vorhanden ist:  
  
```  
Public Function IsFieldMissingThenString(field as Field, strMessage as String) as String  
 If (field.IsMissing) Then  
  Return strMessage  
 Else   
  Return field.Value  
  End If  
End Function  
```  
  
 Fügen Sie den folgenden Ausdruck der Value-Eigenschaft hinzu, um diese Funktion in einem Textfeld zu verwenden:  
  
 `=Code.IsFieldMissingThenString(Fields!FieldName,"Missing")`  
  
 Das Textfeld zeigt entweder den Feldwert oder den Text an, den Sie angegeben haben.  
  
### <a name="using-extended-field-properties"></a>Verwenden von erweiterten Feldeigenschaften  
 Bei den erweiterten Feldeigenschaften handelt es sich um zusätzliche Eigenschaften, die für ein Feld über die Datenverarbeitungserweiterung definiert werden, die vom Datenquellentyp für das Dataset bestimmt wird. Erweiterte Feldeigenschaften sind entweder vordefiniert oder gelten speziell für einen Datenquellentyp. Weitere Informationen finden Sie unter [Erweiterte Feldeigenschaften für eine Analysis Services-Datenbank (SSRS)](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
 Wenn Sie eine Eigenschaft angeben, die für das Feld nicht unterstützt wird, wird der Verweis als **NULL** (**Nothing** in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) ausgewertet. Wenn ein Datenanbieter keine erweiterten Feldeigenschaften unterstützt oder wenn das Feld während des Ausführens der Abfrage nicht gefunden wird, entspricht der Wert für die Eigenschaft bei Eigenschaften vom Typ **Zeichenfolge** und**Objekt** [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]NULL **(** Nothing **in**), und bei Eigenschaften vom Typ **Integer**entspricht er Null (0). Für eine Datenverarbeitungserweiterung können die Vorteile der vordefinierten Eigenschaften genutzt werden, indem die Abfragen optimiert werden, die diese Syntax enthalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
  
  
