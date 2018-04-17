---
title: Syssubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions system table
ms.assetid: 106c1707-e0e0-49b4-ba50-25380c40fab2
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 595c729b9e60a26672b543d83b6fb47e57e8b215
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="syssubscriptions-transact-sql"></a>syssubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jedes in der Datenbank definierte Abonnement. Diese Tabelle wird in der Veröffentlichungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Die eindeutige ID eines Artikels.|  
|**srvid**|**smallint**|Die Server-ID des Abonnenten.|  
|**dest_db**|**sysname**|Der Name der Zieldatenbank.|  
|**status**|**tinyint**|Status des Abonnements:<br /><br /> **0** = inaktiv.<br /><br /> **1** = abonniert.<br /><br /> **2** = aktiv.|  
|**sync_type**|**tinyint**|Der Typ der Erstsynchronisierung:<br /><br /> **1** = Automatic.<br /><br /> **2** = keine|  
|**login_name**|**sysname**|Der Anmeldename, der beim Hinzufügen des Abonnements verwendet wird.|  
|**subscription_type**|**int**|Der Typ des Abonnements:<br /><br /> 0 = Push - der Verteilungs-Agent wird auf dem Verteiler ausgeführt.<br /><br /> 1 = Pull - der Verteilungs-Agent wird auf dem Abonnenten ausgeführt.|  
|**distribution_jobid**|**Binary(16)**|Die Auftrags-ID des Verteilungs-Agents.|  
|**timestamp**|**timestamp**|Der Timestamp.|  
|**update_mode**|**tinyint**|Updatemodus:<br /><br /> **0** = nur Lesezugriff.<br /><br /> **1** = sofortiges Aktualisieren.|  
|**loopback_detection**|**bit**|Gilt für Abonnements, die Teil einer bidirektionalen Transaktionsreplikationstopologie sind. Bestimmt, ob der Verteilungs-Agent Transaktionen des Abonnenten zurück an den Abonnenten sendet:<br /><br /> **0** = sendet zurück.<br /><br /> **1** tut = sendet nicht zurück.|  
|**queued_reinit**|**bit**|Gibt an, ob der Artikel für die Initialisierung oder erneute Initialisierung markiert ist. Der Wert **1** gibt an, dass der abonnierte Artikel für die Initialisierung oder erneute Initialisierung markiert ist.|  
|**nosync_type**|**tinyint**|Der Typ der Abonnementinitialisierung:<br /><br /> **0** = automatisch (Momentaufnahme)<br /><br /> **1** = nur replikationsunterstützung<br /><br /> **2** = Initialisierung von einer Sicherung<br /><br /> **3** = Initialisierung von einer protokollfolgenummer (LSN)<br /><br /> Weitere Informationen finden Sie unter der **@sync_type** Parameter [Sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md).|  
|**mit srvname**|**sysname**|Den Namen des Abonnenten.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
