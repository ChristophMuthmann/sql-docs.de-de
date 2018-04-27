---
title: RTRIM (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- RTRIM function
- trailing blanks
ms.assetid: 529bd43e-3f8a-4682-a33e-569176aa7fc4
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0cc7c5bad8657c9c981fc5d080c359170f909cc8
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="rtrim-ssis-expression"></a>RSCHNEIDEN (SSIS-Ausdruck)
  Gibt einen Zeichenausdruck zurück, nachdem nachfolgende Leerzeichen entfernt wurden.  
  
> [!NOTE]  
>  Mit RTRIM werden keine Pseudoleerzeichen entfernt, wie z. B. Tabulatoren oder Zeilenvorschubzeichen. Unicode stellt Codeelemente für viele verschiedene Arten von Leerzeichen bereit, diese Funktion erkennt jedoch nur das Unicode-Codeelement 0x0020. DBCS-Zeichenfolgen, die in Unicode konvertiert werden, enthalten u. U. andere Leerzeichen als 0x0020. Diese Leerzeichen können von der Funktion nicht entfernt werden. Zum Entfernen aller Arten von Leerzeichen können Sie die RTrim-Methode von Microsoft Visual Basic .NET in einem Skript verwenden, das aus der Skriptkomponente ausgeführt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RTRIM(character expression)  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ein Zeichenausdruck, aus dem Leerzeichen entfernt werden sollen.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 RTRIM kann nur mit dem DT_WSTR-Datentyp verwendet werden. Ein *character_expression* -Argument, das ein Zeichenfolgenliteral oder eine Datenspalte mit dem DT_STR-Datentyp ist, wird implizit in den DT_WSTR-Datentyp umgewandelt, bevor RTRIM ausgeführt wird. Andere Datentypen müssen explizit in den DT_WSTR-Datentyp umgewandelt werden. Weitere Informationen finden Sie unter [Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md) und [CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 RTRIM gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel werden nachfolgende Leerzeichen aus einem Zeichenfolgenliteral entfernt. Als Ergebnis wird "Hello" zurückgegeben.  
  
```  
RTRIM("Hello   ")  
```  
  
 In diesem Beispiel werden nachfolgende Leerzeichen aus einer Verkettung der Spalten **FirstName** und **LastName** entfernt.  
  
```  
RTRIM(FirstName + " " + LastName)  
```  
  
 In diesem Beispiel werden nachfolgende Leerzeichen aus der **FirstName** -Variablen entfernt.  
  
```  
RTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [LTRIM &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)   
 [TRIM &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/trim-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
