---
title: Anzeigen einer gespeicherten Ablaufverfolgung (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: sql-trace
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b24ae09ade807ae60210dcb36d61a7649ff173d8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-a-saved-trace-transact-sql"></a>Anzeigen einer gespeicherten Ablaufverfolgung (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Sie integrierte Funktionen verwenden, um eine gespeicherte Ablaufverfolgung anzuzeigen.  
  
### <a name="to-view-a-specific-trace"></a>So zeigen Sie eine bestimmte Ablaufverfolgung an  
  
1.  Führen Sie **fn_trace_getinfo** aus, und geben Sie die ID der Ablaufverfolgung an, zu der Informationen benötigt werden. Diese Funktion gibt eine Tabelle zurück, in der die Ablaufverfolgung, die Ablaufverfolgungseigenschaft und Informationen zur Eigenschaft aufgelistet sind.  
  
     Rufen Sie die Funktion folgendermaßen auf:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>So zeigen Sie alle vorhandenen Ablaufverfolgungen an  
  
1.  Führen Sie **fn_trace_getinfo** aus, indem Sie `0` oder `default`angeben. Diese Funktion gibt eine Tabelle zurück, in der alle Ablaufverfolgungen, deren Eigenschaften und Informationen zu diesen Eigenschaften aufgelistet sind.  
  
     Rufen Sie die Funktion folgendermaßen auf:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>.NET Framework-Sicherheit  
 Um die integrierte **fn_trace_getinfo**-Funktion auszuführen, benötigt der Benutzer die folgende Berechtigung:  
  
 ALTER TRACE auf dem Server.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [Anzeigen und Analysieren von Ablaufverfolgungen mit SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
