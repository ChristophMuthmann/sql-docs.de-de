---
title: "CountRows-Funktion (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# CountRows-Funktion (Berichts-Generator und SSRS)
  Gibt die Anzahl der Zeilen im angegebenen Bereich zurück, einschließlich der Zeilen mit NULL-Werten.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Syntax  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### Parameter  
 *Bereich*  
 (**String**) Der Name eines Datasets, eines Datenbereichs oder einer Gruppe mit den zu zählenden Berichtselementen.  
  
 *Rekursiv*  
 (**Enumerationstyp**) Optional. **Simple** (Standard) oder **RdlRecursive**. Gibt an, ob die Aggregation rekursiv auszuführen ist.  
  
## Rückgabetyp  
 Gibt einen Wert vom Typ **Integer**zurück.  
  
## Hinweise  
 **CountRows** zählt alle Zeilen im angegebenen Bereich, einschließlich der Zeilen mit NULL-Werten.  
  
 Der Wert *scope* darf kein Ausdruck sein und muss auf den aktuellen Bereich oder einen enthaltenen Bereich verweisen.  
  
 Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) und [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
 Weitere Informationen zu rekursiven Aggregaten finden Sie unter [Erstellen von rekursiven Hierarchiegruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## Beispiel  
 Das folgende Codebeispiel zeigt einen Ausdruck, der die Anzahl der Zeilen in einer Zeilengruppe mit dem Namen `GroupbyCategory` (basierend auf dem Ausdruck `[Category]`) berechnet.  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  