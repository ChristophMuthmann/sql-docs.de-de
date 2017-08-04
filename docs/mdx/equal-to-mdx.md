---
title: = (Gleich) (MDX) | Microsoft Docs
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
- =
dev_langs:
- kbMDX
helpviewer_keywords:
- equals operator (=)
- = (equals operator)
ms.assetid: 5e1f3b58-a646-4fc1-a3f1-19090a5437b7
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9e446cf812f57a3cc3df74728b74c072d1b089bc
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="-equal-to-mdx"></a>= (Ist gleich) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt eine Vergleichsoperation aus, die bestimmt, ob der Wert eines MDX-Ausdrucks (Multidimensional Expressions) gleich dem Wert eines anderen MDX-Ausdrucks ist.  
  
> [!NOTE]  
>  Um Objekte zu vergleichen, verwenden Sie die [IS &#40; MDX &#41; ](../mdx/is-mdx.md) Operator. Verwenden Sie z. B. den IS-Operator, um zu prüfen, ob das aktuelle Element auf einer Abfrageachse ein spezifisches Element ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>Parameter  
 *MDX_Expression*  
 Ein gültiger MDX-Ausdruck.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der auf den folgenden Bedingungen basiert:  
  
-   **"true"** , wenn der Wert des ersten Parameters gleich dem Wert des zweiten Parameters ist.  
  
-   **"false"** , wenn der Wert des ersten Parameters ungleich dem Wert des zweiten Parameters ist.  
  
-   **"true"** Wenn beide Parameter null sind oder einen Parameter null ist, und der andere Parameter 0 ist gleich.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Abfrage enthält Beispiele für diese Bedingungen:  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

