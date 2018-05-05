---
title: StrToSet (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STRTOSET
dev_langs:
- kbMDX
helpviewer_keywords:
- StrToSet function
ms.assetid: 1700a563-6527-450a-8d3b-975c65bb6e51
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 34008751a017e97d353cca7c90db1de5e6710d98
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die durch eine Zeichenfolge im MDX-Format (Multidimensional Expressions) angegebene Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Specification*  
 Ein gültiger Zeichenfolgenausdruck, der direkt oder indirekt eine Menge angibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **StrToSet** Funktion gibt den im Zeichenfolgenausdruck angegebenen Satz zurück. Die **StrToSet** Funktion wird in der Regel mit benutzerdefinierten Funktionen verwendet, um eine mengenspezifikation aus einer externen Funktion zurück, an eine MDX-Anweisung, oder wenn eine MDX-Abfrage parametrisiert wird.  
  
-   Wenn das CONSTRAINED-Flag verwendet wird, darf die mengenspezifikation qualifizierte oder nicht qualifizierte Elementnamen enthalten oder eine Menge von Tupeln, die qualifizierte oder nicht qualifizierte Elementnamen in geschweiften Klammern enthält {}. Dieses Flag wird verwendet, um das Risiko von Injection-Angriffen über die angegebene Zeichenfolge zu reduzieren. Wenn eine Zeichenfolge bereitgestellt wird, die nicht direkt zu qualifizierten oder nicht qualifizierten Elementnamen aufgelöst werden kann, wird eine Fehlermeldung angezeigt, die besagt, dass die durch das CONSTRAINED-Flag in der STRTOSET-Funktion vorgegebenen Einschränkungen verletzt wurden.  
  
-   Wenn das CONSTRAINED-Flag nicht verwendet wird, kann der angegebene Mengenausdruck zu einem gültigen MDX-Ausdruck (Multidimensional Expressions) aufgelöst werden, der eine Menge zurückgibt.  
  
-   Weitere Informationen zu den Unterschieden zwischen Mengen und Elementen finden Sie in den Abschnitten "Verwenden von Mengenausdrücken" und "Verwenden von Elementausdrücken".  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die Menge der Elemente der State-Province-Attributhierarchie mit der **StrToSet** Funktion. Die Mengenspezifikation stellt einen gültigen MDX-Mengenausdruck bereit.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird aufgrund des CONSTRAINED-Flags ein Fehler zurückgegeben. Die Mengenspezifikation stellt zwar einen gültigen MDX-Mengenausdruck bereit, das CONSTRAINED-Flag erfordert jedoch qualifizierte oder nicht qualifizierte Elementnamen in der Mengenspezifikation.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird das Reseller Sales Amount-Measure für die Country-Elemente Germany und Canada zurückgegeben. Die in der angegebenen Zeichenfolge bereitgestellte Mengenspezifikation enthält qualifizierte Elementnamen, wie vom CONSTRAINED-Flag angefordert.  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
