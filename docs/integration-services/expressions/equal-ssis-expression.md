---
title: == (Gleich) (SSIS-Ausdruck) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- equal operator (==)
- == (equal operator)
ms.assetid: 36fd2354-7b93-4c95-9cf3-51ee24568950
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2944b2ac0c650f3a7a3d447d20b34bee5fa27e20
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="-equal-ssis-expression"></a>== (Gleich) (SSIS-Ausdruck)
  Führt einen Vergleich aus, um zu ermitteln, ob zwei Ausdrücke gleich sind. Die Ausdrucksauswertung konvertiert viele Datentypen automatisch vor dem Vergleich. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
 Für manche Datentypen muss jedoch der Ausdruck eine explizite Umwandlung einschließen, damit der Ausdruck erfolgreich ausgewertet werden kann. Weitere Informationen zu zulässigen Datentypumwandlungen finden Sie unter [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
expression1 == expression2  
  
```  
  
## <a name="arguments"></a>Argumente  
 *expression1, expression2*  
 Ein gültiger Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_BOOL  
  
## <a name="remarks"></a>Hinweise  
 Wenn einer der Ausdrücke im Vergleich NULL ist, ist das Ergebnis des Vergleichs NULL. Wenn beide Ausdrücke NULL sind, ist das Ergebnis NULL.  
  
 Für die Ausdrucksgruppe ( *expression1* und *expression2*) muss eine der folgenden Regeln eingehalten werden:  
  
-   **Numerisch**   *expression1* und *expression2* müssen einen numerischen Datentyp aufweisen. Die Schnittmenge der Datentypen muss ein numerischer Datentyp gemäß der Regeln zu den impliziten numerischen Konvertierungen sein, die die Ausdrucksauswertung ausführt. Die Schnittmenge der beiden numerischen Datentypen darf nicht NULL sein. Weitere Informationen finden Sie unter [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
-   **Zeichen** : *expression1* und *expression2* müssen zu einem der Datentypen DT_STR oder DT_WSTR ausgewertet werden. Die beiden Ausdrücke können zu verschiedenen Zeichenfolgen-Datentypen ausgewertet werden.  
  
    > [!NOTE]  
    >  Bei Zeichenfolgenvergleichen wird nach Groß-/Kleinschreibung, Akzent, Kana und Breite unterschieden.  
  
-   **Datum, Uhrzeit oder Datum/Uhrzeit** Sowohl *expression1* als auch *expression2* müssen zu einem der folgenden Datentypen ausgewertet werden: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET oder DT_FILETIME.  
  
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
  
-   **Logisch**   *expression1* und *expression2* müssen zu einem booleschen Wert ausgewertet werden.  
  
-   **GUID:** *expression1* und *expression2* müssen zum Datentyp DT_GUID ausgewertet werden.  
  
-   **Binary:** *expression1* und *expression2* müssen zum Datentyp DT_BYTES ausgewertet werden.  
  
-   **BLOB:** *expression1* und *expression2* müssen zum gleichen BLOB-Datentyp (Binary Large Object Block) ausgewertet werden: DT_TEXT, DT_NTEXT oder DT_IMAGE.  
  
 Weitere Informationen zu Datentypen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird zu TRUE ausgewertet, falls das aktuelle Datum der 4. Juli 2003 ist. Weitere Informationen finden Sie unter [GETDATE &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
 "7/4/2003" == GETDATE()  
  
 In diesem Beispiel wird zu TRUE ausgewertet, falls der Wert in der **ListPrice** -Spalte 500 ist.  
  
```  
ListPrice == 500  
```  
  
 In diesem Beispiel wird die **LPrice**-Variable verwendet. Es wird zu TRUE ausgewertet, falls der Wert in der **LPrice** -Spalte 500 entspricht. Der Datentyp der Variablen muss numerisch sein, damit der Ausdruck erfolgreich analysiert wird.  
  
```  
@LPrice == 500  
```  
  
## <a name="see-also"></a>Siehe auch  
 [\! = &#40; Ungleich &#41; &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/unequal-ssis-expression.md)   
 [Operatorrangfolge und Assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

