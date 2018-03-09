---
title: "Beibehalten des Standardwerts für die Konfigurationsoption „locks“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: f214f05b-5f0b-4786-b2ad-b8b4b6e58d72
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d747490a7b4e1e78c76257d7312aeb7d0cc16b61
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="keep-the-locks-configuration-option-default-value"></a>Beibehalten des Standardwerts für die Konfigurationsoption 'locks'
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Diese Regel überprüft den Wert der Sperrenkonfigurationsoption. Durch diese Option wird die maximale Anzahl verfügbarer Sperren festgelegt. Diese schränkt ein, wie viel Arbeitsspeicher [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] für Sperren verwendet. In der Standardeinstellung 0 kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] Sperrstrukturen je nach Systemanforderungen dynamisch zuordnen bzw. deren Zuordnung aufheben.  
  
 Wenn Sperren einen Wert ungleich 0 (null) hat, werden Stapelverarbeitungsaufträge angehalten, und es wird eine Fehlermeldung angezeigt, dass keine Sperren vorhanden sind, wenn der angegebene Wert überschritten wird.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Verwenden Sie die gespeicherte Systemprozedur sp_configure, um den Wert von Sperren mithilfe der folgenden Anweisung auf die Standardeinstellung zu ändern:  
  
```  
EXEC sp_configure 'locks', 0;  
```  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Konfigurieren der Serverkonfigurationsoption Sperren](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)  
  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
  
 [Microsoft Knowledge Base-Artikel 271509](http://go.microsoft.com/fwlink/?linkid=117788)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
