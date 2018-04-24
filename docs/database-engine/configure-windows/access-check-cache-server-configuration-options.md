---
title: Serverkonfigurationsoptionen für den Zugriffsüberprüfungscache | Microsoft-Dokumentation
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
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1c566507fd7d146e88de860660487056901d525f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="access-check-cache-server-configuration-options"></a>Serverkonfigurationsoptionen für den Zugriffsüberprüfungscache
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Beim Zugriff auf Datenbankobjekte durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die Zugriffsprüfung in einer internen Struktur zwischengespeichert, die als **access check result cache**bezeichnet wird. Die Optionen **access check cache quota** und **access check cache bucket count** steuern die Anzahl der Einträge und Anzahl der Hashbuckets, die für den **Zugriffsprüfungscache**verwendet werden. In seltenen Fällen kann die Leistung durch das Ändern dieser Optionen verbessert werden.  
  
 Die Standardwerte 0 geben an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diese Optionen verwaltet. Microsoft empfiehlt, diese Optionen nur auf Anweisung des Microsoft-Kundendiensts zu ändern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
