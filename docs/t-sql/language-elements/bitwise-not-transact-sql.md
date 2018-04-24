---
title: ~ (Bitwise NOT) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ~_TSQL
- bitwise
- NOT
- "~"
- Bitwise NOT
dev_langs:
- TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ac213793f2b54625b2955caffbf2790ca1886755
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="-bitwise-not-transact-sql"></a>~ (Bitweises NOT) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Führt eine bitweise logische NOT-Operation für einen ganzzahligen Wert durch.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
~ expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) (expression) eines beliebigen Datentyps der ganzzahligen Datentypkategorie oder des Datentyps **bit**, **binary** oder **varbinary**. *expression* wird in der bitweisen Operation als binäre Zahl behandelt.  
  
> [!NOTE]  
>  Nur eines der *expression*-Argumente kann in einer bitweisen Operation vom Datentyp **binary** oder **varbinary** sein.  
  
## <a name="result-types"></a>Ergebnistypen  
 **int**, wenn die Eingabewerte vom Typ **int** sind.  
  
 **smallint**, wenn die Eingabewerte vom Typ **smallint** sind  
  
 **tinyint**, wenn die Eingabewerte vom Typ **tinyint** sind  
  
 **bit**, wenn die Eingabewerte vom Typ **bit** sind  
  
## <a name="remarks"></a>Remarks  
 Mit dem bitweisen **~**-Operator wird ein bitweises logisches NOT für *expression* durchgeführt, indem jedes Bit abgearbeitet wird. Wenn *expression* den Wert 0 (null) besitzt, wird für die Bits im Resultset 1 festgelegt. Andernfalls wird das Bit im Ergebnis gelöscht auf 0 (null) festgelegt. Mit anderen Worten, Einsen werden zu Nullen und Nullen werden zu Einsen geändert.  
  
> [!IMPORTANT]  
>  Beim Durchführen aller bitweisen Operationen ist es wichtig, auf die Speicherlänge des Ausdrucks zu achten, der bei der bitweisen Operation verwendet wird. Beim Speichern von Werten wird empfohlen, dieselbe Anzahl von Bytes zu verwenden. Beispielsweise wird beim Speichern des dezimalen Werts 5 als **tinyint**, **smallint** oder **int** dieser Wert mit unterschiedlicher Byteanzahl abgespeichert: Bei **tinyint** wird 1 Byte verwendet, bei **smallint** 2 Bytes, und bei **int** werden 4 Bytes belegt. Daher kann eine bitweise Operation mit einem dezimalen **int**-Wert andere Ergebnisse erzeugen als eine direkte binäre oder hexadezimale Umwandlung, besonders bei Verwendung des **~**-Operators (bitweises NOT). Eine bitweise NOT-Operation kann auf eine Variable kürzerer Länge angewendet werden. In diesem Fall kann es vorkommen, dass bei der Konvertierung in einen längeren Datentyp die höherwertigen acht Bits nicht auf den erwarteten Wert festgelegt werden. Es wird empfohlen, die Variable mit dem kleineren Datentyp in den größeren Datentyp zu konvertieren und anschließend die NOT-Operation mit dem Ergebnis durchzuführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Tabelle mithilfe des **int**-Datentyps erstellt, um die Werte zu speichern, und die beiden Werte in eine Zeile eingefügt.  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 Die folgende Abfrage führt das bitweise NOT für die Spalten `a_int_value` und `b_int_value` durch.  
  
```  
SELECT ~ a_int_value, ~ b_int_value  
FROM bitwise;  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
--- ---   
-171  -76   
  
(1 row(s) affected)  
```  
  
 Die binäre Darstellung von 170 (`a_int_value` oder `A`) ist `0000 0000 1010 1010`. Die Durchführung einer bitweisen NOT-Operation mit diesem Wert erzeugt das binäre Ergebnis `1111 1111 0101 0101`, was dem dezimalen Wert -171 entspricht. Die binäre Darstellung von 75 ist `0000 0000 0100 1011`. Die Durchführung der bitweisen NOT-Operation ergibt `1111 1111 1011 0100`, was dem dezimalen Wert -76 entspricht.  
  
```  
 (~A)     
         0000 0000 1010 1010  
         -------------------  
         1111 1111 0101 0101  
(~B)     
         0000 0000 0100 1011  
         -------------------  
         1111 1111 1011 0100  
```  
  
 
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Bitweise Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  


