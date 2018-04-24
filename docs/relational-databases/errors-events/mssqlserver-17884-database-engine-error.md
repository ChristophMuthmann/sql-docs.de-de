---
title: MSSQLSERVER_17884 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f8724c810333c1073c3c57fb9cb77ad70fc72de
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver17884"></a>MSSQLSERVER_17884
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|17884|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SRV_SCHEDULER_DEADLOCK|  
|Meldungstext|Neue Abfragen, die dem Prozess im %d-Knoten zugewiesen sind, wurden in den letzten %d Sekunden von keinem Arbeitsthread abgerufen. Die Ursache hierfür können blockierende Abfragen oder Abfragen mit langer Ausführungszeit sein, wodurch die Clientantwortzeit beeinträchtigt wird. Erhöhen Sie mithilfe der Konfigurationsoption „Max. Anzahl von Arbeitsthreads“ die Anzahl zulässiger Threads, oder optimieren Sie aktuell ausgeführte Abfragen.  SQL-Prozessnutzung: %d%%. Leerlauf des Systems: %d%%.|  
  
## <a name="explanation"></a>Erklärung  
In den Zeitplanungsmodulen gibt es kein Anzeichen von Fortschritt. Die Ursache können Deadlocks sein, bei denen keine Threads fortgeführt werden können und/oder keine neue Arbeit aufgenommen und verarbeitet werden kann. Wenn die Prozessnutzung niedrig ist, können andere Prozesse auf dem Computer möglicherweise dazu führen, dass auf die Serverprozess-CPU nicht mehr zugegriffen werden kann.  
  
## <a name="user-action"></a>Benutzeraktion  
Bestimmen Sie die Ursache für die Blockierung und den fehlenden Fortschritt, und lösen Sie die Situation entsprechend. Wenn die Prozessnutzung niedrig ist, prüfen Sie die Systemlast, die von anderen Prozessen verursacht wird.  
  
