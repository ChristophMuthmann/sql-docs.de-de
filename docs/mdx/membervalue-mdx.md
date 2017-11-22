---
title: MemberValue (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
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
ms.openlocfilehash: 2d6a74903eb98002864e8d3ae5a68e5af4f07112
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  
