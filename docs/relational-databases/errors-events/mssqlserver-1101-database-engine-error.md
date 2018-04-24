---
title: MSSQLSERVER_1101 | Microsoft-Dokumentation
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
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c45d4531ee2b505a49218126f8bda63536be9098
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1101"></a>MSSQLSERVER_1101
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1101|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|NOALLOCPG|  
|Meldungstext|Eine neue Seite für die '%.*ls'-Datenbank konnte nicht zugeordnet werden, weil in der Dateigruppe '%.\*ls' nicht genügend Speicherplatz verfügbar ist. Speicherplatz kann durch Löschen von Objekten in der Dateigruppe, Hinzufügen von Dateien zur Dateigruppe oder Festlegen der automatischen Vergrößerung für vorhandene Dateien in der Dateigruppe gewonnen werden.|  
  
## <a name="explanation"></a>Erklärung  
In einer Dateigruppe ist kein Speicherplatz verfügbar.  
  
## <a name="user-action"></a>Benutzeraktion  
Durch die folgenden Aktionen kann Speicherplatz in der Dateigruppe verfügbar gemacht werden.  
  
-   Aktivieren Sie AUTOGROW.  
  
-   Fügen Sie der Dateigruppe weitere Dateien hinzu.  
  
-   Geben Sie Speicherplatz frei, indem sich nicht benötigte Indizes oder Tabellen in der Dateigruppe löschen.  
  
