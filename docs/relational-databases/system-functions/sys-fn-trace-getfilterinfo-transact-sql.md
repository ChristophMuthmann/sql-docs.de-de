---
title: Sys. fn_trace_getfilterinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_trace_getfilterinfo
- fn_trace_getfilterinfo_TSQL
dev_langs: TSQL
helpviewer_keywords:
- status information [SQL Server], filters
- sys.fn_trace_getfilterinfo function
- filters [SQL Server], traces
- fn_trace_getfilterinfo function
ms.assetid: 09fe4a28-ff8a-4655-9da1-4654d5bc514d
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c9792a3a4d3e6bb0d0c9732eab89388614a5af84
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfntracegetfilterinfo-transact-sql"></a>sys.fn_trace_getfilterinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über die auf eine angegebene Ablaufverfolgung angewendeten Filter zurück.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen erweiterte Ereignisse.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn_trace_getfilterinfo ( trace_id )  
```  
  
## <a name="arguments"></a>Argumente  
 *trace_id*  
 Die ID der Ablaufverfolgung. *Trace_id* ist **Int**, hat keinen Standardwert.  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
 Gibt die folgenden Informationen zurück. Weitere Informationen zu den Spalten finden Sie unter [Sp_trace_setfilter &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**columnid**|**int**|Die ID der Spalte, auf die der Filter angewendet wird|  
|**logical_operator**|**int**|Gibt an, ob der Operator AND oder OR angewendet wird|  
|**comparison_operator**|**int**|Gibt die Art des Vergleichs an:<br /><br /> 0 = Gleich<br /><br /> 1 = Ungleich<br /><br /> 2 = Größer als<br /><br /> 3 = Kleiner als<br /><br /> 4 = Größer als oder gleich<br /><br /> 5 = Kleiner als oder gleich<br /><br /> 6 = Wie<br /><br /> 7 = Nicht wie|  
|**Wert**|**sql_variant**|Gibt den Wert an, auf den der Filter angewendet wird|  
  
## <a name="remarks"></a>Hinweise  
 Der Benutzer legt *Trace_id* Wert zum Identifizieren, ändern und Steuern der Ablaufverfolgung. Wenn die ID einer bestimmten Ablaufverfolgung übergeben **Fn_trace_getfilterinfo** gibt Informationen zu allen Filtern dieser Ablaufverfolgung zurück. Wenn die angegebene Ablaufverfolgung keinen Filter aufweist, gibt diese Funktion ein leeres Rowset zurück. Wird eine ungültige ID übergeben, gibt die Funktion ein leeres Rowset zurück. Ähnliche Informationen zu ablaufverfolgungen finden Sie unter [Sys. fn_trace_getinfo &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER TRACE-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt Informationen zu allen Filtern der Ablaufverfolgung Nummer 2 zurück.  
  
```  
SELECT * FROM fn_trace_getfilterinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 ["sp_trace_generateevent" &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Sys. fn_trace_geteventinfo &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [Sys. fn_trace_gettable &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
