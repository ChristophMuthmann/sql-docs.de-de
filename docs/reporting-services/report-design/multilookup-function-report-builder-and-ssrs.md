---
title: "Multilookup-Funktion (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Multilookup-Funktion (Berichts-Generator und SSRS)
  Gibt den Satz der ersten übereinstimmenden Werte für den angegebenen Satz von Namen aus einem Dataset mit Name-Wert-Paaren zurück.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Syntax  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### Parameter  
 *source_expression*  
 (**VariantArray**) Ein Ausdruck, der im aktuellen Bereich ausgewertet wird, und der den Satz der zu suchenden Namen oder Schlüssel angibt. Beispiel für einen mehrwertigen Parameter: `=Parameters!IDs.value`.  
  
 *destination_expression*  
 (**Variant**) Ein Ausdruck, der für jede Zeile in einem Dataset ausgewertet wird, und der den Namen oder den Schlüssel für die Übereinstimmung angibt. Beispiel: `=Fields!ID.Value`.  
  
 *result_expression*  
 (**Variant**) Ein Ausdruck, der für die Zeile im Dataset ausgewertet wird, für die *source_expression* = *destination_expression* gilt, und der den abzurufenden Wert angibt. Beispiel: `=Fields!Name.Value`.  
  
 *Dataset (dataset)*  
 Eine Konstante, die den Namen eines Datasets im Bericht angibt. Beispiel: "Colors".  
  
## Rückgabewert  
 Gibt einen Wert vom Typ **VariantArray**zurück; gibt **Nothing** zurück, wenn keine Übereinstimmung vorhanden ist.  
  
## Hinweise  
 Verwenden Sie **Multilookup**, um eine Wertemenge aus einem Dataset für Name-Wert-Paare abzurufen, in dem jedes Paar über eine 1:1-Beziehung verfügt. **MultiLookup** ist mit dem Aufrufen von **Lookup** für eine Menge von Namen oder Schlüsseln vergleichbar. Beispiel: Für einen mehrwertigen Parameter, der auf Primärschlüsselbezeichnern basiert, können Sie **Multilookup** in einem Ausdruck in einem Textfeld in einer Tabelle verwenden, um zugeordnete Werte aus einem Dataset abzurufen, das nicht an den Parameter oder die Tabelle gebunden ist.  
  
 Mit**Multilookup** wird Folgendes ausgeführt:  
  
-   Der Quellausdruck wird im aktuellen Bereich ausgewertet, und ein Array von Variant-Objekten wird generiert.  
  
-   Für jedes Objekt im Array wird [Lookup-Funktion &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/lookup-function-report-builder-and-ssrs.md) aufgerufen und dem Rückgabearray das Ergebnis hinzugefügt.  
  
-   Der Satz von Ergebnissen wird zurückgegeben.  
  
 Verwenden Sie die [Lookup-Funktion](../../reporting-services/report-design/lookup-function-report-builder-and-ssrs.md), um einen einzelnen Wert aus einem Dataset mit Name-Wert-Paaren für einen angegebenen Namen abzurufen, wenn eine 1:1-Beziehung vorhanden ist. Verwenden Sie [LookupSet-Funktion &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/lookupset-function-report-builder-and-ssrs.md), um mehrere Werte aus einem Dataset mit Name-Wert-Paaren für einen Namen abzurufen, wenn eine 1:n-Beziehung besteht.  
  
 Es gelten folgende Einschränkungen:  
  
-   **Multilookup** wird ausgewertet, nachdem alle Filterausdrücke angewendet wurden.  
  
-   Nur eine Suchebene wird unterstützt. Ein Quell-, Ziel- oder Ergebnisausdruck kann keinen Verweis auf eine Suchfunktion einschließen.  
  
-   Quell- und Zielausdrücke müssen den gleichen Datentyp ergeben.  
  
-   Quell-, Ziel- und Ergebnisausdrücke können keine Verweise auf Berichts- oder Gruppenvariablen einschließen.  
  
-   **Multilookup** kann nicht als Ausdruck für die folgenden Berichtselemente verwendet werden:  
  
    -   Dynamische Verbindungszeichenfolgen für eine Datenquelle.  
  
    -   Berechnete Felder in einem Dataset.  
  
    -   Abfrageparameter in einem Dataset.  
  
    -   Filter in einem Dataset.  
  
    -   Berichtsparameter.  
  
    -   Die Eigenschaft „Report.Language“.  
  
 Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) und [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
## Beispiel  
 Angenommen, ein Dataset mit dem Namen "Category" enthält das Feld "CategoryList", das eine durch Trennzeichen getrennte Liste von Kategoriebezeichnern enthält, wie z. B. "2, 4, 2, 1".  
  
 Das Dataset "CategoryNames" enthält den Kategoriebezeichner und den Kategorienamen, wie in der folgenden Tabelle gezeigt.  
  
|ID|Name|  
|--------|----------|  
|1|Accessories|  
|2|Bikes|  
|3|Clothing|  
|4|Components|  
  
 Verwenden Sie für die Suche der Namen, die der Liste der Bezeichner entsprechen, **Multilookup**. Sie müssen zuerst die Liste in ein Zeichenfolgenarray aufteilen, **Multilookup** aufrufen, um die Kategorienamen abzurufen, und die Ergebnisse zu einer Zeichenfolge verketten.  
  
 Wenn der folgende Ausdruck in ein Textfeld in einem Datenbereich platziert wird, der an das Dataset "Category" gebunden ist, wird "Bikes, Components, Bikes, Accessories" angezeigt:  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## Beispiel  
 Angenommen, ein Dataset "ProductColors" enthält ein Farbbezeichnerfeld "ColorID" und ein Farbwertfeld "Color", wie in der folgenden Tabelle gezeigt.  
  
|ColorID|Farbe|  
|-------------|-----------|  
|1|Red|  
|2|Blue|  
|3|Green|  
  
 Angenommen, der mehrwertige Parameter *MyColors* ist nicht an ein Dataset für seine verfügbaren Werte gebunden. Die Standardwerte für den Parameter sind auf 2 und 3 festgelegt. Wenn der folgende Ausdruck in einem Textfeld in einer Tabelle platziert wird, werden die ausgewählten Werte für den Parameter zu einer durch Trennzeichen getrennten Liste verkettet, und es wird "Blue, Green" angezeigt.  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  