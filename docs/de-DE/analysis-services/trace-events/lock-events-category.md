---
title: Sperren-Ereigniskategorie | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7e1b7a18c7ed5f763674ade69647a26f775cfb98
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="lock-events-category"></a>Sperren-Ereigniskategorie
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
