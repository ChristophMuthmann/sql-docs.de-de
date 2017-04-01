---
title: "&#196;ndern von Ablaufverfolgungsvorlagen | Microsoft Docs"
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
  - "Vorlagen [SQL Server], SQL Server Profiler"
  - "Profiler [SQL Server Profiler], Vorlagen"
  - "Ablaufverfolgungsvorlagen [SQL Server]"
  - "Ändern von Ablaufverfolgungsvorlagen"
  - "SQL Server Profiler, Vorlagen"
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# &#196;ndern von Ablaufverfolgungsvorlagen
  Sie können Vorlagen ändern, wenn diese in einer Datei auf dem lokalen Computer gespeichert sind und auf dem Computer [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ausgeführt wird. Sie können auch Vorlagen ändern, die aus diesen Dateien abgeleitet wurden. Beim Ändern vorhandener Vorlagen bearbeiten Sie die Eigenschaften der Vorlage, wie Ereignisklassen und Datenspalten, in derselben Reihenfolge, in der die Eigenschaften ursprünglich festgelegt wurden. Dies geschieht über die Registerkarte **Ereignisauswahl** im Dialogfeld **Ablaufverfolgungseigenschaften** . Ereignisklassen und Datenspalten können hinzugefügt oder entfernt werden, und Filter können geändert werden. Nach dem Ändern der Vorlage wird eine benutzerspezifische Vorlage erstellt, und die ursprüngliche Systemvorlage bleibt unverändert. Weitere Informationen finden Sie unter [Speichern von Ablaufverfolgungen und Ablaufverfolgungsvorlagen](../../tools/sql-server-profiler/save-traces-and-trace-templates.md).  
  
 Möglicherweise müssen Sie eine Vorlage von einer vorhandenen Ablaufverfolgungsdatei ableiten, z. B. falls Sie vergessen haben, welche Vorlage ursprünglich zum Erstellen der Ablaufverfolgung verwendet wurde (oder wenn diese Datei nicht gespeichert wurde) oder falls Sie eine Ablaufverfolgung später erneut ausführen möchten. Bei vorhandenen Ablaufverfolgungen können Sie die Eigenschaften zwar anzeigen, aber nicht ändern. Um die Eigenschaften zu ändern, müssen Sie die Ablaufverfolgung beenden oder anhalten. Weitere Informationen finden Sie unter [Ableiten einer Vorlage von einer Ablaufverfolgungsdatei oder Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md) und [Ableiten einer Vorlage von einer zurzeit ausgeführten Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md).  
  
 **So erstellen Sie eine Ablaufverfolgungsvorlage**  
  
 [Erstellen einer Ablaufverfolgungsvorlage &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
 **So führen Sie eine Ablaufverfolgung mithilfe einer Ablaufverfolgungsvorlage aus**  
  
 [Erstellen einer Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 **So ändern Sie eine Ablaufverfolgungsvorlage**  
  
 [Verwenden von SQL Server Profiler](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)  
  
 [Verwenden von Transact-SQL](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
 **So fügen Sie zu einer Ablaufverfolgungsvorlage oder -datei Ereignisse hinzu bzw. entfernen sie**  
  
 [Verwenden von SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Verwenden von Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
## Siehe auch  
 [Starten einer Ablaufverfolgung](../../tools/sql-server-profiler/start-a-trace.md)  
  
  