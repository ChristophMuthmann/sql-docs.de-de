---
title: Syscollector_config_store (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_config_store_TSQL
- syscollector_config_store
dev_langs: TSQL
helpviewer_keywords:
- data collector view
- syscollector_config_store view
ms.assetid: f15f6b05-6808-4b76-b6a8-48dec844cf63
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6811c1ab9fef0f15422f1d51ac9b969476e58699
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="syscollectorconfigstore-transact-sql"></a>syscollector_config_store (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Eigenschaften zurück, die im Gegensatz zu einer Sammlungssatzinstanz für den gesamten Datensammler gelten. Jede Zeile in dieser Sicht beschreibt eine bestimmte Datensammlereigenschaft, wie den Namen des Verwaltungs-Data Warehouse und den Namen der Instanz, in der sich das Verwaltungs-Data Warehouse befindet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|parameter_name|**vom Datentyp nvarchar(128)**|Der Name der Eigenschaft. Lässt keine NULL-Werte zu.|  
|parameter_value|**sql_variant**|Der tatsächliche Wert der Eigenschaft. Lässt NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die SELECT-Berechtigung für die Sicht oder die Mitgliedschaft in der festen Datenbankrolle dc_operator, dc_proxy oder dc_admin.  
  
## <a name="remarks"></a>Hinweise  
 Die Liste der verfügbaren Eigenschaften ist festgelegt, und deren Werte können nur mithilfe der geeigneten gespeicherten Prozedur geändert werden. In der folgenden Tabelle werden die Eigenschaften beschrieben, die durch diese Sicht verfügbar gemacht werden.  
  
|Eigenschaftsname|Beschreibung|  
|-------------------|-----------------|  
|CacheDirectory|Der Name des Verzeichnisses im Dateisystem, in dem die Sammlertyppakete temporäre Informationen speichern.<br /><br /> NULL = das standardmäßige temporäre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verzeichnis verwendet wird.|  
|CacheWindow|Gibt die Datenbeibehaltungsrichtlinie des Cacheverzeichnisses für fehlgeschlagene Datenuploads an.<br /><br /> -1 = Daten aus allen fehlgeschlagenen Uploads beibehalten.<br /><br /> 0 - Keine Daten aus fehlgeschlagenen Uploads beibehalten.<br /><br /> *n*= Daten aus beibehalten  *n*  vorherigen fehlgeschlagenen uploadversuchen, wobei  *n*  > = 1.<br /><br /> Verwenden Sie die gespeicherte Prozedur sp_syscollector_set_cache_window, um diesen Wert zu ändern.|  
|CollectorEnabled|Gibt den Status des Datensammlers an.<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert<br /><br /> Verwenden Sie entweder die gespeicherte Prozedur sp_syscollector_enable_collector oder die gespeicherte Prozedur sp_syscollector_disable_collector, um diesen Wert zu ändern.|  
|MDWDatabase|Der Name des Verwaltungs-Data Warehouses. Verwenden Sie die gespeicherte Prozedur sp_syscollector_set_warehouse_database_name, um diesen Wert zu ändern.|  
|MDWInstance|Der Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz für das Verwaltungs-Data Warehouse. Verwenden Sie die gespeicherte Prozedur sp_syscollector_set_warehouse_instance_name, um diesen Wert zu ändern.|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die syscollector_config_store-Sicht abgefragt.  
  
```tsql  
SELECT parameter_name, parameter_value  
FROM msdb.dbo.syscollector_config_store;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Sichten des Datensammlers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [Sp_syscollector_set_warehouse_database_name &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)   
 [Sp_syscollector_set_warehouse_instance_name &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
