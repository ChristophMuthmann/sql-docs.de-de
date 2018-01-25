---
title: DBCC FREESYSTEMCACHE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs: TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
caps.latest.revision: "35"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d5c6924da3ef9ac85683c857c786337b9d9b978b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Gibt alle nicht verwendeten Cacheeinträge aus allen Caches frei. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] löscht nicht verwendete Cacheeinträge aktiv im Hintergrund und macht so neuen Speicherplatz für aktuelle Einträge verfügbar. Sie können mit diesem Befehl jedoch nicht verwendete Einträge aus allen Caches oder aus einem angegebenen Cache für den Ressourcenkontrollenpool löschen.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
```sql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>Argumente  
 ('ALL' [,*Pool_name* ])  
 ALL gibt alle unterstützten Caches an.  
 *Pool_name* gibt einen Cache für die Ressourcenkontrolle. Nur diesem Pool zugeordnete Einträge werden freigegeben.  
  
 MARK_IN_USE_FOR_REMOVAL  
 Gibt zurzeit verwendete Einträge asynchron aus den jeweiligen Caches nach ihrer Verwendung frei. Neue Einträge, die nach der Ausführung von DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL im Cache erstellt wurden, sind nicht betroffen.  
  
 NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Hinweise  
Durch das Ausführen von DBCC FREESYSTEMCACHE wird der Plancache für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht. Durch das Löschen des Plancaches wird eine Neukompilierung aller nachfolgenden Ausführungspläne verursacht, und möglicherweise entsteht plötzlich eine temporäre Verringerung der Abfrageleistung. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll enthält für jeden geleerten Cachespeicher im Plancache folgende Meldung zur Information: "Von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wurden für den '%s'-Cachespeicher (Bestandteil des Plancaches) %d Leerungen des Cachespeichers gefunden, die von 'DBCC FREEPROCCACHE'- oder 'DBCC FREESYSTEMCACHE'-Vorgängen ausgelöst wurden". Diese Meldung wird alle fünf Minuten protokolliert, solange der Cache innerhalb dieses Zeitintervalls geleert wird.

## <a name="result-sets"></a>Resultsets  
DBCC FREESYSTEMCACHE gibt Folgendes zurück: "DBCC-Ausführung wurde abgeschlossen. Falls DBCC Fehlermeldungen ausgegeben hat, wenden Sie sich an den Systemadministrator."
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die ALTER SERVER STATE-Berechtigung auf dem Server.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. Freigeben nicht verwendeter Cacheeinträge aus einem Cache für den Ressourcenkontrollenpool  
Im folgenden Beispiel wird veranschaulicht, wie Caches geleert werden, die einem angegebenen Ressourcenpool für die Ressourcenkontrolle zugeordnet sind.
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. Freigeben von Einträgen aus den jeweiligen Caches nach ihrer Verwendung  
Im folgenden Beispiel wird die MARK_IN_USE_FOR_REMOVAL-Klausel dazu verwendet, alle Einträge von allen aktuellen Caches nach ihrer Verwendung freizugeben.
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)
  
  
