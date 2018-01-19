---
title: "Öffnen (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPEN_TSQL
- OPEN
dev_langs: TSQL
helpviewer_keywords:
- opening cursors
- cursors [SQL Server], opening
- populating cursors [SQL Server]
- OPEN statement
- Transact-SQL cursors, opening
ms.assetid: fd1c5e3b-6045-4a42-b646-3fca76e874c1
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 92ba2ddafe591c570300918bfb968ae44debea62
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="open-transact-sql"></a>OPEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Öffnet eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Servercursor und füllt den Cursor durch Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)] angegebene auf der DECLARE CURSOR oder SET-Anweisung *Cursor_variable* Anweisung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OPEN { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>Argumente  
 GLOBAL  
 Gibt an, dass *Cursor_name* auf einen globalen Cursor verweist.  
  
 *cursor_name*  
 Der Name eines deklarierten Cursors. Wenn sowohl ein globaler als auch ein lokaler Cursor mit vorhanden *Cursor_name* als Buchstabenfolge, *Cursor_name* bezieht sich auf den globalen Cursor, wenn GLOBAL angegeben, andernfalls ist *Cursor_name* bezieht sich auf den lokalen Cursor.  
  
 *cursor_variable_name*  
 Der Name einer Cursorvariablen, die auf einen Cursor verweist.  
  
## <a name="remarks"></a>Hinweise  
 Falls der Cursor mit der Option INSENSITIVE oder STATIC deklariert wird, erstellt OPEN eine temporäre Tabelle für das Resultset. OPEN schlägt fehl, wenn die Größe einer Zeile im Resultset die Maximalgröße für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabellen überschreitet. Falls der Cursor mit der Option KEYSET deklariert wird, erstellt OPEN eine temporäre Tabelle für das Keyset. Die temporären Tabellen werden in tempdb gespeichert.  
  
 Nachdem ein Cursor geöffnet wurde, verwenden Sie den @@CURSOR_ROWS Funktion, um die Anzahl von qualifizierenden Zeilen im letzten geöffneten Cursor.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt das asynchrone Generieren von keysetgesteuerten oder statischen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Cursorn nicht. [!INCLUDE[tsql](../../includes/tsql-md.md)] -Cursorvorgänge, z. B. OPEN oder FETCH, sind in Batches enthalten. Daher ist das asynchrone Generieren von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Cursorn nicht erforderlich. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt weiterhin asynchrone keysetgesteuerte oder statische AP -Servercursor (Application Programming Interface), wobei Cursoroperationen des Typs „Open“ mit niedriger Latenz ein Problem darstellen. Dies ist auf Clientroundtrips zurückzuführen, die für jeden Cursorvorgang ausgeführt werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Cursor geöffnet, und es werden alle Zeilen abgerufen.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN Employee_Cursor;  
  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM Employee_Cursor  
END;  
  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
