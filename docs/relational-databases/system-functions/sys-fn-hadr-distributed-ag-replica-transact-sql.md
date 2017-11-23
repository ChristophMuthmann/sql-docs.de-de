---
title: Sys.fn_hadr_distributed_ag_replica (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_replica
- sys.fn_hadr_distributed_ag_replica_TSQL
- fn_hadr_distributed_ag_replica
- fn_hadr_distributed_ag_replica_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.fn_hadr_distributed_ag_replica
ms.assetid: a1e5f9cb-c350-4bb4-a04f-7394f6f25d62
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fe90c7a863b70dc2d40994a333e80d620640d1f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnhadrdistributedagreplica-transact-sql"></a>Sys.fn_hadr_distributed_ag_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Verwendet, um die lokale verfügbarkeitsgruppe ein Replikat in einer verteilten verfügbarkeitsgruppe zuzuordnen.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_hadr_distributed_ag_replica( lag_Id, replica_id )  
```  
  
## <a name="arguments"></a>Argumente  
 "*Lag_Id*"  
 Ist der Bezeichner der verteilten verfügbarkeitsgruppe. *Lag_Id* Typ **"uniqueidentifier"**.  
  
 "*Replica_id*"  
 Ist der Bezeichner eines Replikats in der verteilten verfügbarkeitsgruppe. *Replica_id* Typ **"uniqueidentifier"**.  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
 Gibt die folgenden Informationen zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Eindeutige Bezeichner (GUID) der lokalen verfügbarkeitsgruppe.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="using-sysfnhadrdistributedagreplica"></a>Verwenden von sys.fn_hadr_distributed_ag_replica  
 Das folgende Beispiel gibt eine Tabelle mit der lokalen Verfügbarkeit Gruppen-ID, die dem angegebenen verteilte verfügbarkeitsgruppe und dem Replikat zugeordnet ist.  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @replicaId uniqueidentifier = 'D5517513-04A8-FD82-14C6-E684EC913935'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_replica(@lagId, @replicaId)  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [AlwaysOn-Verfügbarkeitsgruppen Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [AlwaysOn-Verfügbarkeitsgruppen &#40; SQLServer &#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Verteilte Verfügbarkeitsgruppen &#40; AlwaysOn-Verfügbarkeitsgruppen &#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
