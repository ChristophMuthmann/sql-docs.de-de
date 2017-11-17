---
title: SET SHOWPLAN_TEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHOWPLAN_TEXT
- SET_SHOWPLAN_TEXT_TSQL
- SET SHOWPLAN_TEXT
- SHOWPLAN_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_TEXT statement
- canceling statement execution
- SHOWPLAN_TEXT option
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: 2c4f3fc8-ff2c-4790-8b74-e7e8ef58f9a6
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7abd42acdcbfa4274686d3d8162e727cf36e5ee7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-showplantext-transact-sql"></a>SET SHOWPLAN_TEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bewirkt, dass Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht ausführt. Stattdessen gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Informationen zur Ausführung der Anweisungen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET SHOWPLAN_TEXT { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Die Einstellung von SET SHOWPLAN_TEXT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Wenn SET SHOWPLAN_TEXT auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ausführungsinformationen für jede [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung zurück, ohne sie auszuführen. Wenn diese Option auf ON festgelegt ist, werden Ausführungsplaninformationen zu allen weiteren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anweisungen zurückgegeben, bis die Option auf OFF festgelegt wird. Wenn beispielsweise eine CREATE TABLE-Anweisung ausgeführt wird, während SET SHOWPLAN_TEXT auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei einer nachfolgenden SELECT-Anweisung, die dieselbe Tabelle betrifft, eine Fehlermeldung zurück. In dieser wird der Benutzer informiert, dass diese Tabelle nicht vorhanden ist. Daher schlagen spätere Verweise auf diese Tabelle fehl. Wenn SET SHOWPLAN_TEXT auf OFF festgelegt wird, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anweisungen aus, ohne einen Bericht mit Ausführungsplaninformationen zu generieren.  
  
 SET SHOWPLAN_TEXT soll lesbare Ausgabe für Microsoft Win32-eingabeaufforderungsanwendungen zurückgeben, z. B. die **Osql** Hilfsprogramm. SET SHOWPLAN_ALL gibt eine detailliertere Ausgabe zurück, die in Programmen verwendet werden kann, die diese Ausgabe verarbeiten.  
  
 SET SHOWPLAN_TEXT und SET SHOWPLAN_ALL können in gespeicherten Prozeduren nicht angegeben werden. Sie müssen die einzigen Anweisungen in einem Batch sein.  
  
 SET SHOWPLAN_TEXT gibt ein Rowset in Form einer hierarchischen Struktur zurück, die die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageprozessor beim Ausführen einer Anweisung durchgeführten Schritte darstellt. Jede in der Ausgabe widergespiegelte Anweisung enthält zuerst eine Zeile mit dem Text der Anweisung, auf die mehrere Zeilen mit den Details der Ausführungsschritte folgen. In der Tabelle wird die in der Ausgabe enthaltene Spalte dargestellt.  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**StmtText**|Für Zeilen, die nicht vom Typ PLAN_ROW sind, enthält diese Spalte den Text der [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung. Für Zeilen vom Typ PLAN_ROW enthält diese Spalte eine Beschreibung des Vorgangs. Diese Spalte enthält den physischen Operator und optional auch den logischen Operator. Diese Spalte kann auch eine Beschreibung folgen der vom physischen Operator bestimmt wird. Weitere Informationen zu physischen Operatoren finden Sie unter der **Argument** Spalte [SET SHOWPLAN_ALL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-showplan-all-transact-sql.md).|  
  
 Weitere Informationen zu den physischen und logischen Operatoren, die in der Showplanausgabe angezeigt werden können, finden Sie unter [Showplan logischen und physischen Operatoren Verweis](../../relational-databases/showplan-logical-and-physical-operators-reference.md)  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Verwendung von SET SHOWPLAN_TEXT benötigen Sie für die Ausführung der Anweisungen, auf die SET SHOWPLAN_TEXT angewendet wird, ausreichende Berechtigungen sowie die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die verwiesen wird.  
  
 Für SELECT, INSERT, UPDATE, DELETE, EXEC *Stored_procedure*, und den AUSFÜHRUNGSTYP *User_defined_function* -Anweisungen, um einen Showplan zu erstellen, der Benutzer muss:  
  
-   Berechtigungen für die Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  
  
-   Die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die von den Transact-SQL-Anweisungen verwiesen wird, wie z. B. Tabellen, Sichten usw.  
  
 Für alle anderen Anweisungen, z. B. DDL, USE *Database_name*, SET, DECLARE, dynamisches SQL usw., nur die entsprechenden Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen erforderlich sind.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird gezeigt, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei der Verarbeitung von Anweisungen Indizes verwendet.  
  
 In der folgenden Abfrage wird ein Index verwendet:  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
StmtText                                             
---------------------------------------------------  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;   
  
StmtText                                                                                                                                                                                        
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Seek(OBJECT:([AdventureWorks2012].[Production].[Product].[PK_Product_ProductID]), SEEK:([AdventureWorks2012].[Production].[Product].[ProductID]=CONVERT_IMPLICIT(int,[@1],0)) ORDERED FORWARD)   
```  
  
 In der folgenden Abfrage wird kein Index verwendet:  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
StmtText                                                                  
------------------------------------------------------------------------  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;   
  
StmtText                                                                                                                                                                                                  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Scan(OBJECT:([AdventureWorks2012].[Production].[ProductCostHistory].[PK_ProductCostHistory_ProductCostID]), WHERE:([AdventureWorks2012].[Production].[ProductCostHistory].[StandardCost]<[@1]))  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)  
  
  

