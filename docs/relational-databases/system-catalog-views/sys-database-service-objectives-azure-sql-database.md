---
title: Sys.database_service_objectives (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 08/30/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Elastischen pool
- elastischen Pool, Verwaltung
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08c801fe0f7d917de2c520e788320ec3677d8a6e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>Sys.database_service_objectives (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Ggf. für eine Azure SQL-Datenbank oder einer Azure SQL Data Warehouse die Edition (Dienstebene), der dienstziel (Tarif) und der Name des elastischen Pools zurückgegeben werden soll. Wenn der master-Datenbank in einer Azure SQL-Datenbankserver angemeldet, gibt die Informationen für alle Datenbanken zurück. Für Azure SQL Data Warehouse müssen Sie mit der master-Datenbank verbunden sein.  
  
  
 Informationen zu den Preisen von finden Sie unter [SQL-Datenbank-Optionen und Leistungsstufen: SQL-Datenbank – Preise](https://azure.microsoft.com/en-us/pricing/details/sql-database/) und [SQL Data Warehouse – Preise](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Um die Einstellungen zu ändern, finden Sie unter [ALTER DATABASE (Azure SQL-Datenbank)](../../t-sql/statements/alter-database-azure-sql-database.md) und [ALTER DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
  
 Die sys.database_service_objectives-Ansicht enthält die folgenden Spalten.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|int|Die ID der Datenbank, eindeutig innerhalb einer Instanz von Azure SQL-Datenbankserver. Mit beigetreten [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|-Edition|sysname|Die Dienstebene für die Datenbank oder vorhandenem Data Warehouse: **grundlegende**, **Standard**, **Premium** oder **Data Warehouse**.|  
|service_objective|sysname|Der Tarif der Datenbank. Gibt zurück, wenn die Datenbank in einem elastischen Pool befindet, **ElasticPool**.<br /><br /> Auf der **grundlegende** -Ebene gibt **grundlegende**.<br /><br /> **Einzelne Datenbank in eine standard-Dienstebene** gibt einen der folgenden zurück: S0, S1, S2 oder S3.<br /><br /> **Einzelne Datenbank in einem Premium-Dienstebene** gibt Folgendes zurück: P1, P2, P4, P6/P3 oder P11.<br /><br /> **SQL Data Warehouse** DW100 über DW2000 zurückgibt.|  
|elastic_pool_name|sysname|Der Name des der [elastischen Pool](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) , die die Datenbank angehört. Gibt **NULL** , wenn die Datenbank eine einzelne Datenbank oder eine Warehoue Daten ist.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **DbManager** -Berechtigung für die master-Datenbank.  Auf Datenbankebene muss der Benutzer der Ersteller oder Besitzer sein.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel kann für die Masterdatenbank oder Benutzerdatenbanken ausgeführt werden. Die Abfrage gibt die Namen Service und Leistungsinformationen über die Ebene der Datenbank(en).  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
