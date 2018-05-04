---
title: MSpublications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- MSpublications
- MSpublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublications system table
ms.assetid: 7a0b3457-7265-4f24-a255-7f055d908f20
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e5e6b1f9ab0d4cbd42e88ae4480d55625ba434e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mspublications-transact-sql"></a>MSpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSpublications** -Tabelle enthält eine Zeile für jede Veröffentlichung, die von einem Verleger repliziert wird. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Die ID des Verlegers|  
|**publisher_db**|**sysname**|Der Name der Verlegerdatenbank.|  
|**Veröffentlichung**|**sysname**|Der Name der Veröffentlichung.|  
|**publication_id**|**int**|Die ID der Veröffentlichung.|  
|**publication_type**|**int**|Der Typ der Veröffentlichung:<br /><br /> **0** = transaktionsveröffentlichung.<br /><br /> **1** = Snapshot.<br /><br /> **2** = befindet.|  
|**thirdparty_flag**|**bit**|Gibt an, ob eine Veröffentlichung ist eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **1** Datenquelle außer = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**independent_agent**|**bit**|Zeigt an, ob ein Verteilungs-Agent im Einzelplatzmodus für diese Veröffentlichung vorhanden ist.|  
|**immediate_sync**|**bit**|Zeigt an, ob bei jeder Ausführung des Momentaufnahme-Agents Synchronisierungsdateien erstellt oder neu erstellt werden.|  
|**allow_push**|**bit**|Zeigt an, ob für die angegebene Veröffentlichung Pushabonnements erstellt werden können.|  
|**allow_pull**|**bit**|Zeigt an, ob für die angegebene Veröffentlichung Pullabonnements erstellt werden können.|  
|**allow_anonymous**|**bit**|Zeigt an, ob für die angegebene Veröffentlichung anonyme Abonnements erstellt werden können.|  
|**description**|**nvarchar(255)**|Die Beschreibung der Veröffentlichung.|  
|**$vendor_name**|**Nvarchar(100)**|Der Name des Herstellers, wenn der Verleger keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank ist.|  
|**Beibehaltungsdauer**|**int**|Die Beibehaltungsdauer der Veröffentlichung (in Stunden).|  
|**sync_method**|**int**|Synchronisierungsmethode:<br /><br /> **0** = Native (erzeugt im einheitlichen Modus massenkopierausgabe aller Tabellen).<br /><br /> **1** = Character (erzeugt eine im Zeichenmodus massenkopierausgabe aller Tabellen).<br /><br /> **3** = Concurrent (erzeugt im einheitlichen Modus massenkopierausgabe aller Tabellen, jedoch nicht die Tabelle gesperrt, während der Momentaufnahme).<br /><br /> **4** = Concurrent_c (erzeugt eine im Zeichenmodus massenkopierausgabe aller Tabellen, jedoch nicht die Tabelle gesperrt, während der Momentaufnahme)<br /><br /> Die Werte **3** und **4** stehen für die Transaktionsreplikation und Mergereplikation, aber nicht für die momentaufnahmereplikation.|  
|**allow_subscription_copy**|**bit**|Aktiviert oder deaktiviert die Option zum Kopieren der Abonnementdatenbanken, die diese Veröffentlichung abonniert haben. **0** bedeutet, dass das Kopieren deaktiviert ist, und **1** bedeutet, dass diese Einstellung aktiviert ist.|  
|**thirdparty_options**|**int**|Gibt an, ob die Anzeige einer Veröffentlichung in den Ordner "Replikation" in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] unterdrückt wird:<br /><br /> **0** = heterogene Veröffentlichung angezeigt, in dem Ordner "Replikation" in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].<br /><br /> **1** = unterdrückt die Anzeige im Ordner "Replikation" in eine heterogene Veröffentlichung [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|**allow_queued_tran**|**bit**|Gibt an, ob die Veröffentlichung verzögerte Updates über eine Warteschlange zulässt:<br /><br /> **0 =** Veröffentlichung ist nicht in Warteschlange.<br /><br /> **1** = Veröffentlichung mit Warteschlange.|  
|**options**|**int**|Für diese Version sind keine Informationen verfügbar.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
