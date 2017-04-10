---
title: "&gt; (Gr&#246;&#223;er als) (SSIS-Ausdruck) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Größer als-Operator (>)"
  - "> (Größer als-Operator)"
ms.assetid: 2e22efa3-eeb1-4984-a95c-9bccdcf98892
caps.latest.revision: 47
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 47
---
# &gt; (Gr&#246;&#223;er als) (SSIS-Ausdruck)
  Führt einen Vergleich aus, um zu ermitteln, ob der erste Ausdruck größer ist als der zweite. Die Ausdrucksauswertung konvertiert viele Datentypen automatisch vor dem Vergleich.  
  
> [!NOTE]  
>  Vergleiche, die die Datentypen DT_TEXT, DT_NTEXT oder DT_IMAGE verwenden, werden von diesem Operator nicht unterstützt.  
  
 Für manche Datentypen muss jedoch der Ausdruck eine explizite Umwandlung einschließen, damit der Ausdruck erfolgreich ausgewertet werden kann. Weitere Informationen zu zulässigen Datentypumwandlungen finden Sie unter [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
## Syntax  
  
```  
  
expression1 > expression2  
  
```  
  
## Argumente  
 *expression1, expression2*  
 Ein gültiger Ausdruck. Beide Ausdrücke müssen implizit konvertierbare Datentypen besitzen.  
  
## Ergebnistypen  
 DT_BOOL  
  
## Hinweise  
 Wenn einer der Ausdrücke im Vergleich NULL ist, ist das Ergebnis des Vergleichs NULL. Wenn beide Ausdrücke NULL sind, ist das Ergebnis NULL.  
  
 Für die Ausdrucksgruppe ( *expression1* und *expression2*) muss eine der folgenden Regeln eingehalten werden:  
  
-   **Numerisch**   *expression1* und *expression2* müssen einen numerischen Datentyp aufweisen. Die Schnittmenge der Datentypen muss ein numerischer Datentyp gemäß den Regeln zu den impliziten numerischen Konvertierungen sein, die die Ausdrucksauswertung ausführt. Die Schnittmenge der beiden numerischen Datentypen darf nicht NULL sein. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
-   **Zeichen**   *expression1* und *expression2* müssen zu einem der Datentypen DT_STR oder DT_WSTR ausgewertet werden. Die beiden Ausdrücke können zu verschiedenen Zeichenfolgen-Datentypen ausgewertet werden.  
  
    > [!NOTE]  
    >  Bei Zeichenfolgenvergleichen wird nach Groß-/Kleinschreibung, Akzent, Kana und Breite unterschieden.  
  
-   **Datum, Uhrzeit oder Datum/Uhrzeit**   *expression1* und *expression2* müssen zu einem der folgenden Datentypen ausgewertet werden: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET oder DT_FILETIME.  
  
    > [!NOTE]  
    >  Das System unterstützt keine Vergleiche zwischen einem Ausdruck, der zu einem Uhrzeitdatentyp ausgewertet wird, und einem Ausdruck, der entweder zu einem Datums- oder zu einem Datums-/Uhrzeitdatentyp ausgewertet wird. In diesem Fall wird ein Fehler generiert.  
  
     Beim Vergleich der Ausdrücke werden die folgenden Konvertierungsregeln in der angegebenen Reihenfolge angewendet:  
  
    -   Wenn zwei Ausdrücke zu dem gleichen Datentyp ausgewertet werden, wird der Datentyp verglichen.  
  
    -   Wenn ein Ausdruck den DT_DBTIMESTAMPOFFSET-Datentyp aufweist, wird der andere Ausdruck implizit in DT_DBTIMESTAMPOFFSET konvertiert, und ein DT_DBTIMESTAMPOFFSET-Vergleich wird ausgeführt. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
    -   Wenn ein Ausdruck den DT_DBTIMESTAMP2-Datentyp aufweist, wird der andere Ausdruck implizit in DT_DBTIMESTAMP2 konvertiert, und ein DT_DBTIMESTAMP2-Vergleich wird ausgeführt.  
  
    -   Wenn ein Ausdruck den DT_DBTIME2-Datentyp aufweist, wird der andere Ausdruck implizit in DT_DBTIME2 konvertiert, und ein DT_DBTIME2-Vergleich wird ausgeführt.  
  
    -   Wenn ein Ausdruck einen anderen Datentyp als DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 oder DT_DBTIME2 aufweist, werden die Ausdrücke vor dem Vergleichen in den DT_DBTIMESTAMP-Datentyp konvertiert.  
  
     Beim Vergleichen der Ausdrücke gelten folgende Annahmen:  
  
    -   Wenn jeder Ausdruck einen Datentyp aufweist, der Millisekunden umfasst, wird angenommen, dass bei dem Datentyp mit der geringsten Anzahl von Ziffern für Millisekunden die verbleibenden Ziffern Nullen sind.  
  
    -   Wenn jeder Ausdruck einen Datumsdatentyp aufweist, jedoch nur ein Ausdruck einen Zeitzonenoffset umfasst, wird angenommen, dass der Datumsdatentyp ohne Zeitzonenoffset in koordinierter Weltzeit (Coordinated Universal Time; UTC) ausgedrückt ist.  
  
 Weitere Informationen zu Datentypen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Beispiele für Ausdrücke  
 In diesem Beispiel wird zu TRUE ausgewertet, falls das aktuelle Datum der 4. Juli 2003 oder davor ist. Weitere Informationen finden Sie unter [GETDATE &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
```  
"7/4/2003" > GETDATE()  
```  
  
 In diesem Beispiel wird zu TRUE ausgewertet, falls der Wert in der **ListPrice** -Spalte größer als 500 ist.  
  
```  
ListPrice > 500  
```  
  
 In diesem Beispiel wird die **LPrice**-Variable verwendet. Es wird zu TRUE ausgewertet, falls der Wert in der **LPrice** -Spalte größer als 500 ist. Der Datentyp der Variablen muss numerisch sein, damit der Ausdruck analysiert wird.  
  
```  
@LPrice > 500  
```  
  
## Siehe auch  
 [&#60; &#40;Kleiner als&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/less-than-ssis-expression.md)   
 [&#62;= &#40;Größer oder gleich&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)   
 [&#60;= &#40;Kleiner oder gleich&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)   
 [== &#40;Gleich&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/equal-ssis-expression.md)   
 [Operatorenrangfolge und -assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  