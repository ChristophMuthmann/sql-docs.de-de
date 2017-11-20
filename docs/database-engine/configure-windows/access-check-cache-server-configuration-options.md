---
title: "Serverkonfigurationsoptionen für den Zugriffsüberprüfungscache | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8efe371a915906e6f4f23df9cbd1f853ec20eb7c
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="access-check-cache-server-configuration-options"></a>Serverkonfigurationsoptionen für den Zugriffsüberprüfungscache
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Beim Zugriff auf Datenbankobjekte durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die Zugriffsprüfung in einer internen Struktur zwischengespeichert, die als **access check result cache**bezeichnet wird. Die Optionen **access check cache quota** und **access check cache bucket count** steuern die Anzahl der Einträge und Anzahl der Hashbuckets, die für den **Zugriffsprüfungscache**verwendet werden. In seltenen Fällen kann die Leistung durch das Ändern dieser Optionen verbessert werden.  
  
 Die Standardwerte 0 geben an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diese Optionen verwaltet. Microsoft empfiehlt, diese Optionen nur auf Anweisung des Microsoft-Kundendiensts zu ändern.  
  
## <a name="see-also"></a>Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

