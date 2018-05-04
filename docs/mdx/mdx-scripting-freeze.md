---
title: FREEZE-Anweisung (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FREEZE
dev_langs:
- kbMDX
helpviewer_keywords:
- FREEZE statement
- locking cell values [MDX]
ms.assetid: 59f1e860-6f37-41af-97d6-7708bdaac933
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: bf02f73b4c1de617a0c66e34882cc63c32cd0517
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-scripting---freeze"></a>MDX-Skripts - fixiert werden soll
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Fixiert die Zellenwerte eines angegebenen Teilcubes auf die aktuellen Werte. Wenn die Zellenwerte fixiert sind, wirken sich Änderungen an anderen Zellen nicht auf die fixierten Zellen aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>Argumente  
 *Subcube_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der einen Teilcube zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **FIXIEREN** -Anweisung fixiert die Werte von Zellen in einem angegebenen Teilcube, sodass nachfolgende Anweisungen in einem MDX Skript ändern ihrer Werte in nachfolgenden Berechnungsdurchläufen übergibt.  
  
 Im folgenden Beispiel stellen A und B Teilcubes in einem MDX-Berechnungsskript dar:  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 An diesem Punkt ist sowohl A als auch B gleich 3.  
  
 Wir fügen Sie nun die **fixieren** Funktion, die Zellen im Teilcube A zu sperren:  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 A ist jetzt gleich 2, und B ist gleich 3.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Skriptanweisungen & #40; MDX & #41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
