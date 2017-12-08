---
title: "LANGUAGE und FORMAT_STRING für FORMATTED_VALUE | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7534ff5f-954e-47d4-a2ed-4b5b8ccb30e6
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 757e4e6dd284117d0e686e7908c7c71e1ba28636
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-cell-properties---formattedvalue-property"></a>MDX-Cell Properties - FORMATTED_VALUE-Eigenschaft
  Die FORMATTED_VALUE-Eigenschaft basiert auf den Interaktionen der Eigenschaften VALUE, FORMAT_STRING und LANGUAGE der Zelle. In diesem Thema wird erläutert, wie diese Eigenschaften beim Erstellen der FORMATTED_VALUE-Eigenschaft interagieren.  
  
## <a name="value-formatstring-language-properties"></a>Eigenschaften VALUE, FORMAT_STRING und LANGUAGE  
 In der folgenden Tabelle wird das Wesen dieser Eigenschaften beschrieben, um ihre kombinierte Verwendung zu erklären.  
  
 VALUE  
 Der unformatierte Wert der Zelle.  
  
 FORMAT_STRING  
 Die Formatierungsvorlage, die für den Wert der Zelle übernommen werden soll, um die FORMATTED_VALUE-Eigenschaft zu generieren  
  
 LANGUAGE  
 Die Gebietsschemaspezifikation, die zusätzlich zu FORMAT_STRING übernommen werden soll, um eine lokalisierte Version von FORMATTED_VALUE zu generieren  
  
## <a name="formattedvalue-constructed"></a>Erstellte FORMATTED_VALUE-Eigenschaft  
 Die FORMATTED_VALUE-Eigenschaft wird mithilfe des Werts aus der VALUE-Eigenschaft und durch Anwenden der Formatvorlage erstellt, die in der FORMAT_STRING-Eigenschaft für diesen Wert angegeben wird. Wenn der Formatierungswert ein **benanntes Formatierungsliteral** ist, ändert die Spezifikation der LANGUAGE-Eigenschaft darüber hinaus die Ausgabe von FORMAT_STRING, sodass diese der Sprachverwendung für die benannte Formatierung folgt. Benannte Formatierungsliterale sind jeweils so definiert, dass eine Lokalisierung möglich ist. `"General Date"` ist beispielsweise eine Spezifikation, die lokalisiert werden kann, im Gegensatz zur Vorlage `"YYYY-MM-DD hh:nn:ss",` , die angibt, dass das Datum ungeachtet der Sprachspezifikation entsprechend der Definition durch die Vorlage dargestellt werden soll.  
  
 Wenn ein Konflikt zwischen der FORMAT_STRING-Vorlage und der LANGUAGE-Spezifikation vorliegt, überschreibt die FORMAT_STRING-Vorlage die LANGUAGE-Spezifikation. Wenn beispielsweise FORMAT_STRING="$ #0" und LANGUAGE=1034 (Spanien) sowie VALUE=123.456, dann gilt FORMATTED_VALUE="$ 123" anstelle von FORMATTED_VALUE="€ 123". Das erwartete Format ist Euro, da der Wert der Formatvorlage die angegebene Sprache überschreibt.  
  
