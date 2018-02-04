---
title: dbo.sysalerts (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7565ee20e5fdec3a94c413b8204629ce6ee2f48d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Warnung. Eine Warnung ist eine Nachricht, die als Reaktion auf ein Ereignis gesendet wird. Eine Warnung kann Nachrichten über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Umgebung hinaus weiterleiten. Eine Warnung kann eine E-Mail- oder eine Pagernachricht sein. Außerdem kann eine Warnung einen Task generieren.  Diese Tabelle wird in der **msdb** -Datenbank gespeichert.
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Warnungs-ID.|  
|**name**|**sysname**|Name der Warnung.|  
|**event_source**|**nvarchar(100)**|Die Quelle des Ereignisses: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**event_category_id**|**int**|Zur künftigen Verwendung reserviert.|  
|**event_id**|**int**|Zur künftigen Verwendung reserviert.|  
|**message_id**|**int**|Benutzerdefinierte Nachrichten-ID oder Verweis auf die **sysmessages** -Nachricht, die diese Warnung auslöst.|  
|**severity**|**int**|Schweregrad, der diese Warnung auslöst.|  
|**enabled**|**tinyint**|Status der Warnung:<br /><br /> **0** = Deaktiviert.<br /><br /> **1** = Aktiviert.|  
|**delay_between_responses**|**int**|Wartezeit in Sekunden zwischen den Benachrichtigungen für diese Warnung.|  
|**last_occurrence_date**|**int**|Letztes Auftreten (Datum) der Warnung.|  
|**last_occurrence_time**|**int**|Letztes Auftreten (Tageszeit) der Warnung.|  
|**last_response_date**|**int**|Letzte Benachrichtigung (Datum) der Warnung.|  
|**last_response_time**|**int**|Letzte Benachrichtigung (Tageszeit) der Warnung.|  
|**notification_message**|**nvarchar(512)**|Zusätzliche, mit der Warnung gesendete Informationen.|  
|**include_event_description**|**tinyint**|Bitmaske, die darstellt, ob die Ereignisbeschreibung per E-mail, Pager oder Net Send gesendet wird. Diagramm unten für Werte angezeigt.|  
|**database_name**|**nvarchar(512)**|Datenbank, in der die Warnung auftreten muss, damit sie ausgelöst wird.|  
|**event_description_keyword**|**nvarchar(100)**|Muster, dem der Fehler entsprechen muss, damit die Warnung ausgelöst wird.|  
|**occurrence_count**|**int**|Anzahl der Warnungsauftritte.|  
|**count_reset_date**|**int**|Tag (Datum), an dem die Anzahl auf **0**zurückgesetzt wird.|  
|**count_reset_time**|**int**|Tageszeit, zu der die Anzahl auf **0**zurückgesetzt wird.|  
|**job_id**|**uniqueidentifier**|ID des Tasks, der ausgeführt wird, wenn die Warnung auftritt.|  
|**has_notification**|**int**|Anzahl der Operatoren, die eine E-Mail-Benachrichtigung erhalten, wenn die Warnung auftritt.|  
|**flags**|**int**|Reserviert.|  
|**performance_condition**|**nvarchar(512)**|Reserviert.|  
|**category_id**|**int**|Reserviert.|  
  
 ## <a name="remarks"></a>Hinweise

Die folgende Tabelle zeigt die Werte für die Bitmaske Include_event_description. Der decimal-Wert wird von dbo.sysalerts zurückgegeben. 

|Decimal | BINARY | Bedeutung |
|------|------|------|
|0 |0000 |keine Nachricht |
|1 |0001 |E-Mail |
|2 |0010 |Pager |
|3 |0011 |Pager und e-Mail |
|4 |0100 |NET SEND |
|5 |0101 |NET SEND- und -e-Mail |
|6 |0110 |NET SEND- und pager |
|7 |0111 |NET SEND- und Pager-e-Mail |
  
