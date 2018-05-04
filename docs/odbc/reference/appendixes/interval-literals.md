---
title: Intervall Literale | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval literals [ODBC]
- interval data type [ODBC], literals
ms.assetid: f9e6c3c7-4f98-483f-89d8-ebc5680f021b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e86666c4b956b0f926644f0470d7bdf6e8d8dbff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="interval-literals"></a>Intervall-Literale
ODBC erfordert, dass alle Treiber die Konvertierung von Datentyp SQL_CHAR oder SQL_VARCHAR alle C-Intervall-Datentypen unterstützt. Wenn die zugrunde liegenden Datenquelle Interval-Datentypen nicht unterstützt, allerdings muss der Treiber das richtige Format des Werts im Feld SQL_CHAR kennen, um diese Konvertierungen zu unterstützen. Entsprechend muss ODBC an, dass alle ODBC C Typ SQL_CHAR oder SQL_VARCHAR, konvertiert werden, damit ein Treiber, in welchem Format ein Intervall, in das Zeichenfeld gespeichert wissen muss haben soll. Dieser Abschnitt beschreibt die Syntax für Literale für Intervall, das der Treiber-Writer verwenden, um die Felder SQL_CHAR während der Konvertierung in bzw. aus C-Intervalldatentypen überprüfen muss.  
  
