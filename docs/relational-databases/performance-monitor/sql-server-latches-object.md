---
title: SQL Server, Latches-Objekt | Microsoft-Dokumentation
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
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e78f8c7cc588ccabe14fc9d754871268fc66b69f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-latches-object"></a>SQL Server, Latches-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das **SQLServer:Latches** -Objekt in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält Leistungsindikatoren zur Überwachung interner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ressourcensperren, die als Latches bezeichnet werden. Das Überwachen der Latches für die Ermittlung der Benutzeraktivität und der Ressourcennutzung kann Ihnen dabei helfen, Leistungsengpässe zu erkennen.  
  
 In dieser Tabelle werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Batches** -Leistungsindikatoren beschrieben.  
  
|Batches-Leistungsindikatoren von SQL Server|Description|  
|---------------------------------|-----------------|  
|**Durchschnittliche Wartezeit für Latch (in Millisekunden)**|Durchschnittliche Latchwartezeit (in Millisekunden) für wartende Latchanforderungen.|  
|**Basis für durchschnittliche Latchwartezeit**|Nur zur internen Verwendung.| 
|**Latchwartezeit/Sekunde**|Anzahl der Latchanforderungen, für die Batches nicht sofort erteilt werden konnten.|  
|**Anzahl der SuperLatches-Objekte**|Anzahl der Batches, die zurzeit SuperLatches-Objekte sind.|  
|**SuperLatches-Heraufstufungen/Sekunde**|Anzahl der SuperLatches-Objekte, die in der letzten Sekunde zu normalen Batches herabgestuft wurden.|  
|**SuperLatches-Höherstufungen/Sekunde**|Anzahl der Batches, die in der letzten Sekunde zu SuperLatches-Objekten heraufgestuft wurden.|  
|**Gesamtwartezeit für Latch (in Millisekunden)**|Gesamtwartezeit (in Millisekunden) für Latchanforderungen, die in der vergangenen Sekunde warten mussten.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
