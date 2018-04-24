---
title: SQL Server, Broker/DBM-Transport-Objekt | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: caedbed7827753bcd099103d6d70d4f99d447048
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-broker---dbm-transport-object"></a>SQL Server, Broker/DBM-Transport-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das **Broker/DBM-Transport**-Leistungsobjekt enthält Leistungsindikatoren, die Netzwerkinformationen für Service Broker und die Datenbankspiegelung melden. In der nachfolgenden Tabelle sind die in diesem Objekt enthaltenen Indikatoren aufgelistet.  
  
|SQL Server, Broker/DBM-Transport-Leistungsindikator|Description|  
|------------------------------------------------|-----------------|  
|**Aktuelle Bytes für E/A-Empfangsvorgänge**|Dieser Leistungsindikator gibt die Anzahl der Bytes an, die von den aktuell ausgeführten Transportempfangsvorgängen gelesen werden müssen.|  
|**Aktuelle Bytes für E/A-Sendungen**|Dieser Leistungsindikator gibt die Anzahl der Bytes in Nachrichtenfragmenten an, die aktuell über das Netzwerk gesendet werden.|  
|**Aktuelle Nachrichtenfragmente für E/A-Sendungen**|Dieser Leistungsindikator gibt die Gesamtanzahl der Nachrichtenfragmente an, die über das Netzwerk gesendet werden.|  
|**P1-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 1 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P2-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 2 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P3-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 3 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P4-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 4 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P5-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 5 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P6-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 6 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P7-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 7 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P8-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 8 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P9-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 9 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**P10-Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente mit Priorität 10 an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**Nachrichtenfragment-Empfangsvorgänge/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente an, die pro Sekunde über das Netzwerk empfangen werden.|   
|**Nachrichtenfragmente gesendet/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente aller Prioritäten an, die pro Sekunde über das Netzwerk gesendet werden.|  
|**Durchschn. Größe von empfangenen Nachrichtenfragmenten**|Dieser Leistungsindikator gibt die durchschnittliche Größe der Nachrichtenfragmente an, die über das Netzwerk empfangen wurden.|  
|**Msg Fragment Recv Size Avg Base**|Nur zur internen Verwendung.| 
|**Durchschn. Größe gesendeter Nachrichtenfragmente**|Dieser Leistungsindikator gibt die durchschnittliche Größe der Nachrichtenfragmente an, die über das Netzwerk gesendet werden.|  
|**Basis für durchschn. Größe gesendeter Nachrichtenfragmente**|Nur zur internen Verwendung.|
|**Anzahl der geöffneten Verbindungen**|Dieser Leistungsindikator gibt die Anzahl der Netzwerkverbindungen an, die Service Broker aktuell geöffnet hat.|  
|**Ausstehende Bytes für E/A-Empfangsvorgänge**|Dieser Leistungsindikator gibt die Anzahl der Bytes an, die in Nachrichtenfragmenten enthalten sind, die zwar über das Netzwerk empfangen, jedoch noch nicht in einer Warteschlange gespeichert oder verworfen wurden.|  
|**Ausstehende Bytes für E/A-Sendevorgänge**|Dieser Leistungsindikator gibt die Gesamtanzahl der Bytes in Nachrichtenfragmenten an, die für das Senden über das Netzwerk bereit sind.|  
|**Ausstehende Nachrichtenfragmente für E/A-Empfangsvorgänge**|Dieser Leistungsindikator gibt die Anzahl der Nachrichtenfragmente an, die zwar über das Netzwerk empfangen, jedoch noch nicht in einer Warteschlange gespeichert oder verworfen wurden.|  
|**Ausstehende Nachrichtenfragmente für E/A-Sendevorgänge**|Dieser Leistungsindikator gibt die Gesamtanzahl der Nachrichtenfragmente an, die für das Senden über das Netzwerk bereit sind.|  
|**Bytes von E/A-Empfangsvorgängen/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der pro Sekunde über das Netzwerk von Service Broker- und Datenbankspiegelungs-Endpunkten empfangenen Bytes an.|  
|**Bytes von E/A-Empfangsvorgängen gesamt**|Dieser Leistungsindikator gibt die Gesamtanzahl der über das Netzwerk von Service Broker- und Datenbankspiegelungs-Endpunkten empfangenen Bytes an.|  
|**Durchschn. Länge von E/A-Empfangsvorgängen**|Dieser Leistungsindikator gibt die durchschnittliche Anzahl der Bytes für einen Transportempfangsvorgang an.|  
|**Basis für durchschn. Länge empfangener E/A**|Nur zur internen Verwendung.|
|**E/A empfangen/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der E/A-Transportempfangsvorgänge pro Sekunde an, die die Service Broker- bzw. DBM-Transportschicht abgeschlossen hat. Beachten Sie, dass ein Transportempfangsvorgang mehrere Nachrichtenfragmente enthalten kann.|  
|**Bytes von empfangenen E/A-Pufferkopien/Sekunde**|Die Rate, mit der Pufferfragmente im Speicher durch E/A-Transportempfangsvorgänge verschoben werden mussten.|
|**Anzahl empfangener E/A-Pufferkopien**|Die Anzahl von Verschiebungen von Pufferfragmenten im Speicher durch E/A-Transportempfangsvorgänge.| 
|**Bytes von E/A-Sendungen/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der von Service Broker- und Datenbankspiegelungs-Endpunkten über das Netzwerk gesendeten Bytes pro Sekunde an.|   
|**Bytes von E/A-Sendungen gesamt**|Dieser Leistungsindikator gibt die Gesamtanzahl der von Service Broker- und Datenbankspiegelungs-Endpunkten über das Netzwerk gesendeten Bytes an.| 
|**Durchschn. E/A-Sendelänge**|Dieser Leistungsindikator gibt die durchschnittliche Größe in Byte für jeden Transportsendevorgang an. Beachten Sie, dass ein Transportsendevorgang mehrere Nachrichtenfragmente enthalten kann.|  
|**Basis für durchschn. Länge gesendeter E/A**|Nur zur internen Verwendung.|
|**E/A-Sendungen/Sekunde**|Dieser Leistungsindikator gibt die Anzahl der E/A-Transportsendevorgänge pro Sekunde an, die abgeschlossen wurden. Beachten Sie, dass ein Transportsendevorgang mehrere Nachrichtenfragmente enthalten kann.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
