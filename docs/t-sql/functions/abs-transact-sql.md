---
title: ABS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ABS_TSQL
- ABS
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], positive
- values [SQL Server], absolute
- ABS function
- absolute positive value
ms.assetid: e2ea7a6d-3e2f-472c-afbc-437d3b835c03
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ab75a2147946366fba194f654a3710b32f68d626
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Eine mathematische Funktion, die den absoluten (positiven) Wert des angegebenen numerischen Ausdrucks zurückgibt. (`ABS` ändert negative Werte in positive Werte. `ABS` wirkt sich nicht auf Nullwerte oder positive Werte aus.)
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumente  
*numeric_expression*  
Ein Ausdruck der genauen numerischen oder ungefähren numerischen Datentypkategorie.
  
## <a name="return-types"></a>Rückgabetypen  
Gibt denselben Typ wie *Numerischer Ausdruck*zurück.
  
## <a name="examples"></a>Beispiele  
In diesem Beispiel werden die Ergebnisse dargestellt, die zurückgegeben werden, wenn die `ABS`-Funktion auf drei verschiedene Zahlen angewendet wird.
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
Die `ABS`-Funktion kann einen Überlauffehler zur Folge haben, wenn der absolute Wert einer Zahl größer ist als die größte Zahl, die von dem angegebenen Datentyp dargestellt werden kann. Beispielsweise hat der Datentyp `int` einen Wertebereich von `-2,147,483,648` bis `2,147,483,647`. Durch das Berechnen des absoluten Werts für die ganze Zahl mit Vorzeichen, `-2,147,483,648`, tritt ein Überlauffehler auf, da der absolute Wert größer ist als der positive Bereich für den `int`-Datentyp.
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
Gibt die folgende Fehlermeldung zurück:
  
"Meldung 8115, Ebene 16, Status 2, Zeile 3"
  
"Arithmetischer Überlauffehler beim Konvertieren des Ausdrucks in den Datentyp int."

  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Mathematische Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Integrierte Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

