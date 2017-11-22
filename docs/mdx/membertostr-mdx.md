---
title: MemberToStr (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MEMBERTOSTR
dev_langs: kbMDX
helpviewer_keywords: MemberToStr function
ms.assetid: 2076b24a-603a-4d74-91bd-a3d347739bcd
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: afbc6a17e21b36f2235f5213e6a869641333fb9d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeichenfolge im MDX-Format (Multidimensional Expressions) zurück, die einem angegebenen Element entspricht.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion gibt eine Zeichenfolge zurück, die den eindeutigen Namen eines Elements enthält. Sie wird in der Regel verwendet, um den eindeutigen Namen eines Elements an eine externe Funktion zu übergeben.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Zeichenfolge [Geography].[Geography].[Country].&[United States] zurückgegeben:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
