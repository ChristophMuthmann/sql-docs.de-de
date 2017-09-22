---
title: '@@CURSOR_ROWS (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CURSOR_ROWS'
- '@@CURSOR_ROWS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CURSOR_ROWS function'
- cursors [SQL Server], last-opened
- last-opened cursor
- asynchronous cursors [SQL Server]
ms.assetid: 31bd7a97-7f28-42a8-ba24-24d16d22973d
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 10a3a6cabae8d25de670cbacb037a62f4c5a2d54
ms.contentlocale: de-de
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40cursorrows-transact-sql"></a>& #x 40; & #x 40; CURSOR_ROWS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die Anzahl der kennzeichnenden Zeilen zurück, die sich aktuell im letzten für die Verbindung geöffneten Cursor befinden. Zur Verbesserung der Leistung kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] große statische und keysetgesteuerte Cursor asynchron auffüllen. @@CURSOR_ROWS aufgerufen werden, um zu bestimmen, dass die Anzahl der Zeilen, die für einen Cursor qualifizieren, zu dem Zeitpunkt abgerufen werden @@CURSOR_ROWS aufgerufen wird.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```
@@CURSOR_ROWS  
```  
  
## <a name="return-types"></a>Rückgabetypen
**integer**
  
## <a name="return-value"></a>Rückgabewert  
  
|Rückgabewert|Description|  
|---|---|
|-*m*|Der Cursor wird asynchron aufgefüllt. Der zurückgegebene Wert (-*m*) ist die Anzahl der Zeilen, die derzeit im Keyset.|  
|-1|Der Cursor ist dynamisch. Da dynamische Cursor alle Änderungen widerspiegeln, ändert sich die Anzahl der Zeilen, die den Cursor kennzeichnen, ständig. Es kann nie definitiv mitgeteilt werden, dass alle gekennzeichneten Zeilen abgerufen wurden.|  
|0|Es wurden keine Cursor geöffnet, keine Zeilen kennzeichnen den zuletzt geöffneten Cursor, oder der zuletzt geöffnete Cursor wurde geschlossen oder seine Zuordnung aufgehoben.|  
|*n*|Der Cursor ist vollständig aufgefüllt. Der zurückgegebene Wert (*n*) ist die Gesamtzahl der Zeilen im Cursor.|  
  
## <a name="remarks"></a>Hinweise  
Die Anzahl von zurückgegebene@CURSOR_ROWS ist negativ, wenn der letzte Cursor asynchron geöffnet wurde. Keysetgesteuerte oder statische Cursor werden asynchron geöffnet, wenn der Wert für Sp_configure Cursor Threshold größer als 0 ist und die Anzahl der Zeilen im Cursorresultset größer als der cursorschwellenwert ist.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird ein Cursor deklariert und `SELECT` zur Anzeige des Werts von `@@CURSOR_ROWS` verwendet. Die Einstellung hat den Wert `0`, bevor der Cursor geöffnet wird, und den Wert `-1`, um anzugeben, dass das Keyset des Cursors asynchron aufgefüllt wird.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@CURSOR_ROWS;  
DECLARE Name_Cursor CURSOR FOR  
SELECT LastName ,@@CURSOR_ROWS FROM Person.Person;  
OPEN Name_Cursor;  
FETCH NEXT FROM Name_Cursor;  
SELECT @@CURSOR_ROWS;  
CLOSE Name_Cursor;  
DEALLOCATE Name_Cursor;  
GO             
```  
  
Im Folgenden werden die Resultsets aufgeführt.
  
`-----------`
  
 `0`  
  
`LastName`
  
`---------------`
  
`Sanchez`
  
`-----------`
  
 `-1`  
  
## <a name="see-also"></a>Siehe auch
[Cursorfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[OPEN &#40; Transact-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  

