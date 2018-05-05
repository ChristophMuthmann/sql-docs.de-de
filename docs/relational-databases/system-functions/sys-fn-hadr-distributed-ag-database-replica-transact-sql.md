---
title: Sys.fn_hadr_distributed_ag_database_replica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_database_replica
- sys.fn_hadr_distributed_ag_database_replica_TSQL
- fn_hadr_distributed_ag_database_replica
- fn_hadr_distributed_ag_database_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_database_replica
ms.assetid: 0e6202a1-e872-4f53-99d7-c16b6f712efc
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3166e1c46db60d2a5d7b97753c6fc5ce0ae5cc2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnhadrdistributedagdatabasereplica-transact-sql"></a>Sys.fn_hadr_distributed_ag_database_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Verwendet, um die Datenbank in der lokalen verfügbarkeitsgruppe eine Datenbank in einer verteilten verfügbarkeitsgruppe zuordnen.  
   
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_hadr_distributed_ag_database_replica( lag_Id, database_id )  
```  
  
## <a name="arguments"></a>Argumente  
 "*Lag_Id*"  
 Ist der Bezeichner der verteilten verfügbarkeitsgruppe. *Lag_Id* Typ **"uniqueidentifier"**.  
  
 "*Database_id*"  
 Ist der Bezeichner der Datenbank in einer verteilten verfügbarkeitsgruppe. *Database_id* Typ **"uniqueidentifier"**.  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
 Gibt die folgenden Informationen zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**group_database_id**|**uniqueidentifier**|Die ID der Datenbank, in der lokalen verfügbarkeitsgruppe.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="using-sysfnhadrdistributedagdatabasereplica"></a>Verwenden von sys.fn_hadr_distributed_ag_database_replica  
 Das folgende Beispiel übergibt in der Datenbank-ID in einer verteilten verfügbarkeitsgruppe. Es gibt eine Tabelle mit der Datenbank-ID, die die lokale verfügbarkeitsgruppe zugeordnet.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @databaseId uniqueidentifier = '3FFA882A-C4C3-5B9E-A203-8F44BD9659F7'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_database_replica(@lagId, @databaseId)  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen Always On-Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Verteilte Verfügbarkeitsgruppen &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40; Transact-SQL &#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
