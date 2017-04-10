---
title: "Deadlock Graph (Ereignisklasse) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Deadlock Graph (Ereignisklasse)"
ms.assetid: 20f92233-c912-4382-8993-8e2e23d03fbe
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# Deadlock Graph (Ereignisklasse)
  Die **Deadlock Graph** -Ereignisklasse stellt eine XML-Beschreibung für ein Deadlock bereit. Diese Klasse tritt zusammen mit der **Lock:Deadlock** -Ereignisklasse auf.  
  
## Deadlock Graph-Ereignisklasse (Datenspalten)  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**EventClass**|**int**|Ereignistyp = 148.|27|Nein|  
|**EventSequence**|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|Nein|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer. Bei diesem Ereignis ist der Wert immer 1.|60|Ja|  
|**LoginName**|**nvarchar**|Anmeldename des Benutzers (Anmeldung der [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherheit oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format „DOMAIN\username“). Bei diesem Ereignis ist der Wert immer mit dem Systembenutzer identisch.|11|Ja|  
|**LoginSid**|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der sys.server_principals-Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig. Bei diesem Ereignis ist der Wert immer mit der SID des Systembenutzers identisch.|41|ja|  
|**ServerName**|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|Nein|  
|**SessionLoginName**|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie z. B. mit Login1 eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und mit Login2 eine Anweisung ausführen, zeigt **SessionLoginName** Login1 an, und **LoginName** zeigt Login2 an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|Ja|  
|**SPID**|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|**StartTime**|**datetime**|Der Zeitpunkt, an dem der Deadlock entdeckt wurde.|14|ja|  
|**TextData**|**ntext**|XML-Beschreibung des Deadlocks.|1|Ja|  
|**TransactionID**|**bigint**|Wird nicht verwendet.|4|ja|  
  
## Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Lock:Deadlock (Ereignisklasse)](../../relational-databases/event-classes/lock-deadlock-event-class.md)  
  
  