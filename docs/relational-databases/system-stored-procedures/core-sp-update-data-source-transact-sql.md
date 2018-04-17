---
title: sp_update_data_source (Transact-SQL) | Microsoft Docs
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
- sp_update_data_source
- sp_update_data_source_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_data_source
- management data warehouse, data collector stored procedures
- core.sp_update_data_source stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 66b95f96-6df7-4657-9b3c-86a58c788ca5
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 042f03a9004a357e0b7a488494533d7f778247b9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="corespupdatedatasource-transact-sql"></a>core.sp_update_data_source (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert eine vorhandene Zeile oder fügt eine neue Zeile in der core.source_info_internal-Tabelle des Verwaltungs-Data Warehouse ein. Diese Prozedur wird von der Laufzeitkomponente des Datensammlers bei jedem Hochladen von Daten in das Verwaltungs-Data Warehouse durch ein Uploadpaket aufgerufen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
core.sp_update_data_source [ @collection_set_uid = ] 'collection_set_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @days_until_expiration = ] days_until_expiration  
    , [ @source_id = ] source_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumente  
 [ @collection_set_uid =] '*Collection_set_uid*"  
 Die GUID für den Sammlungssatz. *Collection_set_uid* ist **"uniqueidentifier"**, verfügt über keinen Standardwert. Um die GUID zu erhalten, fragen Sie die dbo.syscollector_collection_sets-Sicht in der MSDB-Datenbank ab.  
  
 [ @machine_name =] '*Machine_name*"  
 Der Name des Servers, auf dem sich der Sammlungssatz befindet. *Computername* ist **Sysname** verfügt über keinen Standardwert.  
  
 [ @named_instance =] '*Named_instance*"  
 Der Name der Instanz für den Sammlungssatz. *Named_instance* ist **Sysname**, verfügt über keinen Standardwert.  
  
> [!NOTE]  
>  *Named_instance* muss der vollqualifizierte Instanzname sein, besteht aus den Computernamen und den Instanznamen im Format *Computername*\\*Instancename*.  
  
 [ @days_until_expiration =] *Days_until_expiration*  
 Die Anzahl der Tage, die in der Beibehaltungsdauer für Momentaufnahmedaten verbleiben. *Days_until_expiration* ist **"smallint"**.  
  
 [ @source_id =] *Source_id*  
 Der eindeutige Bezeichner für die Quelle des Updates. *Source_ID* ist **Int** und wird als OUTPUT zurückgegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Jedes Mal, wenn ein Uploadpaket mit dem Hochladen von Daten in das Verwaltungs-Data Warehouse beginnt, ruft die Laufzeitkomponente des Datensammlers core.sp_update_data_source auf. Die core.source_info_internal-Tabelle wird aktualisiert, wenn nach dem letzten Hochladen eine der folgenden Änderungen durchgeführt wurde:  
  
-   Ein neuer Sammlungssatz wurde hinzugefügt.  
  
-   Der Wert für days_until_expiration wurde geändert.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Mdw_writer** (mit EXECUTE-Berechtigung) erforderlich ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Datenquelle aktualisiert (in diesem Fall der Sammlungssatz für die Datenträgerverwendung), die Anzahl der Tage bis zum Ablaufdatum festgelegt und der Bezeichner für die Quelle zurückgegeben. In diesem Beispiel wird die Standardinstanz verwendet.  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @source_id int;  
EXEC core.sp_update_data_source   
@collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
@machine_name = '<computername>',  
@named_instance = 'MSSQLSERVER',  
@days_until_expiration = 10,  
@source_id = @source_id OUTPUT;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Verwaltungs-Data Warehouse](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
