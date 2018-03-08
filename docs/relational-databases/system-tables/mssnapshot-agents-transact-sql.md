---
title: MSsnapshot_agents (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSsnapshot_agents
- MSsnapshot_agents_TSQL
dev_langs: TSQL
helpviewer_keywords: MSsnapshot_agents system table
ms.assetid: aeae0a2e-4c21-4c45-be65-1e426fa52bdd
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 057db5ff4dbb7e9a9cfcfd5f36ae391f51160544
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssnapshotagents-transact-sql"></a>MSsnapshot_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSsnapshot_agents** -Tabelle enthält eine Zeile für jede Momentaufnahme-Agent mit dem lokalen Verteiler zugeordneten. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Die ID des Momentaufnahme-Agents.|  
|**name**|**nvarchar(100)**|Der Name des Momentaufnahme-Agents|  
|**publisher_id**|**smallint**|Die ID des Verlegers|  
|**publisher_db**|**sysname**|Der Name der Verlegerdatenbank.|  
|**Veröffentlichung**|**sysname**|Der Name der Veröffentlichung.|  
|**publication_type**|**int**|Der Typ der Veröffentlichung:<br /><br /> **0** = transaktionsveröffentlichung.<br /><br /> **1** = Snapshot.<br /><br /> **2** = befindet.|  
|**local_job**|**bit**|Gibt an, ob sich ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Auftrag auf dem lokalen Verteiler befindet.|  
|**job_id**|**Binary(16)**|Die Auftrags-ID|  
|**profile_id**|**int**|Der Konfigurations-ID aus der [MSagent_profiles &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) Tabelle.|  
|**dynamic_filter_login**|**sysname**|Der Wert für die Bewertung der [SUSER_SNAME &#40; Transact-SQL &#41; ](../../t-sql/functions/suser-sname-transact-sql.md) -Funktion in parametrisierten Filtern, die eine Partition zu definieren. Diese Spalte wird für eine partitionierte Momentaufnahme verwendet.|  
|**den Wert**|**sysname**|Der Wert für die Bewertung der [HOST_NAME &#40; Transact-SQL &#41; ](../../t-sql/functions/host-name-transact-sql.md) -Funktion in parametrisierten Filtern, die eine Partition zu definieren. Diese Spalte wird für eine partitionierte Momentaufnahme verwendet.|  
|**publisher_security_mode**|**smallint**|Der Sicherheitsmodus, der vom Agent beim Herstellen einer Verbindung mit dem Verleger verwendet wird. Dies kann einer der folgenden Modi sein:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Authentifizierung.|  
|**publisher_login**|**sysname**|Der Anmeldename, der beim Herstellen einer Verbindung mit dem Verleger verwendet wird|  
|**publisher_password**|**nvarchar(524)**|Der verschlüsselte Wert des Kennworts, das verwendet wird, um eine Verbindung mit dem Verleger herzustellen.|  
|**job_step_uid**|**uniqueidentifier**|Die eindeutige ID des Auftragsschritts des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents, in dem der Agent gestartet wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
