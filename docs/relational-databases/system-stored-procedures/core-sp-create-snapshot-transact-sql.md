---
title: sp_create_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_create_snapshot
- sp_create_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- management data warehouse, data collector stored procedures
- data collector [SQL Server], stored procedures
- core.sp_create_snapshot stored procedure
- sp_create_snapshot
ms.assetid: ff297bda-0ee2-4fda-91c8-7000377775e3
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b0ff5c71ec0516b51040c157eb517fcd0402ca3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="corespcreatesnapshot-transact-sql"></a>core.sp_create_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt eine Zeile in die core.snapshots-Sicht des Verwaltungs-Data Warehouse ein. Diese Prozedur wird jedes Mal aufgerufen, wenn Daten durch ein Uploadpaket in das Verwaltungs-Data Warehouse hochgeladen werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
core.sp_create_snapshot [ @collection_set_uid = ] 'collection_set_uid'  
    , [ @collector_type_uid = ] 'collector_type_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @log_id = ] log_id  
    , [ @snapshot_id = ] snapshot_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumente  
 [ @collection_set_uid =] '*Collection_set_uid*"  
 Die GUID für den Sammlungssatz. *Collection_set_uid* ist **"uniqueidentifier"** verfügt über keinen Standardwert. Um die GUID zu erhalten, fragen Sie die dbo.syscollector_collection_sets-Sicht in der MSDB-Datenbank ab.  
  
 [ @collector_type_uid =] '*Collector_type_uid*"  
 Die GUID für einen Sammlertyp. *Collector_type_uid* ist **"uniqueidentifier"** verfügt über keinen Standardwert. Um die GUID zu erhalten, fragen Sie die dbo.syscollector_collector_types-Sicht in der MSDB-Datenbank ab.  
  
 [ @machine_name=] '*Machine_name*"  
 Der Name des Servers, auf dem sich der Sammlungssatz befindet. *Computername* ist **Sysname**, verfügt über keinen Standardwert.  
  
 [ @named_instance=] '*Named_instance*"  
 Der Name der Instanz für den Sammlungssatz. *Named_instance* ist **Sysname**, verfügt über keinen Standardwert.  
  
 [ @log_id = ] *log_id*  
 Der eindeutige Bezeichner, der dem Ereignisprotokoll des Sammlungssatzes auf dem Server zugeordnet ist, der die Daten gesammelt hat. *Log_id* ist **"bigint"** verfügt über keinen Standardwert. Zum Abrufen des Werts für *Log_id*, Fragen Sie die syscollector_execution_log-Sicht in der Msdb-Datenbank.  
  
 [ @snapshot_id =] *Snapshot_id*  
 Der eindeutige Bezeichner für eine Zeile, die in der core.snapshots-Sicht eingefügt wird. *Snapshot_id* ist **Int** und wird als OUTPUT zurückgegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Jedes Mal, wenn ein Uploadpaket mit dem Hochladen von Daten in das Verwaltungs-Data Warehouse startet, ruft die Laufzeitkomponente des Datensammlers core.sp_create_snapshot  auf.  
  
 Diese Prozedur führt eine Überprüfung auf Folgendes durch:  
  
-   collection_set_uid stimmt mit einem vorhandenen Eintrag in der core.source_info_internal-Tabelle überein.  
  
-   collector_type_uid stimmt mit einem vorhandenen Eintrag in der core.supported_collector_types-Sicht überein.  
  
 Schlägt eine der oben aufgeführten Überprüfungen fehl, so schlägt die Prozedur fehl und gibt einen Fehler zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Mdw_writer** (mit EXECUTE-Berechtigung) erforderlich ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Momentaufnahme für den Sammlungssatz für die Datenträgerverwendung erstellt, dem Verwaltungs-Data Warehouse hinzugefügt und der Momentaufnahmebezeichner zurückgegeben. In diesem Beispiel wird die Standardinstanz verwendet.  
  
```  
USE <management_data_warehouse>;  
DECLARE @snapshot_id int;  
EXEC core.sp_create_snapshot   
    @collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
    @collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @machine_name = '<computername>',  
    @named_instance = 'MSSQLSERVER',  
    @log_id = 11, -- ID of the log for the collection set  
    @snapshot_id = @snapshot_id OUTPUT;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Verwaltungs-Data Warehouse](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
