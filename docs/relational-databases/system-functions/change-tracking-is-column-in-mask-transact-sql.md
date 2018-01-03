---
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs: TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ca1e489937aba92270fe73978f017c35b4fca99
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="changetrackingiscolumninmask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Interpretiert den SYS_CHANGE_COLUMNS-Wert, der von der CHANGETABLE(CHANGES …)-Funktion zurückgegeben wird. Dies ermöglicht es einer Anwendung zu ermitteln, ob die angegebene Spalte in den Werten enthalten ist, die für SYS_CHANGE_COLUMNS zurückgegeben werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>Argumente  
 *column_id*  
 Die ID der zu überprüfenden Spalte. Die Spalte ID erhalten Sie, indem Sie mit der [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) Funktion.  
  
 *change_columns*  
 Ist die Binärdaten aus der Spalte SYS_CHANGE_COLUMNS der der [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) Daten.  
  
## <a name="return-type"></a>Rückgabetyp  
 **bit**  
  
## <a name="return-values"></a>Rückgabewerte  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK gibt die folgenden Werte zurück.  
  
|Rückgabewert|Description|  
|------------------|-----------------|  
|0|Die angegebene Spalte befindet sich nicht in der *Change_columns* Liste.|  
|1|Die angegebene Spalte ist der *Change_columns* Liste.|  
  
## <a name="remarks"></a>Hinweise  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK führt keine Überprüfungen zum Überprüfen der *Column_id* -Werts der *Change_columns* Parameter aus der Tabelle, aus der abgerufen wurde die  *Column_id* abgerufen wurde.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird bestimmt, ob die `Salary`-Spalte in der `Employees`-Tabelle aktualisiert wurde. Die `COLUMNPROPERTY` Funktion gibt die Spalten-ID der `Salary` Spalte. Für die lokale Variable `@change_columns` müssen die Ergebnisse einer Abfrage unter Verwendung von CHANGETABLE als Datenquelle festgelegt werden.  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Änderungsnachverfolgungsfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
