---
title: SET STATISTICS TIME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_TIME_TSQL
- SET STATISTICS TIME
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- time [SQL Server], statement processing statistics
- SET STATISTICS TIME statement
- STATISTICS TIME option
- statements [SQL Server], statistical information
- parsing [SQL Server], SET STATISTICS TIME statement
- compile times [SQL Server]
- execution processing time [SQL Server]
ms.assetid: eec2e1cd-a29d-4cf3-a271-be9d61506f15
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: acd4684ea6b44f3a7371424eb6c90305e78841fc
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-statistics-time-transact-sql"></a>SET STATISTICS TIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Zeigt an, wie viele Millisekunden zum Analysieren, Kompilieren und Ausführen jeder Anweisung benötigt wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET STATISTICS TIME { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn SET STATISTICS TIME auf ON festgelegt ist, wird die Zeitstatistik für eine Anweisung angezeigt. Bei OFF wird die Zeitstatistik nicht angezeigt.  
  
 Die Einstellung von SET STATISTICS TIME wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist nicht möglich, im Fibermodus exakte Statistiken bereitgestellt, die aktiviert wird, wenn Sie aktivieren die **Lightweightpooling** Konfigurationsoption.  
  
 Die **cpu** Spalte in der **Sysprocesses** Tabelle wird nur aktualisiert, wenn eine Abfrage mit SET STATISTICS TIME ON ausgeführt wird. Wenn SET STATISTICS TIME auf OFF festgelegt ist **0** wird zurückgegeben.  
  
 Die Einstellungen ON und OFF wirken sich auch auf die CPU-Spalte in der Prozessinfo-Sicht für den Verwaltungsordner Aktuelle Aktivität in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] aus.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Verwenden von SET STATISTICS TIME müssen Benutzer über entsprechende Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung verfügen. Die SHOWPLAN-Berechtigung ist nicht erforderlich.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel werden die Serverausführungs-, Analyse- und Kompilierzeit gezeigt.  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS TIME ON;  
GO  
SELECT ProductID, StartDate, EndDate, StandardCost   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS TIME OFF;  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
(269 row(s) affected)  
  
SQL Server Execution Times:  
   CPU time = 0 ms,  elapsed time = 2 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET STATISTICS IO &#40; Transact-SQL &#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  

