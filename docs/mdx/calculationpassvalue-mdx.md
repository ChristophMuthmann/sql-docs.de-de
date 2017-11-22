---
title: CalculationPassValue (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CALCULATIONPASSVALUE
dev_langs: kbMDX
helpviewer_keywords: CalculationPassValue function
ms.assetid: 1b4012cb-c8c7-441a-bb9c-59430703b189
caps.latest.revision: "45"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 749d3329c4036616c937158f80e818c90a09c3ef
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue (MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt entweder den numerischen oder den Zeichenfolgenwert eines MDX-Ausdrucks (Multidimensional Expressions) zurück, der über den angegebenen Berechnungsdurchlauf eines Cubes ausgewertet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      Numeric syntax  
CalculationPassValue(Numeric_Expression,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
String syntax  
CalculationPassValue(String_Expression ,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
```  
  
## <a name="arguments"></a>Argumente  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
 *String_Expression*  
 Ein gültiger Zeichenfolgenausdruck, bei dem es sich in der Regel um einen gültigen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, der eine als Zeichenfolge ausgedrückte Zahl zurückgibt.  
  
 *Pass_Value*  
 Ein gültiger numerischer Ausdruck, der die Berechnungsdurchlaufnummer angibt.  
  
 ABSOLUTE  
 Ein zugriffsflagwert, der angibt, die *Pass_Value* Parameter enthält den nullbasierten Index des Berechnungsdurchlaufs. ABSOLUTE ist der Standard-Zugriffsflagwert, der verwendet wird, wenn kein Zugriffsflagwert angegeben ist.  
  
 RELATIVE  
 Ein zugriffsflagwert, der angibt, die *Pass_Value* Parameter enthält einen relativen Offset vom Berechnungsdurchlauf der auslösenden Berechnung. Wenn der Offset in einen Berechnungsdurchlaufindex kleiner als null (0) aufgelöst wird, wird Berechnungsdurchlauf 0 verwendet, und es tritt kein Fehler auf.  
  
 ALL  
 Wenn dieses Flag festgelegt wird, sind alle Werte NULL, die nicht vom Speichermodul geladen werden. Wenn das Flag nicht festgelegt wird, werden die Werte ohne jegliche Berechnungen aggregiert.  
  
## <a name="remarks"></a>Hinweise  
 Bei einem numerischer Ausdruck gibt die Funktion einen numerischen Wert zurück, indem sie den angegebenen numerischen MDX-Ausdruck im angegebenen Berechnungsdurchlauf auswertet, optional geändert durch ein Zugriffsflag und einen Zugriffsflagmodifizierer.  
  
 Wenn ein Zeichenfolgenausdruck angegeben wird, die Funktion gibt einen Zeichenfolgenwert zurück, durch das Auswerten des angegebene MDX-Zeichenfolgenausdruck im angegebenen Berechnungsdurchlauf auswertet, und optional geändert durch ein Zugriffsflag und einen zugriffsflagmodifizierer*.*  
  
 Durch die automatische rekursionsauflösung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], diese Funktion hat kaum noch praktischen nutzen.  
  
> [!NOTE]  
>  Nur Administratoren können die **CalculationPassValue** Funktion innerhalb eines MDX-Skripts. Wenn ein MDX-Skript mit dieser Funktion im Kontext einer Rolle ausgeführt wird, die nicht über Administratorprivilegien verfügt, tritt ein Fehler auf.  
  
## <a name="see-also"></a>Siehe auch  
 [CalculationCurrentPass &#40; MDX &#41;](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40; MDX &#41;](../mdx/iif-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
