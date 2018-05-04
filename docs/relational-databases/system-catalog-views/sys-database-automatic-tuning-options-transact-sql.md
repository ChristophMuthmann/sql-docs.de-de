---
title: Sys.database_automatic_tuning_options (Transact-SQL) | Microsoft Docs
description: Erfahren Sie, wie automatische Optimierungsoptionen für eine SQL-Datenbank anzeigen
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs:
- TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: 24
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 6b1ddbb9fd87c91182b3e43d9ac8e89465eb77f7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>Sys.Database\_automatische\_Tuning_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Die automatische Optimierung Optionen für diese Datenbank zurückgegeben.  

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|Der Name der Option für die automatische Optimierung. Verweisen auf [ALTER DATABASE legen AUTOMATIC_TUNING &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) für die verfügbaren Optionen.|  
|**desired_state**|**smallint**|Gibt den gewünschten Betriebsmodus für die automatische Optimierung Option explizit vom Benutzer festgelegten an.<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|Textbeschreibung für den gewünschten Betriebsmodus des Option Automatische Optimierung.<br />OFF<br />ON|  
|**actual_state**|**smallint**|Gibt den Betriebsmodus der automatischen Optimierung Option an.<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|Die textbeschreibung der tatsächlichen Betriebsmodus des Option Automatische Optimierung.<br />OFF<br />ON|  
|**reason**|**smallint**|Gibt an, warum die tatsächlichen und den gewünschten Status unterschiedlich sind.<br />2 = DISABLED<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED ANNEHMEN|   
|**reason_desc**|**nvarchar(60)**|Beschreibung des Grunds, warum die tatsächlichen und den gewünschten Status unterschiedlich sind.<br />DEAKTIVIERT = Option ist deaktiviert, vom System<br />QUERY_STORE_OFF = der Abfragespeicher ist deaktiviert.<br />QUERY_STORE_READ_ONLY = Query Store befindet sich in nur-Lese-Modus<br />NOT_SUPPORTED = verfügbar nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition| 
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW DATABASE STATE`-Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [Automatische Optimierung](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
