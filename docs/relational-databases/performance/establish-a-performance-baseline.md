---
title: Festlegen einer Leistungsbasislinie | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database performance [SQL Server], baselines
- monitoring performance [SQL Server], baselines
- tuning databases [SQL Server], baselines
- server performance [SQL Server], baselines
- performance [SQL Server], baselines
- baseline performance [SQL Server]
- measurements for baseline statistics [SQL Server]
- monitoring server performance [SQL Server], establishing baseline
- database monitoring [SQL Server], baselines
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8eb3a143b53f3328453f4f3688e79fb5b42f4dbb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="establish-a-performance-baseline"></a>Festlegen einer Leistungsbasislinie
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Wenn Sie ermitteln möchten, ob das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -System einwandfrei arbeitet, sollten Sie die Leistung in regelmäßigen Abständen messen, selbst wenn keine Probleme auftreten, um eine Basislinie für die Serverleistung zu erstellen. Vergleichen Sie jede neue Messreihe mit den zuvor erfassten Messungen.  
  
 Die folgenden Bereiche wirken sich auf die Leistung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aus:  
  
-   Systemressourcen (Hardware)  
  
-   Netzwerkarchitektur  
  
-   Das Betriebssystem  
  
-   Datenbankanwendungen  
  
-   Clientanwendungen  
  
 Es sollten mindestens die folgenden Basislinienmessungen vorgenommen werden:  
  
-   Leistung bei Spitzen- und Normalbetrieb.  
  
-   Antwortzeiten für Produktionsabfragen oder Batchbefehle.  
  
-   Zeiten für das Sichern und Wiederherstellen von Datenbanken.  
  
 Nach dem Erstellen einer Basislinie für die Serverleistung sollten Sie die Basislinienstatistik mit der aktuellen Serverleistung vergleichen. Zahlen, die deutlich über oder unter der Basislinie liegen, sollten näher untersucht werden. Sie können ein Hinweis auf Bereiche, die optimiert oder neu konfiguriert werden müssen, sein. Wenn beispielsweise die Zeitdauer zum Ausführen einer Reihe von Abfragen steigt, sollten Sie die Abfragen untersuchen, um festzustellen, ob sie neu geschrieben werden können oder ob Spaltenstatistiken oder neue Indizes hinzugefügt werden müssen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
