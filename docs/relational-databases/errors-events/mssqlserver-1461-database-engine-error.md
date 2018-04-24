---
title: MSSQLSERVER_1461 | Microsoft-Dokumentation
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
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fad5bc18b5d549e8c8dca5aaaf083a10599851fb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1461|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBM_SAFETY_MISMATCH|  
|Meldungstext|Für die "%.*ls"-Datenbank wurden bei den Servern unterschiedliche Sicherheitsstufen für die Datenbankspiegelung gefunden. Die Sicherheitsstufe FULL wird verwendet.|  
  
## <a name="explanation"></a>Erklärung  
Die Spiegelungsverbindungen wurden unterbrochen, als die Sicherheitsstufe der Transaktion geändert wurde, da die Sicherheitseinstellungen der Transaktion für die Prinzipal- und Spiegeldatenbank inkonsistent waren. Es wird die Standardsicherheitseinstellung der Sicherheit für vollständige Transaktionen verwendet. Die Sitzung wird im Modus für hohe Sicherheit ausgeführt.  
  
## <a name="user-action"></a>Benutzeraktion  
Wenn Sie die Transaktionssicherheit initiieren möchten, führen Sie die ALTER DATABASE *Datenbank_Name* SET PARTNER SAFETY OFF-Anweisung für die Prinzipaldatenbank erneut aus.  
  
