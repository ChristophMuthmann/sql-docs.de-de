---
title: Untergeordnete Elemente (MDX) | Microsoft Docs
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
- CHILDREN
dev_langs:
- kbMDX
helpviewer_keywords:
- Children function
ms.assetid: ce2c3069-914c-44a3-8a4c-5cbd4fb71e4c
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 03cb4f1a05e9be35a92c63c5904816ed8d0ad227
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="children-mdx"></a>Children (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Menge der untergeordneten Elemente eines angegebenen Elements zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.Children  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Kinder** Funktion gibt eine natürlich geordnete Menge, die die untergeordneten Elemente eines angegebenen Elements enthält. Wenn das angegebene Element nicht über untergeordnete Elemente verfügt, gibt die Funktion eine leere Menge zurück.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden die untergeordneten Elemente des United States-Element der Geography-Hierarchie in der Geography-Dimension zurückgegeben.  
  
```  
SELECT [Geography].[Geography].[Country].&[United States].Children ON 0  
FROM [Adventure Works]  
```  
  
 Das folgende Beispiel gibt alle Elemente in der **Measures** Dimension auf der Spaltenachse einschließlich aller berechneten Elemente sowie die Menge aller untergeordneten Elemente der der `[Product].[Model Name]` -Attributhierarchie auf der Zeilenachse der **Adventure Works** Cube.  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
  
```  
  
|Release|Verlauf|  
|-------------|-------------|  
|[!INCLUDE[ssBOL2005_R03](../includes/ssbol2005-r03-md.md)]|**Geänderter Inhalt:**<br /> – Syntax und Argumente zur Verdeutlichung aktualisiert.<br /><br /> – Aktualisierte Beispiele wurden hinzugefügt.|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
