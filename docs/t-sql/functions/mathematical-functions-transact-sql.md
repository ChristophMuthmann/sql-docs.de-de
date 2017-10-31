---
title: Mathematische Funktionen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec4a6767acab606d6459b439683a88a0cae1caf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mathematical-functions-transact-sql"></a>Mathematische Funktionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Die folgenden Skalarfunktionen führen Berechnungen aus, die in der Regel auf als Argumente angegebenen Eingabewerten basieren, und geben einen numerischen Wert zurück.  
  
||||  
|-|-|-|  
|[ABS](../../t-sql/functions/abs-transact-sql.md)|[GRAD](../../t-sql/functions/degrees-transact-sql.md)|[RAND](../../t-sql/functions/rand-transact-sql.md)|  
|[ACOS](../../t-sql/functions/acos-transact-sql.md)|[EXP](../../t-sql/functions/exp-transact-sql.md)|[RUNDEN](../../t-sql/functions/round-transact-sql.md)|  
|[ASIN](../../t-sql/functions/asin-transact-sql.md)|[FLOOR](../../t-sql/functions/floor-transact-sql.md)|[ANMELDEN](../../t-sql/functions/sign-transact-sql.md)|  
|[ATAN](../../t-sql/functions/atan-transact-sql.md)|[PROTOKOLL](../../t-sql/functions/log-transact-sql.md)|[SIN](../../t-sql/functions/sin-transact-sql.md)|  
|[ATN2](../../t-sql/functions/atn2-transact-sql.md)|[LOG10](../../t-sql/functions/log10-transact-sql.md)|[SQRT](../../t-sql/functions/sqrt-transact-sql.md)|  
|[HÖCHSTWERT](../../t-sql/functions/ceiling-transact-sql.md)|[PI](../../t-sql/functions/pi-transact-sql.md)|[QUADRAT](../../t-sql/functions/square-transact-sql.md)|  
|[COS](../../t-sql/functions/cos-transact-sql.md)|[STROMVERSORGUNG](../../t-sql/functions/power-transact-sql.md)|[TAN](../../t-sql/functions/tan-transact-sql.md)|  
|[COT](../../t-sql/functions/cot-transact-sql.md)|[BOGENMASS (RADIANT)](../../t-sql/functions/radians-transact-sql.md)||  
  
> [!NOTE]  
>  Arithmetische Funktionen, wie ABS, CEILING, DEGREES, FLOOR, POWER, RADIANS und SIGN, geben Werte des gleichen Datentyps wie der Eingabewert zurück. Trigonometrische und andere Funktionen, einschließlich EXP, LOG, LOG10, SQUARE und SQRT, umgewandelt Eingabewertes in **"float"** und Zurückgeben einer **"float"** Wert.  
  
 Alle mathematischen Funktionen, ausgenommen RAND, sind deterministisch. Sie geben somit bei jedem Aufrufen mit bestimmten Eingabewerten immer die gleichen Ergebnisse zurück. RAND ist nur deterministisch, wenn ein Startwert (seed) angegeben wird. Weitere Informationen zum Funktionsdeterminismus finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="see-also"></a>Siehe auch  
  [Arithmetische Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)  
  [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  

