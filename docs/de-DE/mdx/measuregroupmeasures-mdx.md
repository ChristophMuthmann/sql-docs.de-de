---
title: MeasureGroupMeasures (MDX) | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- MeasureGroupMeasures function
ms.assetid: 69d9b205-1ca7-4741-9ca9-c7926bc87ead
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: e1b30c09b51e89a6e3951a03144353207e5dadd3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt eine Menge der Measures zurück, die zur angegebenen Measuregruppe gehören.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>Argumente  
 *MeasureGroupName*  
 Ein gültiger Zeichenfolgenausdruck, der den Namen der Measuregruppe enthält, aus der die Menge der Measures abgerufen werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Die angegebene Zeichenfolge muss genau mit dem Namen der Measuregruppe übereinstimmen. Die Verwendung von eckigen Klammern für Measuregruppennamen, die Leerzeichen enthalten, ist nicht erforderlich.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden alle Measures in der Internet Sales-Measuregruppe im Adventure Works-Cube zurückgegeben.  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
