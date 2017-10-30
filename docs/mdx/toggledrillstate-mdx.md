---
title: ToggleDrillState (MDX) | Microsoft Docs
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
- TOGGLEDRILLSTATE
dev_langs:
- kbMDX
helpviewer_keywords:
- ToggleDrillState function
ms.assetid: 26fa1a0d-3ed1-45dc-955d-0591d49e4db9
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3b9676ef7df22333d4b9674f7b14744a17bf5b0f
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Schaltet den Drillstatus von Elementen zwischen den Modi für Drilldown und Drillup um.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Set_Expression2*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Rekursive*  
 (Optional). Ein Schlüsselwort, das einen rekursiven Vergleich von Mengen angibt. Die **ToggleDrillState** Funktion ist eine Kombination der **DrillupMember** und **DrilldownMember** Funktionen. Rekursion gilt nur, wenn das Element enthalten ist das **DrilldownMember** Zustand.  
  
 *Include_calc_members*  
 (Optional). Ein Flag, das anzeigt, ob berechnete Elemente eingeschlossen werden sollen, wenn sie vorhanden sind (auf Drilldownebene).  
  
## <a name="remarks"></a>Hinweise  
 Die **ToggleDrillState** -Funktion schaltet den Drillstatus für jedes Element der zweiten Menge, die in der ersten Menge vorhanden ist. Die erste Menge kann Tupel beliebiger Dimensionalität aufweisen, die zweite Menge muss jedoch ausschließlich Elemente einer einzigen Dimension enthalten. Die **ToggleDrillState** Funktion ist eine Kombination der **DrillupMember** und **DrilldownMember** Funktionen. Wenn das Element *m*der zweiten Menge in der ersten Menge vorhanden ist und diesem Element ein Drilldown ist (d. h., hat der m unmittelbar folgt), klicken Sie dann `DrillupMember(Set_Expression1, {m})` auf das Element oder Tupel in der ersten Menge angewendet wird. Wenn für das *m* Element wird oben ein Drilldown ausgeführt (es ist keine Nachfolger des *m* , die unmittelbar folgt *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` auf der ersten Menge angewendet wird.  
  
 Wenn das optionale **REKURSIVE** Flag verwendet wird, werden Sie Drillup und Drilldown rekursiv angewendet. Weitere Informationen über das rekursive Flag finden Sie unter der [DrillupMember](../mdx/drillupmember-mdx.md) und [DrilldownMember](../mdx/drilldownmember-mdx.md) Funktionen.  
  
 Abfrage der XMLA-Eigenschaft MdpropMdxDrillFunctions können Sie den Grad der Unterstützung, die der Server die drillingfunktionen bereitgestellt; finden Sie unter [unterstützten XMLA-Eigenschaften &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) für Details.  
  
 Finden Sie unter [Datenbankjournal: Festlegen der MDX-Funktionen: The ToggleDrillState() Funktion](http://go.microsoft.com/fwlink/?LinkId=517759) Szenarien und Beispiele, die mit dieser Funktion.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein Drilldown für das Australia-Element der ersten Menge und ein Drillup für das United States-Element der ersten Menge ausgeführt.  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

