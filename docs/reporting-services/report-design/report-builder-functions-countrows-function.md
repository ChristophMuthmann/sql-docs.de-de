---
title: CountRows-Funktion (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 8013a03e8f108a8ae625a8946fca148c65ed8ea8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="report-builder-functions---countrows-function"></a>Funktionen des Berichts-Generators: CountRows-Funktion
  Gibt die Anzahl der Zeilen im angegebenen Bereich zurück, einschließlich der Zeilen mit NULL-Werten.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Bereich*  
 (**String**) Der Name eines Datasets, eines Datenbereichs oder einer Gruppe mit den zu zählenden Berichtselementen.  
  
 *Rekursiv*  
 (**Enumerationstyp**) Optional. **Simple** (Standard) oder **RdlRecursive**. Gibt an, ob die Aggregation rekursiv auszuführen ist.  
  
## <a name="return-type"></a>Rückgabetyp  
 Gibt einen Wert vom Typ **Integer**zurück.  
  
## <a name="remarks"></a>Hinweise  
 **CountRows** zählt alle Zeilen im angegebenen Bereich, einschließlich der Zeilen mit NULL-Werten.  
  
 Der Wert *scope* darf kein Ausdruck sein und muss auf den aktuellen Bereich oder einen enthaltenen Bereich verweisen.  
  
 Weitere Informationen finden Sie in der [Aggregatfunktionsreferenz (Berichts-Generator und SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) und unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen (Berichts-Generator und SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Weitere Informationen zu rekursiven Aggregaten finden Sie unter [Creating Recursive Hierarchy Groups (Report Builder and SSRS) (Erstellen von rekursiven Hierarchiegruppen (Berichts-Generator und SSRS))](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Beispiel  
 Das folgende Codebeispiel zeigt einen Ausdruck, der die Anzahl der Zeilen in einer Zeilengruppe mit dem Namen `GroupbyCategory` (basierend auf dem Ausdruck `[Category]`) berechnet.  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken (Berichts-Generator und SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
