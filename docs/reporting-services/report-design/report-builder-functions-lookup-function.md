---
title: Lookup-Funktion (Berichts-Generator und SSRS) | Microsoft Docs
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
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4426bffe23295c623d0bba5592c1488cb0ede770
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---lookup-function"></a>Berichts-Generator Funktionen - Lookup-Funktion
  Gibt den ersten übereinstimmenden Wert für den angegebenen Namen aus einem Dataset mit Name-Wert-Paaren zurück.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parameter  
 *source_expression*  
 (**Variant**) Ein Ausdruck, der im aktuellen Bereich ausgewertet wird und den zu suchenden Namen oder Schlüssel angibt. Beispiel: `=Fields!ProdID.Value`.  
  
 *destination_expression*  
 (**Variant**) Ein Ausdruck, der für jede Zeile in einem Dataset ausgewertet wird, und der den Namen oder den Schlüssel für die Übereinstimmung angibt. Beispiel: `=Fields!ProductID.Value`.  
  
 *result_expression*  
 (**Variant**) Ein Ausdruck, der für die Zeile im Dataset ausgewertet wird, für die *source_expression* = *destination_expression*gilt, und der den abzurufenden Wert angibt. Beispiel: `=Fields!ProductName.Value`.  
  
 *Dataset (dataset)*  
 Eine Konstante, die den Namen eines Datasets im Bericht angibt. Beispiel: "Products".  
  
## <a name="return"></a>Rückgabewert  
 Gibt einen Wert vom Typ **Variant**zurück; gibt **Nothing** zurück, wenn keine Übereinstimmung vorhanden ist.  
  
## <a name="remarks"></a>Hinweise  
 Rufen Sie für ein Name-Wert-Paar, für das eine 1:1-Beziehung vorhanden ist, den Wert mithilfe von **Lookup** aus dem angegebenen Dataset ab. Beispiel: Für ein ID-Feld in einer Tabelle können Sie das entsprechende Namensfeld mithilfe von **Lookup** aus einem Dataset abrufen, das nicht an den Datenbereich gebunden wird.  
  
 Mit**Lookup** wird Folgendes ausgeführt:  
  
-   Der Quellausdruck wird im aktuellen Bereich ausgewertet.  
  
-   Der Zielausdruck wird für jede Zeile des angegebenen Datasets ausgewertet, nachdem Filter angewendet wurden, und zwar anhand der Sortierung des angegebenen Datasets.  
  
-   Bei der ersten Übereinstimmung von Quellausdruck und Zielausdruck wird der Ergebnisausdruck für diese Zeile im Dataset ausgewertet.  
  
-   Der Ergebnisausdruckswert wird zurückgegeben.  
  
 Um mehrere Werte für einen einzelnen Namen oder ein Schlüsselfeld abzurufen, für das eine 1:n-Beziehung vorhanden ist, verwenden Sie [LookupSet-Funktion &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookupset-function.md). Aufzurufende **Suche** für eine Wertemenge verwenden [Multilookup Function &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-design/report-builder-functions-multilookup-function.md).  
  
 Es gelten folgende Einschränkungen:  
  
-   **Lookup** wird ausgewertet, nachdem alle Filterausdrücke angewendet wurden.  
  
-   Nur eine Suchebene wird unterstützt. Ein Quell-, Ziel- oder Ergebnisausdruck kann keinen Verweis auf eine Suchfunktion einschließen.  
  
-   Quell- und Zielausdrücke müssen den gleichen Datentyp ergeben. Der Rückgabetyp ist der gleiche wie der Datentyp des ausgewerteten Ergebnisausdrucks.  
  
-   Quell-, Ziel- und Ergebnisausdrücke können keine Verweise auf Berichts- oder Gruppenvariablen einschließen.  
  
-   **Lookup** kann nicht als Ausdruck für die folgenden Berichtselemente verwendet werden:  
  
    -   Dynamische Verbindungszeichenfolgen für eine Datenquelle.  
  
    -   Berechnete Felder in einem Dataset.  
  
    -   Abfrageparameter in einem Dataset.  
  
    -   Filter in einem Dataset.  
  
    -   Berichtsparameter.  
  
    -   Die Eigenschaft „Report.Language“.  
  
 Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) und [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Beispiel  
 Nehmen Sie im folgenden Beispiel an, dass eine Tabelle an ein Dataset gebunden wird, das ein Feld für den Produktbezeichner "ProductID" enthält. Ein separates Dataset mit dem Namen "Product" enthält den entsprechenden Produktbezeichner "ID" und den Produktnamen "Name".  
  
 Im folgenden Ausdruck vergleicht **Lookup** in jeder Zeile des Datasets „Product“ den Wert von „ProductID“ mit „ID“. Wenn eine Übereinstimmung gefunden wird, wird der Wert des Felds „Name“ für diese Zeile zurückgegeben.  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  

