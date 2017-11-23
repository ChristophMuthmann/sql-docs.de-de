---
title: Sp_prepare (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs: TSQL
helpviewer_keywords: sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b32c3f6e5d07b29caf6baedc46d5342452d80a91
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spprepare-transact-sql"></a>sp_prepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Bereitet eine parametrisierte [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung und gibt eine Anweisung *behandeln* für die Ausführung. Sp_prepare wird aufgerufen, indem ID = 11 in einem tabular Data Stream (TDS)-Paket.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>Argumente  
 *Handle*  
 Ein SQL Server generierter *vorbereitete Handle* Bezeichner. *handle* ist ein erforderlicher Parameter mit einem **int** -Rückgabewert.  
  
 *params*  
 Identifiziert parametrisierte Anweisungen. Die *params* -Definition der Variablen wird in der Anweisung an die Stelle der Parametermarkierungen gesetzt. *params* ist ein erforderlicher Parameter, der einen Eingabewert vom Typ **ntext**, **nchar**,oder **nvarchar** erfordert. Geben Sie einen NULL-Wert ein, wenn die Anweisung nicht parametrisiert ist.  
  
 *stmt*  
 Definiert das Resultset des Cursors. Die *Stmt* -Parameter ist erforderlich und erfordert eine **Ntext**, **Nchar**, oder **Nvarchar** Eingabewert.  
  
 *Optionen*  
 Ein optionaler Parameter, der eine Beschreibung der Spalten im Cursorresultset zurückgibt. *Optionen* erfordert die folgenden **Int** Eingabewert.  
  
|Wert|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine einfache Anweisung vorbereitet und ausgeführt.  
  
```  
Declare @P1 int;  
Exec sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
Exec sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel wird eine einfache Anweisung vorbereitet und ausgeführt.  
  
```  
Declare @P1 int;  
Exec sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
Exec sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

