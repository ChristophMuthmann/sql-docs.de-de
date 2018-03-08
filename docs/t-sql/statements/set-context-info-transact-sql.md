---
title: SET CONTEXT_INFO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_CONTEXT_INFO_TSQL
- SET CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- context information [SQL Server]
- CONTEXT_INFO option
- SET CONTEXT_INFO statement
ms.assetid: a0b7b9f3-dbda-4350-a274-bd9ecd5c0a74
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4a93e9f40690f37c0c161c635aea95589d47ef1e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="set-contextinfo-transact-sql"></a>SET CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ordnet bis zu 128 Byte an binären Informationen der aktuellen Sitzung oder Verbindung zu.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET CONTEXT_INFO { binary_str | @binary_var }  
```  
  
## <a name="arguments"></a>Argumente  
 *binary_str*  
 Ist eine **binäre** -Konstante oder eine Konstante, die implizit in **binäre**, der aktuellen Sitzung oder Verbindung zugeordnet werden soll.  
  
 **@***Binary_var*  
 Ist eine **Varbinary** oder **binäre** Variablen mit einem Kontextwert, der aktuellen Sitzung oder Verbindung zugeordnet werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Die bevorzugte Vorgehensweise zum Abrufen von Kontextinformationen für die aktuelle Sitzung stellt die Verwendung der CONTEXT_INFO-Funktion dar. Informationen zum Sitzungskontext befindet sich auch in der **Context_info** Spalten in der folgenden Systemsichten:  
  
-   **sys.dm_exec_requests**  
  
-   **sys.dm_exec_sessions**  
  
-   **sys.sysprocesses**  
  
 SET CONTEXT_INFO kann nicht in einer benutzerdefinierten Funktion angegeben werden. Sie können mit SET CONTEXT_INFO keinen NULL-Wert angeben, da in den Sichten, die diese Werte enthalten, keine NULL-Werte zugelassen sind.  
  
 SET CONTEXT_INFO akzeptiert keine Ausdrücke, bei denen es sich nicht um Konstanten oder Variablennamen handelt. Die Kontextinformationen auf das Ergebnis eines Funktionsaufrufes festlegen möchten, müssen Sie zuerst das Ergebnis des Funktionsaufrufs in auch eine **binäre** oder **Varbinary** Variable.  
  
 Wenn Sie SET CONTEXT_INFO in einer gespeicherten Prozedur oder einem Trigger ausführen, ist im Gegensatz zu anderen SET-Anweisungen der neue Wert für die Kontextinformationen persistent, nachdem die gespeicherte Prozedur oder der Trigger beendet wurden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-setting-context-information-by-using-a-constant"></a>A. Festlegen von Kontextinformationen durch Verwenden einer Konstante  
 Im folgenden Beispiel wird die Verwendung von `SET CONTEXT_INFO` durch das Festlegen des Wertes und Anzeigen der Ergebnisse erläutert. Beachten Sie, dass zum Abfragen von `sys.dm_exec_sessions` die SELECT- und VIEW SERVER STATE-Berechtigungen erforderlich sind. Bei Verwendung der CONTEXT_INFO-Funktion gilt dies nicht.  
  
```  
SET CONTEXT_INFO 0x01010101;  
GO  
SELECT context_info   
FROM sys.dm_exec_sessions  
WHERE session_id = @@SPID;  
GO  
```  
  
### <a name="b-setting-context-information-by-using-a-function"></a>B. Festlegen von Kontextinformationen durch Verwenden einer Funktion  
 Im folgenden Beispiel wird veranschaulicht, wie mit der Ausgabe einer Funktion den Kontextwert festgelegt, in dem der Wert von der Funktion zuerst werden in platziert muss einem **binäre** Variable.  
  
```  
DECLARE @BinVar varbinary(128);  
SET @BinVar = CAST(REPLICATE( 0x20, 128 ) AS varbinary(128) );  
SET CONTEXT_INFO @BinVar;  
  
SELECT CONTEXT_INFO() AS MyContextInfo;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [Sys. dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [Sys. dm_exec_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)  
  
  
