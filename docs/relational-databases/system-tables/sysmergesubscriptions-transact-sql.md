---
title: Sysmergesubscriptions (Transact-SQL) | Microsoft Docs
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
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1cc4216c383ee387b495e7933fd5da7a4832479e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden bekannten Abonnenten und stellt eine lokale Tabelle auf dem Verleger dar. Diese Tabelle wird in der Veröffentlichungs- und in der Abonnementdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|Die ID des Servers. Diese wird verwendet, um das Feld srvid dem serverspezifischen Wert zuzuordnen, wenn eine Kopie der Abonnementdatenbank auf einen anderen Server migriert wird.|  
|db_name|**sysname**|Der Name der abonnierenden Datenbank.|  
|pubid|**uniqueidentifier**|Die ID der Veröffentlichung, aus der das aktuelle Abonnement erstellt wurde.|  
|datasource_type|**int**|Der Typ der Datenquelle:<br /><br /> **0** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **2** = Jet OLE DB.|  
|subid|**uniqueidentifier**|Die eindeutige ID für das Abonnement.|  
|replnickname|**binary**|Der komprimierte Spitzname für das Replikat.|  
|replicastate|**uniqueidentifier**|Ein eindeutiger Bezeichner, anhand dessen bestimmt wird, ob die vorhergehende Synchronisierung erfolgreich war. Dafür wird der Wert auf dem Verleger mit dem Wert auf dem Abonnenten verglichen.|  
|status|**tinyint**|Status des Abonnements:<br /><br /> **0** = inaktiv.<br /><br /> **1** = aktiv.<br /><br /> **2** = gelöscht.|  
|subscriber_type|**int**|Der Typ des Abonnenten:<br /><br /> **1** = global.<br /><br /> **2** = lokal.<br /><br /> **3** = anonym.|  
|subscription_type|**int**|Der Typ des Abonnements:<br /><br /> **0** = Push.<br /><br /> **1** = Pullabonnement.<br /><br /> **2** = anonym.|  
|sync_type|**tinyint**|Typ der Synchronisierung:<br /><br /> **1** = Automatic.<br /><br /> **2** = keine Synchronisierung.|  
|description|**nvarchar(255)**|Kurze Beschreibung des Abonnements.|  
|priority|**real**|Gibt die Priorität des Abonnements an und lässt die Implementierung von prioritätsbasierten Routinen zur Konfliktlösung zu. Ist gleich **0,00** für alle lokalen oder anonymen Abonnements.|  
|recgen|**bigint**|Die Nummer der zuletzt empfangenen Generierung.|  
|recguid|**uniqueidentifier**|Die eindeutige ID der zuletzt empfangenen Generierung.|  
|sentgen|**bigint**|Nummer der zuletzt gesendeten Generierung.|  
|sentguid|**uniqueidentifier**|Die eindeutige ID der zuletzt gesendeten Generierung.|  
|schemaversion|**int**|Die Nummer des zuletzt empfangenen Schemas.|  
|schemaguid|**uniqueidentifier**|Die eindeutige ID des zuletzt empfangenen Schemas.|  
|last_validated|**datetime**|Die **"DateTime"** der letzten erfolgreichen Überprüfung der Abonnentendaten.|  
|attempted_validate|**datetime**|Der letzte **"DateTime"** , dass die Überprüfung des Abonnements versucht wurde.|  
|last_sync_date|**datetime**|Die **"DateTime"** der Synchronisierung.|  
|last_sync_status|**int**|Der Abonnementstatus:<br /><br /> **0** = alle Aufträge sind zu starten.<br /><br /> **1** = ein oder mehrere Aufträge werden gestartet.<br /><br /> **2** = alle Aufträge wurden erfolgreich ausgeführt.<br /><br /> **3** = mindestens ein Auftrag wird ausgeführt.<br /><br /> **4** = alle Aufträge sind geplant und im Leerlauf befindet.<br /><br /> **5** = mindestens ein Auftrag versucht, führen Sie nach einem vorherigen Fehler.<br /><br /> **6** = mindestens ein Auftrag konnte nicht erfolgreich ausgeführt.|  
|last_sync_summary|**sysname**|Die Beschreibung der letzten Synchronisierungsergebnisse.|  
|metadatacleanuptime|**datetime**|Der letzte **"DateTime"** , dass abgelaufene Metadaten aus Systemtabellen der Mergereplikation entfernt wurde.|  
|partition_id|**int**|Identifiziert die vorausberechnete Partition, zu der das Abonnement gehört.|  
|cleanedup_unsent_changes|**bit**|Gibt an, dass Metadaten für nicht gesendete Änderungen auf dem Abonnenten bereinigt wurden.|  
|replica_version|**int**|Identifiziert die Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für den Abonnenten, zu dem das Abonnement gehört. Die folgenden Werte sind möglich:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|Nur interne Verwendung.|  
|application_name|**nvarchar(128)**|Nur interne Verwendung.|  
|subscriber_number|**int**|Nur interne Verwendung.|  
|last_makegeneration_datetime|**datetime**|Der letzte **"DateTime"** , die der Makegeneration-Prozess für den Verleger ausgeführt wurden. Weitere Informationen finden Sie unter den - MakeGenerationInterval-Parameter im [Replikationsmerge-Agent](../../relational-databases/replication/agents/replication-merge-agent.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
