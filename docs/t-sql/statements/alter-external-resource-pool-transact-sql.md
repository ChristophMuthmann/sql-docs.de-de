---
title: ALTER EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
caps.latest.revision: 
author: jeannt
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb4073a8114e953dc9df87614a63e074ab8c9683
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-external-resource-pool-transact-sql"></a>ALTER EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Gilt für:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] und [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Ändert eine externe ressourcenkontrollenpool, die Ressourcen angibt, die von externen Prozessen verwendet werden kann. 

+ Für [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] in [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], bestimmt der externe Pool `rterm.exe`, `BxlServer.exe`, und anderen Prozessen, die von ihnen erzeugt.

+ Für [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] in SQL Server-2017, bestimmt der externe Pool die R-Prozesse, die für die vorherige Version aufgeführt sowie `python.exe`, `BxlServer.exe`, und anderen Prozessen, die von ihnen erzeugt.

 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Syntax

```sql
ALTER EXTERNAL RESOURCE POOL { pool_name | "default" }
[ WITH (
    [ MAX_CPU_PERCENT = value ]
    [ [ , ] AFFINITY CPU =
            {
                AUTO
              | ( <cpu_range_spec> )
              | NUMANODE = (( <NUMA_node_id> )
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

{ *Pool_name* | "Default"}  
Der Name eines vorhandenen benutzerdefinierten externen Ressourcenpools oder der standardressourcenpool für externe, die erstellt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist.
"Default" muss in Anführungszeichen eingeschlossen werden ("") oder Klammern ([]) bei Verwendung mit `ALTER EXTERNAL RESOURCE POOL` auf Konflikte mit vermeiden `DEFAULT`, also von einem System reservierten Wort.


MAX_CPU_PERCENT =*Wert*  
Gibt die maximale durchschnittliche CPU-Bandbreite, die alle Anforderungen in den externen Ressourcenpool empfangen kann, wenn CPU-Konflikte bestehen. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.


AFFINITÄT {CPU = AUTO | ( \<CPU_range_spec >) | NUMANODE = (\<NUMA_node_range_spec >)}  
Fügen Sie des externe Ressourcenpools an bestimmte CPUs. Der Standardwert ist AUTO.

CPU-AFFINITÄT = **(** \<CPU_range_spec > **)** ordnet den externen Ressourcenpool zu den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPUs, die durch den angegebenen CPU_IDs identifiziert. Bei Verwendung von AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**, der externe Ressourcenpool zugeordnet ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] physischen CPUs, die dem angegebenen NUMA entsprechen Knoten oder-Knotenbereich.


MAX_MEMORY_PERCENT =*Wert*  
Gibt den gesamten Serverspeicher an, der Anforderungen in diesem externen Ressourcenpool verwendet werden kann. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.


MAX_PROCESSES =*Wert*  
Gibt die maximale Anzahl von Prozessen, die für den externen Ressourcenpool zulässig. Geben Sie 0, um einen unbegrenzten Schwellenwert für den Pool festzulegen, das nur von Computerressourcen danach gebunden ist. Die Standardeinstellung ist 0.

## <a name="remarks"></a>Hinweise

Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementiert den Ressourcenpool, beim Ausführen der [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) Anweisung.

Allgemeine Informationen zu Ressourcenpools finden Sie unter [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [Sys. resource_governor_external_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), und [Sys. dm_resource_governor_external_resource_pool_affinity &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  

Informationen speziell für die Verwendung der externen Ressourcenpools, um zu steuern, Machine Learning-Aufträgen finden Sie unter [Ressourcenkontrolle für Machine Learning in SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)...
## <a name="permissions"></a>Berechtigungen

Erfordert `CONTROL SERVER` Berechtigung.

## <a name="examples"></a>Beispiele

Die folgende Anweisung ändert einen externen Pool, beschränken die CPU-Auslastung auf 50 Prozent und der maximale Arbeitsspeicher auf 25 Prozent des verfügbaren Arbeitsspeichers auf dem Computer.
  
```sql
ALTER EXTERNAL RESOURCE POOL ep_1
WITH (
    MAX_CPU_PERCENT = 50
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 25
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>Siehe auch

[Die Ressourcenkontrolle für Machine Learning in SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)

[Externe Skripts aktiviert (Serverkonfigurationsoption)](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

[DROP EXTERNAL RESOURCE POOL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)

[ALTER RESOURCE POOL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)

[Erstellen Sie WORKLOAD GROUP &#40; Transact-SQL &#41;](../../t-sql/statements/create-workload-group-transact-sql.md)

[Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

[ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
