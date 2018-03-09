---
title: Sys. sp_cdc_generate_wrapper_function (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cdc_generate_wrapper_function_TSQL
- sp_cdc_generate_wrapper_function
- sys.sp_cdc_generate_wrapper_function_TSQL
- sys.sp_cdc_generate_wrapper_function
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_generate_wrapper_function
- sp_cdc_generate_wrapper_function
ms.assetid: 85bc086d-8a4e-4949-a23b-bf53044b925c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b32fc0848943814052a72e4b3f91eb4f5556a4bc
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysspcdcgeneratewrapperfunction-transact-sql"></a>sys.sp_cdc_generate_wrapper_function (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Generiert Skripts zur Erstellung von Wrapperfunktionen für die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbaren Change Data Capture-Abfragefunktionen. Die in den generierten Wrappern unterstützte API ermöglicht die Angabe des Abfrageintervalls als datetime-Intervall. Aus diesem Grund eignet sich die Funktion ideal in vielen Warehousinganwendungen, einschließlich der Anwendungen, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketdesignern entwickelt werden, die Change Data Capture-Technologie zur Bestimmung inkrementeller Ladevorgänge verwenden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.sp_cdc_generate_wrapper_function  
    [ [ @capture_instance sysname = ] 'capture_instance'  
    [ , [ @closed_high_end_point = ] closed_high_end_pt  
    [ , [ @column_list = ] 'column_list'  
```  
  
```  
  
[ , [ @update_flag_list = ] 'update_flag_list'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @capture_instance=] '*Capture_instance*"  
 Die Aufzeichnungsinstanz, für die Skripts generiert werden sollen. *Capture_instance* ist **Sysname** und hat den Standardwert NULL. Wenn ein Wert weggelassen oder explizit auf NULL gesetzt wird, werden Wrapperskripts für alle Aufzeichnungsinstanzen generiert.  
  
 [ @closed_high_end_point=] *High_end_pt_flag*  
 Das Flagbit, das angibt, ob Änderungen, deren Commitzeit gleich dem oberen Endpunkt ist, von der generierten Prozedur innerhalb des Extrahierungsintervalls eingeschlossen werden sollen. *High_end_pt_flag* ist **Bit** und hat den Standardwert 1 gibt an, dass der Endpunkt eingeschlossen werden soll. Ein Wert von 0 gibt an, dass alle Commitzeiten unter dem oberen Endpunkt liegen müssen.  
  
 [ @column_list=] '*Column_list*"  
 Eine Liste erfasster Spalten, die in das Resultset eingeschlossen werden sollen, das von der Wrapperfunktion zurückgegeben wird. *Column_list* ist **nvarchar(max)** und hat den Standardwert NULL. Bei Angabe von NULL werden alle aufgezeichneten Spalten eingeschlossen.  
  
 [ @update_flag_list=] '*Update_flag_list*"  
 Eine Liste enthaltener Spalten, für die das von der Wrapperfunktion zurückgegebene Resultset ein Updateflag enthält. *Update_flag_list* ist **nvarchar(max)** und hat den Standardwert NULL. Bei Angabe von NULL werden keine Updateflags eingeschlossen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Spaltentyp|Description|  
|-----------------|-----------------|-----------------|  
|**Funktionsname**|**nvarchar(145)**|Name der generierten Funktion.|  
|**create_script**|**nvarchar(max)**|Das Skript, mit dem die Wrapperfunktion der Aufzeichnungsinstanz erstellt wird.|  
  
## <a name="remarks"></a>Hinweise  
 Das Skript zur Erstellung der Wrapperfunktion für eine Abfrage aller Änderungen für eine Aufzeichnungsinstanz wird immer generiert. Wenn die Aufzeichnungsinstanz Abfragen für Nettoänderungen unterstützt, wird auch das Skript zur Generierung einer Wrapperfunktion für diese Abfrage generiert1.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie Sie mit `sys.sp_cdc_generate_wrapper_function` Wrapper für alle Change Data Capture-Funktionen erstellen.  
  
```  
DECLARE @wrapper_functions TABLE (  
    function_name sysname,  
    create_script nvarchar(max));  
  
INSERT INTO @wrapper_functions  
EXEC sys.sp_cdc_generate_wrapper_function;  
  
DECLARE @create_script nvarchar(max);  
DECLARE #hfunctions CURSOR LOCAL fast_forward  
FOR   
    SELECT create_script FROM @wrapper_functions;  
  
OPEN #hfunctions;  
FETCH #hfunctions INTO @create_script;  
WHILE (@@fetch_status <> -1)  
BEGIN  
    EXEC sp_executesql @create_script  
    FETCH #hfunctions INTO @create_script  
END;  
  
CLOSE #hfunctions;  
DEALLOCATE #hfunctions;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für Change Data Capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Change Data Capture &#40; SSIS &#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)  
  
  
