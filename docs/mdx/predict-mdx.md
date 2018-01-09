---
title: Vorhersagen (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PREDICT
dev_langs: kbMDX
helpviewer_keywords: Predict function
ms.assetid: a82f3edd-249b-4559-98d3-6e10d81a095d
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d7266e462167dcae27a30b033c368f910b6dfc0f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="predict-mdx"></a>Predict (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

    
> [!CAUTION]  
>  Diese Funktion wird derzeit aufgrund interner Inkonsistenzen entfernt.  
>   
>  Im Beispielabschnitt finden Sie eine Problemumgehung, in der ein DMX-Ausdruck verwendet wird.  
  
 Gibt einen Wert eines numerischen Ausdrucks zurück, der über einem Data Mining-Modell ausgewertet wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Predict(Mining_Model_Name,String_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Mining_Model_Name*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen eines Miningmodells darstellt.  
  
 *String_Expression*  
 Ein gültiger Zeichenfolgenausdruck, der einen gültigen DMX-Ausdruck für das angegebene Miningmodell ergibt.  
  
## <a name="remarks"></a>Remarks  
 Die **Predict** -Funktion wertet den angegebenen Zeichenfolgenausdruck innerhalb des Kontexts des angegebenen Miningmodells.  
  
 Data Mining-Syntax und -Funktionen werden im Data Mining Expressions (DMX)-Verweis dokumentiert.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden mittels des Customer Clusters-Miningmodells der Name des Clusters und die Entfernung eines bestimmten Kunden von diesem vorhergesagt:  
  
```  
WITH MEMBER MEASURES.CLNAME AS   
PREDICT("Customer Clusters", "Cluster()")  
MEMBER MEASURES.CLDISTANCE AS   
PREDICT("Customer Clusters", "ClusterDistance(Cluster())")  
SELECT {MEASURES.CLNAME, MEASURES.CLDISTANCE} ON 0   
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Customer].&[12012])  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
