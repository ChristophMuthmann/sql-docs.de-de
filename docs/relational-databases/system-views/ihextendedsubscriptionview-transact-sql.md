---
title: IHextendedSubscriptionView (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHextendedSubscriptionView_TSQL
- IHextendedSubscriptionView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedSubscriptionView view
ms.assetid: 124756a4-463a-4a81-bf5b-de7e8ffc7a62
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f938ff6df875bf761b58667b328af223eb3af8ee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **IHextendedSubscriptionView** -Sicht macht Informationen zu Abonnements für eine nicht - SQL Server-Veröffentlichung verfügbar. Diese Sicht wird in der **distribution** -Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Der eindeutige Bezeichner für einen Artikel.|  
|**dest_db**|**sysname**|Der Name der Zieldatenbank.|  
|**srvid**|**smallint**|Der eindeutige Bezeichner für einen Abonnenten.|  
|**login_name**|**sysname**|Der zum Herstellen einer Verbindung mit einem Abonnenten verwendete Anmeldename.|  
|**distribution_jobid**|**binary**|Identifiziert den Auftrag des Verteilungs-Agents.|  
|**publisher_database_id**|**int**|Identifiziert die Veröffentlichungsdatenbank.|  
|**subscription_type**|**int**|Der Typ des Abonnements:<br /><br /> **0** = Push - der Verteilungs-Agent wird ausgeführt, auf dem Abonnenten.<br /><br /> **1** = Pull - der Verteilungs-Agent wird ausgeführt, auf dem Verteiler.|  
|**sync_type**|**tinyint**|Der Typ der Erstsynchronisierung:<br /><br /> **1** = automatisch<br /><br /> **2** = keine|  
|**status**|**tinyint**|Status des Abonnements:<br /><br /> **0** = inaktiv<br /><br /> **1** = abonniert<br /><br /> **2** = aktiv|  
|**snapshot_seqno_flag**|**bit**|Gibt an, ob eine Momentaufnahmesequenznummer verwendet wird.|  
|**independent_agent**|**bit**|Gibt an, ob ein eigenständiger Verteilungs-Agent für diese Veröffentlichung vorhanden ist.<br /><br /> **0** = die Veröffentlichung verwendet einen freigegebenen Verteilungs-Agent, und jedes Verlegerdatenbank und Abonnentendatenbank-Paar besitzt einen einzelnen freigegebenen Agent.<br /><br /> **1** = es ist ein eigenständiger Verteilungs-Agent für diese Veröffentlichung.|  
|**subscription_time**|**datetime**|Nur interne Verwendung.|  
|**loopback_detection**|**bit**|Gilt für Abonnements, die Teil einer bidirektionalen Transaktionsreplikationstopologie sind. Bestimmt, ob der Verteilungs-Agent Transaktionen des Abonnenten zurück an den Abonnenten sendet:<br /><br /> **1** tut = sendet nicht zurück.<br /><br /> **0** = sendet zurück.|  
|**agent_id**|**int**|Der eindeutige Bezeichner des Verteilungs-Agents.|  
|**update_mode**|**tinyint**|Gibt den Typ des Updatemodus an, der wie folgt lauten kann:<br /><br /> **0** = schreibgeschützt.<br /><br /> **1** = sofortiges Update.<br /><br /> **2** = verzögertes Update über Message Queuing.<br /><br /> **3** = sofortiges Aktualisieren mit verzögertem Aktualisieren mithilfe von Message Queuing.<br /><br /> **4** = verzögertes Update mithilfe von SQL Server-Warteschlange.<br /><br /> **5** = sofortiges Aktualisieren mit Failover Update über eine Warteschlange mithilfe von SQL Server-Warteschlange.|  
|**publisher_seqno**|**varbinary(16)**|Die Sequenznummer der Transaktion auf dem Verleger für dieses Abonnement.|  
|**ss_cplt_seqno**|**varbinary(16)**|Die Sequenznummer, die den Abschluss der Verarbeitung der gleichzeitigen Momentaufnahme anzeigt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Heterogene Datenbankreplikation](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
