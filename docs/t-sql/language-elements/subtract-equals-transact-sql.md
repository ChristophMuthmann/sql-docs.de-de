---
title: = (EQUALS subtrahieren) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- -=
- -=_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, -=
- -= (subtract equals)
ms.assetid: 2a2056b5-1dfa-4ea8-8cfc-6331a2f94da9
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d90b7030c76bae406ec2d764bf19c96202be9d86
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="--subtract-equals-transact-sql"></a>-= (Subtract EQUALS) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Subtrahiert zwei Zahlen und legt einen Wert auf das Ergebnis des Vorgangs fest. Angenommen, eine Variable @x gleich 35 ist, klicken Sie dann @x = 2 nimmt den ursprünglichen Wert des @x, subtrahiert 2 und legt @x auf diesen neuen Wert (33).  
  
## <a name="syntax"></a>Syntax  
  
```  
expression -= expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Datentyps der Kategorie "numeric" mit Ausnahme von Typen der **Bit** -Datentyp.  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt einen Wert vom Datentyp des Arguments zurück, das in der Rangfolge höher steht. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen finden Sie unter [-&#40; Subtrahieren &#41; &#40; Transact-SQL &#41; ](../../t-sql/language-elements/subtract-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
