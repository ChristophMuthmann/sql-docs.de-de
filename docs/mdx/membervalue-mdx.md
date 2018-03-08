---
title: MemberValue (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MEMBERVALUE
dev_langs: kbMDX
helpviewer_keywords: MemberValue function
ms.assetid: f9b2af16-2b81-48e4-ae81-99f64e4bbc98
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 615b49f12079b8cf47045e3c56635e17fcdae691
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den Wert eines Elements zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der zu einem Element ausgewertet wird.  
  
## <a name="return-value"></a>Rückgabewert  
 Der zurückgegebene Elementwert enthält die folgenden Informationen, die in der Reihenfolge aufgelistet werden, in der diese im Rückgabewert angezeigt werden:  
  
-   Die Wertbindung, sofern diese definiert wurde.  
  
-   Der Schlüssel mit dem ursprünglichen Datentyp, wenn keine Namensbindung vorhanden ist bzw. der Schlüssel und die Beschriftung an dieselbe Spalte gebunden sind.  
  
-   Die Beschriftung des Elements.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden die Wertbindung, der Elementschlüssel sowie die Beschriftung für das erste Datum in der Date-Dimension im Adventure Works-Cube zurückgegeben.  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
