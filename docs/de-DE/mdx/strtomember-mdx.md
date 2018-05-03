---
title: StrToMember (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STRTOMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- StrToMember function
ms.assetid: eb8a3dc0-5ae4-434e-b321-680a81a59e67
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 32cd3674777bf309a9c23f9021208749c15d489f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="strtomember-mdx"></a>StrToMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das durch eine Zeichenfolge im MDX-Format (Multidimensional Expressions) angegebene Element zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Name*  
 Ein gültiger Zeichenfolgenausdruck, der direkt oder indirekt ein Element angibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **StrToMember** -Funktion gibt den im Zeichenfolgenausdruck angegebene Element zurück. Die **StrToMember** Funktion wird meist mit benutzerdefinierten Funktionen verwendet, um eine Elementspezifikation aus einer externen Funktion zurück, an eine MDX-Anweisung, oder wenn eine MDX-Abfrage parametrisiert wird.  
  
-   Wenn das CONSTRAINED-Flag verwendet wird, muss der Elementname direkt zu einem qualifizierten oder nicht qualifizierten Elementnamen aufgelöst werden können. Dieses Flag wird verwendet, um das Risiko von Injection-Angriffen über die angegebene Zeichenfolge zu reduzieren. Wenn eine Zeichenfolge bereitgestellt wird, die nicht direkt zu einem qualifizierten oder nicht qualifizierten Elementnamen aufgelöst werden kann, wird eine Fehlermeldung angezeigt, die besagt, dass die durch das CONSTRAINED-Flag in der STRTOMEMBER-Funktion vorgegebenen Einschränkungen verletzt wurden.  
  
-   Wenn das CONSTRAINED-Flag nicht verwendet wird, kann das angegebene Element entweder direkt zu einem Elementnamen aufgelöst werden oder zu einem gültigen MDX-Ausdruck (Multidimensional Expressions) aufgelöst werden, der zu einem Namen aufgelöst wird.  
  
-   Weitere Informationen zu den Unterschieden zwischen Mengen und Elementen finden Sie in den Abschnitten "Verwenden von Mengenausdrücken" und "Verwenden von Elementausdrücken".  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel gibt das Reseller Sales Amount-Measure für das Bayern-Element in der State-Province-Attributhierarchie mit der **StrToMember** Funktion. Die angegebene Zeichenfolge stellt den qualifizierten Elementnamen bereit.  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 Das folgende Beispiel gibt das Reseller Sales Amount-Measure für das Bayern-Element, das mit der **StrToMember** Funktion. Da der Elementname nur einen nicht qualifizierten Elementnamen bereitstellt, gibt die Abfrage die erste Instanz des angegebenen Elements zurück, die sich in diesem Fall in der Customer Geography-Hierarchie in der Customer-Dimension befindet, die sich nicht mit Reseller Sales überschneidet. Die bewährte Methode sieht vor, immer den qualifizierten Namen anzugeben, um erwartete Ergebnisse zu erhalten.  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 Im folgende Beispiel gibt das Reseller Sales Amount-Measure für das Bayern-Element in der State-Province-Attributhierarchie mit der **StrToMember** Funktion. Der bereitgestellte Elementname wird zu einem qualifizierten Elementnamen aufgelöst.  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird aufgrund des CONSTRAINED-Flags ein Fehler zurückgegeben. Die bereitgestellte Elementnamen-Zeichenfolge enthält zwar einen gültigen MDX-Elementausdruck, der zu einem qualifizierten Elementnamen aufgelöst wird, das CONSTRAINED-Flag erfordert jedoch qualifizierte oder nicht qualifizierten Elementnamen in der Elementnamen-Zeichenfolge.  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
