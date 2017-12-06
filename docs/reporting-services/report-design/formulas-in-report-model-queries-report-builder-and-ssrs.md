---
title: Formeln in Berichtsmodellabfragen (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
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
f1_keywords: "10151"
ms.assetid: fbf68c59-7afc-4afe-bfcd-40ce84629af0
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5c0d653cac98162a50b04c016a228f04843cf643
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="formulas-in-report-model-queries-report-builder-and-ssrs"></a>Formeln in Berichtsmodellabfragen (Berichts-Generator und SSRS)
  Formeln sind Berechnungen, die für Werte in einem Bericht ausgeführt werden, die ein Berichtsmodell als Datenquelle verwenden. Formel werden im **Dialogfeld "Formeln definieren"** im Berichtsmodell-Abfrage-Designer definiert, wenn Sie eine Abfrage für eine Berichtsmodell-Datenquelle definieren. Eine Formel kann Funktionen, Operatoren, Konstanten und Verweise auf Felder oder Entitäten enthalten. Mithilfe von Formeln können Sie numerische und Textdaten kombinieren, aggregieren, filtern und auswerten. Sie können Formeln erstellen und als neue Felder speichern oder die Formeln vorhandener Felder ändern.  
  
 Formeln sind keine RDL-Ausdrücke und beginnen nicht mit einem Gleichheitszeichen (=). Weitere Informationen zu RDL-Ausdrücken finden Sie unter [Ausdrücke (Berichts-Generator und SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 Formeln können folgendermaßen aussehen:  
  
-   **Sum Line Total**  
  
-   6+12  
  
-   **SUM**(**IF**(**Finished Goods Flag**, "Finished", "Unfinished"))  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="references"></a>References  
 Ein Verweis ist ein Feldname. Dabei kann es sich um einen vorhandenen Feldnamen in der Entität handeln oder einen berechneten Feldnamen, den Sie erstellt und zur Feldliste hinzugefügt haben. Der Verweis informiert den Berichts-Generator, wo die Werte bzw. Daten, die Sie in einer Formel verwenden möchten, zu finden sind. Sie können in einer Formel auf Felder innerhalb der Kontextentität oder auf Felder in anderen Entitäten verweisen oder den Wert aus einem Feld in mehreren Formeln verwenden.  
  
 Wenn Sie Verweise verwenden, führt der Berichts-Verarbeiter die Formel für jeden Wert in dem Feld aus. Beispiel: Ein Feld enthält die jährlichen Gesamtumsätze für die vergangenen fünf Jahre. Das Feld enthält fünf Werte, die jeweils den Gesamtumsatz eines bestimmten Jahrs darstellen. Wenn die Formel einen Verweis auf dieses Feld enthält, berechnet die Formel den neuen Wert anhand der einzelnen Werte.  
  
## <a name="operators"></a>Operatoren  
 Operatoren geben den Typ der Berechnung an, die Sie für die Werte einer Formel ausführen möchten. Es gibt drei verschiedene Typen von Berechnungsoperatoren: arithmetische Operatoren, Vergleichsoperatoren und Textoperatoren. Operatoren werden mithilfe von Symbolen angegeben, z. B. durch das Pluszeichen (+).  
  
 **Arithmetische Operatoren.** Arithmetische Operatoren führen grundlegende mathematische Operationen wie Additionen, Subtraktionen oder Multiplikationen durch, kombinieren Zahlen und führen zu numerischen Ergebnissen.  
  
 **Vergleichsoperatoren.** Mithilfe von Vergleichsoperatoren können Sie zwei Werte vergleichen. Werden zwei Werte mithilfe dieser Operatoren verglichen, ist das Ergebnis ein logischer Wert, und zwar entweder TRUE oder FALSE.  
  
 **Textverkettungsoperator.** Verwenden Sie das kaufmännische Und-Zeichen (&) zum Verknüpfen bzw. Verketten einer oder mehrerer Textzeichenfolgen, um ein einzelnes Stück Text zu erzeugen.  
  
##  <a name="Constants"></a> Konstanten  
 Eine Konstante ist ein Wert, der nicht berechnet wird und sich somit nicht ändert. Berichts-Generator verwendet die folgenden Konstanten: **True**, **False**und **Empty**. Diese Konstanten werden zur Auswertung boolescher Felder verwendet. Beispiel: Es gibt ein Feld mit dem Namen IsDiscontinued. Die einzigen gültigen Werte für dieses Feld sind True, False oder Empty (" ").  
  
##  <a name="Functions"></a> Funktionen  
 Funktionen sind vordefinierte Formeln, die Berechnungen mithilfe bestimmter Werte ausführen. Diese so genannten *Argumente*werden in einer bestimmten Reihenfolge angegeben. Bei Argumenten kann es sich um Literalwerte oder Felder oder Kombinationen aus beiden handeln. Werden Felder in Formeln verwendet, stellt der Feldname die jeweilige Instanz des Felds dar. Handelt es sich bei dem Argument um einen Literalwert, müssen Sie u. U. mithilfe bestimmter Zeichen darauf hinweisen, dass es sich bei dem Argument um einen Literalwert handelt.  
  
 Mithilfe von Funktionen können einfache oder komplexe Berechnungen ausgeführt werden. Die Struktur einer Funktion beginnt mit dem Funktionsnamen, gefolgt von einer öffnenden Klammer, den Argumenten für die Funktion, die durch Kommas voneinander getrennt sind, und einer schließenden Klammer.  
  
 ![Beispiel für eine Funktion](../../reporting-services/report-design/media/functionexample.gif "An example of a function")  
  
 Argumente können aus Feldverweisen, Zahlen, Text und logischen Werten wie **TRUE** oder **FALSE**bestehen. Argumente können auch aus Konstanten, Formeln oder anderen Funktionen bestehen. Die Argumente, die Sie eingeben, müssen einen gültigen Wert für das jeweilige Argument ergeben. Wenn in der Formel z. B. zwei ganze Zahlen multipliziert werden, kann das Ergebnis keine Textzeichenfolge sein.  
  
 Der Berichts-Generator enthält die folgenden neun Kategorien von häufig verwendeten Funktionen:  
  
|||  
|-|-|  
|Aggregatfunktionen|**AVG**, **COUNT**, **COUNTDISTINCT**, **MAX**, **MIN**, **STDEV**, **STDEVP**, **SUM**, **VAR**, **VARP**|  
|Bedingte Funktionen|**IF**, **IN**, **SWITCH**|  
|Konvertierungsfunktionen|**INT**, **DECIMAL**, **FLOAT**, **TEXT**|  
|Datums- und Uhrzeitfunktionen|**DATE**, **DATEADD**, **DATEDIFF**, **DATETIME**, **DATEONLY**, **DAY**, **DAYOFWEEK**, **DAYOFYEAR**, **HOUR**, **MINUTE**, **MONTH**, **NOW**, **QUARTER**, **SECOND**, **TIMEONLY**, **TODAY**, **WEEK**, **YEAR**|  
|Informationsfunktionen|**GETUSERCULTURE**, **GETUSERID**|  
|Logische Funktionen|**AND**, **NOT**, **OR**|  
|Mathematische Funktionen|**MOD**, **ROUND**, **TRUNC**|  
|Operatoren|Addition (+), Division (/), Gleich (=), Potenzierung (^), Größer als (>), Größer als oder gleich (>=), Kleiner als (<), Kleiner als oder gleich (<=), Multiplikation (*), Negation (-), Ungleich (<>), Subtraktion (-)|  
|Textfunktionen|**CONCAT**, **FIND**, **LEFT**, **LENGTH**, **LOWER**, **LTRIM**, **REPLACE**, **RIGHT**, **RTRIM**, **SUBSTRING**, **UPPER**|  
  
  
