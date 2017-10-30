---
title: CREATE MEASURE-Anweisung (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: f264ba96-cbbe-488b-8ac9-b3056a6e997b
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 97edb823814647bc87b155250cad88dfeb5cf5f5
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---create-measure"></a>MDX-Datendefinition - MEASURE erstellen
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Erstellt ein Measure in einem tabellarischen Modell.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE MEASURE Table_Name[Measure_Name] = DAX_Expression  
[; CREATE MEASURE ...n]  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Tabellenname*  
 Ein gültiges Zeichenfolgenliteral, das den Namen der Tabelle bereitstellt, in dem das Measure erstellt wird.  
  
 *Measure_Name*  
 Ein gültiges Zeichenfolgenliteral, das einen Measurenamen bereitstellt.  
  
 *DAX_Expression*  
 Ein gültiger DAX-Ausdruck, der einen einzelnen skalaren Wert zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die *Measure_Name* muss in eckige Klammern eingeschlossen werden.  
  
 Die CREATE MEASURE-Anweisung kann nur innerhalb einer MDX-Skriptdefinition verwendet werden; finden Sie unter [MdxScript-Element &#40; ASSL &#41; ](../analysis-services/scripting/objects/mdxscript-element-assl.md).  
  
 Sie können auch ein berechnetes Element definieren, das in einer einzelnen Abfrage verwendet wird. Wenn Sie ein berechnetes Element definieren möchten, das auf eine einzelne Abfrage beschränkt ist, verwenden Sie die WITH-Klausel in der SELECT-Anweisung. Weitere Informationen finden Sie unter [Erstellen von Measures in MDX](../analysis-services/multidimensional-models/mdx/mdx-building-measures.md).  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Datendefinitionsanweisungen &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

