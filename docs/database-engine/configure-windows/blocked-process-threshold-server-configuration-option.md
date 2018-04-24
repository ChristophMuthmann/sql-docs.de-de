---
title: Schwellenwert für blockierte Prozesse (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- thresholds [SQL Server]
- blocked process threshold option
ms.assetid: 3d46d143-bc6a-4220-8b55-6baa37547c25
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9124b99177579c4cc5044bbd055a3f5268fee3a9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="blocked-process-threshold-server-configuration-option"></a>Schwellenwert für blockierte Prozesse (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Mit der Option **Schwellenwert für blockierte Prozesse** geben Sie den Schwellenwert in Sekunden an, bei dem Berichte zu blockierten Prozessen generiert werden. Der Schwellenwert kann auf einen Wert zwischen 0 und 86.400 festgelegt werden. Standardmäßig werden für blockierte Prozesse keine Berichte erstellt. Dieses Ereignis wird nicht für Systemtasks und Tasks generiert, die auf Ressourcen warten, die keine bekannten Deadlocks generieren.  
  
 Sie können eine [Warnung](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef) festlegen, die bei der Generierung dieses Ereignisses erfolgen soll. So können Sie beispielsweise angeben, dass Administrator eine Aufforderung zur Ergreifung der geeigneten Maßnahmen erhalten soll, um die Blockierung zu lösen.  
  
 Für den Schwellenwert für blockierte Prozesse wird der Hintergrundthread der Deadlocküberwachung verwendet, um auf einen Zeitwert zu warten, der größer oder ein Vielfaches des konfigurierten Schwellenwerts ist. Das Ereignis wird pro Berichtsintervall einmal für jeden blockierten Task generiert.  
  
 Der Bericht zu blockierten Prozessen erfolgt auf Grundlage der besten Leistung. Eine Berichterstellung in Echtzeit oder annähernder Echtzeit kann nicht sichergestellt werden.  
  
 Die Einstellung tritt ohne Beenden und Neustarten des Servers sofort in Kraft.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Wert für `blocked process threshold` auf `20` Sekunden festgelegt. Hiermit wird für jeden blockierten Task ein Bericht zu blockierten Prozessen generiert.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 20 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Blocked Process Report-Ereignisklasse](../../relational-databases/event-classes/blocked-process-report-event-class.md)  
  
  
