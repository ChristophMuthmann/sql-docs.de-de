---
title: "Überwachungsvolltextereignisklasse | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 95e4c5fd-e16f-446e-b42b-105495a8f39a
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 847a78fe4a4587d201909290b771e7357cd7a956
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="audit-fulltext-event-class"></a>Überwachungsvolltextereignisklasse
  Die **Audit Fulltext** -Ereignisklasse tritt auf, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Verbindung mit dem Volltextfilterdaemon-Prozess herstellt und mit diesem kommuniziert.  
  
## <a name="audit-fulltext-event-class-data-columns"></a>Überwachungsvolltextereignisklasse – Datenspalten  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**Fehler**|**int**|Wenn dieses Ereignis einen Fehler meldet, ist dies die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlernummer.|31|ja|  
|**EventSequence**|**int**|Die Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|Nein|  
|**EventSubClass**|**int**|Der Typ der bei der Anmeldung verwendeten Verbindung. 1 = Nicht im Pool, 2 = Im Pool.|21|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|**SessionLoginName**|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie z. B. mit Login1 eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und mit Login2 eine Anweisung ausführen, zeigt **SessionLoginName** Login1 an, und **LoginName** zeigt Login2 an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|**SPID**|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|**StartTime**|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|**Success**|**int**|1 = Erfolg 0 = Fehler. Der Wert 1 deutet beispielsweise auf eine erfolgreiche Überprüfung der Berechtigungen hin, während die Überprüfung bei dem Wert 0 fehlgeschlagen ist.|23|ja|  
|**TargetLoginName**|**int**|Für Aktionen, die auf einen Anmeldenamen abzielen (z. B. das Hinzufügen eines neuen Anmeldenamens), der Anmeldename, auf den abgezielt wird.|42|ja|  
|**TargetLoginSid**|**int**|Für Aktionen, die auf einen Anmeldenamen abzielen (z. B. das Hinzufügen eines neuen Anmeldenamens), die Sicherheits-ID (SID), auf die abgezielt wird.|43|ja|  
|**TextData**|**ntext**|Textinformationen zum Volltextereignis. In der Regel enthält dieses Feld Informationen zur Verbindung zwischen dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess und dem Volltextfilterdaemonprozess.|1|ja|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
