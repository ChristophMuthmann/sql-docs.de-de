---
title: Sp_enum_sqlagent_subsystems (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 946c623004db5efaeb470b26b74daaba9f5271bb
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spenumsqlagentsubsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Subsysteme.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>Argumente  
 Keine  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**subsystem**|**nvarchar(40)**|Der Name des Subsystems.|  
|**description**|**nvarchar(512)**|Beschreibung des Subsystems.|  
|**subsystem_dll**|**nvarchar(510)**|DLL-Modul, das das Subsystem enthält.|  
|**agent_exe**|**nvarchar(510)**|Ausführbares Modul, das vom Subsystem verwendet wird.|  
|**start_entry_point**|**nvarchar(30)**|Prozedur, die der SQL Server-Agent während der Ausführung der Auftragsschritte aufruft.|  
|**event_entry_point**|**nvarchar(30)**|Prozedur, die der SQL Server-Agent während der Ausführung der Auftragsschritte aufruft.|  
|**stop_entry_point**|**nvarchar(30)**|Prozedur, die der SQL Server-Agent während der Ausführung der Auftragsschritte aufruft.|  
|**max_worker_threads**|**int**|Maximale Anzahl von Threads [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent für dieses Subsystem startet.|  
|**subsystem_id**|**int**|Bezeichner für das Subsystem.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Prozedur listet die in der Instanz verfügbaren Subsysteme auf.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen Datenbankrolle **SQLAgentOperatorRole** in der **msdb** -Datenbank sein.  
  
 Weitere Informationen zu **SQLAgentOperatorRole**, finden Sie unter [SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Sicherheit für SQL Server-Agent](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
