---
title: ALTER RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_RESOURCE_POOL_TSQL
- ALTER RESOURCE POOL
dev_langs: TSQL
helpviewer_keywords: ALTER RESOURCE POOL
ms.assetid: 9c1c4cfb-0e3b-4f01-bf57-3fce94c7d1d4
caps.latest.revision: "47"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4edf3d8f20cc3705a6303d55f471dfa74c250f74
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="alter-resource-pool-transact-sql"></a>ALTER RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert eine vorhandene Ressourcenpoolkonfiguration der Ressourcenkontrolle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER RESOURCE POOL { pool_name | "default" }  
[WITH  
    ( [ MIN_CPU_PERCENT = value ]  
    [ [ , ] MAX_CPU_PERCENT = value ]   
    [ [ , ] CAP_CPU_PERCENT = value ]   
    [ [ , ] AFFINITY {
                        SCHEDULER = AUTO 
                      | ( <scheduler_range_spec> ) 
                      | NUMANODE = ( <NUMA_node_range_spec> )
                      }]   
    [ [ , ] MIN_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]   
    [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
    [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
)]   
[;]  
  
<scheduler_range_spec> ::=  
{SCHED_ID | SCHED_ID TO SCHED_ID}[,…n]  
  
<NUMA_node_range_spec> ::=  
{NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID}[,…n]  
```  
  
## <a name="arguments"></a>Argumente  
 { *Pool_name* | **"Default"** }  
 Der Name eines vorhandenen benutzerdefinierten Ressourcenpools oder der Standardressourcenpool, der bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wird.  
  
 "default" muss bei Verwendung mit ALTER RESOURCE POOL in Anführungszeichen ("") oder Klammern ([]) eingeschlossen werden, um einen Konflikt mit DEFAULT zu vermeiden, das ein vom System reserviertes Wort darstellt. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Verwenden vordefinierte Arbeitsauslastungsgruppen und Ressourcenpools werden ausschließlich Kleinbuchstabe Namen, z. B. "Default". Dies sollte bei Servern beachtet werden, die bei der Sortierung zwischen Groß-/Kleinschreibung unterscheiden. Server, die bei der Sortierung keine Groß- und Kleinschreibung unterscheiden, z. B. SQL_Latin1_General_CP1_CI_AS, behandeln "default" und "Default" gleich.  
  
 MIN_CPU_PERCENT =*Wert*  
 Gibt die garantierte durchschnittliche CPU-Bandbreite für alle Anforderungen im Ressourcenpool an, wenn CPU-Konflikte bestehen. *Wert* ist eine ganze Zahl mit einem Standardwert von 0. Der zulässige Bereich für *Wert* liegt zwischen 0 und 100.  
  
 MAX_CPU_PERCENT =*Wert*  
 Gibt die maximale durchschnittliche CPU-Bandbreite an, die allen Anforderungen im Ressourcenpool zugewiesen wird, wenn CPU-Konflikte bestehen. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.  
  
 CAP_CPU_PERCENT =*Wert*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Ziel maximale CPU-Kapazität für Anforderungen im Ressourcenpool an. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.  
  
> [!NOTE]  
>  Aufgrund der statistischen Eigenschaften der CPU-Governance bemerken Sie möglicherweise gelegentliche Spitzen im CAP_CPU_PERCENT angegebenen Wert überschreitet.  
  
 AFFINITY {SCHEDULER = AUTO | (Scheduler_range_spec) | NUMANODE = (NUMA_node_range_spec)}  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Fügt den Ressourcenpool an bestimmte Zeitplanungsmodule an. Der Standardwert ist AUTO.  
  
 AFFINITY SCHEDULER = (Scheduler_range_spec) ordnet den Ressourcenpool den von den angegebenen IDs identifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeitplänen zu. Diese IDs zugeordnet werden, um die Werte in der Scheduler_id-Spalte in [DM_OS_SCHEDULERS &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).  
  
 Wenn Sie AFFINITY NAMANODE = (NUMA_node_range_spec) verwenden, wird der Ressourcenpool den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeitplanungsmodulen zugeordnet, die den physischen CPUs zugeordnet werden, die dem angegebenen NUMA-Knoten oder -Knotenbereich entsprechen. Sie können die Zuordnung zwischen der physischen NUMA-Konfiguration und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zeitplanungsmodul-IDs mithilfe der folgenden Transact-SQL-Abfrage ermitteln.  
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc 
   ON osn.node_id = sc.parent_node_id 
      AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*Wert*  
 Gibt den Mindestarbeitsspeicher an, der für diesen Ressourcenpool reserviert ist und nicht gemeinsam mit anderen Ressourcenpools verwendet werden kann. *Wert* ist eine ganze Zahl mit einem Standardwert von 0. Der zulässige Bereich für *Wert* liegt zwischen 0 und 100.  
  
 MAX_MEMORY_PERCENT =*Wert*  
 Gibt den gesamten Serverspeicher an, der für Anforderungen in diesem Ressourcenpool verwendet werden kann. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.  
  
 MIN_IOPS_PER_VOLUME =*Wert*  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die minimalen E/A-Vorgänge pro Sekunde (IOPS) pro Datenträgervolume an, die für den Ressourcenpool reserviert werden sollen. Der zulässige Bereich für *Wert* liegt zwischen 0 bis 2 ^ 31-1 (2.147.483.647). 0 gibt an, dass kein minimaler Schwellenwert für den Pool gilt.  
  
 MAX_IOPS_PER_VOLUME =*value*  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die maximalen E/A-Vorgänge pro Sekunde (IOPS) pro Datenträgervolume an, die für den Ressourcenpool zulässig sein sollen. Der zulässige Bereich für *Wert* liegt zwischen 0 bis 2 ^ 31-1 (2.147.483.647). 0 gibt einen unbegrenzten Schwellenwert für den Pool an. Die Standardeinstellung ist 0.  
  
 Wenn MAX_IOPS_PER_VOLUME für einen Pool auf den Wert 0 festgelegt ist, wird der Pool überhaupt nicht kontrolliert und kann alle IOPS im System annehmen, selbst wenn für andere Pools MIN_IOPS_PER_VOLUME festgelegt ist. Für diesen Fall wird empfohlen, dass Sie den MAX_IOPS_PER_VOLUME-Wert für diesen Pool auf eine höhere Zahl festlegen (z. B. auf den Maximalwert 2^31-1), wenn E/A-Vorgänge für diesen Pool kontrolliert werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 Die Werte für MAX_CPU_PERCENT und MAX_MEMORY_PERCENT müssen größer oder gleich den Werten für MIN_CPU_PERCENT und MIN_MEMORY_PERCENT sein.  
  
 MAX_CPU_PERCENT können CPU-Kapazität über den Wert MAX_CPU_PERCENT, sofern dieser verfügbar ist. Es kann jedoch auch periodische Spitzen oben CAP_CPU_PERCENT, sollte arbeitsauslastungen nicht CAP_CPU_PERCENT für längere Zeiträume, selbst wenn Sie zusätzlicher CPU-Kapazität verfügbar ist überschreiten.  
  
 Der gesamte CPU-Prozentsatz für jede zugeordnete Komponente (Zeitplanungsmodul(e) oder NUMA-Knoten) darf 100 % nicht überschreiten.  
  
 Sie sollten bei der Ausführung von DDL-Anweisungen mit dem Status der Ressourcenkontrolle vertraut sein. Weitere Informationen finden Sie unter [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 Wenn Sie eine Einstellung zur planauswirkung zu ändern, die neue Einstellung werden erst wirksam zuvor zwischengespeicherte Pläne nach dem Ausführen von DBCC FREEPROCCACHE (*Pool_name*), wobei *Pool_name* ist der Name einer Ressource Ressourcenpool der Ressourcenkontrolle.  
  
-   Wenn Sie AFFINITY aus mehreren Zeitplanungsmodulen auf einen einzelnen Planer ändern, ist das Ausführen von DBCC FREEPROCCACHE nicht erforderlich, da parallele Pläne im seriellen Modus ausgeführt werden können. Allerdings so effizient wie einen Plan als ein serieller Plan kompiliert möglicherweise nicht.  
  
-   Wenn Sie AFFINITY für mehrere Planer aus einem einzelnen Zeitplan ändern, ist das Ausführen von DBCC FREEPROCCACHE nicht erforderlich. Serielle Pläne jedoch kann nicht parallel ausgeführt werden, damit das Löschen des Zwischenspeichers jeweiligen auf neue Pläne aus, um potenziell die Möglichkeit wird mit der Parallelität kompiliert werden.  
  
> [!CAUTION]  
>  Löschen zwischengespeicherter Pläne aus einem Ressourcenpool, die mehr als eine Arbeitsauslastungsgruppe zugeordnet ist wirkt sich auf alle Arbeitsauslastungsgruppen mit dem benutzerdefinierten Ressourcenpool identifizierten *Pool_name*.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle standardmäßigen Ressourcenpooleinstellungen für den `default`-Pool beibehalten, außer für `MAX_CPU_PERCENT`, die in `25` geändert wird.  
  
```  
ALTER RESOURCE POOL "default"  
WITH  
     ( MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 Im folgenden Beispiel legt `CAP_CPU_PERCENT` die feste Obergrenze auf 80 % fest, und `AFFINITY SCHEDULER` wird auf den individuellen Wert 8 sowie einen Bereich von 12 bis 16 festgelegt.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ALTER RESOURCE POOL Pool25  
WITH(   
     MIN_CPU_PERCENT = 5,  
     MAX_CPU_PERCENT = 10,       
     CAP_CPU_PERCENT = 80,  
     AFFINITY SCHEDULER = (8, 12 TO 16),   
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
);  
  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
