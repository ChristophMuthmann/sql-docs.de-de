---
title: Protokolldateien für Standardablaufverfolgung deaktiviert | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 833df2f5974e85c996faefbf7af7ec1761fdd6a4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="default-trace-log-files-disabled"></a>Protokolldateien für Standardablaufverfolgung deaktiviert
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Diese Regel überprüft den Wert der Option Standardablaufverfolgung aktiviert der gespeicherten Prozedur sp_configure, um festzustellen, ob die Standardablaufverfolgung auf ON (1) oder OFF (0) festgelegt ist. Wenn diese Option aktiviert ist, stellt die Standardablaufverfolgung Informationen über Konfigurations- und DDL-Änderungen an [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]bereit. In manchen Fällen sind diese Informationen für Kunden sowie den Kundendienst- und Support von [!INCLUDE[msCoName](../../includes/msconame-md.md)] bei der Behebung von Fehlern bei [!INCLUDE[ssDE](../../includes/ssde-md.md)]hilfreich.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Aktivieren Sie die Ablaufverfolgung mit der gespeicherten Prozedur sp_configure, indem Sie den Wert von "Standardablaufverfolgung aktiviert" auf 1 festlegen.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
