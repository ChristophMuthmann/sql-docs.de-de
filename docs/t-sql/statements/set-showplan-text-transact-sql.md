---
title: SET SHOWPLAN_TEXT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0ade3c22c437984724cbb7956951d85cdc17d8f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-showplantext-transact-sql"></a>SET SHOWPLAN_TEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bewirkt, dass Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht ausführt. Stattdessen gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Informationen zur Ausführung der Anweisungen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET SHOWPLAN_TEXT { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 Die Einstellung von SET SHOWPLAN_TEXT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Wenn SET SHOWPLAN_TEXT auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ausführungsinformationen für jede [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung zurück, ohne sie auszuführen. Wenn diese Option auf ON festgelegt ist, werden Ausführungsplaninformationen zu allen weiteren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anweisungen zurückgegeben, bis die Option auf OFF festgelegt wird. Wenn beispielsweise eine CREATE TABLE-Anweisung ausgeführt wird, während SET SHOWPLAN_TEXT auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei einer nachfolgenden SELECT-Anweisung, die dieselbe Tabelle betrifft, eine Fehlermeldung zurück. In dieser wird der Benutzer informiert, dass diese Tabelle nicht vorhanden ist. Daher schlagen spätere Verweise auf diese Tabelle fehl. Wenn SET SHOWPLAN_TEXT auf OFF festgelegt wird, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anweisungen aus, ohne einen Bericht mit Ausführungsplaninformationen zu generieren.  
  
 Verwenden Sie SET SHOWPLAN_TEXT, um eine lesbare Ausgabe für Microsoft Win32-Befehlszeilenanwendungen, z.B. das Hilfsprogramm **osql**, zurückzugeben. SET SHOWPLAN_ALL gibt eine detailliertere Ausgabe zurück, die in Programmen verwendet werden kann, die diese Ausgabe verarbeiten.  
  
 SET SHOWPLAN_TEXT und SET SHOWPLAN_ALL können in gespeicherten Prozeduren nicht angegeben werden. Sie müssen die einzigen Anweisungen in einem Batch sein.  
  
 SET SHOWPLAN_TEXT gibt ein Rowset in Form einer hierarchischen Struktur zurück, die die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageprozessor beim Ausführen einer Anweisung durchgeführten Schritte darstellt. Jede in der Ausgabe widergespiegelte Anweisung enthält zuerst eine Zeile mit dem Text der Anweisung, auf die mehrere Zeilen mit den Details der Ausführungsschritte folgen. In der Tabelle wird die in der Ausgabe enthaltene Spalte dargestellt.  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**StmtText**|Für Zeilen, die nicht vom Typ PLAN_ROW sind, enthält diese Spalte den Text der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung. Für Zeilen vom Typ PLAN_ROW enthält diese Spalte eine Beschreibung des Vorgangs. Diese Spalte enthält den physischen Operator und optional auch den logischen Operator. Auf die Spalte kann auch eine Beschreibung folgen, die vom physischen Operator bestimmt wird. Weitere Informationen zu physischen Operatoren finden Sie in der **Argument**-Spalte unter [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md).|  
  
 Weitere Informationen zu den physischen und logischen Operatoren, die in der Showplanausgabe angezeigt werden, finden Sie unter [Referenz zu logischen und physischen Showplanoperatoren](../../relational-databases/showplan-logical-and-physical-operators-reference.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Verwendung von SET SHOWPLAN_TEXT benötigen Sie für die Ausführung der Anweisungen, auf die SET SHOWPLAN_TEXT angewendet wird, ausreichende Berechtigungen sowie die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die verwiesen wird.  
  
 Damit die Anweisungen SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure* und EXEC *user_defined_function* einen Showplan erstellen, benötigt der Benutzer Folgendes:  
  
-   Berechtigungen für die Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  
  
-   Die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die von den Transact-SQL-Anweisungen verwiesen wird, wie z. B. Tabellen, Sichten usw.  
  
 Für alle anderen Anweisungen, z.B. DDL, USE *database_name*, SET, DECLARE, dynamische SQL-Anweisungen usw., werden nur die entsprechenden Berechtigungen für die Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen benötigt.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)  
  
  
