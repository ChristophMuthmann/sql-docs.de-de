---
title: DefaultMember (MDX) | Microsoft Docs
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
- DefaultMember
dev_langs:
- kbMDX
helpviewer_keywords:
- DefaultMember function
ms.assetid: c1b53b3a-6e73-4c41-a4fe-9f5c96da5463
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 738d66b3c6486c51978d3a68f5fbca73598c0382
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt das Standardelement einer Hierarchie zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>Argumente  
 *Hierarchy_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Das Standardelement eines Attributs wird zum Auswerten von Ausdrücken verwendet, wenn ein Attribut nicht in einer Abfrage enthalten ist.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die **DefaultMember** -Funktion in Verbindung mit der **Namen** -Funktion verwendet, um das Standardelement der Destination Currency-Dimension im Adventure Works-Cube zurückzugeben. Das Beispiel gibt **US-Dollar**. Die **Namen** Funktion dient zum Zurückgeben der Name des Measures anstelle der Standardeigenschaft des Measures, also **Wert**.  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [Definieren eines Standardelements](../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  

