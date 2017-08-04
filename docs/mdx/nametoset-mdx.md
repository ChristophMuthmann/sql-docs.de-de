---
title: NameToSet (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NAMETOSET
dev_langs:
- kbMDX
helpviewer_keywords:
- NameToSet function
ms.assetid: e02e17d5-4309-49cb-84c7-5b445ac2bd94
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b615ddfdf8698e1d495e6d6070e489aa448d4c96
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="nametoset-mdx"></a>NameToSet (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Menge zurück, die das durch eine Zeichenfolge im MDX-Format (Multidimensional Expressions) angegebene Element enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
NameToSet(Member_Name)   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Name*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen eines Elements darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der angegebene Elementname vorhanden ist, die **NameToSet** Funktion gibt eine Menge mit diesem Element zurück. Andernfalls gibt die Funktion eine leere Menge zurück.  
  
> [!NOTE]  
>  Der angegebene Elementname muss zwingend ein Elementname sein. Ein Elementausdruck ist nicht zulässig. Um einen Elementausdruck verwenden zu können, finden Sie unter [StrToSet &#40; MDX &#41; ](../mdx/strtoset-mdx.md).  
  
## <a name="example"></a>Beispiel  
 Im Folgenden wird der Standardmeasurewert des angegebenen Elementnamens zurückgegeben.  
  
```  
SELECT NameToSet('[Date].[Calendar].[July 2001]') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

