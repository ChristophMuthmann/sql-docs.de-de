---
title: Sperren-Ereigniskategorie | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8b2e6ba2dc66621bd74026f8aceb8c35eed4f0b1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="lock-events-category"></a>Sperren-Ereigniskategorie
  Die Locked Events-Ereigniskategorie enthält die in der folgenden Tabelle beschriebenen Ereignisklassen.  
  
|Ereignisklasse|Ereignis-ID|Description|  
|-----------------|--------------|-----------------|  
|Deadlock|50|Erfasst alle Deadlockereignisse für Metadatensperren seit Beginn der Ablaufverfolgung.|  
|Lock:timeout|51|Erfasst alle Timeoutereignisse für Metadatensperren seit Beginn der Ablaufverfolgung.|  
|Lock Acquired|52|Sammelt Informationen zu Sperren, die seit Beginn der Ablaufverfolgung erworben wurden.|  
|Lock Released|53|Sammelt Informationen zu Sperren, die seit Beginn der Ablaufverfolgung freigegeben wurden.|  
|Lock Waiting|54|Sammelt Informationen zu Sperren, die sich seit Beginn der Ablaufverfolgung im Wartezustand befinden.|  
  
 Informationen zu den Spalten, die den einzelnen Lock-Ereignisklassen zugeordnet sind, finden Sie unter [Lock Events Data Columns](../../analysis-services/trace-events/lock-events-data-columns.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Ablaufverfolgungsereignisse](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
