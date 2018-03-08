---
title: "Richtige Überlappung von „Affinity Mask“ und „Affinity I/O Mask“ | Microsoft-Dokumentation"
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
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
caps.latest.revision: "11"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e5cbd2637a1728311172998b1d81c3390112355b
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="correct-affinity-mask-and-affinity-input-and-output-mask-overlap"></a>Correct Affinity Mask and Affinity Input and Output Mask Overlap
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Diese Regel überprüft, ob die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] über einen oder mehrere Prozessoren verfügt, die sowohl für die Verwendung mit der Option „Affinity Mask“ als auch mit der Option „Affinity I/O Mask“ zugeordnet wurde. Auf einem Computer, der über einen oder mehrere Prozessoren verfügt, bestimmen die Optionen Affinity Mask und Affinity I/O Mask, welche CPUs von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Das Aktivieren einer CPU mit den beiden Optionen Affinity Mask und Affinity I/O Mask kann die Leistung beeinträchtigen, da die Prozessoren übermäßig beansprucht werden.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Wenn Sie entweder die Option Affinity Mask oder die Option Affinity I/O Mask festlegen, sollten Sie beide Optionen festlegen, jedoch jede CPU nicht mehr als einmal aktivieren.  
  
 Aktivieren Sie in den Optionen Affinity Mask und Affinity I/O Mask nicht dieselbe CPU. Die Bits, die den einzelnen CPUs entsprechen, sollten sich jeweils in einem der folgenden Zustände befinden:  
  
-   0 für die Option Affinity Mask und die Option Affinity I/O Mask  
  
-   0 für die Option Affinity Mask und 1 für die Option Affinity I/O Mask  
  
-   1 für die Option Affinity Mask und 0 für die Option Affinity I/O Mask  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Affinitätsmaske (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)  
  
 [Affinity I/O Mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)  
  
 [Affinity64 Mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)  
  
 [affinity64 I/O mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
