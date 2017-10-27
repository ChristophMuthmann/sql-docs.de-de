---
title: MSSQLSERVER_137 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5b7b73da0a46159521addd7ebc76b32d00881318
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver137"></a>MSSQLSERVER_137
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|137|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|P_SCALAR_VAR_NOTFOUND|  
|Meldungstext|Die "%.*ls"-Skalarvariable muss deklariert werden.|  
  
## <a name="explanation"></a>Erklärung  
Dieser Fehler tritt auf, wenn in einem SQL-Skript eine Variable verwendet wird, ohne dass die Variable zuerst deklariert wurde. Im folgenden Beispiel wird beispielsweise Fehler 137 für die SET- und die SELECT-Anweisung zurückgegeben, weil **@mycol** nicht deklariert wurde.  
  
SET @mycol = 'ContactName';  
  
SELECT @mycol;  
  
Eine der etwas komplizierteren Ursachen für diesen Fehler ist u. a. die Verwendung einer Variablen, die außerhalb der EXECUTE-Anweisung deklariert wurde. Angenommen, die in der SELECT-Anweisung angegebene Variable **@mycol** ist für die SELECT-Anweisung lokal. Das bedeutet, dass sie sich außerhalb der EXECUTE-Anweisung befindet.  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20);  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>Benutzeraktion  
Überprüfen Sie, ob alle in einem SQL-Skript verwendeten Variablen deklariert wurden, bevor sie an anderer Stelle im Skript verwendet werden.  
  
Schreiben Sie das Skript um, sodass es nicht auf Variablen in der EXECUTE-Anweisung verweist, die außerhalb davon deklariert wurden. Beispiel:  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20) ;  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>Siehe auch  
[EXECUTE &#40;Transact-SQL&#41;](~/t-sql/language-elements/execute-transact-sql.md)  
[SET-Anweisungen &#40;Transact-SQL&#41;](~/t-sql/statements/set-statements-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](~/t-sql/language-elements/declare-local-variable-transact-sql.md)  
  

