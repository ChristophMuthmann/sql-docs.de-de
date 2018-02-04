---
title: fn_cdc_has_column_changed (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_has_column_changed_TSQL
- sys.fn_cdc_has_column_changed
- fn_cdc_has_column_changed_TSQL
- fn_cdc_has_column_changed
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_cdc_has_column_changed
- fn_cdc_has_column_changed
ms.assetid: 2b9e6278-050d-4ffc-8d1a-09606180facc
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2c8918fe44c6534de5829556754a837752b8cfb
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysfncdchascolumnchanged-transact-sql"></a>sys.fn_cdc_has_column_changed (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Identifiziert, ob die angegebene Updatemaske darauf hinweist, dass die angegebene Spalte in der zugeordneten Änderungszeile aktualisiert wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_cdc_has_column_changed ( 'capture_instance','column_name' , update_mask )  
```  
  
## <a name="arguments"></a>Argumente  
 **'** *capture_instance* **'**  
 Der Name der Aufzeichnungsinstanz. *Capture_instance* ist **Sysname**.  
  
 **"** *Column_name* **"**  
 Die aufgezeichnete Spalte der angegebenen Aufzeichnungsinstanz, für die ein Bericht erstellt werden soll. *Column_name* ist **Sysname**.  
  
 *update_mask*  
 Die Maske zur Identifizierung aktualisierter Spalten in einer zugeordneten Änderungszeile. *update_mask* ist **varbinary(128)**  
  
## <a name="return-type"></a>Rückgabetyp  
 **bit**  
  
## <a name="remarks"></a>Hinweise  
 Sie können diese Funktion zum Extrahieren von Informationen aus einer Updatemaske verwenden, die in einer Abfrage nach Änderungsdaten zurückgegeben wurde. Sie empfiehlt sich besonders dann, wenn Sie eine Updatemaske nachgelagert verarbeiten und wissen müssen, ob eine bestimmte Spalte in der zugeordneten Änderungszeile geändert wurde. Weitere Informationen finden Sie unter [Informationen zu Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
 Wenn diese Informationen als Teil einer Abfrage von Änderungsdaten zurückgegeben werden soll, es wird empfohlen, dass Sie die Funktionen verwenden [Sys. fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) und [Sys. fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) statt diese Funktion. Verwenden Sie die Funktion Fn_cdc_get_column_ordinal, bevor Sie Abfragen für Änderungsdaten, damit die gewünschte Spaltenordnungszahl nur einmal berechnet wird. Verwenden Sie Fn_cdc_is_bit_set innerhalb der Abfrage, um die Informationen aus der updatemaske für jede zurückgegebene Zeile zu extrahieren.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle sysadmin oder in der festen Datenbankrolle db_owner. Für alle anderen Benutzer ist die SELECT-Berechtigung für alle aufgezeichneten Spalten in der Quelltabelle und, wenn eine Gatingrolle für die Aufzeichnungsinstanz definiert wurde, eine Mitgliedschaft in dieser Datenbankrolle erforderlich.  
  
## <a name="see-also"></a>Siehe auch  
 [cdc.&#60;capture_instance&#62;_CT &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)   
 [cdc.captured_columns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
  
  
