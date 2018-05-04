---
title: DROP MEMBER-Anweisung (MDX) | Microsoft Docs
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
- DROP
- Member
- DROP_MEMBER
- DROP MEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- deleting calculated members
- calculated members [MDX]
- DROP MEMBER statement
- dropping calculated members
- removing calculated members
ms.assetid: e9819976-a9ec-4c48-b0b5-3f6938e200f5
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a49ce890fb3a98e26f67f1b1e648decd4372c7ac
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-member"></a>MDX-Datendefinition - DROP-Element
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Entfernt ein berechnetes Element.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>Argumente  
 *Cube_Name*  
 Ein gültiger Zeichenfolgenausdruck, der einen Cubenamen bereitstellt.  
  
 *Member_Identifier*  
 Ein gültiger Zeichenfolgenausdruck, der einen Elementnamen oder Elementschlüssel bereitstellt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie MEMBER-Anweisung & #40; MDX & #41;](../mdx/mdx-data-definition-create-member.md)   
 [MDX-Datendefinitionsanweisungen &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
