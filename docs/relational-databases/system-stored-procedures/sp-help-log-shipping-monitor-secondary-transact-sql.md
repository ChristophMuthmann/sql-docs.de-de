---
title: Sp_help_log_shipping_monitor_secondary (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/02/2016
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
- sp_help_log_shipping_monitor_secondary
- sp_help_log_shipping_monitor_secondary_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_log_shipping_monitor_secondary
ms.assetid: 3ac091ea-c9a8-4c05-a0b6-1ccf4e001339
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 612571cd299a0474b1d405d8d9885487eba70a16
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sphelplogshippingmonitorsecondary-transact-sql"></a>sp_help_log_shipping_monitor_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu einer sekundären Datenbank aus den Überwachungstabellen zurück.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_log_shipping_monitor_secondary  
[ @secondary_server = ] 'secondary_server',  
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@secondary_server =** ] "*Secondary_server*"  
 Der Name des sekundären Servers. *secondary_server* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 [  **@secondary_database =** ] "*Secondary_database*"  
 Der Name der sekundären Datenbank. *secondary_database* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Column|Description|  
|------------|-----------------|  
|**secondary_server**|Der Name der sekundären Instanz von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in der Protokollversandkonfiguration.|  
|**secondary_database**|Der Name der sekundären Datenbank in der Protokollversandkonfiguration.|  
|**secondary_id**|Die ID für den sekundären Server in der Protokollversandkonfiguration.|  
|**primary_server**|Der Name der primären Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in der Protokollversandkonfiguration.|  
|**primary_database**|Der Name der primären Datenbank in der Protokollversandkonfiguration|  
|**restore_threshold**|Die Anzahl der zulässigen Minuten zwischen Wiederherstellungsvorgängen, bevor eine Warnung generiert wird.|  
|**threshold_alert**|Die Warnung, die ausgelöst wird, wenn die Wiederherstellungsschwelle überschritten wird.|  
|**threshold_alert_enabled**|Legt fest, ob Warnungen für Wiederherstellungsschwellen aktiviert sind.<br /><br /> 1 = Aktiviert.<br /><br /> 0 = Deaktiviert.|  
|**last_copied_file**|Der Dateiname der letzten Sicherungsdatei, die auf den sekundären Server kopiert wurde.|  
|**last_copied_date**|Datum und Uhrzeit des letzten Kopiervorgangs auf den sekundären Server|  
|**last_copied_date_utc**|Datum und Uhrzeit des letzten Kopiervorgangs auf den sekundären Server in UTC (Coordinated Universal Time).|  
|**last_restored_file**|Der Dateiname der letzten Sicherungsdatei, die in der sekundären Datenbank wiederhergestellt wurde.|  
|**last_restored_date**|Datum und Uhrzeit des letzten Wiederherstellungsvorgangs für die sekundäre Datenbank.|  
|**last_restored_date_utc**|Datum und Uhrzeit des letzten Wiederherstellungsvorgangs auf dem sekundären Server in UTC (Coordinated Universal Time).|  
|**history_retention_period**|Die Zeitdauer in Minuten, die Verlaufsdatensätze des Protokollversands für eine bestimmte sekundäre Datenbank vor dem Löschen aufbewahrt werden.|  
  
## <a name="remarks"></a>Hinweise  
 **sp_help_log_shipping_monitor_secondary** muss aus der **master** -Datenbank auf dem Überwachungsserver ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
