---
title: "Schließen (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE_TSQL
- CLOSE
dev_langs:
- TSQL
helpviewer_keywords:
- closing cursors
- cursors [SQL Server], closing
- CLOSE statement
ms.assetid: 21546874-97e3-4b93-970f-87c27f6b78c7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7315b45fa3b13b96fa01c7833ed1370f72e4bab8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="close-transact-sql"></a>CLOSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Schließt einen geöffneten Cursor, indem die Zuordnung des aktuellen Resultsets zum Cursor aufgehoben wird und alle Cursorsperren für die Zeilen, auf die der Cursor positioniert ist, freigegeben werden. CLOSE sorgt dafür, dass die Daten für ein erneutes Öffnen verfügbar sind, jedoch sind das Abrufen und positionierte Aktualisieren von Daten erst dann zulässig, wenn der Cursor erneut geöffnet wird. CLOSE muss bei einem geöffneten Cursor ausgeführt werden. Wurde ein Cursor lediglich deklariert oder bereits geschlossen, darf CLOSE nicht angewendet werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CLOSE { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>Argumente  
 GLOBAL  
 Gibt an, dass *Cursor_name* auf einen globalen Cursor verweist.  
  
 *Cursorname*  
 Der Name eines geöffneten Cursors. Wenn sowohl ein globaler als auch ein lokaler Cursor mit vorhanden *Cursor_name* als Buchstabenfolge, *Cursor_name* bezieht sich auf den globalen Cursor, wenn GLOBAL angegeben, andernfalls ist *Cursor_name* bezieht sich auf den lokalen Cursor.  
  
 *cursor_variable_name*  
 Der Name einer Cursorvariablen, die mit einem geöffneten Cursor verknüpft ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die richtige Platzierung der `CLOSE`-Anweisung in einem cursorbasierten Prozess gezeigt.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Cursor](../../relational-databases/cursors.md)   
 [Cursors &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [Aufheben der ZUORDNUNG &#40; Transact-SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [Abrufen von Daten &#40; Transact-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40; Transact-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  

