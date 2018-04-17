---
title: Sys.external_data_sources (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0f082cc4246236133fe7439514d0cc2b64d3c7e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysexternaldatasources-transact-sql"></a>Sys.external_data_sources (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Enthält eine Zeile für jede externe Datenquelle in der aktuellen Datenbank für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 Enthält eine Zeile für jede externe Datenquelle auf dem Server für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|Objekt-ID für die externe Datenquelle.||  
|name|**sysname**|Der Name der externen Datenquelle.||  
|location|**nvarchar(4000)**|Die Verbindungszeichenfolge, die das Protokoll, IP-Adresse und Port für die externe Datenquelle enthält.||  
|type_desc|**nvarchar(255)**|Der Datenquellentyp ist als Zeichenfolge angezeigt.|HADOOP, RDBMS, SHARD_MAP_MANAGER, RemoteDataArchiveTypeExtDataSource|  
|Typ|**tinyint**|Der Datenquellentyp ist als Zahl angezeigt.|0 – HADOOP<br /><br /> 1 - RDBMS<br /><br /> 2 – SHARD_MAP_MANAGER<br /><br /> 3 – RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|Geben Sie für HADOOP, die IP- und Port Speicherort des Hadoop-Ressourcen-Managers. Dies wird verwendet, für die Übermittlung des Auftrags für eine Hadoop-Datenquelle.<br /><br /> NULL für andere Arten von Daten aus externen Quellen.||  
|credential_id|**int**|Die Objekt-ID der Datenbank, begrenzt Anmeldeinformationen zur Verbindung mit der externen Datenquelle.||  
|database_name|**sysname**|Für ein RDBMS, den Namen der Remotedatenbank. Für Typen: SHARD_MAP_MANAGER, den Namen der Shard-Schema-Manager-Datenbank. NULL für andere Arten von Daten aus externen Quellen.||  
|shard_map_name|**sysname**|Für den Typ SHARD_MAP_MANAGER, den Namen des der shardzuordnung. NULL für andere Arten von Daten aus externen Quellen.||  
  
## <a name="permissions"></a>Berechtigungen  
 Die Sichtbarkeit der Metadaten in Katalogsichten ist auf sicherungsfähige Elemente eingeschränkt, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
