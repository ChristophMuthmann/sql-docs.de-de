---
title: MSdistribution_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSdistribution_history
- MSdistribution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_history system table
ms.assetid: 55665bd2-9e1d-4efc-8f60-c63a24f66b28
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7196fcd36a995b0e1e8feb3f7436d1f634da375c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="msdistributionhistory-transact-sql"></a>MSdistribution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSdistribution_history** -Tabelle enthält Verlaufszeilen für die Verteilungs-Agents mit dem lokalen Verteiler zugeordneten. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
## <a name="definition"></a>Definition  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|Die ID des Verteilungs-Agents.|  
|**RunStatus**|**int**|Der Status wird ausgeführt:<br /><br /> **1** = Start.<br /><br /> **2** = erfolgreich ausgeführt werden.<br /><br /> **3** = wird ausgeführt.<br /><br /> **4** = im Leerlauf.<br /><br /> **5** = wiederholen.<br /><br /> **6** = Fehler.|  
|**start_time**|**datetime**|Der Zeitpunkt, zu dem mit der Ausführung des Auftrags begonnen wird.|  
|**Uhrzeit**|**datetime**|Der Zeitpunkt der Protokollierung der Meldung.|  
|**duration**|**int**|Die Dauer der Meldungssitzung in Sekunden.|  
|**Kommentare**|**nvarchar(4000)**|Der Meldungstext.|  
|**xact_seqno**|**varbinary(16)**|Die Sequenznummer der zuletzt verarbeiteten Transaktion.|  
|**current_delivery_rate**|**float**|Die durchschnittliche Anzahl der Befehle, die seit dem letzten Verlaufseintrag pro Sekunde übermittelt wurden.|  
|**current_delivery_latency**|**int**|Die Latenzzeit zwischen dem Eintritt des Befehls in die Verteilungsdatenbank und seiner Anwendung auf den Abonnenten seit dem letzten Verlaufseintrag. In Millisekunden|  
|**delivered_transactions**|**int**|Die Gesamtzahl der in der Sitzung übermittelten Transaktionen.|  
|**delivered_commands**|**int**|Die Gesamtzahl der in der Sitzung übermittelten Befehle.|  
|**average_commands**|**int**|Die durchschnittliche Anzahl der in der Sitzung übermittelten Befehle.|  
|**delivery_rate**|**float**|Die durchschnittliche Anzahl der pro Sekunde übermittelten Befehle.|  
|**delivery_latency**|**int**|Die Latenzzeit zwischen dem Eintritt des Befehls in die Verteilungsdatenbank und seiner Anwendung auf den Abonnenten. In Millisekunden|  
|**total_delivered_commands**|**bigint**|Die Gesamtzahl der seit der Erstellung des Abonnements übermittelten Befehle.|  
|**Fehler-ID**|**int**|Die ID des Fehlers in der **MSrepl_error** -Systemtabelle.|  
|**updateable_row**|**bit**|Legen Sie auf **1** Wenn die Verlaufszeile überschrieben werden kann.|  
|**timestamp**|**timestamp**|Die Timestampspalte dieser Tabelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
