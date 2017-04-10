---
title: "PreConnect:Starting-Ereignisklasse | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "PreConnect:Starting-Ereignisklasse"
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# PreConnect:Starting-Ereignisklasse
  Die PreConnect:Starting-Ereignisklasse zeigt an, dass die Ausführung eines LOGON-Triggers oder der Klassifizierungsfunktion der Ressourcenkontrolle beginnt.  
  
## Datenspalten der PreConnect:Starting-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|Nein|  
|SPID|**int**|Die ID des Serverprozesses, von dem das Ereignis ausgelöst wird.|12|ja|  
|EventSubClass|**int**|1 für die benutzerdefinierte Klassifizierungsfunktion.|21|ja|  
|StartTime|**datetime**|Der Zeitpunkt, an dem die benutzerdefinierte Klassifizierungsfunktion beginnt.|14|ja|  
|ObjectID|**int**|Die ID des benutzerdefinierten Klassifizierungsobjekts.|22|ja|  
|ObjectName|**nvarchar(256)**|Der zweiteilige Name der benutzerdefinierten Klassifizierungsfunktion. Beispiel: dbo.classifier.|34|ja|  
  
## Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [PreConnect:Completed (Ereignisklasse)](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)  
  
  