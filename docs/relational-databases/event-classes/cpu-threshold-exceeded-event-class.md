---
title: "CPU Threshold Exceeded (Ereignisklasse) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "CPU Threshold Exceeded (Ereignisklasse)"
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# CPU Threshold Exceeded (Ereignisklasse)
  Die CPU Threshold Exceeded-Ereignisklasse zeigt an, dass die Ressourcenkontrolle eine Abfrage entdeckt hat, die den für REQUEST_MAX_CPU_TIME_SEC festgelegten CPU-Grenzwert überschritten hat.  
  
> [!NOTE]  
>  Das Erkennungsintervall für dieses Ereignis beträgt fünf Sekunden. Es wird auf jeden Fall ein Ereignis erzeugt, wenn eine Abfrage den festgelegten Grenzwert um mindestens fünf Sekunden überschreitet. Falls jedoch eine Abfrage den festgelegten Grenzwert um weniger als fünf Sekunden überschreitet, kann es sein, dass die Überschreitung je nach Zeitpunkt der Abfrage und dem Zeitpunkt des letzten Erkennungslaufs nicht erkannt wird.  
  
## Datenspalten der CPU Threshold Exceeded-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|**int**|CPU-Verwendung in Millisekunden|18|ja|  
|EventClass|**int**|214|27|Nein|  
|EventSubClass|**int**|CPU-Grenzwertüberschreitung|21|ja|  
|GroupID|**int**|ID der Gruppe, in der die Überschreitung aufgetreten ist|66|ja|  
|OwnerID|**int**|SPID des Prozesses, der die Überschreitung verursacht hat|58|ja|  
|SPID|**int**|ID des Serverprozesses, von dem das Ereignis ausgelöst wird<br /><br /> Hinweis: Diese SPID kann sich von der tatsächlichen Benutzer-SPID unterscheiden, wenn die CPU-Verwendung von einem Systemthread als Hintergrundaufgabe überprüft wird.|12|ja|  
|StartTime|**datetime**|Zeitpunkt, zu dem das Ereignis ausgelöst wurde|14|ja|  
  
## Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  