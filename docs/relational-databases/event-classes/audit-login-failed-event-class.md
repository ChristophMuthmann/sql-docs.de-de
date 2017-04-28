---
title: Audit Login Failed-Ereignisklasse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Audit Login Failed event class
ms.assetid: 6b83963b-b685-429d-92ba-5173f6f0000d
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 732ae060110139e4f106c4745b104ef46a83ac74
ms.lasthandoff: 04/11/2017

---
# <a name="audit-login-failed-event-class"></a>Audit Login Failed-Ereignisklasse
  Die **Audit Login Failed** -Ereignisklasse zeigt an, dass ein Benutzer versucht hat, sich bei [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anzumelden, und dass die Anmeldung fehlgeschlagen ist. Ereignisse in dieser Klasse werden durch neue Verbindungen oder durch Verbindungen ausgelöst, die aus einem Verbindungspool wiederverwendet werden.  
  
## <a name="audit-login-failed-event-class-data-columns"></a>Datenspalten der Audit Login Failed-Ereignisklasse  
  
|Datenspaltenname|Datentyp|Beschreibung|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Name der Clientanwendung, die die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|10|ja|  
|**ClientProcessID**|**int**|Die ID, die der Hostcomputer dem Prozess zuweist, in dem die Clientanwendung ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn die Clientprozess-ID durch den Client bereitgestellt wird.|9|ja|  
|**DatabaseID**|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|**DatabaseName**|**nvarchar**|Name der Datenbank, in der die Benutzeranweisung ausgeführt wird.|35|Ja|  
|**Fehler**|**int**|Fehlernummer eines bestimmten Ereignisses. Dies ist häufig die in der **sys.messages** -Katalogsicht gespeicherte Fehlernummer.|31|ja|  
|**EventClass**|**int**|Ereignistyp = 20.|27|Nein|  
|**EventSequence**|**int**|Die Sequenz eines bestimmten Ereignisses innerhalb der Anforderung.|51|Nein|  
|**HostName**|**nvarchar**|Der Name des Computers, auf dem der Client ausgeführt wird. Diese Datenspalte wird aufgefüllt, wenn der Hostname durch den Client bereitgestellt wird. Der Hostname kann mithilfe der HOST_NAME-Funktion bestimmt werden.|8|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|**LoginName**|**nvarchar**|Anmeldename des Benutzers ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsanmeldung oder Windows-Anmeldeinformationen im Format DOMAIN\username).|11|ja|  
|**NTDomainName**|**nvarchar**|Windows-Domäne, zu der der Benutzer gehört.|7|ja|  
|**NTUserName**|**nvarchar**|Windows-Benutzername.|6|ja|  
|**RequestID**|**int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|**ServerName**|**nvarchar**|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, für die eine Ablaufverfolgung ausgeführt wird.|26|Nein|  
|**SessionLoginName**|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie z. B. mit Login1 eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und mit Login2 eine Anweisung ausführen, zeigt **SessionLoginName** Login1 an, und **LoginName** zeigt Login2 an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|**SPID**|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|**StartTime**|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|Ja|  
|**Success**|**int**|1 = Erfolg 0 = Fehler. Dieses Ereignis zeigt immer einen Fehler an.|23|Ja|  
|**TextData**|**ntext**|Textwert, der von der Ereignisklasse abhängt, die in der Ablaufverfolgung aufgezeichnet wurde.|1|ja|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