### <a name="examples"></a>Beispiele  
 In den folgenden Beispielen werden die Ausgaben veranschaulicht, die bei der Verwendung von LANGUAGE in Verbindung mit FORMAT_STRING erhalten werden.  
  
 Im ersten Beispiel wird das Formatieren numerischer Werte erläutert, während im zweiten Beispiel das Formatieren von Datums- und Uhrzeitwerten erklärt wird.  
  
 Für jedes Beispiel wird der MDX-Code (Multidimensional Expressions) angegeben.  
  
 `with`  
  
 `member measures.A as 5040, FORMAT_STRING="Currency"`  
  
 `member measures.B as measures.A, LANGUAGE=1034`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="$#,##0.00"`  
  
 `member measures.D as measures.A, FORMAT_STRING="Scientific"`  
  
 `member measures.E as measures.A, LANGUAGE=1034 , FORMAT_STRING="Scientific"`  
  
 `member measures.F as 0.5040, FORMAT_STRING="Percent"`  
  
 `member measures.G as measures.F, LANGUAGE=1034`  
  
 `member measures.H as 0, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.I as 59, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.J as 0, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `member measures.K as -312, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F, measures.G, measures.H, measures.I, measures.J, measures.K} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 Damit werden die folgenden Ergebnisse erhalten, die beim Ausführen der obigen MSX-Abfrage mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] über einen Server und einen Client mit dem Gebietsschema 1033 transponiert wurden:  
  
|Member|FORMATTED_VALUE|Erklärung|  
|------------|----------------------|-----------------|  
|A|$5,040.00|FORMAT_STRING wird auf `Currency` festgelegt, und LANGUAGE ist `1033`(geerbt vom Wert des Systemgebietsschemas).|  
|B|€5.040,00|FORMAT_STRING wird auf `Currency` festgelegt (geerbt von A), und LANGUAGE wird explizit auf `1034` (Spanien) festgelegt, wodurch das Euro-Symbol, das abweichende Dezimaltrennzeichen und das abweichende Tausendertrennzeichen erhalten werden.|  
|C|$5.040,00|FORMAT_STRING wird auf `$#,##0.00` (eine Überschreibung von Currency) von A festgelegt, und LANGUAGE wird explizit auf `1034` (Spanien) festgelegt. Da die FORMAT_STRING-Eigenschaft das Währungssymbol explizit auf $ festgelegt hat, wird der FORMATTED_VALUE mit dem Dollarzeichen dargestellt. Da jedoch `.` (Punkt) und `,` (Komma) Platzhalter für Dezimaltrennzeichen und Tausendertrennzeichen sind, wird entsprechend der Sprachspezifikation eine Ausgabe generiert, in der Dezimal- und Tausendertrennzeichen lokalisiert sind.|  
|D|5.04E+03|FORMAT_STRING wird auf `Scientific` und LANGUAGE auf `1033`(geerbt vom Wert des Systemgebietsschemas) festgelegt, dadurch wird `.` (Punkt) als Dezimaltrennzeichen verwendet.|  
|E|5,04E+03|FORMAT_STRING wird auf `Scientific` und LANGUAGE wird explizit auf `1034,` festgelegt. Dadurch wird `,` (Komma) als Dezimaltrennzeichen erhalten.|  
|V|50.40%|FORMAT_STRING wird auf `Percent` und LANGUAGE auf `1033`(geerbt vom Wert des Systemgebietsschemas) festgelegt, dadurch wird `.` (Punkt) als Dezimaltrennzeichen verwendet.<br /><br /> Beachten Sie, dass VALUE von 5040 in 0.5040 geändert wurde.|  
|G|50,40%|FORMAT_STRING wird auf `Percent`(geerbt von F) und LANGUAGE wird explizit auf `1034` festgelegt, sodass `,` (Komma) als Dezimaltrennzeichen verwendet wird.<br /><br /> Beachten Sie, dass VALUE vom Wert von F geerbt wurde.|  
|H|Nein|FORMAT_STRING wird auf `YES/NO`, VALUE auf 0 und LANGUAGE explizit auf `1034`festgelegt. Da im Englischen und im Spanischen kein Unterschied zwischen NO besteht, liegt für den Benutzer auch kein Unterschied im FORMATTED_VALUE vor.|  
|I|SI|FORMAT_STRING wird auf `YES/NO`, VALUE auf 59 und LANGUAGE explizit auf `1034`festgelegt. Entsprechend der Definition für YES/NO-Formatierungen ist jeder Wert ungleich null (0) gleich YES, und da LANGUAGE auf Spanisch festgelegt ist, ist FORMATTED_VALUE gleich SI.|  
|J|Desactivado|FORMAT_STRING wird auf `ON/OFF`, VALUE auf 0 und LANGUAGE explizit auf `1034`festgelegt. Entsprechend der Definition für ON/OFF-Formatierungen ist jeder Wert gleich null (0) gleich OFF, und da LANGUAGE auf Spanisch festgelegt ist, ist FORMATTED_VALUE gleich „Desactivado“.|  
|K|Activado|FORMAT_STRING wird auf `ON/OFF`, VALUE auf -312 und LANGUAGE explizit auf `1034`festgelegt. Entsprechend der Definition für ON/OFF-Formatierungen ist jeder Wert ungleich null (0) gleich ON, und da LANGUAGE auf Spanisch festgelegt ist, ist FORMATTED_VALUE gleich Activado.|  
  
 `with`  
  
 `member measures.A as 'CDate("1959-03-12 06:30")'`  
  
 `member measures.B as measures.A, FORMAT_STRING="Long Date"`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="General Date"`  
  
 `member measures.D as measures.A, LANGUAGE=1034, FORMAT_STRING="Long Date"`  
  
 `member measures.E as measures.A, LANGUAGE=1041 , FORMAT_STRING="General Date"`  
  
 `member measures.F as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Date"`  
  
 `member measures.G as measures.A, FORMAT_STRING="Long Time"`  
  
 `member measures.H as measures.A, FORMAT_STRING="Short Time"`  
  
 `member measures.I as measures.A, LANGUAGE=1034 , FORMAT_STRING="Long Time"`  
  
 `member measures.J as measures.A, LANGUAGE=1034 , FORMAT_STRING="Short Time"`  
  
 `member measures.K as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Time"`  
  
 `member measures.L as measures.A, LANGUAGE=1041 , FORMAT_STRING="Short Time"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F`  
  
 `, measures.G, measures.H, measures.I, measures.J, measures.K, measures.L} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 Damit werden die folgenden Ergebnisse erhalten, die beim Ausführen der obigen MSX-Abfrage mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] über einen Server und einen Client mit dem Gebietsschema 1033 transponiert wurden:  
  
|Member|FORMATTED_VALUE|Erklärung|  
|------------|----------------------|-----------------|  
|A|3/12/1959 6:30:00 AM|FORMAT_STRING wird durch den CDate()-Ausdruck implizit auf `General Date` festgelegt, und LANGUAGE ist `1033` (Englisch), geerbt vom Wert des Systemgebietsschemas.|  
|B|Thursday, March 12, 1959|FORMAT_STRING wird explizit auf `Long Date` festgelegt, und LANGUAGE ist `1033` (geerbt vom Wert des Systemgebietsschemas).|  
|C|12/03/1959 6:30:00|FORMAT_STRING wird explizit auf `General Date` festgelegt, und LANGUAGE ist explizit `1034` (Spanisch).<br /><br /> Beachten Sie, dass Monat und Tag im Unterschied zur US-Formatierung vertauscht sind.|  
|D|jueves, 12 de marzo de 1959|FORMAT_STRING wird explizit auf `Long Date` festgelegt, und LANGUAGE ist explizit `1034` (Spanisch).<br /><br /> Beachten Sie, dass Monat und Wochentag in Spanisch angegeben werden.|  
|E|1959/03/12 6:30:00|FORMAT_STRING wird explizit auf `General Date` festgelegt, und LANGUAGE ist explizit `1041` (Japanisch).<br /><br /> Beachten Sie, dass das Datum jetzt im Format Jahr/Monat/Tag Stunde:Minute:Sekunde angegeben wird.|  
|V|1959年3月12日|FORMAT_STRING wird explizit auf `Long Date` festgelegt, und LANGUAGE ist explizit `1041` (Japanisch).|  
|G|6:30:00 AM|FORMAT_STRING wird explizit auf `Long Time` festgelegt, und LANGUAGE ist `1033` (Englisch), geerbt vom Wert des Systemgebietsschemas.|  
|H|06:30|FORMAT_STRING wird explizit auf `Short Time` festgelegt, und LANGUAGE ist `1033` (Englisch), geerbt vom Wert des Systemgebietsschemas.|  
|I|6:30:00|FORMAT_STRING wird explizit auf `Long Time` und LANGUAGE explizit auf `1034` (Spanisch) festgelegt.|  
|J|06:30|FORMAT_STRING wird explizit auf `Short Time` und LANGUAGE explizit auf `1034` (Spanisch) festgelegt.|  
|K|6:30:00|FORMAT_STRING wird explizit auf `Long Time` und LANGUAGE explizit auf `1041` (Japanisch) festgelegt.|  
|L|06:30|FORMAT_STRING wird explizit auf `Short Time` und LANGUAGE explizit auf `1041` (Japanisch) festgelegt.|  
  
## <a name="see-also"></a>Siehe auch  
 [FORMAT_STRING-Inhalt &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [Verwenden von Zelleigenschaften &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [Erstellen und Verwenden von Eigenschaftswerten &#40; MDX &#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)   
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
