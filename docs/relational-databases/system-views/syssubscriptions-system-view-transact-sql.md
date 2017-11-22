---
title: Syssubscriptions (Systemsicht) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs: TSQL
helpviewer_keywords: syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81135d7c10ac1c9404837015740d74b71e65817d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (Systemsicht) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **Syssubscriptions** -Sicht macht Informationen zum Abonnement verfügbar. Diese Sicht wird in der distribution-Datenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Die eindeutige ID eines abonnierten Artikels.|  
|**srvID**|**smallint**|Die Server-ID des Abonnenten.|  
|**dest_db**|**sysname**|Der Name der Abonnementdatenbank.|  
|**status**|**tinyint**|Status des Abonnements:<br /><br /> **0** = inaktiv.<br /><br /> **1** = abonniert.<br /><br /> **2** = aktiv.|  
|**sync_type-Typ**|**tinyint**|Der Typ der Erstsynchronisierung:<br /><br /> **1** = Automatic.<br /><br /> **2** = none.|  
|**login_name**|**sysname**|Der Anmeldename, der für die Verbindung mit dem Verleger zum Hinzufügen des Abonnements verwendet wird.|  
|**subscription_type**|**int**|Der Typ des Abonnements:<br /><br /> **0** = Push - der Verteilungs-Agent wird ausgeführt, auf dem Verteiler.<br /><br /> **1** = Pull - der Verteilungs-Agent wird ausgeführt, auf dem Abonnenten.|  
|**distribution_jobid**|**Binary(16)**|Gibt den zum Synchronisieren des Abonnements verwendeten Verteilungs-Agent-Auftrag an.|  
|**timestmap**|**timestamp**|Datum und Uhrzeit der Erstellung des Abonnements.|  
|**update_mode**|**tinyint**|Updatemodus:<br /><br /> **0** = schreibgeschützt.<br /><br /> **1** = sofortiges Aktualisieren.|  
|**loopback_detection**|**bit**|Gilt für Abonnements, die Teil einer bidirektionalen Transaktionsreplikationstopologie sind. Bestimmt, ob der Verteilungs-Agent Transaktionen des Abonnenten zurück an den Abonnenten sendet:<br /><br /> **0** = sendet zurück.<br /><br /> **1** tut = sendet nicht zurück.|  
|**queued_reinit**|**bit**|Gibt an, ob der Artikel für die Initialisierung oder erneute Initialisierung markiert ist. Der Wert **1** gibt an, dass der abonnierte Artikel für die Initialisierung oder erneute Initialisierung markiert ist.|  
|**nosync_type**|**tinyint**|Der Typ der Abonnementinitialisierung:<br /><br /> **0** = automatisch (Momentaufnahme)<br /><br /> **1** = nur replikationsunterstützung<br /><br /> **2** = Initialisierung von einer Sicherung<br /><br /> **3** = Initialisierung von einer protokollfolgenummer (LSN)<br /><br /> Weitere Informationen finden Sie unter der  **@sync_type**  Parameter [Sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**mit srvname**|**sysname**|Den Namen des Abonnenten.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
