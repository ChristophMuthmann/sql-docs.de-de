---
title: RAND (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RAND
- RAND_TSQL
dev_langs: TSQL
helpviewer_keywords:
- RAND function
- values [SQL Server], random float
- random float value
ms.assetid: 363c84d6-b9fa-49ba-9a75-e44f27535ff6
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 665367907867911d9097fa17d3d05e356a35a014
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="rand-transact-sql"></a>RAND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Gibt einen pseudozufälligen Schlüsselbytes **"float"** Wert von 0 bis 1, exklusiv.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RAND ( [ seed ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Startwert*  
 Eine ganze Zahl [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) (**"tinyint"**, **"smallint"**, oder **Int**), die den Ausgangswert zurückgibt. Wenn *Ausgangswert* nicht angegeben wird, die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ein Ausgangswerts nach dem Zufallsprinzip zugewiesen. Für einen bestimmten Ausgangswert ist das zurückgegebene Ergebnis immer gleich.  
  
## <a name="return-types"></a>Rückgabetypen  
 **float**  
  
## <a name="remarks"></a>Hinweise  
 Bei wiederholten Aufrufen von RAND() mit demselben Ausgangswert werden dieselben Ergebnisse zurückgegeben.  
  
 Wenn für eine bestimmte Verbindung RAND() mit einem angegebenen Ausgangswert aufgerufen wird, führen alle nachfolgenden Aufrufe von RAND() zu Ergebnissen, die auf dem RAND()-Ausgangsaufruf basieren. Durch die folgende Abfrage wird z. B. immer dieselbe Nummernreihenfolge zurückgegeben.  
  
```  
SELECT RAND(100), RAND(), RAND()   
```  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel führt zu vier Zufallszahlen, die von der RAND-Funktion generiert werden.  
  
```  
DECLARE @counter smallint;  
SET @counter = 1;  
WHILE @counter < 5  
   BEGIN  
      SELECT RAND() Random_Number  
      SET @counter = @counter + 1  
   END;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Mathematische Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  
