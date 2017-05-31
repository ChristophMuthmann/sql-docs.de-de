---
title: PreConnect:Starting-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de236e420c1f8f754b4af60a6710a0e9fafc7acf
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="preconnectstarting-event-class"></a>PreConnect:Starting-Ereignisklasse
  Die PreConnect:Starting-Ereignisklasse zeigt an, dass die Ausführung eines LOGON-Triggers oder der Klassifizierungsfunktion der Ressourcenkontrolle beginnt.  
  
## <a name="preconnectstarting-event-class-data-columns"></a>Datenspalten der PreConnect:Starting-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|215|27|Nein|  
|SPID|**int**|Die ID des Serverprozesses, von dem das Ereignis ausgelöst wird.|12|ja|  
|EventSubClass|**int**|1 für die benutzerdefinierte Klassifizierungsfunktion.|21|ja|  
|StartTime|**datetime**|Der Zeitpunkt, an dem die benutzerdefinierte Klassifizierungsfunktion beginnt.|14|ja|  
|ObjectID|**int**|Die ID des benutzerdefinierten Klassifizierungsobjekts.|22|Ja|  
|ObjectName|**nvarchar(256)**|Der zweiteilige Name der benutzerdefinierten Klassifizierungsfunktion. Beispiel: dbo.classifier.|34|ja|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [PreConnect:Completed (Ereignisklasse)](../../relational-databases/event-classes/preconnect-completed-event-class.md)   
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)  
  
  
