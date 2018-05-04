---
title: Log_shipping_secondary_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary_databases_TSQL
- log_shipping_secondary_databases
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary_databases system table
ms.assetid: ba2374af-86b8-480c-a10c-51e7c4e3ae23
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b21229c59cf54e500c47942a2bc2d763c776b330
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="logshippingsecondarydatabases-transact-sql"></a>log_shipping_secondary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Speichert einen Datensatz pro sekundärer Datenbank in einer Protokollversandkonfiguration. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**secondary_database**|**sysname**|Der Name der sekundären Datenbank in der Protokollversandkonfiguration.|  
|**secondary_id**|**uniqueidentifier**|Die ID für den sekundären Server in der Protokollversandkonfiguration.|  
|**restore_delay**|**int**|Die Zeitspanne in Minuten an, die der sekundäre Server vor dem Wiederherstellen einer bestimmten Sicherungsdatei wartet. Die Standardeinstellung beträgt 0 Minuten.|  
|**restore_all**|**bit**|Ist der Wert gleich 1, stellt der sekundäre Server bei Ausführung des Wiederherstellungsauftrags alle verfügbaren Sicherungen des Transaktionsprotokolls wieder her. Andernfalls wird nach der Wiederherstellung einer Datei beendet.|  
|**restore_mode**|**bit**|Der Wiederherstellungsmodus für die sekundäre Datenbank.<br /><br /> 0 = Das Protokoll wird mit NORECOVERY wiederhergestellt.<br /><br /> 1 = Das Protokoll wird mit STANDBY wiederhergestellt.|  
|**disconnect_users**|**bit**|Ist der Wert gleich 1, werden Benutzer beim Ausführen eines Wiederherstellungsvorgangs von der sekundären Datenbank getrennt. Die Standardeinstellung = 0.|  
|**block_size**|**int**|Die Größe in Bytes, die als Blockgröße für das Sicherungsmedium verwendet wird.|  
|**buffer_count**|**int**|Die Gesamtanzahl der beim Sicherungs- oder Wiederherstellungsvorgang verwendeten Puffer.|  
|**max_transfer_size**|**int**|Die Größe in Bytes, der maximalen Eingabe- oder ausgabeanforderung ausgestellt hat [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Sicherungsmedium.|  
|**last_restored_file**|**nvarchar(500)**|Der Dateiname der letzten Sicherungsdatei, die in der sekundären Datenbank wiederhergestellt wurde.|  
|**last_restored_date**|**datetime**|Datum und Uhrzeit des letzten Wiederherstellungsvorgangs für die sekundäre Datenbank.|  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Sp_add_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [Sp_delete_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [log_shipping_secondary &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
