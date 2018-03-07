---
title: = (Subtraktionszuweisung) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
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
- assignment operators, -=
- augmented operators, -=
- -= (subtract equals)
- -= (subtraction assignment)
ms.assetid: 2a2056b5-1dfa-4ea8-8cfc-6331a2f94da9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e42283367d3035ce4d7fcaecb4f7c96bcb7fed68
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="--subtraction-assignment-transact-sql"></a>= (Subtraktionszuweisung) (Transact-SQL)
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
 Weitere Informationen finden Sie unter [-&#40; Subtraktion &#41; &#40; Transact-SQL &#41; ](../../t-sql/language-elements/subtract-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
