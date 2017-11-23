---
title: LookupCube (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LOOKUPCUBE
dev_langs: kbMDX
helpviewer_keywords: LookupCube function
ms.assetid: 243fa101-328a-4016-86e0-d8b5977e15a9
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ecd1810908dfda4d3e9f4e8c36d4c35ba6e37185
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Wert eines MDX-Ausdrucks (Multidimensional Expressions) zurück, der über einem anderen angegebenen Cube in derselben Datenbank ausgewertet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Numeric expression syntax  
LookupCube(Cube_Name, Numeric_Expression )  
  
String expression syntax  
LookupCube(Cube_Name, String_Expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen eines Cubes angibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
 *String_Expression*  
 Ein gültiger Zeichenfolgenausdruck, bei dem es sich in der Regel um einen gültigen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, der eine Zeichenfolge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Ausdruck angegeben wird, die **LookupCube** Funktion wertet den angegebenen numerischen Ausdruck im angegebenen Cube, und gibt den sich ergebenden numerischen Wert zurück.  
  
 Wenn ein Zeichenfolgenausdruck angegeben wird, die **LookupCube** Funktion wertet den angegebenen Zeichenfolgenausdruck im angegebenen Cube, und gibt den sich ergebenden Zeichenfolgenwert zurück.  
  
 Die **LookupCube** -Funktion kann für Cubes innerhalb derselben Datenbank, da der Quellcube, auf denen die MDX-Abfrage, die enthält, die **LookupCube** Funktion ausgeführt wird.  
  
> [!IMPORTANT]  
>  Sie müssen alle notwendigen aktuellen Elemente in dem numerischen oder Zeichenfolgenausdruck angeben, da der Kontext der aktuellen Abfrage nicht für den abgefragten Cube übernommen wird.  
  
 Jeder Berechnung mithilfe der **LookupCube** Funktion unterscheidet sich wahrscheinlich unter schlechter Leistung darunter leiden. Überlegen Sie sich, die Lösung umzugestalten anstatt diese Funktion zu verwenden, damit alle Daten, die Sie benötigen, in einem Cube vorhanden sind.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Abfrage veranschaulicht die Verwendung von LookupCube:  
  
 `WITH MEMBER MEASURES.LOOKUPCUBEDEMO AS`  
  
 `LOOKUPCUBE("Adventure Works", "[Measures].[In" + "ternet Sales Amount]")`  
  
 `SELECT MEASURES.LOOKUPCUBEDEMO  ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
