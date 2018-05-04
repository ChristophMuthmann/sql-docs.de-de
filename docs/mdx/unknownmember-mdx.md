---
title: UnknownMember (MDX) | Microsoft Docs
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
- UnknownMember
dev_langs:
- kbMDX
helpviewer_keywords:
- UnknownMember function
ms.assetid: 5ae39cbe-65c8-4a59-9548-71b28ecf6eb5
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 7fe0fe0706d6b88c19f5683a71de15516dddecec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="unknownmember-mdx"></a>UnknownMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das einer Ebene oder einem Element zugeordnete unbekannte Element zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member expression syntax  
Member_Expression.UnknownMember  
  
Hierarchy_expression syntax  
Hierarchy_Expression.UnknownMember  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Hierarchy_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] erstellt ein unbekanntes Element um eine Hierarchie Faktentabellendaten zuordnen, wenn die Hierarchie nicht bekannt ist. Das unbekannte Element kann sich auf einer der folgenden Ebenen befinden:  
  
-   Auf der obersten Ebene für nicht aggregierte Attributhierarchien.  
  
-   Bei der ersten Ebene unter der **alle** -Ebene für natürliche Hierarchien.  
  
-   Auf jeder Ebene für unnatürliche Hierarchien.  
  
 Wenn ein Elementausdruck angegeben ist, die **UnknownMember** Funktion gibt das unbekannte untergeordnete Element des angegebenen Elements zurück. Wenn das angegebene Element nicht vorhanden ist, gibt die Funktion den Wert NULL zurück.  
  
 Wenn ein Hierarchieausdruck angegeben wird, die **UnknownMember** -Funktion das unbekannte Element auf der obersten Ebene zurückgegeben, falls vorhanden.  
  
 Wenn das unbekannte Element nicht, auf der Ebene oder einem Element vorhanden ist, das **UnknownMember** -Funktion erstellt ein null-Element.  
  
> [!NOTE]  
>  Wenn kein unbekanntes Element in der Hierarchie oder für das Element vorhanden ist, wird ein Fehler generiert.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das unbekannte Element für das All Products-Element in der Product-Attributhierarchie für alle Elemente der Measures-Dimension zurückgegeben.  
  
```  
SELECT [Product].[Product].[All Products].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird das unbekannte Element für die Product Categories-Hierarchie für alle Elemente der Measures-Dimension zurückgegeben.  
  
```  
SELECT [Product].[Product Categories].UnknownMember  
    ON Columns,  
[Measures].Members  
    ON Rows  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
