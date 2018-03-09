---
title: MSSQLSERVER_17204 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: befada4a3c2b5ea56fbe8c6ec6b14f6d5a558886
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17204"></a>MSSQLSERVER_17204
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|17204|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBLKIO_DEVOPENFAILED|  
|Meldungstext|% ls: Die Datei %ls für die Dateinummer %d konnte nicht geöffnet werden.  Betriebssystemfehler: %ls.|  
  
## <a name="explanation"></a>Erklärung  
SQL Server konnte die angegebene Datei aufgrund des angegebenen Fehlers nicht öffnen.  
  
## <a name="user-action"></a>Benutzeraktion  
Erstellen Sie eine Diagnose für das Betriebssystem, und korrigieren Sie es, wiederholen Sie dann den Vorgang.  
  
