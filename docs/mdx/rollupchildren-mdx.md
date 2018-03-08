---
title: RollupChildren (MDX) | Microsoft Docs
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
f1_keywords: ROLLUPCHILDREN
dev_langs: kbMDX
helpviewer_keywords: RollupChildren function
ms.assetid: 6f092540-067d-443f-b631-8523836a0d86
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e3553458eecb094ec76ecb6bf7f65691aaa1c4bd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="rollupchildren-mdx"></a>RollupChildren (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt einen Wert zurück, der durch einen Rollup der Werte der untergeordneten Elemente eines angegebenen Elements mithilfe des angegebenen unären Operators generiert wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Unary_Operator*  
 Ein gültiger Zeichenfolgenausdruck, der einen unären Operator angibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **RollupChildren** Funktion führt ein Rollup der Werte der untergeordneten Elemente des angegebenen Elements mithilfe des angegebenen unären Operators.  
  
 Die folgende Tabelle beschreibt die gültigen unären Operatoren für diese Funktion.  
  
|Operator|Ergebnis|  
|--------------|------------|  
|**+**|Gesamt = Gesamt + aktuelles untergeordnetes Element|  
|**-**|Gesamt = Gesamt - aktuelles untergeordnetes Element|  
|**\***|Gesamt = Gesamt * aktuelles untergeordnetes Element|  
|**/**|Gesamt = Gesamt / aktuelles untergeordnetes Element|  
|**%**|Gesamt = (Gesamt / aktuelles untergeordnetes Element) * 100|  
|**~**|Das untergeordnete Element wird im Rollup nicht verwendet. Sein Wert wird ignoriert.|  
  
 Falls der Operator in der Elementeigenschaft nicht in der Liste aufgeführt ist, tritt ein Fehler auf. Die Reihenfolge der Auswertung wird durch die Reihenfolge der gleichgeordneten Elemente bestimmt, nicht durch die Rangfolge der Operatoren.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine Elementeigenschaft mit dem Namen "Alternate Rollup Operator" verwendet, die alternative Werte für den unären Operator zum Ausführen eines alternativen Rollups der untergeordneten Elemente der Net Profit-Hierarchie in der Account-Dimension enthält. Diese Elementeigenschaft ist im Adventure Works-Cube nicht vorhanden, kann aber erstellt werden. Diese Verwendung von der **RollupChildren** Funktion in einer budgetierungsanwendung zur was-wenn-Analyse verwendet werden konnte.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
