---
title: '@@CURSOR_ROWS (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aa8103fee0cea19b626ef583c057c49ff053f2cc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40cursorrows-transact-sql"></a>&#x40;&#x40;CURSOR_ROWS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt die Anzahl der kennzeichnenden Zeilen zurück, die sich aktuell im letzten für die Verbindung geöffneten Cursor befinden. Zur Verbesserung der Leistung kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] große statische und keysetgesteuerte Cursor asynchron auffüllen. @@CURSOR_ROWS kann aufgerufen werden, um zu bestimmen, dass die Anzahl der einen Cursor kennzeichnenden Zeilen zum Zeitpunkt des Aufrufens von @@CURSOR_ROWS abgerufen wurde.
  
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
|-*m*|Der Cursor wird asynchron aufgefüllt. Der zurückgegebene Wert (-*m*) entspricht der aktuellen Anzahl der Zeilen im Keyset.|  
|-1|Der Cursor ist dynamisch. Da dynamische Cursor alle Änderungen widerspiegeln, ändert sich die Anzahl der Zeilen, die den Cursor kennzeichnen, ständig. Es kann nie definitiv mitgeteilt werden, dass alle gekennzeichneten Zeilen abgerufen wurden.|  
|0|Es wurden keine Cursor geöffnet, keine Zeilen kennzeichnen den zuletzt geöffneten Cursor, oder der zuletzt geöffnete Cursor wurde geschlossen oder seine Zuordnung aufgehoben.|  
|*n*|Der Cursor ist vollständig aufgefüllt. Der zurückgegebene Wert (*n*) entspricht der Gesamtanzahl der Zeilen im Cursor.|  
  
## <a name="remarks"></a>Remarks  
Die von @@CURSOR_ROWS zurückgegebene Zahl ist negativ, wenn der letzte Cursor asynchron geöffnet wurde. Keysetgesteuerte oder statische Cursor werden asynchron geöffnet, wenn der Wert für den Cursorschwellenwert sp_configure größer als 0 (null) ist und die Anzahl der Zeilen im Cursorresultset größer als der Cursorschwellenwert ist.
  
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
  
```
-----------
0  
```

```
LastName
---------------
Sanchez
```

```
-----------
-1
```  
  
## <a name="see-also"></a>Siehe auch
[Cursor Functions &#40;Transact-SQL&#41; (Cursorfunktionen (Transact-SQL))](../../t-sql/functions/cursor-functions-transact-sql.md)  
[OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  
