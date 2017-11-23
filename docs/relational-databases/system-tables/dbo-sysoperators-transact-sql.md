---
title: dbo.sysoperators (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysoperators
- dbo.sysoperators
- dbo.sysoperators_TSQL
- sysoperators_TSQL
dev_langs: TSQL
helpviewer_keywords: sysoperators system table
ms.assetid: c2afa20c-b15f-46ca-ae74-2eb65909409e
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0b48cdf057e17d0c043f2716071868b9188874d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysoperators-transact-sql"></a>dbo.sysoperators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Operator.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID des Operators.|  
|**name**|**sysname**|Name des Operators.|  
|**aktiviert**|**tinyint**|Status der Warnbenachrichtigungen (Boolesch). Beträgt der Wert **1**, kann dieser Operator Benachrichtigungen erhalten, wenn eine Warnung auftritt.|  
|**email_address**|**nvarchar(100)**|E-Mail-Adresse für diesen Operator.|  
|**last_email_date**|**int**|Datum, an dem dieser Operator zuletzt eine Warnbenachrichtigung per E-Mail erhalten hat.|  
|**last_email_time**|**int**|Tageszeit, zu der dieser Operator zuletzt eine Warnbenachrichtigung per E-Mail erhalten hat.|  
|**pager_address**|**nvarchar(100)**|Pageradresse für diesen Operator.|  
|**last_pager_date**|**int**|Datum, an dem dieser Operator zuletzt eine Warnbenachrichtigung per Pager erhalten hat.|  
|**last_pager_time**|**int**|Tageszeit, zu der dieser Operator zuletzt eine Warnbenachrichtigung per Pager erhalten hat.|  
|**weekday_pager_start_time**|**int**|Tageszeit an einem Arbeitstag (Montag bis Freitag), von der an dieser Operator zur Verfügung steht, um eine Warnbenachrichtigung per Pager zu erhalten.|  
|**weekday_pager_end_time**|**int**|Tageszeit an einem Arbeitstag (Montag bis Freitag), von der an dieser Operator nicht zur Verfügung steht, um eine Warnbenachrichtigung per Pager zu erhalten.|  
|**saturday_pager_start_time**|**int**|Tageszeit an einem Samstag, von der an dieser Operator zur Verfügung steht, um eine Warnbenachrichtigung per Pager zu erhalten.|  
|**saturday_pager_end_time**|**int**|Tageszeit an einem Samstag, von der an dieser Operator nicht zur Verfügung steht, um eine Warnbenachrichtigung per Pager zu erhalten.|  
|**sunday_pager_start_time**|**int**|Tageszeit an einem Sonntag, von der an dieser Operator zur Verfügung steht, um eine Warnbenachrichtigung per Pager zu erhalten.|  
|**sunday_pager_end_time**|**int**|Tageszeit an einem Sonntag, von der an dieser Operator nicht zur Verfügung steht, um eine Warnbenachrichtigung per Pager zu erhalten.|  
|**pager_days**|**tinyint**|Bitmaske, die die Arbeitstage darstellt, an denen dieser Operator zur Verfügung steht, um eine Warnbenachrichtigung per Pager zu erhalten.|  
|**netsend_address**|**nvarchar(100)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**last_netsend_date**|**int**|Datum, an dem die neueste Netzwerkmeldung zuletzt an die angegebene Operator-ID gesendet wurde.|  
|**last_netsend_time**|**int**|Uhrzeit, zu der die neueste Netzwerkmeldung zuletzt an die angegebene Operator-ID gesendet wurde.|  
|**category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-Tabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
