---
title: '@@FETCH_STATUS (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 09/18/2017
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
- '@@FETCH_STATUS'
- '@@FETCH_STATUS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- status information [SQL Server], FETCH
- '@@FETCH_STATUS function'
ms.assetid: 93659193-e4ff-4dfb-9043-0c4114921b91
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c377058e568aef6162ecadb46bee2c2b289a6f4b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40fetchstatus-transact-sql"></a>&#x40;&#x40;FETCH_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den Status der letzten Cursor-FETCH-Anweisung zurück, die für einen beliebigen der aktuell von der Verbindung geöffneten Cursor ausgegeben wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **integer**  
  
## <a name="return-value"></a>Rückgabewert  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|0|Die FETCH-Anweisung war erfolgreich.|  
|-1|Die FETCH-Anweisung ist fehlgeschlagen, oder die Zeile war außerhalb des Resultsets.|  
|-2|Die abgerufene Zeile fehlt.|
|–9|Der Cursor führt keinen Abrufvorgang aus.|  
  
## <a name="remarks"></a>Remarks  
 Da @@FETCH_STATUS global für alle Cursor auf einer Verbindung gilt, verwenden Sie @@FETCH_STATUS mit Bedacht. Nachdem eine FETCH-Anweisung ausgeführt wurde, muss der Test von @@FETCH_STATUS durchgeführt werden, bevor eine weitere FETCH-Anweisung für einen anderen Cursor ausgeführt wird. Der Wert von @@FETCH_STATUS wird erst definiert, wenn ein Abrufvorgang auf der Verbindung ausgeführt wurde.  
  
 Ein Benutzer führt z. B. eine FETCH-Anweisung von einem Cursor aus durch und ruft dann eine gespeicherte Prozedur auf, die die Ergebnisse von einem anderen Cursor aus öffnet und verarbeitet. Wenn die Steuerung von der aufgerufenen gespeicherten Prozedur zurückgegeben wird, spiegelt @@FETCH_STATUS die letzte in der Prozedur ausgeführte FETCH-Anweisung wider und nicht die FETCH-Anweisung, die vor dem Aufruf der gespeicherten Prozedur ausgeführt wurde.  
  
 Um den letzten FETCH-Status eines bestimmten Cursors abzurufen, führen Sie eine Abfrage der **fetch_status**-Spalte in der dynamischen Verwaltungsfunktion **sys.dm_exec_cursors** durch.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `@@FETCH_STATUS` zur Steuerung der Cursoraktivitäten in einer `WHILE`-Schleife verwendet.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT BusinessEntityID, JobTitle  
FROM AdventureWorks2012.HumanResources.Employee;  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Cursorfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
