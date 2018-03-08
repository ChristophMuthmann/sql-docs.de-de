---
title: InScope-Funktion (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0c7035ef5f0f7c40504363dbfac696d96fcc3d13
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="report-builder-functions---inscope-function"></a>Funktionen des Berichts-Generators: InScope-Funktion
  Gibt an, ob sich die aktuelle Instanz eines Elements innerhalb des angegebenen Bereichs befindet.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Syntax  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Bereich*  
 (**String**) Der Name eines Datasets, eines Datenbereichs oder einer Gruppe, die einen Bereich angibt.  
  
## <a name="return-type"></a>Rückgabetyp  
 Gibt einen **Boolean**zurück.  
  
## <a name="remarks"></a>Remarks  
 Die **InScope** -Funktion testet den Bereich der aktuellen Instanz eines Berichtselements in Bezug auf die Mitgliedschaft in dem durch den *scope*-Parameter angegebenen Bereich.  
  
 *Scope* darf kein Ausdruck sein.  
  
 Die **InScope** -Funktion wird üblicherweise in Datenbereichen mit dynamischer Bereichsdefinierung eingesetzt. So kann **InScope** beispielsweise in einem Drillthroughlink in einer Datenbereichszelle verwendet werden, um unterschiedliche Berichtsnamen und unterschiedliche Parametersätze bereitzustellen, je nach Zelle, auf die Sie klicken. Dies wird im folgenden Beispiel verdeutlicht:  
  
-   Mit dem folgenden Ausdruck, der in einem Drillthroughlink als Berichtsname verwendet wird, wird der `ProductDetail` -Bericht geöffnet, wenn sich die angeklickte Zelle in der `Month` -Gruppierung befindet; andernfalls wird der `ProductSummary` -Bericht geöffnet.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   Der folgende Ausdruck, der in der **omit** -Eigenschaft eines Drillthroughberichts-Parameters verwendet wird, übergibt Parameter nur dann an den Zielbericht, wenn sich die ausgewählt Zelle in der `Product` -Gruppe befindet.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 Weitere Informationen finden Sie in der [Aggregatfunktionsreferenz (Berichts-Generator und SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) und unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen (Berichts-Generator und SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird angezeigt, ob sich die aktuelle Instanz des Elements innerhalb des `Product` -Datasets, -Datenbereichs oder -Gruppenbereichs befindet.  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken (Berichts-Generator und SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
