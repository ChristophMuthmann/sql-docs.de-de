---
title: In tabellarischen Modellen von Analysis Services unterstützten Datentypen | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0a58767c3365fcff285b51d4b69e6e0cb673358b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-types-supported-in-tabular-models"></a>Unterstützte Datentypen in tabellarischen Modellen
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  In diesem Artikel werden die Datentypen erläutert, die in tabellarischen Modellen verwendet werden können, und die implizite Konvertierung von Datentypen bei der Berechnung oder Verwendung von Daten in einer Data Analysis Expressions (DAX)-Formel beschrieben.  

  
##  <a name="bkmk_data_types"></a> In tabellarischen Modellen verwendete Datentypen  
Wenn Sie Daten importieren oder einen Wert in einer Formel verwenden, werden die Daten in einen der folgenden Datentypen konvertiert, auch wenn die ursprüngliche Datenquelle einen anderen Datentyp enthält. Werte, die sich aus Formeln ergeben, verwenden ebenfalls diese Datentypen.  
  
 Im Allgemeinen werden diese Datentypen implementiert, um genaue Berechnungen in berechneten Spalten zu ermöglichen. Die gleichen Einschränkungen gelten aus Konsistenzgründen auch für den Rest der Daten in Modellen.  
  
 Formate für Zahlen, Währungen, Datumsangaben und Uhrzeiten sollten dem Format des Gebietsschemas auf dem Client folgen, der für die Arbeit mit den Modelldaten verwendet wird. Sie können die Formatierungsoptionen im Modell verwenden, um die Darstellung des Werts zu bestimmen.  
  
||||  
|-|-|-|  
|**Datentyp im Modell**|**Datentyp in DAX**|**Beschreibung**|  
|Ganze Zahl|Ein ganzzahliger 64-Bit (acht Byte)-Wert*<br /><br /> Hinweis:<br />         DAX-Formeln unterstützen keine Datentypen, die zu klein für den kleinsten in der Beschreibung aufgeführten Wert sind.|Zahlen ohne Dezimalstellen. Ganze Zahlen können positiv oder negativ sein, aber müssen ganze Zahlen zwischen -9 223 372 036 854 775 808 (-2^63) und 9 223 372 036 854 775 807 (2^63-1) sein.|  
|Decimal Number|Eine reelle 64-Bit (acht Byte)-Zahl*<br /><br /> Hinweis:<br />         DAX-Formeln unterstützen keine Datentypen, die zu klein für den kleinsten in der Beschreibung aufgeführten Wert sind.|Reelle Zahlen sind Zahlen, die Dezimalstellen aufweisen können. Reelle Zahlen decken viele Werte ab:<br /><br /> Negative Werte von -1,79E +308 bis -2,23E -308<br /><br /> Null (0)<br /><br /> Positive Werte von 2,23E -308 bis -1,79E +308<br /><br /> Die Anzahl der relevanten Stellen wird jedoch auf siebzehn Dezimalstellen beschränkt.|  
|Boolean|Boolean|Entweder ein True oder ein False-Wert.|  
|Text|String|Eine Unicodezeichen-Datenzeichenfolge. Hierbei kann es sich um Zeichenfolgen, Zahlen oder Datumsangaben in einem Textformat dargestellt sein.|  
|Datum|Date/Time|Datumsangaben und Uhrzeiten in einer akzeptierten Form für die Darstellung von Datum und Uhrzeit.<br /><br /> Gültig sind alle Datumsangaben nach dem 1. März 1900.|  
|Währung|Währung|Der Währungsdatentyp lässt Werte zwischen -922 337 203 685 477,5808 und 922 337 203 685 477,5807 mit vier Dezimalstellen unveränderlicher Genauigkeit zu.|  
|–|Leer|Ein leerer Datentyp in DAX, der SQL-NULLEN darstellt und ersetzt. Sie können mit der BLANK-Funktion ein Leerzeichen erstellen und mit der logischen ISBLANK-Funktion nach Leerzeichen suchen.|  
  
 \* Wenn Sie versuchen, Daten zu importieren, die große numerische Werte verfügt, kann Import mit folgender Fehlermeldung fehl:  
  
 In-Memory-Datenbankfehler: die "\<Spaltenname >" Spalte der '\<Tabellenname > "Tabelle enthält einen Wert" 1. 7976931348623157E + 308", die nicht unterstützt wird. Der Vorgang wurde abgebrochen.  
  
 Dieser Fehler tritt auf, da der Modell-Designer diesen Wert zur Darstellung von Nullen verwendet. Die Werte in der folgenden Liste sind zum vorherigen erwähnten Nullwert synonym:  
  
