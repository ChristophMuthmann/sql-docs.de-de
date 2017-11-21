---
title: SET NOCOUNT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NOCOUNT
- SET_NOCOUNT_TSQL
- NOCOUNT_TSQL
- SET NOCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- NOCOUNT option
- number of rows affected by statement
- row affected by statements [SQL Server]
- counting rows
- SET NOCOUNT statement
ms.assetid: eb3e6727-cb26-4bc2-84c7-171cbac02029
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5e8224b906de8f8678a33360be6222aa2120a5b8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-nocount-transact-sql"></a>SET NOCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Beendet die Meldung bezüglich der Anzahl der von betroffenen Zeilen eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung oder gespeicherte Prozedur, die als Teil des Resultsets zurückgegeben wird, festgelegt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET NOCOUNT { ON | OFF }   
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn SET NOCOUNT auf ON festgelegt ist, wird die Anzahl nicht zurückgegeben. Wenn SET NOCOUNT auf OFF festgelegt ist, wird die Anzahl zurückgegeben.  
  
 Der @@ROWCOUNT -Funktion wird aktualisiert, auch wenn SET NOCOUNT auf ON festgelegt ist.  
  
 SET NOCOUNT ON verhindert das Senden der DONE_IN_PROC-Meldungen an den Client, die sonst für jede Anweisung in einer gespeicherten Prozedur gesendet werden. Für gespeicherte Prozeduren, die mehrere-Anweisungen enthalten, die wenige tatsächlichen Daten zurückgeben, oder für Prozeduren, die enthalten [!INCLUDE[tsql](../../includes/tsql-md.md)] Schleifen, Festlegen von SET NOCOUNT auf ON eine erhebliche Leistungssteigerung bewirken, da der Netzwerkverkehr stark reduziert wird bereitstellen kann.  
  
 Die mit SET NOCOUNT angegebene Einstellung ist zur Ausführungszeit und nicht zur Analysezeit wirksam.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @NOCOUNT VARCHAR(3) = 'OFF';  
IF ( (512 & @@OPTIONS) = 512 ) SET @NOCOUNT = 'ON';  
SELECT @NOCOUNT AS NOCOUNT;  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird verhindert, dass die Meldung zur Anzahl der betroffenen Zeilen angezeigt wird.  
  
```  
USE AdventureWorks2012;  
GO  
SET NOCOUNT OFF;  
GO  
-- Display the count message.  
SELECT TOP(5)LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- SET NOCOUNT to ON to no longer display the count message.  
SET NOCOUNT ON;  
GO  
SELECT TOP(5) LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- Reset SET NOCOUNT to OFF  
SET NOCOUNT OFF;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

