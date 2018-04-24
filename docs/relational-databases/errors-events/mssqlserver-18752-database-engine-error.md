---
title: MSSQLSERVER_18752 | Microsoft-Dokumentation
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
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03abdf6dd988fa7a90d605d38030caf0753052a0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver18752"></a>MSSQLSERVER_18752
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|18752|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|REPL_INUSE|  
|Meldungstext|Nur jeweils ein Protokolllese-Agent oder eine protokollbezogene Prozedur (sp_repldone, sp_replcmds oder sp_replshowcmds) kann eine Verbindung mit einer Datenbank herstellen. Falls Sie eine protokollbezogene Prozedur ausgeführt haben, löschen Sie vor dem Starten des Protokolllese-Agents oder dem Ausführen einer weiteren protokollbezogenen Prozedur die Verbindung, über die sie ausgeführt wurde, oder führen Sie 'sp_replflush' über diese Verbindung aus.|  
  
## <a name="explanation"></a>Erklärung  
Nur jeweils ein Protokolllese-Agent oder eine protokollbezogene Prozedur kann eine Verbindung mit einer Datenbank herstellen.  
  
## <a name="user-action"></a>Benutzeraktion  
Stellen Sie sicher, dass kein weiterer Protokolllese-Agent für die gleiche Veröffentlichungsdatenbank ausgeführt wird und dass keine aktive Verbindung zuvor sp_replcmds/sp_repltrans/sp_repldone ausgeführt hat, ohne anschließend sp_replflush auszuführen oder die Verbindung zu trennen.  
  
