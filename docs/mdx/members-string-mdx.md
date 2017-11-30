---
title: Members (Zeichenfolge) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: Members
dev_langs: kbMDX
helpviewer_keywords: Members function
ms.assetid: 21fca354-448b-4b05-93f4-111bde1568f1
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bed8ef7372528320ff18be737c15218d80983690
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="members-string-mdx"></a>Members (Zeichenfolge) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt ein durch einen Zeichenfolgenausdruck angegebenes Element zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Members(Member_Name)   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Name*  
 Ein gültiger Zeichenfolgenausdruck, der einen Elementnamen angibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Members (Zeichenfolge)** Funktion gibt ein einzelnes Element mit dem angegebenen Namen zurück. Normalerweise verwenden Sie die **Members (Zeichenfolge)** -Funktion mit externen Funktionen verwendet, auf die **Members (Zeichenfolge)** -Funktion eine Zeichenfolge, die ein Element kennzeichnet und den **Members (Zeichenfolge)** Funktion gibt den Wert für dieses Element angegeben.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die **Members (Zeichenfolge)** Funktion, um die angegebene Zeichenfolge in ein gültiges Element zu konvertieren, und klicken Sie dann das Standardmeasure für das in der Zeichenfolge angegebene Element zurückgegeben. Die angegebene Zeichenfolge ist in einfache Anführungszeichen eingeschlossen. Das Standardmeasure entspricht dem Reseller Sales Amount-Measure.  
  
```  
SELECT Members ('[Geography].[Geography].[Country].&[United States] ') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
