---
title: dm_db_rda_migration_status (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_migration_status
- sys.dm_db_rda_migration_status_TSQL
- dm_db_rda_migration_status
- dm_db_rda_migration_status_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_rda_migration_status dynamic management view
ms.assetid: faf3901c-a0e0-4e0c-8b1b-86d9f15f34dd
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 088300f865265f330a06e40b7712fa63fd89f02a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch-Datenbank - dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Batch von migrierten Daten aus jeder Stretch-aktivierte Tabelle auf der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Batches werden durch ihre Start- und Endzeit identifiziert.  
  
 **dm_db_rda_migration_status** auf den aktuellen Datenbankkontext begrenzt. Stellen Sie sicher, dass Sie im Kontext Datenbank der Stretch-fähigen Tabellen sind für die Sie Migrationsstatus anzeigen möchten.  
  
 In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], die Ausgabe des **dm_db_rda_migration_status** ist auf 200 Zeilen beschränkt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|Die ID der Tabelle, die von der Zeilen migriert wurden.|  
|**database_id**|**int**|Die ID der Datenbank, von der Zeilen migriert wurden.|  
|**migrated_rows**|**bigint**|Die Anzahl der Zeilen migriert, in diesem Batch.|  
|**start_time_utc**|**datetime**|Die UTC-Zeit, zu der der Batch gestartet wurde.|  
|**end_time_utc**|**datetime**|Die UTC-Zeit, zu dem der Batch beendet.|  
|**error_number**|**int**|Wenn der Batch, die Fehlernummer des Fehlers, die aufgetreten sind fehlschlägt. Andernfalls wird null verwendet.|  
|**error_severity**|**int**|Wenn der Batch, den Schweregrad des Fehlers, die aufgetreten sind fehlschlägt. Andernfalls wird null verwendet.|  
|**error_state**|**int**|Wenn der Batch, den Zustand des Fehlers, die aufgetreten sind fehlschlägt. Andernfalls wird null verwendet.<br /><br /> Die **Error_state** gibt an, die Bedingung oder den Speicherort, in dem der Fehler aufgetreten ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
