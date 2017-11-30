---
title: "Unäre Operatoren | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: unary operators
ms.assetid: bf1b5518-6040-4484-9ce8-79c0eb4373a9
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a2dd50160dbe0185056988cfd866f119d7e330c4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
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
 [Operatoren &#40; MDX-Syntax &#41;](../mdx/operators-mdx-syntax.md)  
  
  
