---
title: CAST (SSIS-Ausdruck) | Microsoft Docs
ms.custom:
- ssisdev020617
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CAST function
- cast operator
- converting data types [Integration Services]
- data types [Integration Services], expressions
- data types [Integration Services], converting
ms.assetid: d4e915cc-1c7b-4b2e-93b0-13a8b0cb9242
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 199dca85523f6ba2f4d53ef89e1b9a73667a6472
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="cast-ssis-expression"></a>CAST (SSIS-Ausdruck)
  Konvertiert einen Ausdruck explizit in einen anderen Datentyp. Der Umwandlungsoperator kann auch als Operator zum Abschneiden dienen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
(type_spec) expression  
  
```  
  
## <a name="arguments"></a>Argumente  
 *type_spec*  
 Ein gültiger [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Datentyp.  
  
 *expression*  
 Ein beliebiger gültiger Ausdruck.  
  
## <a name="result-types"></a>Ergebnistypen  
 Der Datentyp von *type_spec*. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="remarks"></a>Hinweise  
 Im folgenden Diagramm werden zulässige Umwandlungsvorgänge dargestellt.  
  
 ![Zulässige und unzulässige Umwandlungen zwischen Datentypen](../../integration-services/expressions/media/data-conversion.gif "zulässige und unzulässige Umwandlungen zwischen Datentypen")  
  
 Für die Umwandlung in bestimmte Datentypen sind Parameter erforderlich. In der folgenden Tabelle sind diese Datentypen und die zugehörigen Parameter aufgelistet.  
  
|Datentyp|Parameter|Beispiel|  
|---------------|---------------|-------------|  
|DT_STR|*charcount*<br /><br /> *codepage*|(DT_STR,30,1252) wandelt 30 Bytes, oder 30 einzelne Zeichen, mithilfe der 1252-Codepage in den DT_STR-Datentyp um.|  
|DT_WSTR|*Charcount*|(DT_WSTR,20) wandelt 20 Bytepaare, oder 20 Unicode-Zeichen, in den DT_WSTR-Datentyp um.|  
|DT_BYTES|*Bytecount*|(DT_BYTES,50) wandelt 50 Bytes in den DT_BYTES-Datentyp um.|  
|DT_DECIMAL|*Dezimalstellen*|(DT_DECIMAL,2) wandelt einen numerischen Wert mithilfe von 2 Dezimalstellen in den DT_DECIMAL-Datentyp um.|  
|DT_NUMERIC|*Genauigkeit*<br /><br /> *Dezimalstellen*|(DT_NUMERIC,10,3) wandelt einen numerischen Wert mithilfe einer Genauigkeit von 10 und 3 Dezimalstellen in den DT_NUMERIC-Datentyp um.|  
|DT_TEXT|*Codepage*|(DT_TEXT,1252) wandelt einen Wert mithilfe der 1252-Codepage in den DT_TEXT-Datentyp um.|  
  
 Wenn eine Zeichenfolge in einen DT_DATE-Datentyp umgewandelt wird, oder umgekehrt, wird das Gebietsschema der Transformation verwendet. Allerdings weist das Datum das ISO-Format YYYY-MM-DD auf, und zwar unabhängig davon, ob für das Gebietsschema das ISO-Format verwendet wird.  
  
> [!NOTE]  
>  Informationen zum Konvertieren einer Zeichenfolge in einen anderen Datumsdatentyp als DT_DATE finden Sie unter [SQL Server Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Falls die Codepage eine Multibytezeichen-Codepage ist, kann die Anzahl der Bytes und Zeichen abweichen. Durch das Umwandeln von DT_WSTR in DT_STR mit dem gleichen *charcount* -Wert können die letzten Zeichen in der konvertierten Zeichenfolge abgeschnitten werden. Falls in der Spalte der Zieltabelle ausreichend Speicherplatz vorhanden ist, legen Sie für den Wert des *charcount* -Parameters die Anzahl der Bytes fest, die die Multibytecodepage erfordert. Wenn Sie z.B. Zeichendaten mithilfe der 936-Codepage in einen DT_STR-Datentyp umwandeln, sollten Sie für *charcount* einen Wert festlegen, der bis zu zweimal größer als die Anzahl von Zeichen ist, die die Daten erwartungsgemäß enthalten. Falls Sie Zeichendaten mithilfe der UTF-8-Codepage umwandeln, sollten Sie für *charcount* einen Wert festlegen, der bis zu viermal größer ist.  
  
 Weitere Informationen zur Struktur von Datumsdatentypen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="ssis-expression-examples"></a>Beispiele für SSIS-Ausdrücke  
 In diesem Beispiel wird ein numerischer Wert in eine ganze Zahl umgewandelt.  
  
```  
(DT_I4) 3.57  
```  
  
 In diesem Beispiel wird eine ganze Zahl mithilfe der 1252-Codepage in eine Zeichenfolge umgewandelt.  
  
```  
(DT_STR,1,1252)5  
```  
  
 In diesem Beispiel wird eine aus drei Zeichen bestehende Zeichenfolge in Doppelbytezeichen umgewandelt.  
  
```  
(DT_WSTR,3)"Cat"  
```  
  
 In diesem Beispiel wird eine ganze Zahl in eine Dezimalzahl mit zwei Dezimalstellen umgewandelt.  
  
```  
(DT_DECIMAl,2)500  
```  
  
 In diesem Beispiel wird eine ganze Zahl in einen numerischen Wert mit einer Genauigkeit von 7 und drei Dezimalstellen umgewandelt.  
  
```  
(DT_NUMERIC,7,3)4000  
```  
  
 In diesem Beispiel werden Werte in der **FirstName** -Spalte, für die ein **nvarchar** -Datentyp und eine Länge von 50 definiert ist, mithilfe der 1252-Codepage in eine Zeichenfolge umgewandelt.  
  
```  
(DT_STR,50,1252)FirstName  
```  
  
 In diesem Beispiel werden Werte in der Spalte **DateFirstPurchase** des Typs DT_DBDATE in eine Unicode-Zeichenfolge mit einer Länge von 20 Zeichen umgewandelt.  
  
```  
(DT_WSTR,20)DateFirstPurchase  
```  
  
 In diesem Beispiel wird das Zeichenfolgenliteral "True" in einen booleschen Wert umgewandelt.  
  
```  
(DT_BOOL)"True"  
```  
  
 In diesem Beispiel wird ein Zeichenfolgenliteral in DT_DBDATE umgewandelt.  
  
```  
(DT_DBDATE) "1999-10-11"  
```  
  
 In diesem Beispiel wird ein Zeichenfolgenliteral in den DT_DBTIME2-Datentyp umgewandelt, bei dem fünf Ziffern für Millisekunden verwendet werden. (Beim DT_DBTIME2-Datentyp können null bis sieben Ziffern für Millisekunden angegeben werden.)  
  
```  
(DT_DBTIME2, 5) "16:34:52.12345"  
```  
  
 In diesem Beispiel wird ein Zeichenfolgenliteral in den DT_DBTIMESTAMP2-Datentyp umgewandelt, bei dem vier Ziffern für Millisekunden verwendet werden. (Beim DT_DBTIMESTAMP2-Datentyp können null bis sieben Ziffern für Millisekunden angegeben werden.)  
  
```  
(DT_DBTIMESTAMP2, 4) "1999-10-11 16:34:52.1234"  
```  
  
 In diesem Beispiel wird ein Zeichenfolgenliteral in den DT_DBTIMESTAMPOFFSET-Datentyp umgewandelt, bei dem sieben Ziffern für Millisekunden verwendet werden. (Beim DT_DBTIMESTAMPOFFSET-Datentyp können null bis sieben Ziffern für Millisekunden angegeben werden.)  
  
```  
(DT_DBTIMESTAMPOFFSET, 7) "1999-10-11 16:34:52.1234567 + 5:35"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Operatorrangfolge und Assoziativität](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatoren &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/operators-ssis-expression.md)   
 [Integrationsservices &#40; SSIS &#41; Ausdrücke](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [Integration Services-Datentypen in Ausdrücken](../../integration-services/expressions/integration-services-data-types-in-expressions.md)  
  
  
