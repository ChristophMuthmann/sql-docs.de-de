---
title: Sp_trace_setstatus (Transact-SQL) | Microsoft Docs
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
- sp_trace_setstatus_TSQL
- sp_trace_setstatus
dev_langs: TSQL
helpviewer_keywords: sp_trace_setstatus
ms.assetid: 29e7a7d7-b9c1-414a-968a-fc247769750d
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 186fd533d0f35a39ebf8b6f46a14987509bbdff5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sptracesetstatus-transact-sql"></a>sp_trace_setstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert den aktuellen Status der angegebenen Ablaufverfolgung.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen erweiterte Ereignisse.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_trace_setstatus [ @traceid = ] trace_id , [ @status = ] status  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@traceid=** ] *Trace_id*  
 Die ID der zu ändernden Ablaufverfolgung. *Trace_id* ist **Int**, hat keinen Standardwert. Der Benutzer verwendet diesen *Trace_id* Wert zum Identifizieren, ändern und Steuern der Ablaufverfolgung. Informationen zum Abrufen von der *Trace_id*, finden Sie unter [Sys. fn_trace_getinfo &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
 [  **@status=** ] *Status*  
 Gibt die Aktion an, die für die Ablaufverfolgung implementiert werden soll. *Status* ist **Int**, hat keinen Standardwert.  
  
 In der folgenden Tabelle sind die Status aufgelistet, die möglicherweise angegeben werden.  
  
|Status|Description|  
|------------|-----------------|  
|**0**|Beendet die angegebene Ablaufverfolgung.|  
|**1**|Startet die angegebene Ablaufverfolgung.|  
|**2**|Schließt die angegebene Ablaufverfolgung und löscht ihre Definition vom Server.|  
  
> [!NOTE]  
>  Eine Ablaufverfolgung muss beendet werden, bevor sie geschlossen werden kann. Eine Ablaufverfolgung muss beendet und geschlossen werden, bevor sie angezeigt werden kann.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 In der folgenden Tabelle werden die Codewerte beschrieben, die die Benutzer nach Abschluss der gespeicherten Prozedur möglicherweise erhalten.  
  
|Rückgabecode|Description|  
|-----------------|-----------------|  
|**0**|Kein Fehler.|  
|**1**|Unbekannter Fehler.|  
|**8**|Der angegebene Status ist ungültig.|  
|**9**|Das angegebene Ablaufverfolgungshandle ist ungültig.|  
|**13**|Nicht genügend Arbeitsspeicher. Wird zurückgegeben, wenn nicht genügend Arbeitsspeicher zum Ausführen der angegebenen Aktion verfügbar ist.|  
  
 Wenn die Ablaufverfolgung bereits im Status "" angegeben wird, ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück **0**.  
  
## <a name="remarks"></a>Hinweise  
 Parameter aller gespeicherten Prozeduren der SQL-Ablaufverfolgung (**sp_trace_xx**) haben eine strikte Typbindung. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
 Ein Beispiel zum Verwenden gespeicherter Prozeduren der Ablaufverfolgung finden Sie unter [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer müssen über die ALTER TRACE-Berechtigung verfügen.  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. fn_trace_geteventinfo &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 ["sp_trace_generateevent" &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md)  
  
  
