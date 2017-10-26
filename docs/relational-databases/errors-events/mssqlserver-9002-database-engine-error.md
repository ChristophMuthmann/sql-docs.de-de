---
title: MSSQLSERVER_9002 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 73b21170cef772b92ca39df81f5ebf8199e842dd
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9002"></a>MSSQLSERVER_9002
  
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
  

