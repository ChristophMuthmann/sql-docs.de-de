---
title: MSSQLSERVER_2538 | Microsoft-Dokumentation
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
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a3630d0441bd067a1dc78e41b997d4d51d6c7fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2538"></a>MSSQLSERVER_2538
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2538|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|Meldungstext|Datei FILE. Blockanzahl = EXTENTS, verwendete Seiten = USED_PAGES, reservierte Seiten = RESERVED_PAGES.|  
  
## <a name="explanation"></a>Erklärung  
Diese Informationen sind Teil der Ausgabe des Befehls DBCC CHECKALLOC. Bei diesen Informationen handelt es sich um die Zusammenfassung von zugeordneten Blöcken, verwendeten Seiten und reservierten Seiten pro Datei für die angegebene Datenbank.  
  
## <a name="user-action"></a>Benutzeraktion  
InclusionThresholdSetting  
  
