---
title: Cousin (MDX) | Microsoft Docs
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
- COUSIN
dev_langs:
- kbMDX
helpviewer_keywords:
- Cousin function
ms.assetid: 9a416685-d35d-4d9c-a9f6-4574cbe59aea
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8f8e73b19a5c2253275852e38988f1a85a5c9472
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="cousin-mdx"></a>Cousin (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt das untergeordnete Element mit derselben relativen Position unter einem übergeordneten Element wie das angegebene untergeordnete Element zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Ancestor_Member_Expression*  
 Ein gültiger MDX-Elementausdruck (Multidimensional Expressions), der ein Vorgängerelement zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion bezieht sich auf die Reihenfolge und Position von Elementen in Ebenen. Wenn zwei Hierarchien gegeben sind, von denen die eine vier Ebenen und die andere fünf Ebenen aufweist, entspricht der Cousin der dritten Ebene der ersten Hierarchie der dritten Ebene der zweiten Hierarchie.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Cousin des vierten Quartals des Geschäftsjahres 2002 basierend auf seinem Vorgänger auf der Year-Ebene im Geschäftsjahr 2003 abgerufen. Der abgerufene Cousin ist das vierte Quartal des Geschäftsjahres 2003.  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird der Cousin des Monats Juli des Geschäftsjahres 2002 basierend auf seinem Vorgänger auf der Quarter-Ebene im zweiten Quartal des Geschäftsjahres 2004 abgerufen. Der abgerufene Cousin ist der Monat Oktober 2003.  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

