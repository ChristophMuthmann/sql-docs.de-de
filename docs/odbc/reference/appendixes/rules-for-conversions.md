---
title: "Regeln für Konvertierungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06baaaff03f75cbf04da86527a25ea60755a473e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="rules-for-conversions"></a>Regeln für Konvertierungen
Die Regeln in diesem Abschnitt gelten für Konvertierungen, die im Zusammenhang mit numerischen Literalen. Für die Zwecke dieser Regeln können sind die folgenden Begriffe definiert:  
  
-   *Speichern Sie die Zuweisung:* beim Senden von Daten in eine Tabellenspalte in einer Datenbank. Dies tritt auf, während Aufrufe **SQLExecute**, **SQLExecDirect**, und **SQLSetPos**. Bei der Zuordnung von Speicher "Target" bezieht sich auf einer Datenbankspalte und "Quelle" bezieht sich auf Daten in die Anwendungspuffer.  
  
-   *Abruf Zuweisung:* beim Abrufen von Daten aus der Datenbank in Anwendungspuffer. Dies tritt auf, während Aufrufe **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, und **SQLSetPos**. Bei der Zuordnung abrufen "Target" bezieht sich auf den Anwendungspuffer, und "Quelle" bezieht sich auf die Datenbankspalte.  
  
-   *CS:* den Wert in der Zeichenquelle.  
  
-   *NT:* den Wert in das numerische Ziel.  
  
-   *NS:* den Wert in der numerischen Quelle.  
  
-   *CT:* den Wert in der Ziel-Zeichen.  
  
-   Genauigkeit von einer genauen numerisches Literal: die Anzahl der Ziffern, die es enthält.  
  
-   Die Skalierung eines genauen numerischen Literals: die Anzahl der Ziffern rechts neben die ausdrückliche oder konkludente Zeitraum.  
  
-   Die Genauigkeit von einem ungefähren numerischen Literal: die Genauigkeit der Mantisse.  
  
## <a name="character-source-to-numeric-target"></a>Zeichenquelle zu numerischen Ziel  
 Im folgenden sind die Regeln für die Konvertierung aus einer Zeichenquelle (CS) in einem numerischen Ziel (NT):  
  
1.  Ersetzen Sie CS, mit dem Wert, der durch das Entfernen von keine führenden oder nachfolgenden Leerzeichen in CS abgerufen. Wenn CS kein gültiger ist *numerische Literal*, SQLSTATE 22018 (Ungültiger Zeichenwert für Konvertierungsangabe) wird zurückgegeben.  
  
2.  Ersetzen Sie CS, mit dem Wert, der durch das Entfernen der führender Nullen vor dem Dezimaltrennzeichen, nachfolgende Nullen hinter dem Dezimaltrennzeichen oder beides abgerufen.  
  
3.  Konvertieren Sie CS NT. Wenn die Konvertierung in einen Verlust signifikanter Ziffern ergibt, wird die SQLSTATE 22003 (numerischen Wert außerhalb des gültigen Bereichs) zurückgegeben. Wenn die Konvertierung zum Verlust von SQLSTATE 01S07 nicht signifikanten Ziffern führt (Sekundenbruchteile abgeschnitten) wird zurückgegeben.  
  
## <a name="numeric-source-to-character-target"></a>Numerische Quelle zum Ziel Zeichen  
 Es folgen die Regeln zum Konvertieren aus einer numerischen Quelle (NS) an ein Ziel Zeichen (CT):  
  
1.  Können Sie die Länge in Zeichen des CT werden LT Für die Abruf-Zuweisung ist LT gleich der Länge des Puffers in Zeichen abzüglich der Anzahl von Bytes in der Null-Terminierung Zeichen für diese Zeichensatz.  
  
2.  Fälle:  
  
    -   NS einen exakten numerischen Typ handelt, lassen Sie dann die kürzeste Zeichenfolge entsprechen, die die Definition der entspricht YP *exakte numerische-Literal* , dass die Dezimalstellen des YP identisch mit der Skala NS ist und der übersetzte Wert des YP ist die der Absolutbetrag von Notification Services.  
  
    -   Wenn NS einen ungefähren numerischen Typ ist, können Sie eine Zeichenfolge wie folgt lauten YP aus:  
  
         Fall:  
  
         NS ist gleich 0, klicken Sie dann YP 0.  
  
         Lassen Sie die kürzeste Zeichenfolge sein, die die Definition von exakten - entspricht YSN*numerische Literal* und dessen interpretierten Wert ist der Absolute Wert des Notification Services. Wenn die Länge des YSN ist kleiner als das (*Genauigkeit* + 1) des Datentyps der NS, lassen Sie YP YSN gleich.  
  
         Andernfalls YP ist die kürzeste Zeichenfolge, die die Definition der entspricht *ungefähre numerische-Literal* , deren interpretierten Wert den absoluten Wert des NS und deren *Mantisse* besteht aus einer einzelne *Ziffer* also nicht "0", gefolgt von einem *Zeitraum* und ein *unsigned Integer*.  
  
3.  Fall:  
  
    -   Wenn NS kleiner als 0 ist, können Sie das Ergebnis des Y aus:  
  
         "-" &#124; &#124; YP  
  
         wobei "&#124; &#124;" ist der Operator für zeichenfolgenverkettung.  
  
         Andernfalls können Sie Y YP gleich.  
  
4.  Lassen Sie übernehmen die Länge in Zeichen von Y werden.  
  
5.  Fall:  
  
    -   Wenn übernehmen LT entspricht, wird der CT y festgelegt.  
  
    -   Wenn übernehmen LT unterschreitet, wird CT durch entsprechende Anzahl von Leerzeichen auf der rechten Seite Erweiterte y festgelegt.  
  
         Andernfalls (übernehmen > LT), kopieren Sie die ersten Zeichen der LT von Y in CT  
  
         Fall:  
  
         Ist dies eine Store-Zuweisung, geben Sie den Fehler SQLSTATE 22001 (Zeichenfolgendaten, rechts abgeschnitten) zurück.  
  
         Ist dies Zuweisung abrufen, geben Sie die Warnung SQLSTATE 01004 (Zeichenfolgendaten, rechts abgeschnitten) zurück. Wenn die Kopie der Verlust von Dezimalstellen (mit Ausnahme des nachfolgende Nullen) ergibt, ist es treiberdefinierten, ob eines der folgenden Ereignisse eintritt:  
  
         (1) der Treiber schneidet die Zeichenfolge in Y, die eine passende Skalierung (die auch 0 (null) sein kann) und schreibt das Ergebnis in CT  
  
         (2) der Treiber rundet die Zeichenfolge in Y, die eine passende Skalierung (die auch 0 (null) sein kann) und schreibt das Ergebnis in CT  
  
         (3) der Treiber weder schneidet noch rundet aber kopiert nur die ersten Zeichen der LT von Y in CT

