---
title: Sysmail_help_queue_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c95bdba93f23bc3343a64cbf8f5ab63a2fbd209d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailhelpqueuesp-transact-sql"></a>sysmail_help_queue_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Es gibt zwei Warteschlangen in der Datenbank-E-Mail: die E-Mail-Warteschlange und die Statuswarteschlange. In der E-Mail-Warteschlange werden E-Mail-Elemente gespeichert, die darauf warten, gesendet zu werden. In der Statuswarteschlange wird der Status von Elementen gespeichert, die bereits gesendet wurden. Mit dieser gespeicherten Prozedur können Sie den Status der E-Mail- oder der Statuswarteschlange anzeigen. Wenn der Parameter **@queue_type** nicht angegeben ist, wird die gespeicherte Prozedur gibt eine Zeile für jede Warteschlange zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@queue_type** = ] **'***queue_type***'**  
 Optionales Argument, das E-Mails löscht, für die als Typ *queue_type*angegeben ist. *queue_type* ist vom Datentyp **nvarchar(6)** und besitzt keinen Standardwert. Gültige Einträge sind **mail** und **status**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-set"></a>Resultset  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar(6)**|Der Typ der Warteschlange. Mögliche Werte sind **mail** und **status**.|  
|**length**|**int**|Die Anzahl der E-Mail-Elemente in der angegebenen Warteschlange.|  
|**state**|**nvarchar(64)**|Der Status des Überwachungsservers. Mögliche Werte sind **INACTIVE** (Warteschlange ist inaktiv), **NOTIFIED** (Warteschlange wurde benachrichtigt, dass Empfang auftritt) und **RECEIVES_OCCURRING** (Warteschlange empfängt).|  
|**last_empty_rowset_time**|**"DATETIME"**|Das Datum und die Uhrzeit, an dem bzw. zu der die Warteschlange zuletzt leer war. Die Angabe erfolgt im 24-Stunden-Format und in der GMT-Zeitzone.|  
|**last_activated_time**|**"DATETIME"**|Das Datum und die Uhrzeit, an dem bzw. zu der die Warteschlange zuletzt aktiviert war. Die Angabe erfolgt im 24-Stunden-Format und in der GMT-Zeitzone.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie Probleme mit der Datenbank-E-Mail behandeln, verwenden Sie **sysmail_help_queue_sp** , um anzuzeigen, wie viele Elemente sich in der Warteschlange befinden, wie der Status der Warteschlange lautet und wann die Warteschlange zuletzt aktiviert wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** auf diese Prozedur zugreifen.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt sowohl die E-Mail- als auch die Statuswarteschlange zurück.  
  
```  
EXECUTE msdb.dbo.sysmail_help_queue_sp ;  
GO  
```  
  
 Dies ist ein Beispielresultset, das auf Zeilenlänge umformatiert wurde.  
  
```  
queue_type length      state              last_empty_rowset_time  last_activated_time  
---------- -------- ------------------ ----------------------- -----------------------  
mail       0        RECEIVES_OCCURRING 2005-10-07 21:14:47.010 2005-10-10 20:52:51.517  
status     0        INACTIVE           2005-10-07 21:04:47.003 2005-10-10 21:04:47.003  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
