---
title: Sysarticleupdates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fe7ffac2dce09058796e5e41bd40b90d7f65faf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Artikel, der sofort aktualisierte Abonnements unterstützt. Diese Tabelle wird in der replizierten Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Die Identity-Spalte, die eine eindeutige ID für den Artikel bereitstellt.|  
|**pubid**|**int**|Die ID der Veröffentlichung, zu der der Artikel gehört.|  
|**sync_ins_proc**|**int**|Die ID der gespeicherten Prozedur, die synchrone Einfügetransaktionen verarbeitet.|  
|**sync_upd_proc**|**int**|Die ID der gespeicherten Prozedur, die synchrone Updatetransaktionen verarbeitet.|  
|**sync_del_proc**|**int**|Die ID der gespeicherten Prozedur, die synchrone Löschtransaktionen verarbeitet.|  
|**autogen**|**bit**|Zeigt an, dass gespeicherte Prozeduren automatisch generiert werden:<br /><br /> **0** = "false", nicht automatisch.<br /><br /> **1** = "true", automatische.|  
|**sync_upd_trig**|**int**|Die ID des Triggers für die automatische Versionsverwaltung für die Artikeltabelle.|  
|**conflict_tableid**|**int**|Die ID für die Konflikttabelle.|  
|**ins_conflict_proc**|**int**|Die ID der Prozedur verwendet, um zum Schreiben des Konflikts das **Conflict_table**.|  
|**identity_support**|**bit**|Gibt an, ob die automatische Behandlung des Identitätsbereichs aktiviert ist, wenn das verzögerte Aktualisieren über eine Warteschlange verwendet wird. **0** bedeutet, dass keine identitätsbereichsunterstützung vorhanden ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
