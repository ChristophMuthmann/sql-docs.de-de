---
title: RowNumber-Funktion (Berichts-Generator und SSRS) | Microsoft-Dokumentation
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
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 33f3b559c924f6a5cb9751ad938a01f495172701
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="report-builder-functions---rownumber-function"></a>Funktionen des Berichts-Generators: RowNumber-Funktion
  Gibt eine laufende Zählung der Zeilenanzahl für den angegebenen Bereich zurück.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Bereich*  
 (**Zeichenfolge**) Der Name eines Datasets, eines Datenbereichs, einer Gruppe oder NULL (**Nothing** in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), der den Kontext angibt, in dem die Zeilenanzahl ausgewertet wird. Durch**Nothing** wird der äußerste Kontext angegeben, normalerweise das Berichtsdataset.  
  
## <a name="remarks"></a>Hinweise  
 Durch**RowNumber** wird ein wirksamer Wert der Zeilenanzahl innerhalb des festgelegten Bereichs zurückgegeben, ebenso wie von [RunningValue](../../reporting-services/report-design/report-builder-functions-runningvalue-function.md) der wirksame Wert einer Aggregatfunktion zurückgegeben wird. Wenn Sie einen Bereich angeben, geben Sie an, wann die Zeilenanzahl auf 1 zurückzusetzen ist.  
  
 *scope* darf kein Ausdruck sein. *scope* muss ein Gültigkeitsbereich sein. Typische Bereiche, von der äußersten bis zur innersten Einkapselung, sind Berichtsdataset, Datenbereich, Zeilengruppen oder Spaltengruppen.  
  
 Um Werte über Spalten hinweg zu inkrementieren, geben Sie einen Bereich an, der dem Namen einer Spaltengruppe enspricht. Um Zahlen über Zeilen hinweg zu inkrementieren, geben Sie einen Bereich an, der dem Namen einer Zeilengruppe enspricht.  
  
> [!NOTE]  
>  Das Einschließen von Aggregaten, die sowohl eine Zeilengruppe als auch eine Spaltengruppe in einem einzelnen Ausdruck angeben, wird nicht unterstützt.  
  
 Weitere Informationen finden Sie in der [Aggregatfunktionsreferenz (Berichts-Generator und SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) und unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen (Berichts-Generator und SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Folgender Ausdruck ist ein Ausdruck, den Sie für die Eigenschaft **BackgroundColor** einer Detailzeile in einem Tablix-Datenbereich verwenden können, um die Farbe der Detailzeilen für jede Gruppe abzuwechseln, wobei stets mit Weiß begonnen wird.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken (Berichts-Generator und SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
