---
title: MSSQLSERVER_17066 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17066 (Database Engine error)
ms.assetid: 7d650bbf-c583-4af8-9e22-993ee2880d95
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 934f397120b406b0a6ed109e9bae229fef47c5f8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17066"></a>MSSQLSERVER_17066
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|17066|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQLASSERT_ONLY|  
|Meldungstext|SQL Server-Assertion: Datei: \<%s>, Zeile=%d Fehler bei Assertion = '%s'. Dieser Fehler hängt möglicherweise mit dem Ausführungszeitpunkt zusammen. Wenn der Fehler nach dem erneuten Ausführen der Anweisung weiterhin auftritt, überprüfen Sie die Datenbank mit DBCC CHECKDB auf strukturelle Integrität, oder starten Sie den Server neu, um sicherzustellen, dass keine speicherresidenten Datenstrukturen beschädigt sind.|  
  
## <a name="explanation"></a>Erklärung  
Dieser Fehler kann von vorübergehenden Zeitsteuerungsfehlern oder durch Datenbeschädigung im Speicher oder auf dem Datenträger verursacht werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie die Anweisung, die die Ausnahme ausgelöst hat, erneut aus. Wenn der Fehler von einem Zeitsteuerungsereignis verursacht wurde, tritt er möglicherweise nicht wieder auf. Wenn das Problem weiterhin auftritt, führen Sie DBCC CHECKDB zur Überprüfung auf Beschädigungen auf dem Datenträger aus. Starten Sie den Server neu, um sicherzustellen, dass die speicherinternen Datenstrukturen nicht beschädigt sind.  
  
## <a name="see-also"></a>Siehe auch  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
