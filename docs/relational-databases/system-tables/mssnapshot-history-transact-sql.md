---
title: MSsnapshot_history (Transact-SQL) | Microsoft Docs
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
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c5360a12d9606df310fe5e6e46c6aaaaf34f6f37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshothistory-transact-sql"></a>MSsnapshot_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSsnapshot_history** -Tabelle enthält Verlaufszeilen für die Momentaufnahme-Agents mit dem lokalen Verteiler zugeordneten. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|Die ID des Momentaufnahme-Agents.|  
|**RunStatus**|**int**|Der Ausführungsstatus:<br /><br /> **1** = Start.<br /><br /> **2** = erfolgreich ausgeführt werden.<br /><br /> **3** = wird ausgeführt.<br /><br /> **4** = im Leerlauf.<br /><br /> **5** = wiederholen.<br /><br /> **6** = Fehler.|  
|**start_time**|**datetime**|Der Zeitpunkt, zu dem mit der Ausführung des Auftrags begonnen wird.|  
|**Uhrzeit**|**datetime**|Der Zeitpunkt der Protokollierung der Meldung.|  
|**duration**|**int**|Die Dauer der Meldungssitzung in Sekunden.|  
|**Kommentare**|**nvarchar(255)**|Der Meldungstext.|  
|**delivered_transactions**|**int**|Die Gesamtzahl der in der Sitzung übermittelten Transaktionen.|  
|**delivered_commands**|**int**|Die Anzahl der pro Sekunde übermittelten Befehle.|  
|**delivery_rate**|**float(53)**|Die durchschnittliche Anzahl der pro Sekunde übermittelten Befehle.|  
|**Fehler-ID**|**int**|Die ID des Fehlers in der [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) -Systemtabelle.|  
|**timestamp**|**timestamp**|Die Timestampspalte dieser Tabelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
