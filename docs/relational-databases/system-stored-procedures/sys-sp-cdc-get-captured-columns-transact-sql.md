---
title: sp_cdc_get_captured_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns_TSQL
- sp_cdc_get_captured_columns_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.sp_cdc_get_captured_columns
- sp_cdc_get_captured_columns
- change data capture [SQL Server], querying metadata
ms.assetid: d9e680be-ab9b-4e0c-b63a-90658f241df8
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e232446f85dabc19856913ebf2e0cc5f886dc8cb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysspcdcgetcapturedcolumns-transact-sql"></a>sys.sp_cdc_get_captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Metadateninformationen von Change Data Capture für die aufgezeichneten Quellspalten zurück, die von der angegebenen Aufzeichnungsinstanz nachverfolgt wurden. Change Data Capture ist nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_cdc_get_captured_columns   
    [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @capture_instance =] '*Capture_instance*"  
 Der Name der Aufzeichnungsinstanz, die der Quelltabelle zugeordnet ist. *Capture_instance* ist **Sysname** und darf nicht NULL sein.  
  
 Führen Sie zum Bericht über die aufzeichnungsinstanzen für die Tabelle die [sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) gespeicherte Prozedur.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|Name des Quelltabellenschemas.|  
|source_table|**sysname**|Name der Quelltabelle.|  
|capture_instance|**sysname**|Name der Aufzeichnungsinstanz.|  
|column_name|**sysname**|Name der aufgezeichneten Quellspalte.|  
|column_id|**int**|ID der Spalte in der Quelltabelle.|  
|ordinal_position|**int**|Position der Spalte innerhalb der Quelltabelle.|  
|data_type|**sysname**|Datentyp der Spalte.|  
|character_maximum_length|**int**|Maximale Zeichenlänge der zeichenbasierten Spalte; andernfalls NULL.|  
|numeric_precision|**tinyint**|Genauigkeit der Spalte, wenn sie auf numerischen Werten basiert; andernfalls NULL.|  
|numeric_precision_radix|**smallint**|Basis der Genauigkeit der Spalte, wenn sie auf numerischen Werten basiert; andernfalls NULL.|  
|numeric_scale|**int**|Dezimalstellen der Spalte, wenn sie auf numerischen Werten basiert; andernfalls NULL.|  
|datetime_precision|**smallint**|Genauigkeit der Spalte, wenn sie auf datetime-Werten basiert; andernfalls NULL.|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie zum Abrufen von Spalteninformationen zu den aufgezeichneten Spalten zurückgegeben, die durch Abfragen der Capture-Abfragefunktionen Instanz sp_cdc_get_captured_columns [CDC. fn_cdc_get_all_changes_ < Capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) oder [CDC. fn_cdc_get_net_changes_ < Capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md). Die Spaltennamen, IDs und Position bleiben während der Lebensdauer der Aufzeichnungsinstanz konstant. Nur die Spaltendatentypen ändern sich, wenn sich der Datentyp der zugrunde liegenden Quellspalte in der nachverfolgten Tabelle ändert. Spalten, die hinzugefügt oder aus einer Quelltabelle gelöscht haben keine Auswirkung auf die aufgezeichneten Spalten der vorhandenen aufzeichnungsinstanzen.  
  
 Verwendung [sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) zum Abrufen von Informationen über die Datendefinition Anweisungen der Datendefinitionssprache (DDL) in einer Quelltabelle angewendet. Alle DDL-Änderungen, die die Struktur einer nachverfolgten Quellspalte geändert haben, werden im Resultset zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle "db_owner". Für alle anderen Benutzer ist die SELECT-Berechtigung für alle aufgezeichneten Spalten in der Quelltabelle und, wenn eine Gatingrolle für die Aufzeichnungsinstanz definiert wurde, eine Mitgliedschaft in dieser Datenbankrolle erforderlich. Wenn der Aufrufer über keine Berechtigungen zum Anzeigen der Quelldaten verfügt, gibt die Funktion den Fehler 22981 zurück ("Das Objekt ist nicht vorhanden oder der Zugriff wurde verweigert").  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zu den aufgezeichneten Spalten in der `HumanResources_Employee`-Aufzeichnungsinstanz zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_get_captured_columns   
    @capture_instance = N'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_cdc_help_change_data_capture &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
