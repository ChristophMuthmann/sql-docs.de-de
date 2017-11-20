---
title: LTRIM (SSIS-Ausdruck) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- leading blanks
- LTRIM function
ms.assetid: d082f42a-d7e7-49f5-a503-ac44ba630832
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d68b87ab59dab0a5b7bbd199b58a6259eb28daf9
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="ltrim-ssis-expression"></a>LTRIM (SSIS-Ausdruck)
  Gibt einen Zeichenausdruck zurück, nachdem führende Leerzeichen entfernt wurden.  
  
> [!NOTE]  
>  Mit LTRIM werden keine Pseudoleerzeichen, wie z. B. Tabulatoren oder Zeilenvorschubzeichen, entfernt. Unicode stellt Codeelemente für viele verschiedene Arten von Leerzeichen bereit, diese Funktion erkennt jedoch nur das Unicode-Codeelement 0x0020. DBCS-Zeichenfolgen, die in Unicode konvertiert werden, enthalten u. U. andere Leerzeichen als 0x0020. Diese Leerzeichen können von der Funktion nicht entfernt werden. Zum Entfernen aller Arten von Leerzeichen können Sie die LTrim-Methode von Microsoft Visual Basic .NET in einem Skript verwenden, das aus der Skriptkomponente ausgeführt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LTRIM(character expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein Zeichenausdruck, aus dem Leerzeichen entfernt werden sollen.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Hinweise  
 LTRIM kann nur mit dem DT_WSTR-Datentyp verwendet werden. Ein *character_expression* -Argument, das ein Zeichenfolgenliteral oder eine Datenspalte mit dem DT_STR-Datentyp ist, wird implizit in den DT_WSTR-Datentyp umgewandelt, bevor LTRIM ausgeführt wird. Andere Datentypen müssen explizit in den DT_WSTR-Datentyp umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md) und [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LTRIM gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel werden führende Leerzeichen aus einem Zeichenfolgenliteral entfernt. Als Ergebnis wird "Hello" zurückgegeben.  
  
```  
LTRIM("    Hello")  
```  
  
 In diesem Beispiel werden führende Leerzeichen aus der **FirstName** -Spalte entfernt.  
  
```  
LTRIM(FirstName)  
```  
  
 In diesem Beispiel werden führende Leerzeichen aus der **FirstName** -Variablen entfernt.  
  
```  
LTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [RTRIM &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/rtrim-ssis-expression.md)   
 [TRIM &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/trim-ssis-expression.md)   
 [Funktionen &#40; SSIS-Ausdruck &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

