---
title: Unäre Operatoren | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- unary operators
ms.assetid: bf1b5518-6040-4484-9ce8-79c0eb4373a9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 4ee37e10238e0c06b72ae4b188ffbbc740be8335
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="unary-operators"></a>Unäre Operatoren
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  In MDX (Multidimensional Expressions) führt ein unärer Operator einen Vorgang für einen einzelnen Operanden aus, z. B. das Zurückgeben eines negativen oder positiven Wertes eines numerischen Ausdrucks.  
  
 MDX unterstützt die unären Operatoren, die in der folgenden Tabelle aufgelistet sind.  
  
|Operator|Description|  
|--------------|-----------------|  
|[- (Negative) (- (Negativ))](../mdx/negative-mdx.md)|Gibt den negativen Wert eines numerischen Ausdrucks zurück.|  
|[+ (Positive) (+ (Positiv))](../mdx/positive-mdx.md)|Gibt den positiven Wert eines numerischen Ausdrucks zurück.|  
  
 Im folgenden Beispiel wird gezeigt, wie ein unärer Operator verwendet wird, um den negativen Wert eines Measures zurückzugeben.  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 Darüber hinaus mit MDX spezielle unäre Operatoren verwendet, um die durchgeführte Aggregationsvorgang zu bestimmen die [RollupChildren](../mdx/rollupchildren-mdx.md) Funktion. Weitere Informationen zu diesen speziellen Unäroperatoren, finden Sie unter [Hinzufügen einer benutzerdefinierten Aggregation zu einer Dimension](../analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Operatoren &#40;MDX-Syntax&#41;](../mdx/operators-mdx-syntax.md)  
  
  
