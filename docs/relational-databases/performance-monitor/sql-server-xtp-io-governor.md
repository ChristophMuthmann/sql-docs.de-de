---
title: SQL Server XTP IO Governor | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
caps.latest.revision: "2"
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b91fb70a65448057e65947a8f83307033b30dc5d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO Governor
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

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
