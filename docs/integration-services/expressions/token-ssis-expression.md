---
title: TOKEN (SSIS-Ausdruck) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9fdd06bf-5bc9-445c-95bf-709e0ca5989b
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ff578d1f2ba584c64e471fa9514c6fa76e581d8e
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="token--ssis-expression"></a>TOKEN (SSIS-Ausdruck)
  Gibt ein Token (Teilzeichenfolge) aus einer Zeichenfolge zurück – basierend auf den angegebenen Trennzeichen, die Token in der Zeichenfolge trennen, und der Nummer des Tokens, die festlegt, welcher Token zurückgegeben werden soll.  
  
## <a name="syntax"></a>Syntax  
  
```  
TOKEN(character_expression, delimiter_string, occurrence)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Eine Zeichenfolge, die durch Trennzeichen getrennte Token enthält.  
  
 *delimiter_string*  
 Eine Zeichenfolge, die Begrenzungszeichen enthält. "; , " enthält beispielsweise drei Begrenzungszeichen: Semikolon, Leerzeichen und Komma.  
  
 *occurrence*  
 Eine ganze Zahl mit oder ohne Vorzeichen, die angibt, welcher Token zurückgegeben werden soll. Wenn Sie z. B. 3 als Wert für diesen Parameter angeben, wird das dritte Token in der Zeichenfolge zurückgegeben.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion teilt die < Character_expression >-Zeichenfolge in einen Satz von Token, die durch die in der < Delimiter_string > angegebene Trennzeichen getrennt, und klicken Sie dann gibt das n-te Token, wobei N die Anzahl der Vorkommen des Tokens angegeben ist die \<Vorkommen > Parameter. Beispiele für die Verwendung dieser Funktion finden Sie im Abschnitt "Beispiele".  
  
 Die folgenden Hinweise gelten für die TOKEN-Funktion:  
  
-   Die Trennzeichenfolge kann ein oder mehrere Trennzeichen enthalten.  
  
-   Wenn der Wert des \<Vorkommen >-Parameter höher als die Gesamtanzahl der Token in der Zeichenfolge ist, gibt die Funktion NULL zurück.  
  
-   Führende Trennzeichen werden übersprungen.  
  
-   TOKEN kann nur mit dem DT_WSTR-Datentyp verwendet werden. Ein *character_expression* -Argument, das ein Zeichenfolgenliteral oder eine Datenspalte mit dem DT_STR-Datentyp ist, wird implizit in den DT_WSTR-Datentyp umgewandelt, bevor TOKEN ausgeführt wird. Andere Datentypen müssen explizit in den DT_WSTR-Datentyp umgewandelt werden.  
  
-   TOKEN gibt ein NULL-Ergebnis zurück, wenn der character_expression NULL ist.  
  
-   Sie können Variablen und Spalten als Werte für alle Argumente des Ausdrucks verwenden.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Im folgenden Beispiel gibt die TOKEN-Funktion den Wert "ein" zurück. Die Zeichenfolge "ein kleiner weißer Hund" hat 4 durch das Trennzeichen " " (Leerzeichen) getrennte Token: "ein", "kleiner", "weißer", "Hund". Das zweite Argument, eine Trennzeichenfolge, gibt nur ein Trennzeichen (das Leerzeichen) an, das beim Teilen der Eingabezeichenfolge in Token verwendet werden soll. Das letzte Argument 1 legt fest, dass das erste Token zurückgegeben werden soll. In dieser Beispielzeichenfolge ist "ein" das erste Token.  
  
```  
TOKEN("a little white dog"," ",1)  
```  
  
 Im folgenden Beispiel gibt die TOKEN-Funktion den Wert "Hund" zurück. Die Trennzeichenfolge in diesem Beispiel enthält 5 Trennzeichen. Die Eingabezeichenfolge enthält 4 Token: "ein", "kleiner", "weißer", "Hund".  
  
```  
TOKEN("a:little|white dog","| ,.:",4)  
```  
  
 Im folgenden Beispiel gibt die TOKEN-Funktion den Wert "" (eine leere Zeichenfolge) zurück, weil es keine 99 Token in der Zeichenfolge gibt.  
  
```  
TOKEN("a little white dog"," ",99)  
```  
  
 Im folgenden Beispiel gibt die TOKEN-Funktion die vollständige Zeichenfolge zurück. Die Funktion analysiert die Eingabezeichenfolge für Trennzeichen, und da es in der Zeichenfolge keine gibt, fügt es die ganze Zeichenfolge als erstes Token hinzu.  
  
```  
TOKEN("a little white dog","|",1)  
```  
  
 Im folgenden Beispiel gibt die TOKEN-Funktion den Wert "ein" zurück. Es ignoriert alle führenden Leerzeichen.  
  
```  
TOKEN("        a little white dog", " ", 1)  
```  
  
 Im folgenden Beispiel gibt die TOKEN-Funktion das Jahr einer Datumszeichenfolge zurück.  
  
```  
TOKEN("2009/01/01", "/"), 1  
```  
  
 Im folgenden Beispiel gibt die TOKEN-Funktion den Dateinamen des angegebenen Pfads zurück. Wenn der Wert von User::Path z. B. "C:\Programme\Data\MeineDatei.txt" ist, gibt die TOKEN-Funktion "MeineDatei.txt" zurück. Die TOKENCOUNT-Funktion gibt 4 zurück, und die TOKEN-Funktion gibt das 4. Token "MeineDatei.txt" zurück.  
  
```  
TOKEN(@[User::Path], "\\", TOKENCOUNT(@[User::Path], "\\"))  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

