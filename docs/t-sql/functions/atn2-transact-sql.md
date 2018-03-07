---
title: ATN2 (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ATN2
- ATN2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- arctangent
- tangent
- ATN2 function
ms.assetid: 014b291e-7cd7-4c39-b20d-5db3a9f0505d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 022c5cd7655debb529ec00789f075d95278073f6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="atn2-transact-sql"></a>ATN2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt den Winkel im Bogenmaß (Radiant) zwischen der positiven X-Achse und dem Strahl vom Ursprung zum Punkt (x, y) zurück, wobei "x" und "y" die Werte der beiden angegebenen float-Ausdrücke sind.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
ATN2 ( float_expression , float_expression )  
```  
  
## <a name="arguments"></a>Argumente  
*Float_expression* ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von der **"float"** -Datentyp.
  
## <a name="return-types"></a>Rückgabetypen
**float**
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird `ATN2` für die angegebenen Komponenten `x` und `y` berechnet.
  
```sql
DECLARE @x float = 35.175643, @y float = 129.44;  
SELECT 'The ATN2 of the angle is: ' + CONVERT(varchar,ATN2(@x,@y ));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The ATN2 of the angle is: 0.265345                         
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Float und Real &#40; Transact-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
[Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  

