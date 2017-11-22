---
title: SQL Server XTP IO Governor | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
caps.latest.revision: "2"
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 530500f1dafa732f008f3d08de0caaad43ce1021
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO Governor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Das Leistungsobjekt „SQL Server XTP IO Governor“ enthält Leistungsindikatoren, die sich auf den In-Memory OLTP IO Rate Governor beziehen.

In dieser Tabelle werden die Leistungsindikatoren für **SQL Server XTP IO Governor** beschrieben.

|Leistungsindikator|Description|  
|-------------|-----------------|  
|**Nicht genügend Guthabenwartezeiten/Sekunde**|Anzahl von Wartevorgängen aufgrund unzureichenden Guthabens in den Ratenobjekten (pro Sekunde).|
|**E/A ausgestellt/Sekunde**|Anzahl der durch Leerungsthreads ausgegeben E/A pro Sekunde.|
|**Protokollblöcke/Sekunde**|Anzahl der Protokollblöcke, die vom Controller pro Sekunde verarbeitet werden.|
|**Slots für verpasste Guthaben**|Anzahl der Slots für verpasste Guthaben, die beim Warten auf Guthaben vom Ratenobjekt verpasst wurden.|
|**Wartezeit/s für veraltete Ratenobjekte**|Anzahl der Wartevorgänge aufgrund veralteter Ratenobjekte (pro Sekunde).|
|**Gesamtrate veröffentlichter Objekte**|Gesamtanzahl der veröffentlichten Ratenobjekte.|
 

## <a name="see-also"></a>Siehe auch  
[Leistungsindikatoren für SQL Server XTP &#40;In-Memory OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
