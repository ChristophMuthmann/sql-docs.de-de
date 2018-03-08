---
title: Statusberichte (Ereigniskategorie) | Microsoft Docs
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
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c90cfbe7e30d0678d13a329737c21f7d45575e22
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="progress-reports-event-category"></a>Fortschrittsbericht (Ereigniskategorie)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Die Progress Reports-Ereigniskategorie enthält die in der folgenden Tabelle beschriebenen Ereignisklassen.  
  
|Ereignisklasse|Ereignis-ID|Description|  
|-----------------|--------------|-----------------|  
|Progress Report Begin|5|Sammelt alle Progress Report Begin-Ereignisse seit dem Start der Ablaufverfolgung.|  
|Progress Report End|6|Sammelt alle Progress Report End-Ereignisse seit dem Start der Ablaufverfolgung.|  
|Progress Report Current|7|Sammelt alle Progress Report Current-Ereignisse seit dem Start der Ablaufverfolgung. Beispielsweise enthalten während der Verarbeitung die Current Reports Verarbeitungsinformationen zu den verarbeiteten Objekten (Dimensionen, Partitionen, Cube usw.).|  
|Progress Report Error|8|Sammelt alle Progress Report Error-Ereignisse seit dem Start der Ablaufverfolgung.|  
  
 Jedes Progress Report Begin-Ereignis beginnt mit einem Datenstrom aus Progress-Ereignissen und wird durch ein Progress Report End-Ereignis beendet. Der Datenstrom kann jede beliebige Anzahl von Progress Report Current- und Progress Report Error-Ereignissen enthalten.  
  
 Informationen zu den Spalten, die den einzelnen Progress Reports-Ereignisklassen zugeordnet sind, finden Sie unter [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Ablaufverfolgungsereignisse](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
