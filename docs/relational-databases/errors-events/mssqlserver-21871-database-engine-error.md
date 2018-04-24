---
title: MSSQLSERVER_21871 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 39feeca79cfba6215286ca904a0aa3673ea8f91e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver21871"></a>MSSQLSERVER_21871
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21871|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQLErrorNum21871|  
|Meldungstext|Verleger %s der Datenbank %s wurde nicht umgeleitet.|  
  
## <a name="explanation"></a>Erklärung  
**sp_validate_replica_hosts_as_publishers** überprüft die Tabelle MSredirected_publishers in der Verteilungsdatenbank auf einen Eintrag für den identifizierten Verleger und die Verlegerdatenbank.  **sp_validate_replica_hosts_as_publishers** gibt den Fehler 21871 zurück, wenn kein Eintrag gefunden wird.  
  
## <a name="user-action"></a>Benutzeraktion  
**sp_validate_replica_hosts_as_publishers** ist nur für umgeleitete Verleger relevant. Wenn eine veröffentlichte Datenbank Mitglied einer Always On-Verfügbarkeitsgruppe ist, führen Sie die gespeicherte Prozedur **sp_redirect_publisher** aus, um den Verleger und die Verlegerdatenbank mit dem Verfügbarkeitsgruppen-Listener-Namen der Verfügbarkeitsgruppe zu verknüpfen.  
  
