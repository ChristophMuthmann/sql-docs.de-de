---
title: SQL Server, Datenbankreplikat | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fc96130b21ccef9c95dbe8172ef5ef4fc5185616
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-database-replica"></a>SQL Server, Datenbankreplikat
  Das **SQLServer:Datenbankreplikat**-Leistungsobjekt enthält Leistungsindikatoren, die Informationen zu den sekundären Datenbanken einer Always On-Verfügbarkeitsgruppe in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bereitstellen. Dieses Objekt ist auf nur einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz gültig, die ein sekundäres Replikat hostet.  
  
|Indikatorname|Beschreibung|Anzeige für|  
|------------------|-----------------|--------------|  
|**Empfangene Dateibytes/s**|Die Menge der FILESTREAM-Daten, die vom sekundären Replikat für die sekundäre Datenbank in der letzten Sekunde empfangen wurde.|Sekundäres Replikat|  
|**Warteschlange für ausstehende Protokollanwendung**|Anzahl der Protokollblöcke, die darauf warten, in das Datenbankreplikat übernommen zu werden.|Sekundäres Replikat|
|**Warteschlange für bereite Protokollanwendung**|Anzahl der Protokollblöcke, die bereit sind und darauf warten, in das Datenbankreplikat übernommen zu werden.|Sekundäres Replikat| 
|**Empfangene Protokollbytes/s**|Die Menge der Protokolldatensätze, die vom sekundären Replikat für die Datenbank in der letzten Sekunde empfangen wurde.|Sekundäres Replikat|  
|**Verbleibendes Protokoll für Rollbackphase**|Entspricht der Menge an Protokollen in Kilobytes, die für das Ausführen der Rollbackphase verbleiben.|Sekundäres Replikat|  
|**Protokollsendewarteschlange**|Die Menge der Protokolldatensätze in den Protokolldateien der primären Datenbank, die noch nicht an das sekundäre Replikat gesendet wurden. Dieser Wert wird vom primären Replikat an das sekundäre Replikat gesendet. Die Warteschlangengröße umfasst keine FILESTREAM-Dateien, die an ein sekundäres Replikat gesendet wurden.|Sekundäres Replikat|  
|**Gespiegelte Schreibtransaktionen/Sekunde**|Anzahl von Transaktionen, die in die primäre Datenbank geschrieben und beim Senden des Protokolls an die sekundäre Datenbank commitet wurden (in der letzten Sekunde).|Primäres Replikat|  
|**Wiederherstellungswarteschlange**|Menge an Protokolldatensätzen in den Protokolldateien des sekundären Replikats, das noch nicht wiederholt wurde.|Sekundäres Replikat|  
|**Blockierte Wiederholungen/s**|Häufigkeit der Blockierung des REDO-Threads für Sperren von Lesern der Datenbank.|Sekundäres Replikat|  
|**Verbleibende Wiederholungsbytes**|Die verbleibende Protokollmenge in Kilobytes bis zum Abschließen der Wiederherstellungsphase.|Sekundäres Replikat|  
|**Wiederholte Bytes/s**|Menge an Protokolldatensätzen, die in der letzten Sekunde auf der sekundären Datenbank wiederholt wurden.|Sekundäres Replikat|  
|**Rückgängig zu machendes Gesamtprotokoll**|Gesamtanzahl an Kilobytes von Protokollen, die rückgängig zu machen sind.|Sekundäres Replikat|  
|**Transaktionsverzögerung**|Entspricht der Verzögerung beim Warten auf nicht abgeschlossene Commit-Bestätigungen in Millisekunden.|Primäres Replikat|  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Verfügbarkeitsreplikat](../../relational-databases/performance-monitor/sql-server-availability-replica.md)   
 [SQL Server, Datenbanken-Objekt](../../relational-databases/performance-monitor/sql-server-databases-object.md)   
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  