> [!NOTE]  
>  Die vollständige BNF-Syntax für Literale Intervall wird angezeigt, in dem Abschnitt [Intervall Literal Syntax](../../../odbc/reference/appendixes/interval-literal-syntax.md) in Anhang C: SQL-Grammatik.  
  
 Um Intervall Literale nicht als Teil einer SQL­Anweisung übergeben, wird eine Escape-Klausel-Syntax für Literale Intervall definiert. Weitere Informationen finden Sie unter [Date, Time und Timestamp-Literale](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Ein literal Intervall weist das Format:  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 wobei "Intervall" gibt an, dass die Zeichenliterale ein Intervall. Die Anmeldung kann entweder plus oder minus; Es befindet sich außerhalb der Interval-Zeichenfolge und ist optional.  
  
 Der Qualifizierer Intervall kann entweder ein einzelnes Datetime-Feld sein oder bestehen aus zwei Datetime-Feldern im Formular: \< *führende Feld*> TO \< *nachfolgende Feld*>.  
  
-   Wenn das Intervall aus einem einzelnen Feld besteht, kann das einzelne Feld ein nicht-Sekunden-Feld, die möglicherweise durch eine optionale führende Genauigkeit in Klammern begleitet werden. Das Feld für die einzelnen "DateTime" kann auch ein zweites Feld sein, das von der optionale führende Genauigkeit, die optionale-Genauigkeit in Sekundenbruchteilen in Klammern oder beides begleitet werden kann. Wenn eine führende Genauigkeit und einer Genauigkeit von Bruchteilen von Sekunden für ein Sekundenfeld vorhanden sind, werden sie durch Kommas getrennt. Wenn der Wert im Sekundenfeld eine Genauigkeit in Sekundenbruchteilen verfügt, muss sie auch eine führende Genauigkeit verfügen.  
  
-   Wenn das Intervall der führende und nachfolgende Felder besteht, ist das führende Feld ein nicht-Sekunden-Feld, das die Genauigkeit für anführenden Intervallwert Feld in Klammern beigefügt werden kann. Das nachfolgende Feld kann ein nicht-Sekunden-Feld oder ein zweites Feld, das von einer Genauigkeit in Sekundenbruchteilen Intervall in Klammern begleitet werden kann.  
  
 Die Intervall-Zeichenfolge in *Wert* in einfache Anführungszeichen eingeschlossen ist. Sie können ein Jahr-Monat-Literal oder ein Tag-Time-Literal sein. Das Format der Zeichenfolge in *Wert* richtet sich nach den folgenden Regeln:  
  
-   Die Zeichenfolge enthält einen decimal-Wert für jedes Feld, das durch impliziert ist die \< *Intervall* *Qualifizierer*>.  
  
-   Wenn die Genauigkeit Intervall Felder Jahres- und MONATSWERT enthält, werden die Werte dieser Felder durch ein Minuszeichen (-) getrennt.  
  
-   Wenn die Genauigkeit Intervall Felder Tages- und STUNDENFORMAT enthält, werden die Werte dieser Felder durch ein Leerzeichen getrennt.  
  
-   Wenn die Genauigkeit Intervall die Stunde und die unteren Reihenfolge Felder (MINUTE und Sekunde) enthält, werden die Werte dieser Felder durch einen Doppelpunkt getrennt.  
  
-   Wenn die Genauigkeit Intervall ein zweites Feld enthält und die ausdrückliche oder konkludente Sekunden Genauigkeit ungleich NULL ist, ist das Zeichen direkt vor die erste Ziffer des Bruchteils der zweiten einen Zeitraum an.  
  
-   Kein Feld kann mehr als zwei Ziffern lang sein, außer:  
  
    -   Der Wert des Felds führende kann solange die ausdrückliche oder konkludente Genauigkeit für anführenden Intervallwert sein.  
  
    -   Der Bruchteil des zweiten Feldes kann als die Genauigkeit ausdrückliche oder konkludente Sekunden lang sein.  
  
    -   Die nachfolgende Felder führen Sie die üblichen Einschränkungen des gregorianischen Kalenders. (Siehe [Einschränkungen des gregorianischen Kalenders](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md).)  
  
 Die folgende Tabelle enthält Beispiele für gültige Intervall Literale, wie in der ODBC-Escape-Klausel für Intervalle enthalten. Die Syntax der Escape-Klausel lautet wie folgt:  
  
> [!NOTE]  
>  *{Intervall Anmeldung Intervall-Intervall-zeichenfolgenqualifizierer}*  
  
|Literal-Escape-Klausel|Angegebene Intervall abgelaufen ist|  
|---------------------------|------------------------|  
|{INTERVALL "326" YEAR(4)}|Gibt ein Intervall von 326 Jahren. Die Genauigkeit für anführenden Intervallwert ist 4.|  
|{INTERVALL "326" MONTH(3)}|Gibt ein Intervall von Monaten 326 an. Die Genauigkeit für anführenden Intervallwert ist 3.|  
|{DAY(4) INTERVALL '3261'}|Gibt ein Intervall von 3261 Tagen an. Die Genauigkeit für anführenden Intervallwert ist 4.|  
|{HOUR(3) INTERVALL '163'}|Gibt ein Intervall von 163 Tagen an. Die Genauigkeit für anführenden Intervallwert ist 3.|  
|{MINUTE(3) INTERVALL '163'}|Gibt ein Intervall von 163 Minuten an. Die Genauigkeit für anführenden Intervallwert ist 3.|  
|{SECOND(3,2) INTERVALL '223.16'}|Gibt ein Intervall von 223.16 Sekunden an. Das Intervall führende Genauigkeit 3 beträgt, und die Genauigkeit Sekunden beträgt 2.|  
|{INTERVALL "163-11' YEAR(3) MONAT}|Gibt ein Intervall von 163 Jahre und 11 Monaten an. Die Genauigkeit für anführenden Intervallwert ist 3.|  
|{INTERVALL 163 ' 12' DAY(3) STUNDE}|Gibt ein Intervall von 163 Tage und 12 Stunden an. Die Genauigkeit für anführenden Intervallwert ist 3.|  
|{INTERVALL "163 12:39" DAY(3) MINUTE}|Gibt ein Intervall von 163 Tage, 12 Stunden und 39 Minuten an. Die Genauigkeit für anführenden Intervallwert ist 3.|  
|{INTERVALL "163 12:39:59.163" DAY(3) ZU SECOND(3)}|Gibt ein Intervall von 163 Tage, 12 Stunden, 39 Minuten und 59.163 Sekunden an. Das Intervall führende Genauigkeit 3 beträgt, und die Sekunden Genauigkeit 3 beträgt.|  
|{INTERVALL "163:39" HOUR(3) MINUTE}|Gibt ein Intervall von 163 Stunden und 39 Minuten an. Die Genauigkeit für anführenden Intervallwert ist 3.|  
|{INTERVALL "163:39:59.163" HOUR(3) ZU SECOND(4)}|Gibt ein Intervall von 163 Stunden, 39 Minuten und 59.163 Sekunden an. Das Intervall führende Genauigkeit 3 beträgt, und die Genauigkeit von Sekunden ist 4.|  
|{INTERVALL "163:59.163" MINUTE(3) ZU SECOND(5)}|Gibt ein Intervall von 163 Minuten und 59.163 Sekunden an. Das Intervall führende Genauigkeit 3 beträgt, und die Genauigkeit von Sekunden ist 5.|  
|{INTERVAL-"16 23:39:56.23"-TAG, AN DEM ZWEITEN}|Gibt ein Intervall von minus 16 Tage, 23 Stunden, 39 Minuten und 56.23 Sekunden an. Die implizite führende Genauigkeit ist 2, und die implizite Sekunden Genauigkeit ist 6.|  
  
 Die folgende Tabelle enthält Beispiele für ungültige Intervall Literale:  
  
|Literal-Escape-Klausel|Grund Warum ungültig|  
|---------------------------|------------------------|  
|{HOUR(2) INTERVALL '163'}|Die führenden Intervall-Genauigkeit ist 2, aber der Wert des Felds führende 163.|  
|{SECOND(2,2) INTERVALL '223.16'}<br /><br /> {SECOND(3,1) INTERVALL '223.16'}|Im ersten Beispiel die führende Genauigkeit ist zu klein, und im zweiten Beispiel die Sekunden Genauigkeit ist zu klein.|  
|{INTERVALL "223.16" ZWEITE}<br /><br /> {INTERVALL "223" YEAR}|Da die führende Genauigkeit nicht angegeben wird, wird standardmäßig auf 2 ist zu klein für das angegebene Literal.|  
|{INTERVALL "22.1234567" ZWEITE}|Die Genauigkeit für die Sekunden ist nicht vorgegeben, damit bis 6 abzielenden. Das Literal weist sieben Ziffern nach dem Dezimaltrennzeichen an.|  
|{INTERVALL "163-13' YEAR(3) MONAT}<br /><br /> {INTERVALL 163 ' 65' DAY(3) STUNDE}<br /><br /> {INTERVALL "163 62:39" DAY(3) MINUTE}<br /><br /> {INTERVALL "163 12:125:59.163" DAY(3) ZU SECOND(3)}<br /><br /> {INTERVALL "163:144" HOUR(3) MINUTE}<br /><br /> {INTERVALL "163:567:234.163" HOUR(3) ZU SECOND(4)}<br /><br /> {INTERVALL "163:591.163" MINUTE(3) ZU SECOND(5)}|Das nachfolgende Feld befolgt nicht die Regeln des gregorianischen Kalenders.|
