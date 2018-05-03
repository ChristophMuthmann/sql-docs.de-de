---
title: Dimensionen (MDX) | Microsoft Docs
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
- Dimensions
dev_langs:
- kbMDX
helpviewer_keywords:
- Dimensions function
ms.assetid: 64f63aa0-ef74-4415-a0c9-8acc6cd81739
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 493a17424410155be360828e7c998335c2f11aad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dimensions-mdx"></a>Dimensionen (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Hierarchie zurück, die durch einen numerischen Ausdruck oder einen Zeichenfolgenausdruck angegeben ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>Argumente  
 *Hierarchy_Number*  
 Ein gültiger numerischer Ausdruck, der eine Hierarchienummer angibt.  
  
 *Hierarchiename*  
 Ein gültiger Zeichenfolgenausdruck, der einen Hierarchienamen angibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Hierarchienummer angegeben wird, die **Dimensionen** Funktion gibt eine Hierarchie, deren nullbasierte Position innerhalb des Cubes ist angegebenen Hierarchienummer entspricht.  
  
 Wenn ein Hierarchiename angegeben wird, die **Dimensionen** Funktion die angegebene Hierarchie zurück. Normalerweise verwenden Sie diese Zeichenfolgenversion der **Dimensionen** -Funktion mit benutzerdefinierten Funktionen.  
  
> [!NOTE]  
>  Die **Measures** Dimension immer dargestellte `Dimensions(0)`.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele verwenden die **Dimensionen** -Funktion Name, der die Anzahl der Ebenen und der Anzahl von Elementen einer angegebenen Hierarchie, die mithilfe eines numerischen Ausdrucks und einem Zeichenfolgenausdruck zurück.  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
