---
title: AddCalculatedMembers (MDX) | Microsoft Docs
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
- ADDCALCULATEDMEMBERS
dev_langs:
- kbMDX
helpviewer_keywords:
- AddCalculatedMembers function
ms.assetid: c676cf70-7c24-46ea-b88c-d4a389a71d48
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 772e3855c08a863e9bba8c0197731614fd8a3095
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Menge zurück, die durch Hinzufügen berechneter Elemente zu einer angegebenen Menge erstellt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Standardmäßig schließt MDX berechnete Elemente beim Auflösen von Mengenfunktionen aus. Die **AddCalculatedMembers** -Funktion untersucht den Mengenausdruck *Set_Expression,* und schließt berechnete Elemente, die gleichgeordnete Elemente enthalten, die innerhalb des Bereichs der sind dieses Mengenausdrucks.  
  
> [!NOTE]  
>  Die Funktion kann nur mit eindimensionalen Mengenausdrücken verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Verwendung dieser Funktion.  
  
```  
-- This query returns the calculated members for the cube  
-- by retrieving all members, and then excluding non-calculated members.  
SELECT   
   AddCalculatedMembers(  
      {[Measures].Members}  
      )-[Measures].Members ON COLUMNS  
FROM [Adventure Works]   
```  
  
 Das folgende Beispiel gibt die `Measures.[Unit Price]` -Element zusätzlich zu allen berechneten Elementen in der **Measures** Dimension, aus der **Adventure Works** Cube.  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

