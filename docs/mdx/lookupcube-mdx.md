---
title: LookupCube (MDX) | Microsoft Docs
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
- LOOKUPCUBE
dev_langs:
- kbMDX
helpviewer_keywords:
- LookupCube function
ms.assetid: 243fa101-328a-4016-86e0-d8b5977e15a9
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 3cc97425397a1ddbc025e53a81526b7a37ed2ad5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="lookupcube-mdx"></a>LookupCube (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
