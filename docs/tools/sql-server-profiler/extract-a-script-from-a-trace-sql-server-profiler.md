---
title: "Extrahieren eines Skripts aus einer Ablaufverfolgung (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Skripts [SQL Server], Ablaufverfolgungen"
  - "Extrahieren eines Skripts aus einer Ablaufverfolgung [SQL Server]"
ms.assetid: 431126a6-ff91-4818-8763-4442152bd571
caps.latest.revision: 20
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Extrahieren eines Skripts aus einer Ablaufverfolgung (SQL Server Profiler)
  In diesem Thema wird das Extrahieren von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ereignissen aus einer Ablaufverfolgungsdatei oder -tabelle sowie das Speichern in einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skriptdatei mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] beschrieben.  
  
### So extrahieren Sie ein Transact-SQL-Skript aus einer Ablaufverfolgungsdatei oder -tabelle  
  
1.  Öffnen Sie eine Ablaufverfolgungsdatei oder -tabelle, die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ereignisse enthält, die Sie in einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Skriptdatei speichern möchten. Weitere Informationen finden Sie unter [Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) oder [Öffnen einer Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
2.  Zeigen Sie im Menü **Datei** auf **Exportieren**, zeigen Sie auf **SQL Server-Ereignisse extrahieren**, und klicken Sie dann auf **Transact-SQL-Ereignisse extrahieren**.  
  
3.  Geben Sie im Dialogfeld **Speichern unter** einen Namen für die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Datei ein, und klicken Sie dann auf **Speichern**.  
  
## Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  