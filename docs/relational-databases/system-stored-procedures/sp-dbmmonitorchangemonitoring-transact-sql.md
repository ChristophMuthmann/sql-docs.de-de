---
title: Sp_dbmmonitorchangemonitoring (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorchangemonitoring
- sp_dbmmonitorchangemonitoring_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_dbmmonitorchangemonitoring
- database mirroring [SQL Server], monitoring
ms.assetid: 17be755b-673d-4cd4-9544-6ecb4220bed3
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c640f9306d8fe4a484d453bd3846da2e58a25e62
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spdbmmonitorchangemonitoring-transact-sql"></a>sp_dbmmonitorchangemonitoring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert den Wert eines Parameters für die Datenbank-Spiegelungsüberwachung.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dbmmonitorchangemonitoring parameter  
    , value   
```  
  
## <a name="arguments"></a>Argumente  
 *Parameter*  
 Gibt die ID des zu ändernden Parameters an. Aktuell ist nur der folgende Parameter verfügbar:  
  
 1 = Updatezeitraum  
  
 Die Anzahl von Minuten zwischen den Updates der Datenbankspiegelungs-Statustabelle. Das Standardintervall beträgt 1 Minute.  
  
 *value*  
 Gibt den neuen Wert für den zu ändernden Parameter an.  
  
|Parameter|Beschreibung des Wertes|  
|---------------|--------------------------|  
|1|Ganze Zahl zwischen 1 und 120, die einen neuen Updatezeitraum in Minuten angibt.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Updatezeitraum auf 5 Minuten geändert.  
  
```  
EXEC sp_dbmmonitorchangemonitoring 1, 5 ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Sp_dbmmonitoraddmonitoring &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [Sp_dbmmonitordropmonitoring &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [Sp_dbmmonitorhelpmonitoring &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
