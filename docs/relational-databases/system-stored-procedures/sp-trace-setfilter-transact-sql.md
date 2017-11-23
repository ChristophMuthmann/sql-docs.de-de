---
title: Sp_trace_setfilter (Transact-SQL) | Microsoft Docs
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
- sp_trace_setfilter
- sp_trace_setfilter_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_trace_setfilter
ms.assetid: 11e7c7ac-a581-4a64-bb15-9272d5c1f7ac
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 01394d92e71c69de60bbf2015ea58c4c8d53f0a4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sptracesetfilter-transact-sql"></a>sp_trace_setfilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wendet einen Filter auf eine Ablaufverfolgung an. **Sp_trace_setfilter** möglicherweise nur für vorhandene beendete ablaufverfolgungen ausgeführt (*Status* ist **0**). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Gibt einen Fehler zurück, wenn diese gespeicherte Prozedur ausgeführt wird, auf eine Ablaufverfolgung, die nicht vorhanden ist oder deren *Status* nicht **0**.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen erweiterte Ereignisse.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_trace_setfilter [ @traceid = ] trace_id   
          , [ @columnid = ] column_id  
          , [ @logical_operator = ] logical_operator  
          , [ @comparison_operator = ] comparison_operator  
          , [ @value = ] value  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@traceid=** ] *Trace_id*  
 Die ID der Ablaufverfolgung, auf die der Filter festgelegt wird. *Trace_id* ist **Int**, hat keinen Standardwert. Der Benutzer verwendet diesen *Trace_id* Wert zum Identifizieren, ändern und Steuern der Ablaufverfolgung.  
  
 [  **@columnid=** ] *Column_id*  
 Die ID der Spalte, auf die der Filter angewendet wird. *Column_id* ist **Int**, hat keinen Standardwert. Wenn *Column_id* NULL ist, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] löscht alle Filter für die angegebene Ablaufverfolgung.  
  
 [  **@logical_operator**  =] *Logical_operator*  
 Gibt an, ob den AND-Operator (**0**) oder OR (**1**)-Operator angewendet wird. *Logical_operator* ist **Int**, hat keinen Standardwert.  
  
 [  **@comparison_operator=** ] *Comparison_operator*  
 Gibt den Typ des vorzunehmenden Vergleichs an. *Comparison_operator* ist **Int**, hat keinen Standardwert. Die folgende Tabelle enthält die Vergleichsoperatoren und die sie darstellenden Werte.  
  
|Wert|Vergleichsoperator|  
|-----------|-------------------------|  
|**0**|= (Gleich)|  
|**1**|<> (ungleich)|  
|**2**|> (größer als)|  
|**3**|< (kleiner als)|  
|**4**|>= (größer oder gleich)|  
|**5**|< = (kleiner als oder gleich)|  
|**6**|LIKE|  
|**7**|Nicht wie|  
  
 [  **@value=** ] *Wert*  
 Gibt den Wert an, nach dem gefiltert werden soll. Der Datentyp des *Wert* übereinstimmen, dass den Datentyp der Spalte, die gefiltert werden. Wenn der Filter für eine Objekt-ID-Spalte festgelegt ist, ist beispielsweise ein **Int** -Datentyp, *Wert* muss **Int**. Wenn *Wert* ist **Nvarchar** oder **Varbinary**, sie können eine maximale Länge von 8000 haben.  
  
 Wenn der Vergleichsoperator LIKE oder NOT LIKE ist, kann der logische Operator % oder einen anderen für die LIKE-Operation geeigneten Filter enthalten.  
  
 Sie können angeben, dass NULL für *Wert* um Ereignisse mit NULL-Spaltenwerten zu filtern. Nur **0** (= gleich) und **1** (nicht gleich <>) Operatoren sind mit NULL gültig. In diesem Fall entsprechen diese Operatoren den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Operatoren IS NULL und IS NOT NULL.  
  
 Zum Anwenden des Filters aus einem Bereich von Spaltenwerten **Sp_trace_setfilter** muss zweimal ausgeführt werden: einmal mit einem größer-als-oder-gleich ("> =') Vergleichsoperator und einmal mit einem kleiner-als-oder-gleich (" < =') Operator .  
  
 Weitere Informationen zu Datentypen für Datenspalten finden Sie unter der [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 In der folgenden Tabelle werden die Codewerte beschrieben, die die Benutzer nach Abschluss der gespeicherten Prozedur möglicherweise erhalten.  
  
|Rückgabecode|Beschreibung|  
|-----------------|-----------------|  
|0|Kein Fehler.|  
|1|Unbekannter Fehler.|  
|2|Die Ablaufverfolgung wird derzeit ausgeführt. Ändern die Ablaufverfolgung am dieses Mal führt zu einem Fehler.|  
|4|Die angegebene Spalte ist ungültig.|  
|5|Für die angegebene Spalte ist das Filtern nicht zulässig. Dieser Wert wird nur von zurückgegeben **Sp_trace_setfilter**.|  
|6|Der angegebene Vergleichsoperator ist ungültig.|  
|7|Der angegebene logische Operator ist ungültig.|  
|9|Das angegebene Ablaufverfolgungshandle ist ungültig.|  
|13|Nicht genügend Arbeitsspeicher. Wird zurückgegeben, wenn nicht genügend Arbeitsspeicher zum Ausführen der angegebenen Aktion verfügbar ist.|  
|16|Die Funktion ist für diese Ablaufverfolgung ungültig.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_trace_setfilter** ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeicherten Prozedur, die viele der zuvor von erweiterten gespeicherten Prozeduren, die in früheren Versionen von ausgeführten Aktionen ausführt, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwendung **Sp_trace_setfilter** statt der **Xp_trace_set\*Filter** erweiterte gespeicherte Prozeduren erstellen, anwenden, entfernen oder ändern Sie Filter für ablaufverfolgungen. Weitere Informationen finden Sie unter [Filtern einer Ablaufverfolgung](../../relational-databases/sql-trace/filter-a-trace.md).  
  
 Alle Filter für eine bestimmte Spalte müssen zusammen in einer einzigen Ausführung von aktiviert werden **Sp_trace_setfilter**. Wenn ein Benutzer z. B. zwei Filter auf die Spalte application name und einen Filter auf die Spalte username anwenden möchte, muss er die Filter für application name nacheinander angeben. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt einen Fehler zurück, wenn der Benutzer in einem Aufruf einer gespeicherten Prozedur einen Filter für application name angibt und danach ein Filter für username und ein weiterer Filter für application name folgt.  
  
 Parameter aller gespeicherten Prozeduren der SQL-Ablaufverfolgung (**sp_trace_xx**) haben eine strikte Typbindung. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer müssen über die ALTER TRACE-Berechtigung verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden drei Filter für die Ablaufverfolgung `1` festgelegt. Die Filter `N'SQLT%'` und `N'MS%'` werden mithilfe des Vergleichsoperators "`AppName`" für eine Spalte (`10`, Wert `LIKE`) verwendet. Der `N'joe'`-Filter wird mithilfe des Vergleichsoperators "`UserName`" für eine andere Spalte (`11`, Wert `EQUAL`) verwendet.  
  
```  
sp_trace_setfilter  1, 10, 0, 6, N'SQLT%';  
sp_trace_setfilter  1, 10, 0, 6, N'MS%';  
sp_trace_setfilter  1, 11, 0, 0, N'joe';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md)  
  
  