||  
|-|  
|Wert|  
|9223372036854775807|  
|-9223372036854775808|  
|1,7976931348623158e+308|  
|2,2250738585072014e-308|  
  
 Entfernen Sie den Wert aus Ihren Daten, und wiederholen Sie den Importversuch.  
  
> [!NOTE]  
>  Sie können keine Elemente aus einer **varchar(max)** -Spalte importieren, die eine Zeichenfolgenlänge von mehr als 131.072 Zeichen enthält.  
  
### <a name="table-data-type"></a>Table (Datentyp)  
 Außerdem verwendet DAX einen *table* -Datentyp. Dieser Datentyp wird von DAX in vielen Funktionen verwendet, z. B. in Aggregationen und Zeitintelligenzberechnungen. Einige Funktionen erfordern einen Verweis auf eine Tabelle, während andere Funktionen eine Tabelle zurückgeben, die als Eingabe für andere Funktionen verwendet werden kann. In einigen Funktionen, die eine Tabelle als Eingabe erfordern, können Sie einen Ausdruck angeben, der eine Tabelle ergibt. Bei einigen Funktionen ist ein Verweis auf eine Basistabelle erforderlich. Informationen zu den Anforderungen bestimmter Funktionen finden Sie in der [DAX-Funktionsreferenz](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
##  <a name="bkmk_implicit"></a> Implizite und explizite datentypkonvertierungen in DAX-Formeln
  
 Jede DAX-Funktion verfügt über bestimmte Anforderungen im Hinblick auf die Datentypen, die als Eingaben und Ausgaben verwendet werden. Einige Funktionen erfordern z. B. ganze Zahlen für einige Argumente und Daten für andere, während für andere Funktionen Text oder Tabellen erforderlich sind.  
  
 Wenn die Daten in der Spalte, die Sie als Argument angeben, nicht mit dem von der Funktion erforderlichen Datentyp kompatibel ist, gibt DAX in vielen Fällen einen Fehler zurück. Allerdings versucht immer, wenn möglich DAX die Daten implizit in den erforderlichen Datentyp zu konvertieren. Beispiel:  
  
-   Sie können eine Zahl, z. B. "123", als Zeichenfolge eingeben. DAX analysiert die Zeichenfolge und versucht, ihn als Zahlendatentyp anzugeben.  
  
-   Sie können TRUE + 1 hinzufügen und als Ergebnis 2 abrufen, da TRUE implizit in die Zahl 1 konvertiert wird und der Vorgang 1+1 ausgeführt wird.  
  
-   Wenn Sie Werte in zwei Spalten hinzufügen und ein Wert als Text ("12") und der andere als Zahl (12) dargestellt wird, konvertiert DAX die Zeichenfolge implizit in eine Zahl und addiert diese dann zu einem Ergebnis in numerischer Form. Vom folgenden Ausdruck wird 44 zurückgegeben: = "22" + 22  
  
-   Wenn Sie zwei Zahlen verketten möchten, werden sie als Zeichenfolgen dargestellt und dann verkettet. Vom folgenden Ausdruck wird "1234" zurückgegeben: = 12 & 34  
  
 In der folgenden Tabelle werden die impliziten Datentypkonvertierungen zusammengefasst, die in Formeln ausgeführt werden. Im Allgemeinen verhält sich der Designer für semantische Modelle wie Microsoft Excel und führt implizite Konvertierungen aus, wann immer dies möglich und bei dem betreffenden Vorgang erforderlich ist.  
  
### <a name="table-of-implicit-data-conversions"></a>Tabelle mit impliziten datenkonvertierungen  
 Der ausgeführte Konvertierungstyp wird vom Operator bestimmt, der die erforderlichen Werte umwandelt, bevor der entsprechende Vorgang ausgeführt wird. In diesen Tabellen sind die Operatoren aufgeführt. Außerdem wird die Konvertierung angegeben, die bei den einzelnen Datentypen in der Spalte ausgeführt wird, wenn er dem Datentyp in der überschneidenden Zeile zugeordnet wird.  
  
> [!NOTE]  
>  Textdatentypen sind in diesen Tabellen nicht enthalten. Wenn eine Zahl, wie in einem Textformat, in einigen Fällen dargestellt wird versucht der Modell-Designer den Zahlentyp zu bestimmen und ihn als Zahl darzustellen.  
  
#### <a name="addition-"></a>Addition (+)  
  
||||||  
|-|-|-|-|-|  
|Operator (+)|INTEGER|Währung|real|Date/Time|  
|INTEGER|INTEGER|Währung|real|Date/Time|  
|CURRENCY|CURRENCY|CURRENCY|real|Date/Time|  
|real|real|real|real|Date/Time|  
|Date/Time|Date/Time|Date/Time|Date/Time|Date/Time|  
  
 Wenn beispielsweise eine reelle Zahl bei einer Addition in Verbindung mit Währungsdaten verwendet wird, werden beide Werte in REAL konvertiert, und das Ergebnis wird als REAL zurückgegeben.  
  
#### <a name="subtraction--"></a>Subtraktion (-)  
 Klicken Sie in der folgenden Tabelle ist die Zeilenüberschrift der Minuend (linke Seite), und die Spaltenüberschrift ist der Subtrahend (rechte Seite):  
  
||||||  
|-|-|-|-|-|  
|Operator (-)|INTEGER|Währung|real|Date/Time|  
|INTEGER|INTEGER|Währung|real|real|  
|CURRENCY|CURRENCY|CURRENCY|real|real|  
|real|real|real|real|real|  
|Date/Time|Date/Time|Date/Time|Date/Time|Date/Time|  
  
 Wenn beispielsweise ein Datum bei einer Subtraktion mit einem beliebigen anderen Datentyp verwendet wird, werden beide Werte in Datumsangaben konvertiert, und der Rückgabewert ist ebenfalls ein Datum.  
  
> [!NOTE]  
>  Tabellarische Modelle unterstützen auch den unären Operator "-" (negativ). Dieser Operator ändert den Datentyp des Operanden jedoch nicht.  
  
#### <a name="multiplication-"></a>Multiplikation (*)  
  
||||||  
|-|-|-|-|-|  
|Operator (*)|INTEGER|Währung|real|Date/Time|  
|INTEGER|INTEGER|Währung|real|INTEGER|  
|CURRENCY|CURRENCY|real|CURRENCY|CURRENCY|  
|real|real|CURRENCY|real|real|  
  
 Wenn beispielsweise eine ganze Zahl bei einer Multiplikation mit einer reellen Zahl kombiniert wird, werden beide Zahlen in reelle Zahlen konvertiert, und der Rückgabewert ist ebenfalls REAL.  
  
#### <a name="division-"></a>Division (/)  
 In der folgenden Tabelle ist die Zeilenüberschrift der Zähler, und die Spaltenüberschrift ist der Nenner.  
  
||||||  
|-|-|-|-|-|  
|Operator (/)<br /><br /> (Zeile/Spalte)|INTEGER|Währung|real|Date/Time|  
|INTEGER|real|CURRENCY|real|real|  
|CURRENCY|CURRENCY|real|CURRENCY|real|  
|real|real|real|real|real|  
|Date/Time|real|real|real|real|  
  
 Wenn beispielsweise eine ganze Zahl bei einer Division mit einem Währungswert kombiniert wird, werden beide Werte in reelle Zahlen konvertiert, und das Ergebnis ist ebenfalls ein reeller Wert.  
  
#### <a name="comparison-operators"></a>Vergleichsoperatoren  
Es wird nur ein eingeschränkter Satz von gemischten Datentyp Kombinationen für Vergleichsvorgänge unterstützt. Weitere Informationen finden Sie unter [DAX-Operator (Referenz)](https://msdn.microsoft.com/library/ee634237.aspx).  
  
## <a name="bkmk_hand_blanks"></a> Behandlung von Leerzeichen, leeren Zeichenfolgen und Nullwerten  
 In der folgenden Tabelle werden die Unterschiede zwischen DAX und Microsoft Excel, bei der Datenerfassung Behandlung von Leerzeichen zusammengefasst:  
  
||||  
|-|-|-|  
|expression|DAX|Excel|  
|BLANK + BLANK|BLANK|0 (Null)|  
|BLANK +5|5|5|  
|BLANK * 5|BLANK|0 (Null)|  
|5/BLANK|Unendlich|Fehler|  
|0/BLANK|NaN|Fehler|  
|BLANK/BLANK|Leer|Fehler|  
|FALSE OR BLANK|FALSE|FALSE|  
|FALSE AND BLANK|FALSE|FALSE|  
|TRUE OR BLANK|TRUE|TRUE|  
|TRUE AND BLANK|FALSE|TRUE|  
|BLANK OR BLANK|BLANK|Fehler|  
|BLANK AND BLANK|BLANK|Fehler|  
  
 Informationen zur Behandlung von Leerzeichen durch eine bestimmte Funktion oder einen Operator finden Sie in den einzelnen Themen zu den verschiedenen DAX-Funktionen im Abschnitt [DAX-Funktionsreferenz](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
