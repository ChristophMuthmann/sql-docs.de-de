---
title: Numerische Literale Syntax | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a371ac49fe29674a1e9c0d7bb0dd9639ba5aa48
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="numeric-literal-syntax"></a>Numerische Literale Syntax
Die folgende Syntax wird für numerische Literale in ODBC verwendet:  
  
 *numerische Literal* :: = *signiert-numerische-Literal &#124; unsigniert-numerische-Literal*  
  
 *signiert-numerische-Literal* :: = [*Anmeldung*] *unsigniert-numerische-Literal*  
  
 *nicht signierte-numerische-Literal* :: = *exakte numerische-Literal &#124; ungefähre numerische-Literal*  
  
 *exakte numerische-Literal* :: = *unsigned Integer* [*Zeitraum*[*unsigned Integer*]] *&#124; Period unsigniert-ganze Zahl*  
  
 *Anmeldung* :: = *Pluszeichen (+) &#124; Minuszeichen (-)*  
  
 *Ungefähre numerische-Literal* :: = *Mantisse E Exponent*  
  
 *Mantissen* :: = *exakte numerische-Literal*  
  
 *Exponenten* :: = *Ganzzahl mit Vorzeichen*  
  
 *Ganzzahl mit Vorzeichen* :: = [*Anmeldung*] *unsigned Integer*  
  
 *unsigned Integer* :: = *Ziffer...*  
  
 *Pluszeichen* :: =*+*  
  
 *Minuszeichen* :: = -  
  
 *Ziffer* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *Zeitraum* :: =.
