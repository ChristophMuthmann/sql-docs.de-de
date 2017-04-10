---
title: "InScope-Funktion (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# InScope-Funktion (Berichts-Generator und SSRS)
  Gibt an, ob sich die aktuelle Instanz eines Elements innerhalb des angegebenen Bereichs befindet.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Syntax  
  
```  
InScope(scope)  
```  
  
#### Parameter  
 *Bereich*  
 (**String**) Der Name eines Datasets, eines Datenbereichs oder einer Gruppe, die einen Bereich angibt.  
  
## Rückgabetyp  
 Gibt einen **Boolean**zurück.  
  
## Hinweise  
 Die **InScope**-Funktion testet den Bereich der aktuellen Instanz eines Berichtselements in Bezug auf die Mitgliedschaft in dem durch den *scope*-Parameter angegebenen Bereich.  
  
 *Scope* darf kein Ausdruck sein.  
  
 Die **InScope** -Funktion wird üblicherweise in Datenbereichen mit dynamischer Bereichsdefinierung eingesetzt. So kann **InScope** beispielsweise in einem Drillthroughlink in einer Datenbereichszelle verwendet werden, um unterschiedliche Berichtsnamen und unterschiedliche Parametersätze bereitzustellen, je nach Zelle, auf die Sie klicken. Dies wird im folgenden Beispiel verdeutlicht:  
  
-   Mit dem folgenden Ausdruck, der in einem Drillthroughlink als Berichtsname verwendet wird, wird der `ProductDetail` -Bericht geöffnet, wenn sich die angeklickte Zelle in der `Month` -Gruppierung befindet; andernfalls wird der `ProductSummary` -Bericht geöffnet.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   Der folgende Ausdruck, der in der **omit**-Eigenschaft eines Drillthroughberichts-Parameters verwendet wird, übergibt Parameter nur dann an den Zielbericht, wenn sich die ausgewählt Zelle in der `Product`-Gruppe befindet.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) und [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
## Beispiel  
 Im folgenden Codebeispiel wird angezeigt, ob sich die aktuelle Instanz des Elements innerhalb des `Product` -Datasets, -Datenbereichs oder -Gruppenbereichs befindet.  
  
```  
=InScope("Product")  
```  
  
## Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  