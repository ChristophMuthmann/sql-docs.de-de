---
title: COMPRESS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 01500cd6560fd60dda2cb9060c2968d7c010d8e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="compress-transact-sql"></a>COMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Komprimiert den Eingabeausdruck mit dem GZIP-Algorithmus. Durch die Komprimierung wird ein Bytearray des Typs **varbinary(max)** zurückgegeben.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumente  
*expression*  
Die Ausdrücke **nvarchar(***n***)**, **nvarchar(max)**, **varchar(***n***)**, **varchar(max)**, **varbinary(***n***)**, **varbinary(max)**, **char(***n***)**, **nchar(***n***)** oder **binary(***n***)**. Weitere Informationen finden Sie unter [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="return-types"></a>Rückgabetypen
Gibt den Datentyp von **varbinary(max)** zurück, der den komprimierten Inhalt der Eingabe darstellt.
  
## <a name="remarks"></a>Remarks  
Komprimierte Daten können nicht indiziert werden.
  
Über die COMPRESS-Funktion werden die Daten komprimiert, die als Eingabeausdrücke bereitgestellt und für jeden Datenabschnitt ausgelöst werden, der komprimiert werden soll. Informationen zur automatischen Komprimierung beim Speichern auf der Zeilen- oder Seitenebene finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. Komprimieren von Daten beim Einfügen einer Tabelle  
Das folgende Beispiel zeigt, wie Daten aus einer Tabelle komprimiert werden können, die in einer Tabelle enthalten sind:
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. Archivieren einer komprimierten Version von gelöschten Zeilen  
Die folgende Anweisung löscht alte Playerzeilen aus der `player`-Tabelle und speichert diese in einem komprimierten Format in der `inactivePlayer`-Tabelle, um so Speicherplatz einzusparen.
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>Siehe auch
[String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  
