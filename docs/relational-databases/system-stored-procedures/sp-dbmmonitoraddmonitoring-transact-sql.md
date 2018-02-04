---
title: Sp_dbmmonitoraddmonitoring (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_dbmmonitoraddmonitoring
- sp_dbmmonitoraddmonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], monitoring
- sp_dbmmonitoraddmonitoring
ms.assetid: 9489dc30-af29-4363-a172-4645947fc95e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 937769b4af9676447311db51233000a26b0bbfe9
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spdbmmonitoraddmonitoring-transact-sql"></a>sp_dbmmonitoraddmonitoring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Auftrag für den Datenbankspiegelungs-Monitor, der in regelmäßigen Abständen den Spiegelungsstatus für jede gespiegelte Datenbank in der Serverinstanz aktualisiert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dbmmonitoraddmonitoring [ update_period ]  
```  
  
## <a name="arguments"></a>Argumente  
 *update_period*  
 Gibt das Intervall zwischen den Updates in Minuten an. Dieser Wert kann zwischen 1 und 120 Minuten liegen. Der Standardwert ist 1 Minute.  
  
> [!NOTE]  
>  Bei einem zu kurz festgelegten Updatezeitraum kann die Antwortzeit für Clients zunehmen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Diese Prozedur erfordert, dass die Ausführung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents in der Serverinstanz zugelassen wird. Damit der Auftrag für den Datenbankspiegelungs-Monitor ausgeführt wird, muss der Agent ausgeführt werden.  
  
 Wenn die datenbankspiegelung über gestartet wird [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], **Sp_dbmmonitoraddmonitoring** Prozedur wird automatisch ausgeführt. Wenn Sie die Spiegelung manuell mit ALTER DATABASE-Anweisungen starten, überwachen Sie gespiegelte Datenbank auf der Serverinstanz muss ausführen **Sp_dbmmonitoraddmonitoring** manuell.  
  
> [!NOTE]  
>  Wenn das Ausführen **Sp_dbmmonitoraddmonitoring** vor dem Einrichten der datenbankspiegelung, der überwachungsauftrag zwar ausgeführt, aber die in der Datenbank Monitor Verlauf des datenbankspiegelungs gespeichert ist-Statustabelle nicht aktualisiert werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel beginnt mit einem updatezeitraum von Überwachung `3` Minuten.  
  
```  
EXEC sp_dbmmonitoraddmonitoring 3;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
