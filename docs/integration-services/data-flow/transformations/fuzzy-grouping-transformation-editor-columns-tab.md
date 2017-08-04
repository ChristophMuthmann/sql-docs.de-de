---
title: "Für die Fuzzysuche Transformations-Editor (Registerkarte \"Spalten\") | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.fuzzygroupingtransformation.columns.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6040dde176f4f92674fd267388ff28a08499137b
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>Transformations-Editor für Fuzzygruppierung (Registerkarte Spalten)
  Mithilfe der Registerkarte **Spalten** des Dialogfelds **Transformations-Editor für Fuzzygruppierung** können Sie die Spalten angeben, die zum Gruppieren von Zeilen mit doppelten Werten verwendet werden sollen.  
  
 Weitere Informationen zur Transformation für Fuzzygruppierung finden Sie unter [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>enthalten  
 **Verfügbare Eingabespalten**  
 Wählen Sie aus dieser Liste die Eingabespalten, mit denen Zeilen mit doppelten Werten gruppiert werden sollen.  
  
 **Name**  
 Zeigt die Namen der verfügbaren Eingabespalten an.  
  
 **Pass-Through**  
 Wählen Sie aus, ob die Eingabespalte in der Ausgabe der Transformation eingeschlossen sein soll. Alle für die Gruppierung verwendeten Spalten werden automatisch in die Ausgabe kopiert. Sie können weitere Spalten einschließen, indem Sie diese Spalten auswählen.  
  
 **Eingabespalte**  
 Wählen Sie eine der zu einem früheren Zeitpunkt aus der Liste **Verfügbare Eingabespalten** ausgewählten Eingabespalten aus.  
  
 **Ausgabealias**  
 Geben Sie einen beschreibenden Namen für die entsprechende Ausgabespalte ein. Standardmäßig stimmt der Name der Ausgabespalte mit dem Namen der Eingabespalte überein.  
  
 **Gruppenausgabealias**  
 Geben Sie einen beschreibenden Namen für die Spalte ein, die den kanonischen Wert für die gruppierten Duplikate enthalten soll. Der Standardname dieser Ausgabespalte entspricht dem Namen der Eingabespalte mit dem Anhang _clean.  
  
 **Übereinstimmungstyp**  
 Wählen Sie genaue oder Fuzzyübereinstimmungen aus. Zeilen werden als Duplikate angesehen, wenn Sie über alle Spalten hinweg eine genügend große Ähnlichkeit mit dem Typ einer Fuzzyübereinstimmung haben. Wenn Sie für bestimmte Spalten auch die genaue Übereinstimmung angeben, werden in den Spalten mit den genauen Übereinstimmungen nur Zeilen mit identischen Werten als mögliche Duplikate angesehen. Wenn Sie also wissen, dass eine bestimmte Spalte keine Fehler oder Inkonsistenzen enthält, können Sie für diese Spalte die genaue Übereinstimmung angeben, um die Genauigkeit der Fuzzyübereinstimmungen für andere Spalten zu erhöhen.  
  
 **Minimale Ähnlichkeit**  
 Legen Sie mithilfe des Schiebereglers den Schwellenwert für Ähnlichkeit auf Joinebene fest. Je näher der Wert an 1 liegt, desto stärker muss die Ähnlichkeit zwischen Suchwert und Quellwert sein, um als Übereinstimmung zu gelten. Durch eine Erhöhung des Schwellenwertes kann die Geschwindigkeit beim Abgleich erhöht werden, weil als Kandidaten dann weniger Datensätze berücksichtigt werden müssen.  
  
 **Ähnlichkeitsausgabealias**  
 Geben Sie den Namen für eine Ausgabespalte an, die die Ähnlichkeitsergebnisse für den ausgewählten Join enthält. Wenn Sie diesen Wert nicht angeben, wird die Ausgabespalte nicht erstellt.  
  
 **Zahlen**  
 Gibt die Bedeutung führender und nachfolgender Zahlen beim Vergleichen der Spaltendaten an. Wenn beispielsweise führende Zahlen von Bedeutung sind, wird "123 Main Street" nicht mit "456 Main Street" gruppiert.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Neither**|Weder führende noch nachfolgende Zahlen sind von Bedeutung.|  
|**Leading**|Nur führende Zahlen sind von Bedeutung.|  
|**Trailing**|Nur nachfolgende Zahlen sind von Bedeutung.|  
|**LeadingAndTrailing**|Sowohl führende als auch nachfolgende Zahlen sind von Bedeutung.|  
  
 **Vergleichsflags**  
 Weitere Informationen zu den Optionen für das Vergleichen von Zeichenfolgen finden Sie unter [Vergleichen von Zeichenfolgendaten](../../../integration-services/data-flow/comparing-string-data.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Identifizieren Sie ähnlicher Datenzeilen mithilfe der Transformation für Fuzzygruppierung](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
