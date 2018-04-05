---
title: ODER (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OR
dev_langs:
- kbMDX
helpviewer_keywords:
- OR operator
ms.assetid: 7634c08a-5b70-44cd-9422-6555fed6ae05
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3816be8be6945e21d3e6863292d4ed718a2352a2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="or-mdx"></a>OR (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt eine logische Disjunktion mit zwei numerischen Ausdrücken aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>Parameter  
 Expression1  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der einen numerischen Wert zurückgibt.  
  
 Expression2  
 Ein gültiger MDX-Ausdruck, der einen numerischen Wert zurückgibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein boolescher Wert, der zurückgibt **"true"** Wenn eines oder beide Argumente ausgewertet **"true"**ist, andernfalls **"false"**.  
  
## <a name="remarks"></a>Remarks  
 Die **oder** -Operator behandelt beide Argumente als boolesche Werte (null, 0, als **"false"**ist, andernfalls **"true"**), bevor der Operator die logische Disjunktion ausführt. Die folgende Tabelle verdeutlicht, wie die **oder** Operator die logische Disjunktion ausführt.  
  
|*Expression1*|*Expression2*|Rückgabewert|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>Beispiel  
 Die folgende Abfrage enthält ein berechnetes Measure, das die Zeichenfolge "MARRIED OR MALE" zurückgibt, wenn das aktuelle Element auf der Geschlechtshierarchie der Customer-Dimension Männlich oder das aktuelle Element auf der Ehestatushierarchy der Customer-Dimension "Married" ist. Andernfalls wird die Zeichenfolge "UNMARRIED OR FEMALE" zurückgegeben.  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
