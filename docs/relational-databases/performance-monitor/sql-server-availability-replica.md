---
title: "SQL Server, Verfügbarkeitsreplikat | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 327b70f445a9f794152073a39059165f75fd3cad
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-availability-replica"></a>SQL Server, Verfügbarkeitsreplikat
  Das Leistungsobjekt **SQLServer:Availability Replica** enthält Leistungsindikatoren, die Informationen zu den Verfügbarkeitsreplikaten in Always On-Verfügbarkeitsgruppen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bereitstellen. Alle Leistungsindikatoren für Verfügbarkeitsreplikate gelten für das primäre Replikat und auch für die sekundären Replikate, wobei Sende-/Empfangs-Zähler das lokale Replikat wiedergeben. Normalerweise sendet das primäre Replikat die meisten Daten, und die sekundären Replikate empfangen die Daten. Sekundäre Replikate senden jedoch ACKs und weiteren Hintergrunddatenverkehr an die primären Replikate. Auf jedem Verfügbarkeitsreplikat zeigen einige Leistungsindikatoren in Abhängigkeit von der aktuellen Rolle des lokalen Replikats (primär oder sekundär) den Wert 0 an.  
  
|Indikatorname|Beschreibung|  
|------------------|-----------------|  
|**Vom Replikat empfangene Bytes/s**|Anzahl von Bytes, die pro Sekunde vom Verfügbarkeitsreplikat empfangen werden. Durch Pingbefehle und Statusupdates wird selbst für Datenbanken ohne Benutzerupdates Netzwerkdatenverkehr generiert.|  
|**An das Replikat gesendete Bytes/s**|Anzahl von Bytes, die pro Sekunde an das Remoteverfügbarkeitsreplikat gesendet werden. Auf dem primären Replikat ist dies die Anzahl von an das sekundäre Replikat gesendeten Bytes. Auf dem sekundären Replikat ist dies die Anzahl von an das primäre Replikat gesendeten Bytes.|  
|**An den Transport gesendete Bytes/s**|Tatsächliche Anzahl von Bytes, die pro Sekunde über das Netzwerk an das Remoteverfügbarkeitsreplikat gesendet werden. Auf dem primären Replikat ist dies die Anzahl von an das sekundäre Replikat gesendeten Bytes. Auf dem sekundären Replikat ist dies die Anzahl von an das primäre Replikat gesendeten Bytes.|  
|**Flussteuerungsdauer (ms/sek)**|Zeit in Millisekunden, die die Protokolldatenstrom-Meldungen in der letzten Sekunde auf Sendedatenfluss-Steuerung gewartet haben.|  
|**Flusssteuerung/s**|Häufigkeit der Initiierungsvorgänge für die Flusssteuerung in der letzten Sekunde. **Flussteuerungsdauer (ms/sek)** geteilt durch **Flusssteuerung/s** entspricht der durchschnittlichen Zeit pro Wartevorgang.|  
|**Replikat-Empfangsvorgänge/s**|Anzahl von Always On-Nachrichten, die pro Sekunde vom Replikat empfangen werden.|  
|**Erneut gesendete Nachrichten/s**|Anzahl von Always On-Nachrichten, die in der letzten Sekunde erneut gesendet wurden.|  
|**Replikat-Sendevorgänge/s**|Anzahl von Always On-Nachrichten, die pro Sekunde an dieses Verfügbarkeitsreplikat gesendet werden.|  
|**Transport-Sendevorgänge/s**|Tatsächliche Anzahl von Always On-Nachrichten, die pro Sekunde über das Netzwerk an das Remoteverfügbarkeitsreplikat gesendet werden. Auf dem primären Replikat ist dies die Anzahl von an das sekundäre Replikat gesendeten Nachrichten. Auf dem sekundären Replikat ist dies die Anzahl von an das primäre Replikat gesendeten Nachrichten.|  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Datenbankreplikat](../../relational-databases/performance-monitor/sql-server-database-replica.md)   
 [Always On-Verfügbarkeitsgruppen (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)  
  
  

