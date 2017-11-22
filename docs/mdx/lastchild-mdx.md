---
title: LastChild (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LASTCHILD
dev_langs: kbMDX
helpviewer_keywords: LastChild function
ms.assetid: 70d09bd0-4330-4be8-8bb5-7a30f44fb4ae
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7616f8a23386bac4e92049236acbe53bd7adc0e7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lastchild-mdx"></a>LastChild (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt das letzte untergeordnete Element eines Elements zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.LastChild   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der Wert für September 2001 zurückgegeben, das letzte untergeordnete Element des ersten Geschäftsquartals des Geschäftsjahres 2002.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002].LastChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [FirstChild &#40; MDX &#41;](../mdx/firstchild-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
