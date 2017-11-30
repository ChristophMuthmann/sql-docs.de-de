---
title: Sys. fn_cdc_is_bit_set (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- fn_cdc_is_bit_set
- sys.fn_cdc_is_bit_set_TSQL
- sys.fn_cdc_is_bit_set
- fn_cdc_is_bit_set_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.fn_cdc_is_bit_set
- fn_cdc_is_bit_set
ms.assetid: 792fe7cf-b3b8-4f25-8329-78d63f0e6921
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eea5c3c645bdd8ab6a1c0d9a8e18b430d2aa5871
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysfncdcisbitset-transact-sql"></a>sys.fn_cdc_is_bit_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt an, ob eine aufgezeichnete Spalte aktualisiert wurde, indem geprüft wird, ob ihre Ordnungsposition in einer bereitgestellten Bitmaske festgelegt ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_cdc_is_bit_set ( position , update_mask )  
```  
  
## <a name="arguments"></a>Argumente  
 *position*  
 Die Ordnungsposition in der zu überprüfenden Maske. *position* ist **int**  
  
 *update_mask*  
 Die Maske, die aktualisierte Spalten identifiziert. *update_mask* ist **varbinary(128)**  
  
## <a name="return-type"></a>Rückgabetyp  
 **bit**  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion wird in der Regel als Teil einer Änderungsdatenabfrage verwendet, um anzuzeigen, ob eine Spalte geändert wurde. In diesem Szenario wird die Funktion [Sys. fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) vor der Abfrage verwendet, um die erforderliche Spaltenordnungszahl abzurufen. **sys.fn_cdc_is_bit_set** wird dann auf jede Zeile von abgerufenen Änderungsdaten angewendet und stellt die spaltenspezifischen Informationen als Teil des zurückgegebenen Resultsets bereit.  
  
 Es wird empfohlen, diese Funktion anstelle der Funktion [fn_cdc_has_column_changed](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md) zum bestimmen, ob die Spalten für alle Zeilen eines zurückgegebenen Resultsets geändert haben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `sys.fn_cdc_is_bit_set` verwendet, um dem von der Abfragefunktion `cdc.fn_cdc_get_all_changes_HR_Department` generierten Resultset die Spalte '`IsGroupNmUpdated`' voranzustellen, wobei die vorausberechnete Spaltenordnungszahl und der Wert von `__$update_mask` als Argumente für den Aufruf verwendet werden.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10), @GroupNm_ordinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @GroupNm_ordinal = sys.fn_cdc_get_column_ordinal('HR_Department','GroupName');  
  
SELECT sys.fn_cdc_is_bit_set(@GroupNm_ordinal,__$update_mask) as 'IsGroupNmUpdated', *  
FROM cdc.fn_cdc_get_all_changes_HR_Department( @from_lsn, @to_lsn, 'all')  
WHERE __$operation = 4;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Change Data Capture-Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [Sys. fn_cdc_get_column_ordinal &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md)   
 [fn_cdc_has_column_changed &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md)   
 [CDC. fn_cdc_get_all_changes_ &#60; Capture_instance &#62;  &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [CDC. fn_cdc_get_net_changes_ &#60; Capture_instance &#62; &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [Über Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
