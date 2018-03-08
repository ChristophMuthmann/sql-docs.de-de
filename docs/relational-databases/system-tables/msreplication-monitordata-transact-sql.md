---
title: MSreplication_monitordata (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs: TSQL
helpviewer_keywords: MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6bab9e68284c9c8acbbdd1211530edb5014950aa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationmonitordata-transact-sql"></a>MSreplication_monitordata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSreplication_monitordata** -Tabelle enthält zwischengespeicherte Daten, die vom Replikationsmonitor überwacht, die mit einer Zeile für jedes überwachte Abonnement verwendet. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**' lastrefresh '**|**datetime**|Datum und Uhrzeit des Updates der Überwachungsdaten|  
|**computeTime**|**int**|Zeit (in Sekunden) zum Berechnen der Überwachungsdaten|  
|**publication_id**|**int**|Die Veröffentlichung-ID.|  
|**publisher**|**sysname**|Der Name des Verlegers.|  
|**publisher_srvid**|**int**|Server-ID des Verlegers|  
|**publisher_db**|**sysname**|Der Name der Veröffentlichungsdatenbank.|  
|**Veröffentlichung**|**sysname**|Der Name der Veröffentlichung.|  
|**publication_type**|**int**|Der Veröffentlichungstyp. Die folgenden Werte sind möglich:<br /><br /> **0** = transaktionsveröffentlichung<br /><br /> **1** = momentaufnahmeveröffentlichung<br /><br /> **2** = Mergeveröffentlichung|  
|**agent_type-Wert**|**int**|Der Typ des Replikations-Agents. Die folgenden Werte sind möglich.<br /><br /> **1** = Momentaufnahme-Agent<br /><br /> **2** = Protokolllese-Agent<br /><br /> **3** = Verteilungs-Agent<br /><br /> **4** = Merge-Agent<br /><br /> **9** = Warteschlangenlese-Agent|  
|**agent_id-Wert**|**int**|ID des Replikations-Agents|  
|**agent_name**|**sysname**|Name des Replikations-Agent-Auftrags|  
|**job_id**|**uniqueidentifier**|GUID des Replikations-Agent-Auftrags|  
|**status**|**int**|Der Status des Replikations-Agents. Die folgenden Werte sind möglich:<br /><br /> **1** = gestartet<br /><br /> **2** = war erfolgreich<br /><br /> **3** = wird ausgeführt<br /><br /> **4** = im Leerlauf<br /><br /> **5** = wird wiederholt<br /><br /> **6** = Fehler|  
|**isagentrunningnow**|**bit**|Ein Flag, das angibt, ob der Agentauftrag derzeit ein Wert von ausgeführt wird, **1** bedeutet, dass der Auftrag ausgeführt wird.|  
|**Warnung**|**int**|Schwellenwertwarnung, die von einem Abonnement generiert wird. Sie kann das Ergebnis des logischen OR von mindestens einem der folgenden Werte sein.<br /><br /> **1** = Expiration ein Abonnement für eine transaktionsveröffentlichung hat die Beibehaltungsdauer um mehr als den zulässigen Schwellenwert überschritten, als Prozentanteil der Beibehaltungsdauer.<br /><br /> **2** = Latency - die Zeitdauer für die Replikation von Daten von einem Transaktionsverleger auf den Abonnenten überschreitet den Schwellenwert in Sekunden.<br /><br /> **4** = Mergeexpiration - ein Abonnement für eine Mergeveröffentlichung hat die Beibehaltungsdauer um mehr als den zulässigen Schwellenwert überschritten, als Prozentanteil der Beibehaltungsdauer. 8 = mergefastrunduration - die Zeit zum Synchronisieren eines Mergeabonnements über eine schnelle Netzwerkverbindung überschreitet den Schwellenwert (in Sekunden).<br /><br /> **16** = Mergeslowrunduration – die Zeit zum Abschließen der Synchronisierung eines Mergeabonnements überschreitet den Schwellenwert in Sekunden an, über eine langsame oder DFÜ Netzwerkverbindung.<br /><br /> **32** = Mergefastrunspeed-die Übermittlungsrate für Zeilen während der Synchronisierung eines Mergeabonnements konnte die Schwellenwert-Rate in Zeilen pro Sekunde, über eine schnelle Netzwerkverbindung zu verwalten.<br /><br /> **64** = Mergeslowrunspeed-die Übermittlungsrate für Zeilen während der Synchronisierung eines Mergeabonnements konnte die Schwellenwert-Rate in Zeilen pro Sekunde, über eine langsame oder DFÜ Netzwerkverbindung zu verwalten.|  
|**last_distsync**|**datetime**|Datum und die Uhrzeit, wann der Verteilungs-Agent zuletzt ausgeführt wurde|  
|**agentstoptime**|**datetime**|Datum und die Uhrzeit der Beendigung der Momentaufnahme|  
|**distdb**|**sysname**|Name der Verteilungsdatenbank für das Abonnement|  
|**Beibehaltungsdauer**|**int**|Beibehaltungsdauer für die Veröffentlichung|  
|**time_stamp**|**datetime**|Intern-nur zur Verwendung.|  
|**worst_latency**|**int**|Die längste Latenzzeit (in Sekunden) für Datenänderungen, die vom Protokolllese-Agent oder vom Verteilungs-Agent für eine Transaktionsveröffentlichung weitergegeben werden.|  
|**best_latency**|**int**|Die kürzeste Latenzzeit (in Sekunden) für Datenänderungen, die vom Protokolllese-Agent oder vom Verteilungs-Agent für eine Transaktionsveröffentlichung weitergegeben werden.|  
|**avg_latency**|**int**|Die durchschnittliche Latenzzeit (in Sekunden) für Datenänderungen, die vom Protokolllese-Agent oder vom Verteilungs-Agent für eine Transaktionsveröffentlichung weitergegeben werden.|  
|**cur_latency**|**int**|Die Latenzzeit (in Sekunden) für Datenänderungen, die vom Protokolllese-Agent oder vom Verteilungs-Agent während der aktuellen Ausführung weitergegeben werden.|  
|**worst_runspeedPerf**|**int**|Die längste Synchronisierungszeit für die Mergeveröffentlichung|  
|**best_runspeedPerf**|**int**|Die kürzeste Synchronisierungszeit für die Mergeveröffentlichung|  
|**average_runspeedPerf**|**int**|Die durchschnittliche Synchronisierungszeit für die Mergeveröffentlichung|  
|**mergePerformance**|**int**|Die Leistung der letzten Synchronisierung im Vergleich zu allen Synchronisierungen des Abonnements. Sie ergibt sich aus der Übermittlungsrate der letzten Synchronisierung dividiert durch den Durchschnitt aller vorhergegangenen Übermittlungsraten.|  
|**mergelatestsessionrunduration**|**int**|Dauer der letzten Ausführung des Merge-Agents|  
|**mergelatestsessionrunspeed**|**float(53)**|Übermittlungsrate der letzten Ausführung des Merge-Agents|  
|**mergelatestsessionconnectiontype**|**int**|Die für die letzte Merge-Agent-Sitzung verwendete Verbindung. Die folgenden Werte sind möglich:<br /><br /> **1** = lokale Netzwerk (LAN)<br /><br /> **2** = DFÜ-Netzwerkverbindung|  
|**retention_period_unit**|**tinyint**|Gibt die zum Definieren der Beibehaltungsdauer verwendete Einheit an. Die folgenden Werte sind möglich.<br /><br /> **1** = Woche<br /><br /> **2** = Monat<br /><br /> **3** = Jahr|  
  
## <a name="see-also"></a>Siehe auch  
 [Programmgesteuertes Überwachen der Replikation](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sp_replmonitorhelpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [Sp_replmonitorhelppublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [Sp_replmonitorhelppublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [Sp_replmonitorhelpmergesession &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [Sp_replmonitorhelppublicationthresholds &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [Sp_replmonitorhelpmergesessiondetail &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  
