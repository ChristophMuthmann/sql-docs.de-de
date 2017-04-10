---
title: "Anzeigen einer gespeicherten Ablaufverfolgung (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ablaufverfolgungen [SQL Server], anzeigen"
  - "Anzeigen von Ablaufverfolgungen"
  - "Anzeigen von Ablaufverfolgungen"
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# Anzeigen einer gespeicherten Ablaufverfolgung (Transact-SQL)
  In diesem Thema wird beschrieben, wie Sie integrierte Funktionen verwenden, um eine gespeicherte Ablaufverfolgung anzuzeigen.  
  
### So zeigen Sie eine bestimmte Ablaufverfolgung an  
  
1.  Führen Sie **fn_trace_getinfo** aus, und geben Sie die ID der Ablaufverfolgung an, zu der Informationen benötigt werden. Diese Funktion gibt eine Tabelle zurück, in der die Ablaufverfolgung, die Ablaufverfolgungseigenschaft und Informationen zur Eigenschaft aufgelistet sind.  
  
     Rufen Sie die Funktion folgendermaßen auf:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### So zeigen Sie alle vorhandenen Ablaufverfolgungen an  
  
1.  Führen Sie **fn_trace_getinfo** aus, indem Sie `default` oder `0` angeben. Diese Funktion gibt eine Tabelle zurück, in der alle Ablaufverfolgungen, deren Eigenschaften und Informationen zu diesen Eigenschaften aufgelistet sind.  
  
     Rufen Sie die Funktion folgendermaßen auf:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## .NET Framework-Sicherheit  
 Um die integrierte **fn_trace_getinfo**-Funktion auszuführen, benötigt der Benutzer die folgende Berechtigung:  
  
 ALTER TRACE auf dem Server.  
  
## Siehe auch  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [Anzeigen und Analysieren von Ablaufverfolgungen mit SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  