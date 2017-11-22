---
title: ~ (Bitweises NOT) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ~_TSQL
- bitwise
- NOT
- ~
- Bitwise NOT
dev_langs: TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
caps.latest.revision: "42"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6525306bfae5112e1d49a191c52cc0125dfe2e96
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
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
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von einem der Datentypen der Datentypkategorie ' Integer ' die **Bit**, oder die **binäre** oder **Varbinary** Daten Typen. *Ausdruck* wird als eine Binärzahl für die bitweise Operation behandelt.  
  
> [!NOTE]  
>  Nur ein *Ausdruck* sein **binäre** oder **Varbinary** -Datentyp in einer bitweisen Operation.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Int** , wenn die Eingabewerte sind **Int**.  
  
 **"smallint"** , wenn die Eingabewerte sind **"smallint"**.  
  
 **"tinyint"** , wenn die Eingabewerte sind **"tinyint"**.  
  
 **Bit** , wenn die Eingabewerte sind **Bit**.  
  
## <a name="remarks"></a>Hinweise  
 Die  **~**  bitweiser Operator führt eine bitweise logische NOT für die *Ausdruck*, jedes bit abgearbeitet wiederum. Wenn *Ausdruck* hat den Wert 0, werden die Bits im Resultset auf 1 festgelegt ist, andernfalls das entsprechende Bit im Ergebnis auf den Wert 0 deaktiviert ist. Mit anderen Worten, Einsen werden zu Nullen und Nullen werden zu Einsen geändert.  
  
> [!IMPORTANT]  
>  Beim Durchführen aller bitweisen Operationen ist es wichtig, auf die Speicherlänge des Ausdrucks zu achten, der bei der bitweisen Operation verwendet wird. Beim Speichern von Werten wird empfohlen, dieselbe Anzahl von Bytes zu verwenden. Z. B. Speichern des dezimalen Werts 5 als eine **"tinyint"**, **"smallint"**, oder **Int** erzeugt einen Wert mit einer anderen Anzahl von Bytes gespeichert: **"tinyint"** speichert Daten mithilfe von 1 Byte verwendet, **"smallint"** speichert Daten mit 2 Bytes und **Int** speichert Daten mit 4 Bytes. Deshalb Ausführen eines bitweisen Vorgangs auf ein **Int** Dezimalwert kann erzeugen verschiedene Ergebnisse von den über eine direkte binäre oder hexadezimale Umwandlung, besonders, wenn die  **~**  ( Bitweises NOT) Operator wird verwendet. Eine bitweise NOT-Operation kann auf eine Variable kürzerer Länge angewendet werden. In diesem Fall kann es vorkommen, dass bei der Konvertierung in einen längeren Datentyp die höherwertigen acht Bits nicht auf den erwarteten Wert festgelegt werden. Es wird empfohlen, die Variable mit dem kleineren Datentyp in den größeren Datentyp zu konvertieren und anschließend die NOT-Operation mit dem Ergebnis durchzuführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel wird eine Tabelle mit den **Int** Daten geben, um die Werte zu speichern und die beiden Werte in eine Zeile eingefügt.  
  
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
  
 
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Bitweise Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  


