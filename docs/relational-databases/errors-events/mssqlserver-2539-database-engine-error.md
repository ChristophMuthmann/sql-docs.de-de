---
title: MSSQLSERVER_2539 | Microsoft-Dokumentation
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
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26c4dd19ac5e09e39e431d650390eb012ec192e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2539"></a>MSSQLSERVER_2539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2539|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_ALLOCATION_SUMMARY_FOR_DATABASE|  
|Meldungstext|Gesamte Blockanzahl = EXTENTS, verwendete Seiten = USED_PAGES, reservierte Seiten = RESERVED_PAGES in dieser Datenbank.|  
  
## <a name="explanation"></a>Erklärung  
Diese Informationen sind Teil der Ausgabe des Befehls DBCC CHECKALLOC. Es handelt sich um Zusammenfassungsinformationen von zugeordneten Blöcken, verwendeten Seiten und reservierten Seiten für die angegebene Datenbank.  
  
## <a name="user-action"></a>Benutzeraktion  
InclusionThresholdSetting  
  
