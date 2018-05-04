---
title: Sp_help_agent_profile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_help_agent_profile
- sp_help_agent_profile_TSQL
helpviewer_keywords:
- sp_help_agent_profile
ms.assetid: 5637b671-4aa3-497e-9a1c-c99798a1afb4
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: eaf5be20a468efc83e2a18b5c5ad18f12fdeb3ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpagentprofile-transact-sql"></a>sp_help_agent_profile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt das Profil eines bestimmten Agents an. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_agent_profile [ [ @agent_type = ] agent_type ]   
    [ , [ @profile_id = ] profile_id ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@agent_type=**] *agent_type-Wert*  
 Der Typ des Agents. *Agent_type* ist **Int**, hat den Standardwert **0**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Momentaufnahme-Agent|  
|**2**|Protokolllese-Agent|  
|**3**|Verteilungs-Agent|  
|**4**|Merge-Agent|  
|**9**|Warteschlangenlese-Agent|  
  
 [  **@profile_id=**] *Profile_id*  
 Die ID des Profils, das angezeigt werden soll. *Profile_id* ist **Int**, hat den Standardwert **-1**, womit alle Profile in der **MSagent_profiles** Tabelle.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|ID des Profils.|  
|**profile_name**|**sysname**|Eindeutig für den Agenttyp.|  
|**agent_type**|**int**|**1** = Momentaufnahme-Agent<br /><br /> **2** = Protokolllese-Agent<br /><br /> **3** = Verteilungs-Agent<br /><br /> **4** = Merge-Agent<br /><br /> **9** = Warteschlangenlese-Agent|  
|**Typ**|**int**|**0** = System<br /><br /> **1** = Benutzerdefiniert|  
|**description**|**varchar(3000)**|Beschreibung des Profils.|  
|**def_profile**|**bit**|Gibt an, ob dieses Profil das Standardprofil für diesen Agenttyp ist.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_agent_profile** wird für alle Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Replmonitor** feste Datenbankrolle können ausführen **Sp_help_agent_profile**.  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit Replikations-Agent-Profilen](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [Sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [Sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)  
  
  
