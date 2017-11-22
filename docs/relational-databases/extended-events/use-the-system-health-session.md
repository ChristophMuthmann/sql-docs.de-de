---
title: Verwenden der system_health-Sitzung | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: extended-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4bbc1316a33a9b534c7af3fc5fcf3605b6d4a392
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="use-the-systemhealth-session"></a>Verwenden der system_health-Sitzung
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Bei der system_health-Sitzung handelt es sich um eine standardmäßig in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthaltene Sitzung für erweiterte Ereignisse. Diese Sitzung wird automatisch beim Start von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gestartet und ohne merkliche Auswirkungen auf die Leistung ausgeführt. In der Sitzung werden Systemdaten erfasst, mit deren Hilfe Sie Leistungsprobleme in [!INCLUDE[ssDE](../../includes/ssde-md.md)]beheben können. Daher empfiehlt es sich, die Sitzung nicht zu beenden oder zu löschen.  
  
 In der Sitzung werden u. a. folgende Informationen erfasst:  
  
-   „sql_text“ und „session_id“ aller Sitzungen, in denen ein Fehler mit einem Schweregrad >= 20 aufgetreten ist.  
  
-   „sql_text“ und „session_id“ aller Sitzungen, in denen ein arbeitsspeicherbezogener Fehler aufgetreten ist. Zu diesen Fehlern zählen 17803, 701, 802, 8645, 8651, 8657 und 8902.  
  
-   Aufzeichnungen zu allen nicht gelösten Zeitplanungsproblemen. (Diese werden im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll als Fehler 17883 angezeigt.)  
  
-   Alle erkannten Deadlocks.  
  
-   „callstack“, „sql_text“ und „session_id“ aller Sitzungen, die > 15 Sekunden lang auf Latches (oder andere relevante Ressourcen) gewartet haben.  
  
-   „callstack“, „sql_text“ und „session_id“ aller Sitzungen, die > 30 Sekunden lang auf Sperren gewartet haben.  
  
-   „callstack“, „sql_text“ und „session_id“ aller Sitzungen, die lange auf präemptive Wartevorgänge gewartet haben. Die Dauer schwankt je nach Wartetyp. Bei einem präemptiven Wartevorgang wartet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf externe API-Aufrufe.  
  
-   Die Aufrufliste und session_id für Fehler bei der CLR-Belegung und virtuellen Belegung.  
  
-   Die ring_buffer-Ereignisse für den Speicherbroker, die Zeitplanungsmodul-Überwachung, Speicherknoten-OOMs sowie Sicherheit und Konnektivität.  
  
-   Die Systemkomponente ergibt sich aus sp_server_diagnostics.  
  
-   Mit scheduler_monitor_system_health_ring_buffer_recorded erfasster Zustand der Instanz.  
  
-   CLR-Belegungsfehler.  
  
-   Konnektivitätsfehler mit connectivity_ring_buffer_recorded.  
  
-   Sicherheitsfehler mit security_error_ring_buffer_recorded.  
  
## <a name="viewing-the-session-data"></a>Anzeigen der Sitzungsdaten  
 In der Sitzung werden die Daten im Ringpufferziel gespeichert. Zum Anzeigen der Sitzungsdaten verwenden Sie die folgende Abfrage:  
  
```  
SELECT CAST(xet.target_data as xml) FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe  
ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
Um die Sitzungsdaten aus der Ereignisdatei anzuzeigen, verwenden Sie die in Management Studio verfügbare Benutzeroberfläche für erweiterte Ereignisse. Weitere Informationen finden Sie unter [Erweiterte Ansicht von Zieldaten aus erweiterten Ereignissen in SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md).
  
## <a name="restoring-the-systemhealth-session"></a>Wiederherstellen der system_health-Sitzung  
 Wenn Sie die system_health-Sitzung gelöscht haben, können Sie diese wiederherstellen, indem Sie die Datei **u_tables.sql** im Abfrage-Editor ausführen. Diese Datei befindet sich im folgenden Ordner, wobei C: dem Laufwerk entspricht, auf dem Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Programmdateien installiert haben:  
  
 C:\Programme\Microsoft SQL Server\MSSQL13.\<*Instanz-ID*\MSSQL\Install  
  
 Wenn Sie die Sitzung wiederhergestellt haben, müssen Sie die Sitzung mit der ALTER EVENT SESSION-Anweisung oder über den Knoten **Erweiterte Ereignisse** im Objekt-Explorer starten. Andernfalls wird die Sitzung beim nächsten Neustart des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Diensts automatisch gestartet.  
  
## <a name="see-also"></a>Siehe auch  
 [Tools für erweiterte Ereignisse](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
