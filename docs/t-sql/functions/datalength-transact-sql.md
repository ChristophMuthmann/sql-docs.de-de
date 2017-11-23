---
title: DATALENGTH (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs: TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9d9b60d82ad4a711ed7cf67a015491b6ebafa264
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die Anzahl von Bytes zurück, die zum Darstellen eines Ausdrucks verwendet werden.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>Argumente  
*expression*  
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Datentyps.
  
## <a name="return-types"></a>Rückgabetypen
**"bigint"** Wenn *Ausdruck* wird von der **varchar(max)**, **nvarchar(max)** oder **varbinary(max)** -Datentypen; andernfalls **Int**.
  
## <a name="remarks"></a>Hinweise  
DATALENGTH ist besonders hilfreich bei **Varchar**, **Varbinary**, **Text**, **Image**, **Nvarchar**, und **Ntext** Datentypen, da diese Datentypen Daten variabler Länge speichern können.
  
DATALENGTH von NULL ist NULL.
  
> [!NOTE]  
>  Kompatibilitätsgrade können sich auf Rückgabewerte auswirken. Weitere Informationen zu den Kompatibilitätsgraden finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird nach der Länge der `Name`-Spalte in der `Product`-Tabelle gesucht.
  
```sql
-- Uses AdventureWorks  
  
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch
[LEN &#40; Transact-SQL &#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Systemfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  

