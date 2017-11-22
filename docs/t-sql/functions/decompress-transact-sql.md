---
title: DEKOMPRIMIEREN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/30/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords: DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2988959b7ec3f9eccad74b752e7643f1e6675590
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="decompress-transact-sql"></a>DEKOMPRIMIEREN Sie (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Dekomprimieren Sie Eingabeausdruck GZIP-Algorithmus verwenden. Ergebnis der Komprimierung ist Bytearray (varbinary(max)-Typ).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist eine **Varbinary (***n***)**, **varbinary(max)**, oder **binäre (** *n***)**. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Datentyp der **varbinary(max)** Typ. Das Eingabeargument ist mit dem Algorithmus ZIP dekomprimiert. Der Benutzer sollte explizit Ergebnis für einen Zieltyp umgewandelt, bei Bedarf.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-decompress-data-at-query-time"></a>A. Dekomprimiert Daten zum Zeitpunkt der Abfrage  
 Das folgende Beispiel zeigt, wie das Komprimieren von Daten aus einer Tabelle angezeigt:  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. Anzeigen von komprimierten Daten, die mit der berechneten Spalte  
 Im folgende Beispiel wird gezeigt, wie eine Tabelle zum Speichern von dekomprimierten Daten erstellt wird:  
  
```  
CREATE TABLE (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40; Transact-SQL &#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
