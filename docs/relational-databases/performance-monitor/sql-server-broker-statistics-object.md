---
title: SQL Server, Broker-Statistik-Objekt | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- SQLServer:Broker Statistics
- Broker Statistics object
ms.assetid: e9e36f01-93f6-4e6e-90c6-c7f3fd121737
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3f58dcbb8e87608fa8499f57d14caec77de3b7b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-broker-statistics-object"></a>SQL Server, Broker-Statistik-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das SQLServer:Broker-Leistungsobjekt enthält Leistungsindikatoren mit allgemeinen Informationen zu [!INCLUDE[ssSB](../../includes/sssb-md.md)] für eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]. In der folgenden Tabelle sind die in diesem Objekt enthaltenen Indikatoren aufgelistet:  
  
|Broker-Statistik-Leistungsindikatoren in SQL Server|Description|  
|-------------------------------------------|-----------------|  
|**Aktivierungsfehler gesamt**|Die Häufigkeit, mit der eine gespeicherte [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Aktivierungsprozedur mit einem Fehler beendet wurde.|  
|**Broker-Transaktionsrollbacks**|Die Anzahl von Transaktionen, die auf [!INCLUDE[ssSB](../../includes/sssb-md.md)]bezogene DML-Anweisungen enthalten, für die ein Rollback ausgeführt wurde, z. B. SEND und RECEIVE.|  
|**Beschädigte Nachrichten gesamt**|Die Anzahl von beschädigten Nachrichten, die von der Instanz empfangen wurden.|  
|**Aus Übertragungswarteschlange entfernte Nachr./s**|Die Anzahl von Nachrichten, die pro Sekunde aus der [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Warteschlange entfernt wurden.|  
|**Anzahl der Dialogzeitgeberereignisse**|Die Anzahl der aktiven Zeitgeber der Dialogprotokollschicht. Dies entspricht der Anzahl der aktiven Dialoge.|  
|**Gelöschte Nachrichten gesamt**|Die Anzahl von beschädigten Nachrichten, die von der Instanz empfangen wurden, aber nicht an die Warteschlange übermittelt werden konnten.|  
|**Lokale Nachrichten in Warteschlangen gesamt**|Die Anzahl der Nachrichten, die in dieser Instanz in Warteschlangen eingereiht wurden, wobei nur die Nachrichten berücksichtigt werden, die nicht über das Netzwerk eingetroffen sind.|  
|**Lokale Nachrichten in Warteschlangen/Sekunde**|Die Anzahl der Nachrichten pro Sekunde, die in dieser Instanz in Warteschlangen gestellt wurden, wobei nur die Nachrichten berücksichtigt werden, die nicht über das Netzwerk eingetroffen sind.|  
|**Nachrichten in Warteschlangen gesamt**|Die Gesamtanzahl der Nachrichten, die in die Warteschlangen der Instanz gestellt wurden.|  
|**Nachrichten in Warteschlangen/Sekunde**|Die Anzahl der Nachrichten pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden. Dazu zählen Nachrichten aller Prioritätsebenen.|  
|**P1-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 1 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P2-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 2 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P3-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 3 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P4-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 4 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P5-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 5 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P6-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 6 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P7-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 7 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P8-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 8 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P9-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 9 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**P10-Nachrichten in Warteschlange/Sekunde**|Die Anzahl der Nachrichten mit Priorität 10 pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**In Übertragungswarteschlange eingereihte Nachr./Sek**|Die Anzahl von Nachrichten, die pro Sekunde in der [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Übertragungswarteschlange platziert wurden.|  
|**Transportnachrichtenfragmente in Warteschlangen gesamt**|Die Anzahl der Nachrichtenfragmente, die in dieser Instanz in Warteschlangen gestellt wurden, wobei nur die Nachrichten berücksichtigt werden, die über das Netzwerk eingetroffen sind.|  
|**Transportnachrichtenfragmente in Warteschlangen/Sekunde**|Die Anzahl der Nachrichtenfragmente pro Sekunde, die in die Warteschlangen der Instanz gestellt wurden.|  
|**Transportnachrichten in Warteschlangen gesamt**|Die Anzahl der Nachrichten, die in dieser Instanz in Warteschlangen gestellt wurden, wobei nur die Nachrichten berücksichtigt werden, die über das Netzwerk eingetroffen sind.|  
|**Transportnachrichten in Warteschlangen/Sekunde**|Die Anzahl der Nachrichten pro Sekunde, die in dieser Instanz in Warteschlangen gestellt wurden, wobei nur die Nachrichten berücksichtigt werden, die über das Netzwerk eingetroffen sind.|  
|**Weitergeleitete Nachrichten gesamt**|Die Gesamtanzahl der [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Nachrichten, die von diesem Computer aus weitergeleitet wurden.|  
|**Weitergeleitete Nachrichten/Sekunde**|Die Anzahl der Nachrichten, die pro Sekunde von diesem Computer aus weitergeleitet wurden.|  
|**Bytes von weitergeleiteten Nachrichten gesamt**|Die Gesamtgröße der von diesem Computer aus weitergeleiteten Nachrichten in Bytes.|  
|**Bytes von weitergeleiteten Nachrichten/Sekunde**|Die Größe der von diesem Computer aus pro Sekunde weitergeleiteten Nachrichten in Bytes.|  
|**Weitergeleitete verworfene Nachrichten gesamt**|Die Anzahl der von diesem Computer zur Weiterleitung empfangenen Nachrichten, deren Weiterleitung nicht erfolgreich war.|  
|**Weitergeleitete verworfene Nachrichten/Sekunde**|Die Anzahl der von diesem Computer zur Weiterleitung pro Sekunde empfangenen Nachrichten, deren Weiterleitung nicht erfolgreich war.|  
|**Bytes von weitergeleiteten ausstehenden Nachrichten**|Die Gesamtgröße der aktuell weiterzuleitenden Nachrichten.|  
|**Anzahl der weitergeleiteten ausstehenden Nachrichten**|Die Gesamtanzahl der aktuell weiterzuleitenden Nachrichten.|  
|**SQL RECEIVE-Befehle gesamt**|Gesamtzahl der verarbeiteten [!INCLUDE[tsql](../../includes/tsql-md.md)] -RECEIVE-Anweisungen.|  
|**SQL RECEIVE-Befehle/Sekunde**|Die Anzahl der pro Sekunde verarbeiteten [!INCLUDE[tsql](../../includes/tsql-md.md)] -RECEIVE-Anweisungen.|  
|**SQL SEND-Befehle gesamt**|Die Gesamtzahl der ausgeführten [!INCLUDE[tsql](../../includes/tsql-md.md)] -SEND-Anweisungen.|  
|**SQL SEND-Befehle/Sekunde**|Die Anzahl der pro Sekunde ausgeführten [!INCLUDE[tsql](../../includes/tsql-md.md)] -SEND-Anweisungen.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
