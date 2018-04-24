---
title: Eigenständige Datenbanken bei Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- contained database, AlwaysOnAvailabilityGroups
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 74248e29dfa35e6b48da01de75115759c7f0c481
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="contained-databases-with-always-on-availability-groups-sql-server"></a>Eigenständige Datenbanken bei Always On-Verfügbarkeitsgruppen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieses Thema enthält Informationen zum Verwenden einer eigenständigen Datenbank in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] mit [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 **In diesem Thema:**  
  
-   [Erforderliche Komponenten](#Prerequisites)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Vor dem Hinzufügen einer enthaltenen Datenbank zu einer Verfügbarkeitsgruppe muss gewährleistet sein, dass die Serveroption **contained database authentication** auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe hostet, auf **1** gesetzt ist. Weitere Informationen finden Sie unter [Contained Database Authentication (Serverkonfigurationsoption)](../../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md) und [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Contained Databases](../../../relational-databases/databases/contained-databases.md)  
  
  
