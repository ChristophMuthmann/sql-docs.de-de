---
title: Sys. data_spaces (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- data_spaces
- sys.data_spaces_TSQL
- sys.data_spaces
- data_spaces_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.data_spaces catalog view
ms.assetid: f39d55fe-2c0f-472d-a77f-cebc6fea95b5
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f17714f7c16d120891873692769d0d2f764c2626
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysdataspaces-transact-sql"></a>sys.data_spaces (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jeden Datenspeicherplatz. Dies kann eine Dateigruppe, ein Partitionsschema oder eine FILESTREAM-Datendateigruppe sein.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Name des Datenspeicherplatzes, eindeutig innerhalb der Datenbank.|  
|data_space_id|**int**|ID-Nummer des Datenspeicherplatzes, eindeutig innerhalb der Datenbank.|  
|Typ|**char(2)**|Typ des Datenspeicherplatzes:<br /><br /> FG = Dateigruppe (Filegroup)<br /><br /> FD = FILESTREAM-Datendateigruppe<br /><br /> FX = speicheroptimierte Tabellendateigruppe<br /><br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> PS = Partitionsschema (Partition scheme)|  
|type_desc|**nvarchar(60)**|Beschreibung des Datenspeicherplatztyps:<br /><br /> FILESTREAM_DATA_FILEGROUP<br /><br /> MEMORY_OPTIMIZED_DATA_FILEGROUP<br /><br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> PARTITION_SCHEME<br /><br /> ROWS_FILEGROUP|  
|is_default|**bit**|1 = Dies ist der Standard-Datenspeicherplatz. Dieser Standard-Datenspeicherplatz wird verwendet, wenn in einer CREATE TABLE- oder CREATE INDEX-Anweisung keine Dateigruppe und kein Partitionsschema angegeben ist.<br /><br /> 0 = Dies ist nicht der Standard-Datenspeicherplatz.|  
|is_system|**bit**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Der Datenbereich wird für Volltextindexfragmente verwendet.<br /><br /> 0 = Der Datenbereich wird nicht für Volltextindexfragmente verwendet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datenspeicher &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Sys. destination_data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sys. partition_schemes &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
