---
title: Database Mirroring State Change-Ereignisklasse | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- database mirroring [SQL Server], event notifications
- Database Mirroring State Change event class
ms.assetid: f936a99e-2a81-4768-8177-5c969bbe2e04
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8a3f47ce8b68ebb6f81986044dcb1afafda1ecb2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="database-mirroring-state-change-event-class"></a>Database Mirroring State Change-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Durch die **Database Mirroring State Change** -Ereignisklasse wird angegeben, wann sich der Status einer gespiegelten Datenbank ändert. Schließen Sie diese Ereignisklasse in Ablaufverfolgungen ein, von denen die Zustände gespiegelter Datenbanken überwacht werden.  
  
 Wenn die **Database Mirroring State Change** -Ereignisklasse in einer Ablaufverfolgung eingeschlossen ist, ist der damit verbundene Verwaltungsaufwand gering. Der Verwaltungsaufwand wächst möglicherweise mit der Größe der gespiegelten Datenbanken.  
  
## <a name="data-database-mirroring-state-change-event-class-data-columns"></a>Data Database Mirroring State Change (Ereignisklasse-Datenspalten)  
  
|Name der Datenspalte|Datentyp|Description|Column ID|Filterbar|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|Die ID der Datenbank, die durch die USE *database* -Anweisung angegeben wurde, bzw. die ID der Standarddatenbank, wenn für eine bestimmte Instanz keine USE *database* -Anweisung ausgegeben wurde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|**DatabaseName**|**nvarchar**|Der Name der gespiegelten Datenbank.|35|ja|  
|**EventClass**|**int**|Ereignistyp = 167.|27|nein|  
|**EventSequence**|**int**|Die Sequenz der Ereignisklasse im Batch.|51|nein|  
|**IntegerData**|**int**|Die ID des vorherigen Status.|25|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|ja|  
|**LoginSid**|**image**|Sicherheits-ID (SID) des angemeldeten Benutzers. Diese Informationen finden Sie in der **sys.server_principals** -Katalogsicht. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|**RequestID**|**int**|Die ID der Anforderung, die die Anweisung enthält.|49|ja|  
|**ServerName**|**nvarchar**|Der Name der Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|**SessionLoginName**|**nvarchar**|Der Anmeldename des Benutzers, der die Sitzung gestartet hat. Wenn Sie z. B. mit Login1 eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen und mit Login2 eine Anweisung ausführen, zeigt **SessionLoginName** Login1 an, und **LoginName** zeigt Login2 an. Diese Spalte zeigt sowohl den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch den Windows-Anmeldenamen an.|64|ja|  
|**SPID**|**int**|Die ID der Sitzung, in der das Ereignis aufgetreten ist.|12|ja|  
|**StartTime**|**datetime**|Zeitpunkt, zu dem das Ereignis begonnen hat (falls vorhanden).|14|ja|  
|**Status**|**int**|Die neue Spiegelungsstatus-ID:<br /><br /> 0 = Nullbenachrichtigung<br /><br /> 1 = Synchronisierter Prinzipal mit Zeugen<br /><br /> 2 = Synchronisierter Prinzipal ohne Zeugen<br /><br /> 3 = Synchronisierter Spiegel mit Zeugen<br /><br /> 4 = Synchronisierter Spiegel ohne Zeugen<br /><br /> 5 = Verbindung zum Prinzipal verloren<br /><br /> 6 = Verbindung zum Spiegel verloren<br /><br /> 7 = Manuelles Failover<br /><br /> 8 = Automatisches Failover<br /><br /> 9 = Spiegelung angehalten<br /><br /> 10 = Kein Quorum<br /><br /> 11 = Spiegel wird synchronisiert<br /><br /> 12 = Ausgeführter Prinzipal offen gelegt|30|ja|  
|**TextData**|**ntext**|Die Beschreibung der Statusänderung.|1|ja|  
|**TransactionID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|ja|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
