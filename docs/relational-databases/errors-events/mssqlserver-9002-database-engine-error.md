---
title: MSSQLSERVER_9002 | Microsoft-Dokumentation
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
helpviewer_keywords: 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fafb1765edbf93a9c356bda314207c70cb6ffb24
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver9002"></a>MSSQLSERVER_9002
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|9002|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|LOG_IS_FULL|  
|Meldungstext|Das Transaktionsprotokoll für die '%.*ls'-Datenbank ist voll. Die log_reuse_wait_desc-Spalte von sys.databases enthält Informationen dazu, warum Protokollspeicherplatz nicht erneut verwendet werden kann.|  
  
## <a name="explanation"></a>Erklärung  
Das Datenbankprotokoll hat nicht mehr genügend Speicherplatz zur Verfügung. Die **log_reuse_wait_desc**-Spalte in **sys.databases** beschreibt, warum Protokollspeicherplatz nicht erneut verwendet werden kann.  
  
## <a name="user-action"></a>Benutzeraktion  
Bestimmen Sie mit **sys.databases**, warum das Protokoll voll ist, und korrigieren Sie dann die Bedingung. Weitere Informationen finden Sie unter „Problembehandlung bei vollen Transaktionsprotokollen (Fehler 9002)“ in der SQL Server-Onlinedokumentation.  
  
## <a name="see-also"></a>Siehe auch  
[Problembehandlung bei vollen Transaktionsprotokollen &#40;SQL Server-Fehler 9002&#41;](~/relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
