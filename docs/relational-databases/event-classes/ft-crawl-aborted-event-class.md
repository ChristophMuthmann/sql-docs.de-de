---
title: "FT:Crawl Aborted (Ereignisklasse) | Microsoft Docs"
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
  - "Crawl Aborted-Ereignisklasse"
ms.assetid: eead8ea6-5051-4689-ab30-4dfbfda01fb9
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# FT:Crawl Aborted (Ereignisklasse)
  Die **FT:Crawl Aborted**-Ereignisklasse zeigt eine Ausnahme während einer Volltextdurchforstung an. Der Fehler führt normalerweise dazu, dass die Volltextdurchforstung beendet wird. Ausführlichere Fehlerinformationen finden Sie im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Ereignisprotokoll oder im Durchforstungsprotokoll.  
  
## Datenspalten der FT:Crawl Aborted-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID der Datenbank, in der die Volltextdurchforstung ausgeführt wird. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|**Fehler**|**int**|Fehlernummer eines bestimmten Ereignisses. Dies ist häufig die in der **sysmessages** -Tabelle gespeicherte Fehlernummer.|31|ja|  
|**EventClass**|**int**|Ereignistyp = 157.|27|Nein|  
|**EventSequence**|**int**|Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|Nein|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|**ObjectID**|**int**|Vom System zugewiesene ID des Objekts, für das die Volltextdurchforstung ausgeführt wird, wenn der Fehler auftritt.|22|ja|  
|**SessionLoginName**|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie z. B. mit Login1 eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und mit Login2 eine Anweisung ausführen, zeigt **SessionLoginName** Login1 an, und **LoginName** zeigt Login2 an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|Ja|  
|**SPID**|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|**StartTime**|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|**Status**|**int**|Gleichbedeutend mit einem Fehlerzustandscode.|30|ja|  
|**TransactionID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
  
## Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  