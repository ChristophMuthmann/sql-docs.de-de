---
title: Erstellen von RESSOURCENPOOLS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE RESOURCE POOL
- RESOURCE POOL
- CREATE_RESOURCE_POOL_TSQL
- RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE RESOURCE POOL
ms.assetid: 82712505-c6f9-4a65-a469-f029b5a2d6cd
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c6f9a6ae8f0f869eb5ddd32c0189fcbaab198d3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-resource-pool-transact-sql"></a>CREATE RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Ressourcenpool für die Ressourcenkontrolle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ein Ressourcenpool stellt eine Teilmenge der physischen Ressourcen (Arbeitsspeicher, CPUs und E/A) einer Instanz des Datenbankmoduls dar. Mit der Ressourcenkontrolle kann ein Datenbankadministrator Serverressourcen auf Ressourcenpools verteilen, bis zu maximal 64 Pools. Die Ressourcenkontrolle ist nicht in jeder Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE RESOURCE POOL pool_name  
[ WITH  
    (  
        [ MIN_CPU_PERCENT = value ]  
        [ [ , ] MAX_CPU_PERCENT = value ]   
        [ [ , ] CAP_CPU_PERCENT = value ]   
        [ [ , ] AFFINITY {SCHEDULER =  
                  AUTO 
                | ( <scheduler_range_spec> )   
                | NUMANODE = ( <NUMA_node_range_spec> )
                } ]   
        [ [ , ] MIN_MEMORY_PERCENT = value ]  
        [ [ , ] MAX_MEMORY_PERCENT = value ]  
        [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
        [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
    )   
]  
[;]  
  
<scheduler_range_spec> ::=  
{ SCHED_ID | SCHED_ID TO SCHED_ID }[,…n]  
  
<NUMA_node_range_spec> ::=  
{ NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID }[,…n]  
```  
  
## <a name="arguments"></a>Argumente  
 *pool_name*  
 Der benutzerdefinierte Name für den Ressourcenpool. *Pool_name* ist alphanumerisch, kann bis zu 128 Zeichen sein, muss innerhalb einer Instanz eindeutig sein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und Sie müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 MIN_CPU_PERCENT =*Wert*  
 Gibt die garantierte durchschnittliche CPU-Bandbreite für alle Anforderungen im Ressourcenpool an, wenn CPU-Konflikte bestehen. *Wert* ist eine ganze Zahl mit einem Standardwert von 0. Der zulässige Bereich für *Wert* liegt zwischen 0 und 100.  
  
 MAX_CPU_PERCENT =*Wert*  
 Gibt die maximale durchschnittliche CPU-Bandbreite, die allen Anforderungen im Ressourcenpool zugewiesen wird, wenn CPU-Konflikte bestehen. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.  
  
 CAP_CPU_PERCENT =*Wert*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Legt eine feste Obergrenze für die CPU-Bandbreite fest, die für alle Anforderungen im Ressourcenpool gilt. Beschränkt die maximale CPU-Bandbreitenstufe auf den angegebenen Wert. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.  
  
 AFFINITÄT {SCHEDULER = AUTO | ( \<Scheduler_range_spec >) | NUMANODE = (\<NUMA_node_range_spec >)} **betrifft**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Fügt den Ressourcenpool an bestimmte Zeitplanungsmodule an. Der Standardwert ist AUTO.  
  
 AFFINITY SCHEDULER = **(** \<Scheduler_range_spec > **)** ordnet den Ressourcenpool der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Zeitpläne, die von den angegebenen IDs identifizierten. Diese IDs zugeordnet werden, um die Werte in der Scheduler_id-Spalte in [DM_OS_SCHEDULERS &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 
  
 Bei Verwendung von AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**, der Ressourcenpool zugeordnet ist, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Planer, die den physischen CPUs zugeordnet werden, um entsprechen, die angegebenen NUMA-Knoten oder-Knotenbereich. Sie können die Zuordnung zwischen der physischen NUMA-Konfiguration und den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Zeitplanungsmodul-IDs mithilfe der folgenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrage ermitteln. 
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc   
    ON osn.node_id = sc.parent_node_id   
    AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*Wert*  
 Gibt den Mindestarbeitsspeicher an, der für diesen Ressourcenpool reserviert ist und nicht gemeinsam mit anderen Ressourcenpools verwendet werden kann. *Wert* ist eine ganze Zahl mit einem Standardwert von 0 der zulässige Bereich für *Wert* liegt zwischen 0 und 100.  
  
 MAX_MEMORY_PERCENT =*Wert*  
 Gibt den gesamten Serverspeicher an, der für Anforderungen in diesem Ressourcenpool verwendet werden kann. *Wert* ist eine ganze Zahl mit einem Standardwert von 100. Der zulässige Bereich für *Wert* liegt zwischen 1 und 100.  
  
 MIN_IOPS_PER_VOLUME =*Wert*  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die minimalen E/A-Vorgänge pro Sekunde (IOPS) pro Datenträgervolume an, die für den Ressourcenpool reserviert werden sollen. Der zulässige Bereich für *Wert* liegt zwischen 0 bis 2 ^ 31-1 (2.147.483.647). 0 gibt an, dass kein minimaler Schwellenwert für den Pool gilt. Die Standardeinstellung ist 0.  
  
 MAX_IOPS_PER_VOLUME =*Wert*  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die maximalen E/A-Vorgänge pro Sekunde (IOPS) pro Datenträgervolume an, die für den Ressourcenpool zulässig sein sollen. Der zulässige Bereich für *Wert* liegt zwischen 0 bis 2 ^ 31-1 (2.147.483.647). 0 gibt einen unbegrenzten Schwellenwert für den Pool an. Die Standardeinstellung ist 0.  
  
 Wenn MAX_IOPS_PER_VOLUME für einen Pool auf den Wert 0 festgelegt ist, wird der Pool überhaupt nicht kontrolliert und kann alle IOPS im System annehmen, selbst wenn für andere Pools MIN_IOPS_PER_VOLUME festgelegt ist. Für diesen Fall wird empfohlen, dass Sie den MAX_IOPS_PER_VOLUME-Wert für diesen Pool auf eine höhere Zahl festlegen (z. B. auf den Maximalwert 2^31-1), wenn E/A-Vorgänge für diesen Pool kontrolliert werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 MIN_IOPS_PER_VOLUME und MAX_IOPS_PER_VOLUME geben das Minimum und das Maximum für Lese- und Schreibvorgänge pro Sekunde an. Die Lese- und Schreibvorgänge können eine beliebige Größe haben und geben daher keinen Aufschluss über den minimalen bzw. maximalen Durchsatz.  
  
 Die Werte für MAX_CPU_PERCENT und MAX_MEMORY_PERCENT müssen größer oder gleich den Werten für MIN_CPU_PERCENT bzw. MIN_MEMORY_PERCENT sein.  
  
 CAP_CPU_PERCENT unterscheidet sich insofern von MAX_CPU_PERCENT, als dem Pool zugeordnete Arbeitsauslastungen CPU-Kapazität über dem Wert von MAX_CPU_PERCENT verwenden können, sofern sie verfügbar ist, aber nicht über dem Wert von CAP_CPU_PERCENT.  
  
 Der gesamte CPU-Prozentsatz für jede zugeordnete Komponente (Zeitplanungsmodul(e) oder NUMA-Knoten) darf 100 % nicht überschreiten.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie ein Ressourcenpool mit der Bezeichnung `bigPool` erstellt wird. Dieser Pool verwendet die Standardeinstellungen der Ressourcenkontrolle.  
  
```  
CREATE RESOURCE POOL bigPool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 Im folgenden Beispiel werden `CAP_CPU_PERCENT` auf die feste Obergrenze 30 % und `AFFINITY SCHEDULER` auf einen Bereich von 0 bis 63, 128 bis 191 festgelegt. 
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
     MIN_CPU_PERCENT = 10,  
     MAX_CPU_PERCENT = 20,  
     CAP_CPU_PERCENT = 30,  
     AFFINITY SCHEDULER = (0 TO 63, 128 TO 191),  
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
      );  
  
```  
  
 Im folgenden Beispiel wird `MIN_IOPS_PER_VOLUME` auf \<einige Wert > und `MAX_IOPS_PER_VOLUME` auf \<einige Wert >. Diese Werte bestimmen die physischen E/A-Lese- und Schreibvorgänge, die für den Ressourcenpool verfügbar sind.  
  
**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
    MIN_IOPS_PER_VOLUME = 20,  
    MAX_IOPS_PER_VOLUME = 100  
      );  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Erstellen eines Ressourcenpools](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
  


