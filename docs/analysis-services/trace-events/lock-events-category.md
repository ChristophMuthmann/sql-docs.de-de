---
title: Sperren-Ereigniskategorie | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ad434202093984f6064fe4bf80ba79e1b57c3cf8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="lock-events-category"></a>Sperren-Ereigniskategorie
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Die Locked Events-Ereigniskategorie verfügt über die in der folgenden Tabelle beschriebenen Ereignisklassen.  
  
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
  
  
