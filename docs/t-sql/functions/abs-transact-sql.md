---
title: ABS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eed45893b664e79071d1b423f5d84977e11f5a24
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Eine mathematische Funktion, die den absoluten (positiven) Wert des angegebenen numerischen Ausdrucks zurückgibt. (`ABS` Änderungen negative Werte für positive Werte. `ABS`wirkt sich nicht auf NULL oder positive Werte zulässig sind.)
  
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
Im folgenden Beispiel werden die Ergebnisse dargestellt, die entstehen, wenn die `ABS`-Funktion auf drei verschiedene Zahlen angewendet wird.
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
Die `ABS`-Funktion kann einen Überlauffehler zur Folge haben, wenn der absolute Wert einer Zahl größer ist als die größte Zahl, die durch den angegebenen Datentyp dargestellt werden kann. Der `int`-Datentyp kann beispielsweise nur Werte zwischen `-2,147,483,648` und `2,147,483,647` aufnehmen. Durch das Berechnen des absoluten Wertes für die ganze Zahl mit Vorzeichen, `-2,147,483,648`, tritt ein Überlauffehler auf, da der absolute Wert größer ist als der positive Bereich für den `int`-Datentyp.
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
Im Folgenden wird die Fehlermeldung aufgeführt:
  
"Meldung 8115, Ebene 16, Status 2, Zeile 3"
  
"Arithmetischer Überlauffehler beim Konvertieren des Ausdrucks in den Datentyp int."

  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Integrierte Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  


