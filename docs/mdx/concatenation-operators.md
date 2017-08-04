---
title: Verkettungsoperatoren | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- concatenation operators [MDX]
ms.assetid: 9e4c181a-b71e-41ec-98a1-ec8b5b5103b1
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ae299577ece2c712504631fb85eeac4499c4d4c7
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="concatenation-operators"></a>Operator für Verkettungen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Der Operator für Verkettungen ist das Pluszeichen (+). Sie können zwei oder mehr Zeichenfolgen zu einer einzelnen Zeichenfolge kombinieren oder verketten. Sie können auch binäre Zeichenfolgen verketten.  
  
 Der folgende Code ist ein Beispiel für den Operator für Verkettungen, der hier den Produktnamen mit dem eindeutigen Namen des Produkts kombiniert.  
  
```  
WITH MEMBER Measures.ProductName AS   
   Product.Product.CurrentMember.Name + " (" + Product.Product.CurrentMember.UniqueName + ")"  
SELECT   
   {Measures.ProductName} ON COLUMNS,  
   Product.Product.Members ON ROWS  
FROM [Adventure Works]  
```  
  
## <a name="language-considerations"></a>Sprachbezogene Aspekte  
 Haben die beiden in einer Verkettung verwendeten Zeichenfolgen dieselbe Sortierung, hat die sich ergebende verkettete Zeichenfolge dieselbe Sortierung wie die Eingaben. Haben die in einer Verkettung verwendeten Zeichenfolgen unterschiedliche Sortierungen, wird die Sortierung der sich ergebenden verketteten Zeichenfolge durch die Regeln für die Sortierungsrangfolge bestimmt. Weitere Informationen finden Sie unter [Sprachen und Sortierungen &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operatoren &#40; MDX-Syntax &#41;](../mdx/operators-mdx-syntax.md)  
  
  

