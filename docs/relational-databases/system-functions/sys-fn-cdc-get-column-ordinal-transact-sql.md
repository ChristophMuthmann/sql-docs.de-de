---
title: Sys. fn_cdc_get_column_ordinal (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_get_column_ordinal
- fn_cdc_get_column_ordinal_TSQL
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal_TSQL
dev_langs: TSQL
helpviewer_keywords:
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal
ms.assetid: 4bb21a57-2b94-4208-8bdf-6a3e2681d881
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c15bd3ef8ebed161705e3b8e7373cf8574161a27
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfncdcgetcolumnordinal-transact-sql"></a>sys.fn_cdc_get_column_ordinal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Spaltenordnungszahl angegebene Spalte, wie er angezeigt, in wird der [Änderungstabelle](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) der angegebenen Aufzeichnungsinstanz zugeordnet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_cdc_get_column_ordinal ( 'capture_instance','column_name')  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Capture_instance* **"**  
 Der Name der Aufzeichnungsinstanz, in der die angegebene Spalte als aufgezeichnete Spalte identifiziert wird. *Capture_instance* ist **Sysname**.  
  
 **"** *Column_name* **"**  
 Die Spalte, über die berichtet werden soll. *Column_name* ist **Sysname**.  
  
## <a name="return-type"></a>Rückgabetyp  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion dient zum Identifizieren der Ordnungsposition einer in der Change Data Capture-Updatemaske aufgezeichneten Spalte. Es dient hauptsächlich in Verbindung mit der Funktion [Sys. fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) , Informationen aus der updatemaske zu extrahieren, während Abfragen von Änderungsdaten.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die SELECT-Berechtigung für alle aufgezeichneten Spalten der Quelltabelle. Wenn für die Aufzeichnungsinstanz eine Datenbankrolle für die Change Data Capture-Komponente angegeben ist, erfordert dies ebenfalls die Mitgliedschaft in der entsprechenden Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird für die Aufzeichnungsinstanz `VacationHours` die Ordnungsposition der `HumanResources_Employee`-Spalte in der Updatemaske abgerufen. Der Wert wird daraufhin für den Aufruf von `sys.fn_cdc_is_bit_set` verwendet, um Informationen aus der zurückgegebenen Updatemaske zu extrahieren.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10),  @VacationHoursOrdinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @VacationHoursOrdinal = sys.fn_cdc_get_column_ordinal   
    ( 'HumanResources_Employee','VacationHours');  
SELECT *, sys.fn_cdc_is_bit_set(@VacationHoursOrdinal,  
    __$update_mask) as 'VacationHours'  
FROM cdc.fn_cdc_get_net_changes_HumanResources_Employee  
    ( @from_lsn, @to_lsn, 'all with mask');  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Change Data Capture-Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [Über Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [sp_cdc_help_change_data_capture &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [sp_cdc_get_captured_columns &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [Sys. fn_cdc_is_bit_set &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)  
  
  
