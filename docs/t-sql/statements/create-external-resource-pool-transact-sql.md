---
title: Erstellen EXTERNEN RESSOURCENPOOLS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32c33076f26332f2a8510c4660696106bef824b5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-resource-pool-transact-sql"></a>Erstellen Sie EXTERNEN RESSOURCENPOOLS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Erstellt einen externen Pool verwendet, um Ressourcen für externe Prozesse definieren. Für R Services bestimmt, der externe Pool `rterm.exe`, `BxlServer.exe`, und anderen Prozessen, die von ihnen erzeugt. Ein Ressourcenpool stellt eine Teilmenge der physischen Ressourcen (Arbeitsspeicher und CPUs) einer Instanz des Datenbankmoduls dar. Mit der Ressourcenkontrolle kann ein Datenbankadministrator Serverressourcen auf Ressourcenpools verteilen, bis zu maximal 64 Pools.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = ( <NUMA_node_id> )   
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
  
## <a name="arguments"></a>Argumente  
 *pool_name*  
 Ist der benutzerdefinierte Name für den externen Ressourcenpool. *Pool_name* ist alphanumerisch, kann bis zu 128 Zeichen sein, muss innerhalb einer Instanz eindeutig sein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und Sie müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 MAX_CPU_PERCENT =*Wert*  
 Gibt die maximale durchschnittliche CPU-Bandbreite, die allen Anforderungen in den externen Ressourcenpool zugewiesen wird, wenn CPU-Konflikte bestehen. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.  
  
 AFFINITÄT {CPU = AUTO | ( \<CPU_range_spec >) | NUMANODE = (\<NUMA_node_range_spec >)} den externe Ressourcenpool an bestimmte CPUs anfügen. Der Standardwert ist AUTO.  
  
 CPU-AFFINITÄT = **(** \<CPU_range_spec > **)** ordnet den externen Ressourcenpool zu den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPUs, die durch den angegebenen CPU_IDs identifiziert. 
  
 Bei Verwendung von AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**, der externe Ressourcenpool zugeordnet ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] physischen CPUs, die dem angegebenen NUMA entsprechen Knoten oder-Knotenbereich. 
  
 MAX_MEMORY_PERCENT =*Wert*  
 Gibt den gesamten Serverspeicher an, der Anforderungen in diesem externen Ressourcenpool verwendet werden kann. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.  
  
 MAX_PROCESSES =*Wert*  
 Gibt die maximale Anzahl von Prozessen, die für den externen Ressourcenpool zulässig. Geben Sie 0 an, um einen unbegrenzten Schwellenwert festgelegt, für den Pool gebunden werden nur Computerressourcen sein. Die Standardeinstellung ist 0.  
  
## <a name="remarks"></a>Hinweise  
 Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] Ressourcenpool implementiert, beim Ausführen der [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) Anweisung.  
  
 Weitere Informationen zu Ressourcenpools, finden Sie unter [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [Sys. resource_governor_external_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), und [Sys. dm_resource_governor_external_resource_pool_affinity &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert `CONTROL SERVER` Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Anweisung definiert einen externen Pool, der CPU-Auslastung auf 75 Prozent und der maximale Arbeitsspeicher auf 30 Prozent des verfügbaren Arbeitsspeichers auf dem Computer beschränkt.  
  
```  
CREATE EXTERNAL RESOURCE POOL ep_1  
WITH (  
    MAX_CPU_PERCENT = 75  
    , AFFINITY CPU = AUTO  
    , MAX_MEMORY_PERCENT = 30  
);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [externe Skripts aktiviert – Serverkonfigurationsoption](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Bekannte Probleme bei SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [Sys. dm_resource_governor_external_resource_pool_affinity &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  


