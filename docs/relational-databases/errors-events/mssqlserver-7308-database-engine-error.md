---
title: MSSQLSERVER_7308 | Microsoft-Dokumentation
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
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49f67200d7489bf90102325cf3463b5ea58424f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|7308|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|RMT_STA_DISABLED|  
|Meldungstext|Der OLE DB-Anbieter ‚%ls’ kann nicht für verteilte Abfragen verwendet werden, weil der Anbieter so konfiguriert ist, dass er im Singlethread-Apartment-Modus ausgeführt wird.|  
  
## <a name="explanation"></a>Erklärung  
Sie haben einen OLE DB-Anbieter verwendet, der so konfiguriert ist, dass er im Singlethread-Apartment-Modus (STA) ausgeführt wird. OLE DB-Anbieter, die im Singlethread-Apartment-Modus (STA) ausgeführt werden, können nicht für verteilte Abfragen verwendet werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Um diesen Fehler zu beheben, konfigurieren Sie den Anbieter so, dass er im Multithread-Apartment-Modus (MTA) ausgeführt wird. Wenn der Anbieter den MTA nicht unterstützt und der Anbieter nicht auf eine Version aktualisiert werden kann, die MTA unterstützt, ziehen Sie in Erwägung, den Anbieter so zu konfigurieren, dass er außerhalb des Prozesses ausgeführt wird. Der Anbieterhersteller kann Ihnen mitteilen, ob der Anbieter den MTA oder die Ausführung außerhalb des Prozesses unterstützt.  
  
