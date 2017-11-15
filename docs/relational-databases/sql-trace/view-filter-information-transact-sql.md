---
title: Anzeigen von Filterinformationen (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a741b8f1aa4b0095d61c0011518a3f1d855440c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="view-filter-information-transact-sql"></a>Anzeigen von Filterinformationen (Transact-SQL)
  In diesem Thema wird beschrieben, wie mit integrierten Funktionen Filterinformationen zur Ablaufverfolgung angezeigt werden.  
  
### <a name="to-view-filter-information"></a>So zeigen Sie Filterinformationen an  
  
1.  Führen Sie **fn_trace_getfilterinfo** aus, indem Sie die ID der Ablaufverfolgung angeben, zu der Filterinformationen benötigt werden. Diese Funktion gibt eine Tabelle mit den Filtern, der Spalte, auf die die Filter angewendet werden, und den Werten, auf die der Filter angewendet wird, zurück.  
  
     Rufen Sie die Funktion folgendermaßen auf:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getfilterinfo(trace_id)  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Prozeduren von SQL Server Profiler &#40;SQL Server Profiler&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
