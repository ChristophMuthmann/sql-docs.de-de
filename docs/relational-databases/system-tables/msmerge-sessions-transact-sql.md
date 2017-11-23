---
title: MSmerge_sessions (Transact-SQL) | Microsoft Docs
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
- MSmerge_sessions
- MSmerge_sessions_TSQL
dev_langs: TSQL
helpviewer_keywords: MSmerge_sessions system table
ms.assetid: 09ada8fc-c148-4379-9524-7826b1b0216c
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a081578000d831f85f00d8de2da725e6d078e5a8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="msmergesessions-transact-sql"></a>MSmerge_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSmerge_sessions** -Tabelle enthält Verlaufszeilen mit den Ergebnissen des vorheriger auftragssitzungen des Merge-Agent. Bei jedem Ausführen des Merge-Agents wird der Tabelle eine neue Zeile hinzugefügt. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Die ID der Auftragssitzung des Merge-Agents|  
|**agent_id-Wert**|**int**|Die ID des Merge-Agents|  
|**start_time**|**datetime**|Der Zeitpunkt, zu dem die Ausführung des Auftrags begonnen hat|  
|**end_time**|**datetime**|Der Zeitpunkt, zu dem die Ausführung des Auftrags beendet wurde|  
|**duration**|**int**|Die kumulierte Dauer dieser Auftragssitzung in Sekunden|  
|**delivery_time**|**int**|Die Anzahl der Sekunden, die für die Anwendung eines Batches von Änderungen benötigt wurden.|  
|**upload_time**|**int**|Die Anzahl der Sekunden, die für das Hochladen von Änderungen auf den Verleger benötigt wurden.|  
|**download_time**|**int**|Die Anzahl der Sekunden, die für das Herunterladen von Änderungen auf den Abonnenten benötigt wurden.|  
|**delivery_rate**|**float**|Die durchschnittliche Anzahl der pro Sekunde übermittelten Befehle.|  
|**time_remaining**|**int**|Die geschätzte Anzahl der in einer aktiven Sitzung verbleibenden Sekunden.|  
|**percent_complete**|**decimal**|Der geschätzte Prozentsatz der gesamten Änderungen, die in einer aktiven Sitzung bereits übermittelt wurden|  
|**upload_inserts**|**int**|Die Anzahl der auf dem Verleger angewendeten Einfügungen.|  
|**upload_updates**|**int**|Die Anzahl der auf dem Verleger angewendeten Updates.|  
|**upload_deletes**|**int**|Die Anzahl der auf dem Verleger angewendeten Löschungen.|  
|**upload_conflicts**|**int**|Die Anzahl der Konflikte, die während der Anwendung von Änderungen auf dem Verleger aufgetreten sind.|  
|**upload_conflicts_resolved**|**int**|Die Anzahl der Konflikte, die während der Anwendung von Änderungen auf dem Verleger gelöst wurden.|  
|**upload_rows_retried**|**int**|Die Anzahl der auf den Verleger hochgeladenen Zeilen, deren Übermittlung wiederholt werden musste.|  
|**download_inserts**|**int**|Die Anzahl der auf dem Abonnenten angewendeten Einfügungen.|  
|**download_updates**|**int**|Die Anzahl der auf dem Abonnenten angewendeten Updates.|  
|**download_deletes**|**int**|Die Anzahl der auf dem Abonnenten angewendeten Löschungen.|  
|**download_conflicts**|**int**|Die Anzahl der Konflikte, die während der Anwendung von Änderungen auf dem Abonnenten aufgetreten sind.|  
|**download_conflicts_resolved**|**int**|Die Anzahl der Konflikte, die während der Anwendung von Änderungen auf dem Abonnenten gelöst wurden.|  
|**download_rows_retried**|**int**|Die Anzahl der auf den Abonnenten heruntergeladenen Zeilen, deren Übermittlung wiederholt werden musste.|  
|**schema_changes**|**int**|Die Anzahl der während der Sitzung angewendeten Schemaänderungen.|  
|**metadata_rows_cleanedup**|**int**|Die Anzahl der Zeilen mit Metadaten, für die während der Sitzung ein Cleanup ausgeführt wurde.|  
|**RunStatus**|**int**|Der Ausführungsstatus:<br /><br /> **1** = Start.<br /><br /> **2** = erfolgreich ausgeführt werden.<br /><br /> **3** = wird ausgeführt.<br /><br /> **4** = im Leerlauf.<br /><br /> **5** = wiederholen.<br /><br /> **6** = Fehler.|  
|**estimated_upload_changes**|**int**|Die geschätzte Anzahl von Änderungen, die auf dem Verleger angewendet werden mussten|  
|**estimated_download_changes**|**int**|Die geschätzte Anzahl von Änderungen, die auf dem Abonnenten angewendet werden mussten|  
|**connection_type**|**int**|Die während des Hochladens verwendete Verbindung:<br /><br /> **1** = lokale Netzwerk (LAN).<br /><br /> **2** = DFÜ-Netzwerkverbindung.<br /><br /> **3** = websynchronisierung.|  
|**timestamp**|**timestamp**|Die Timestampspalte dieser Tabelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
