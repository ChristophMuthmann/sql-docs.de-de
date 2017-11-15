---
title: Trace File Close-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Trace File Close event class
ms.assetid: 128b7bac-cb64-43e7-ae9b-87b7d2ebb4ef
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4478bfd117f1388d0372081cf76018786d8e9919
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="trace-file-close-event-class"></a>Trace File Close-Ereignisklasse
  Die **Trace File Close** -Ereignisklasse weist darauf hin, dass eine Ablaufverfolgungsdatei während eines Rollovers für Ablaufverfolgungsdateien geschlossen wurde.  
  
## <a name="trace-file-close-event-class-data-columns"></a>Trace File Close-Ereignisklasse (Datenspalten)  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**EventClass**|**int**|Ereignistyp = 150.|27|Nein|  
|**EventSequence**|**int**|Eindeutiger Timestamp des Ereignisses, das während der Ablaufverfolgung ausgelöst wurde. Diese Zahl erhöht sich bei jedem ausgelösten Ereignis gleichmäßig.|51|Nein|  
|**FileName**|**nvarchar**|Logischer Name der geschlossenen Ablaufverfolgungsdatei.|36|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, NULL = Benutzer. Bei dieser Ereignisklasse beläuft sich der Wert immer auf 1.|60|ja|  
|**LoginName**|**nvarchar**|Der Anmeldename des Benutzers ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsanmeldung oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen im Format DOMAIN\username). Bei dieser Ereignisklasse lautet der Wert immer "sa".|11|ja|  
|**ObjectID**|**int**|Vom System zugewiesene ID der Ablaufverfolgung.|22|Ja|  
|**ServerName**|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|Nein|  
|**SessionLoginName**|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie z. B. mit Login1 eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und mit Login2 eine Anweisung ausführen, zeigt **SessionLoginName** Login1 an, und **LoginName** zeigt Login2 an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|**SPID**|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|**StartTime**|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
