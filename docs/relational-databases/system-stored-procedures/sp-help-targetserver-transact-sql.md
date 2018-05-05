---
title: Sp_help_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3b4b9951e431b715debb12d59139bd6378a5d13
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelptargetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet alle Zielserver auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@server_name=** ] **"***Server_name***"**  
 Der Name des Servers, für den Informationen zurückgegeben werden. *Server_name* ist **nvarchar(30)**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Wenn *Server_name* nicht angegeben ist, **Sp_help_targetserver** gibt dieses Resultset zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Server-ID.|  
|**server_name**|**nvarchar(30)**|Servername.|  
|**location**|**nvarchar(200)**|Standort des angegebenen Servers.|  
|**time_zone_adjustment**|**int**|Zeitzonenanpassung ausgehend von der GMT (Greenwich Mean Time) in Stunden.|  
|**enlist_date**|**datetime**|Datum der Eintragung des angegebenen Servers.|  
|**last_poll_date**|**datetime**|Datum, an dem der Server zuletzt nach Aufträgen abgefragt wurde.|  
|**status**|**int**|Status des angegebenen Servers.|  
|**unread_instructions**|**int**|Gibt an, ob auf dem Server ungelesene Anweisungen vorhanden sind. Wenn alle Zeilen heruntergeladen wurden, ist diese Spalte **0**.|  
|**local_time**|**datetime**|Lokales Datum und lokale Uhrzeit auf dem Zielserver. Diese basieren auf der lokalen Zeit des Zielservers zum Zeitpunkt des letzten Abrufs des Masterservers.|  
|**enlisted_by_nt_user**|**Nvarchar(100)**|Microsoft Windows-Benutzer, der den Zielserver eingetragen hat.|  
|**poll_interval**|**int**|Häufigkeit in Sekunden, mit der der Zielserver den Master-SQLServerAgent-Dienst abruft, um Aufträge herunterzuladen und den Auftragsstatus hochzuladen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen dieser gespeicherten Prozedur muss ein Benutzer Mitglied der festen Serverrolle **sysadmin** sein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. Auflisten von Informationen für alle registrierten Zielserver  
 Das folgende Beispiel listet Informationen für alle registrierten Zielserver auf.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. Auflisten von Informationen für einen bestimmten Zielserver  
 Das folgende Beispiel listet Informationen für den Zielserver `SEATTLE2` auf.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_delete_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [dbo.sysdownloadlist &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
