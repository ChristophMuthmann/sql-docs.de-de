---
title: MSsubscriber_schedule-(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MSsubscriber_schedule
- MSsubscriber_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_schedule system table
ms.assetid: ff428306-0ef4-49a3-b536-07ccdf6e2196
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e38c0d789862bc0e2464c74e0ff0ba438c32ffb3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mssubscriberschedule-transact-sql"></a>MSsubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **MSsubscriber_schedule** -Tabelle enthält standardmäßige Merge- und transaktionssynchronisierung Zeitpläne für jedes Verleger/Abonnent-Paar. Diese Tabelle wird in der Verteilungsdatenbank gespeichert.  
  
> [!NOTE]  
>  Diese Systemtabelle wurde als veraltet markiert und ist weiterhin für die Unterstützung von früher Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Der Name des Verlegers.|  
|**subscriber**|**sysname**|Den Namen des Abonnenten.|  
|**agent_type**|**smallint**|Der Agenttyp:<br /><br /> 0 = Verteilungs-Agent<br /><br /> 1 = Merge-Agent|  
|**frequency_type**|**int**|Die Häufigkeit für die Zeitplanung des Verteilungs-Agents:<br /><br /> **1** = einmalige Ausführung.<br /><br /> **2** = bedarfsgesteuert.<br /><br /> **4** = täglich.<br /><br /> **8** = wöchentlich.<br /><br /> **16** = monatlich.<br /><br /> **32** = mit relativem Monatsintervall.<br /><br /> **64** = Autostart.<br /><br /> **128** = wiederholt.|  
|**frequency_interval**|**int**|Der Wert der Häufigkeit festgelegt, die durch Anwenden **Frequency_type**.|  
|**frequency_relative_interval**|**int**|Das Datum des Verteilungs-Agents:<br /><br /> **1** = erster.<br /><br /> **2** = Sekunde.<br /><br /> **4** = Dritter.<br /><br /> **8** = vierter.<br /><br /> **16** = letzter.|  
|**frequency_recurrence_factor**|**int**|Von verwendete Wiederholungsfaktor **Frequency_type**.|  
|**frequency_subday**|**int**|Häufigkeit der erneuten Planung während des definierten Zeitraumes:<br /><br /> **1** = einmal.<br /><br /> **2** = Sekunde.<br /><br /> **4** = Minute.<br /><br /> **8** = Stunde.|  
|**frequency_subday_interval**|**int**|Das Intervall für **Frequency_subday**.|  
|**das Format HHMMSS verwendet**|**int**|Die Tageszeit, zu der der Einsatz des Verteilungs-Agents zum ersten Mal geplant wird (im Format HHMMSS).|  
|**das Format HHMMSS verwendet**|**int**|Die Tageszeit, zu der die Planung des Einsatzes des Verteilungs-Agents beendet wird (im Format HHMMSS).|  
|**active_start_date**|**int**|Das Datum, an dem der Einsatz des Verteilungs-Agents zum ersten Mal geplant wird (im Format YYYYMMDD).|  
|**active_end_date**|**int**|Das Datum, an dem die Planung des Einsatzes des Verteilungs-Agents beendet wird (im Format YYYYMMDD).|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
