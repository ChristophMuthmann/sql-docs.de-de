---
title: MSSQLSERVER_9001 | Microsoft-Dokumentation
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
helpviewer_keywords: 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ed271aa4c3be211d2ced1b20e8fc739f637514e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|9001|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|LOG_NOT_AVAIL|  
|Meldungstext|Das Protokoll für die '%.*ls'-Datenbank ist nicht verfügbar. Überprüfen Sie das Ereignisprotokoll auf verwandte Fehlermeldungen. Beheben Sie ggf. alle Fehler, und starten Sie die Datenbank neu.|  
  
## <a name="explanation"></a>Erklärung  
Das Datenbankprotokoll wurde offline geschaltet Normalerweise ist dies ein Zeichen für einen schwerwiegenden Fehle, der einen Neustart der Datenbank erfordert.  
  
## <a name="user-action"></a>Benutzeraktion  
Diagnostizieren Sie andere Fehler, und starten Sie die Instanz von SQL Server neu, wenn sie sich noch nicht selbst neu gestartet hat.  
  
