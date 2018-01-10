---
title: Previous-Funktion (Berichts-Generator und SSRS) | Microsoft-Dokumentation
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
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 3b7d1ebc6643cea879bf60d978ba38b844d46f03
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="report-builder-functions---previous-function"></a>Funktionen des Berichts-Generators: Previous-Funktion
  Gibt den Wert oder den angegebenen Aggregatwert für die vorherige Instanz eines Elements innerhalb des angegebenen Bereichs zurück.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Previous(expression, scope)  
```  
  
#### <a name="parameters"></a>Parameter  
 *expression*  
 (**Variant** oder **Binär**) Der Ausdruck, mit dem die Daten identifiziert werden und für den der vorherige Wert abgerufen wird, z.B. `Fields!Fieldname.Value` oder `Sum(Fields!Fieldname.Value)`.  
  
 *Bereich*  
 (**Zeichenfolge**) Optional. Der Name einer Gruppe oder eines Datenbereichs oder NULL (**Nothing** in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), der den Bereich angibt, aus dem der durch *expression*angegebene vorherige Wert abgerufen wird.  
  
## <a name="return-type"></a>Rückgabetyp  
 Gibt einen **Variant** - oder **Binary**-Wert zurück.  
  
## <a name="remarks"></a>Remarks  
 Die **Previous** -Funktion gibt den vorherigen Wert für den Ausdruck zurück, der in dem angegebenen Bereich ausgewertet wird, nachdem die Sortierfunktionen und Filter angewendet wurden.  
  
 Wenn *expression* kein Aggregat enthält, wird die **Previous** -Funktion standardmäßig auf den aktuellen Bereich für das Berichtselement festgelegt.  
  
 Verwenden Sie in einer Detailgruppe **Previous** , um den Wert eines Feldverweises in der vorherigen Instanz der Detailzeile anzugeben.  
  
> [!NOTE]  
>  Von der **Previous** -Funktion werden nur Feldverweise in der Detailgruppe unterstützt. Beispielsweise werden in einem Textfeld in der Detailgruppe durch `=Previous(Fields!Quantity.Value)` die Daten für das Feld `Quantity` aus der vorherigen Zeile zurückgegeben. In der ersten Zeile gibt dieser Ausdruck NULL zurück (**Nothing** in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]).  
  
 Wenn *expression* eine Aggregatfunktion enthält, die einen Standardbereich verwendet, aggregiert **Previous** die Daten innerhalb der vorherigen Instanz des im Aggregatfunktionsaufruf angegebenen Bereichs.  
  
 Enthält *expression* eine Aggregatfunktion, die nicht den Standardbereich angibt, muss es sich beim *scope* -Parameter für die **Previous** -Funktion um einen enthaltenen Bereich des im Aggregatfunktionsaufruf angegebenen Bereichs handeln.  
  
 Die Funktionen **Level**, **InScope**, **Aggregat** und **Previous** können nicht im *expression*-Parameter verwendet werden. Die Angabe des *recursive* -Parameters für eine Aggregatfunktion wird nicht unterstützt.  
  
 Weitere Informationen finden Sie in der [Aggregatfunktionsreferenz (Berichts-Generator und SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) und unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen (Berichts-Generator und SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="description"></a>Description  
 Das folgende Codebeispiel stellt bei Angabe in der Standarddatenzeile eines Datenbereichs den Wert für das Feld `LineTotal` in der vorherigen Zeile bereit.  
  
### <a name="code"></a>Code  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### <a name="description"></a>Description  
 Das folgende Codebeispiel zeigt einen Ausdruck, der die Summe der Umsätze an einem bestimmten Tag des Monats und den vorherigen Wert für den Tag des Monats in einem vorhergehenden Jahr berechnet. Der Ausdruck wird einer Zelle in einer Zeile, die zur untergeordneten Gruppe `GroupbyDay`gehört, hinzugefügt. Die übergeordnete Gruppe ist `GroupbyMonth`, deren übergeordnete Gruppe wiederum `GroupbyYear`ist. Der Ausdruck zeigt die Ergebnisse für GroupbyDay (Standardbereich) und anschließend für `GroupbyYear` (der übergeordneten Gruppe der übergeordneten Gruppe `GroupbyMonth`) an.  
  
 Angenommen, in einem Datenbereich verfügt eine übergeordnete Gruppe namens `Year`über die untergeordnete Gruppe `Month`, der wiederum die Gruppe `Day` untergeordnet ist (drei geschachtelte Ebenen). Der Ausdruck `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` in einer mit der Gruppe `Day` verknüpften Zeile gibt den Umsatzwert für denselben Tag und Monat des vorherigen Jahrs zurück.  
  
### <a name="code"></a>Code  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken (Berichts-Generator und SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
