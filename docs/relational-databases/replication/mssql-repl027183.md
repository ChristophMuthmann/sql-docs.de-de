---
title: "MSSQL_REPL027183 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_REPL027183 (Fehler)"
ms.assetid: 52c271ac-1a0e-43d5-85d4-35886d1efd32
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_REPL027183
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|27183|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Vom Mergeprozess konnten Änderungen in Artikeln mit parametrisierten Zeilenfiltern nicht aufgezählt werden. Falls dieser Fehler weiterhin auftritt, erhöhen Sie das Abfragetimeout für diesen Prozess, reduzieren Sie die Beibehaltungsdauer für die Veröffentlichung, und verbessern Sie die Indizes für veröffentlichte Tabellen.|  
  
## Erklärung  
 Dieser Fehler wird ausgelöst, wenn bei der Verarbeitung von Änderungen in einer gefilterten Veröffentlichung ein Merge-Agent-Timeout auftritt. Das Timeout kann durch eines der folgenden Probleme verursacht werden:  
  
-   Die Optimierung für vorausberechnete Partitionen wird nicht verwendet.  
  
-   In den beim Filtern verwendeten Spalten liegt eine Indexfragmentierung vor.  
  
-   Metadaten sind umfangreiche Tabellen, z. B. **MSmerge_tombstone**, **MSmerge_contents**, und **MSmerge_genhistory**.  
  
-   Es sind gefilterte Tabellen, die nicht über einen eindeutigen Schlüssel verknüpft sind, und Joinsfilter mit einer großen Anzahl an Tabellen vorhanden.  
  
## Benutzeraktion  
 So lösen Sie das Problem:  
  
-   Erhöhen Sie den Wert von der **- QueryTimeOut** -Parameter für den Merge-Agent, damit die Verarbeitung fortgesetzt, und Sie sich die zugrunde liegende Ursache des Fehlers widmen. Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
    -   [Arbeiten mit Replikations-Agent-Profilen](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Anzeigen und Ändern von Replikations-Agent-Befehlszeilenparameter & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Replikations-Agent ausführbare Konzepte](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Verwenden Sie, sofern möglich, die Optimierung für vorausberechnete Partitionen. Diese Optimierung wird standardmäßig verwendet, wenn mehrere Veröffentlichungsanforderungen erfüllt sind. Weitere Informationen zu diesen Anforderungen finden Sie unter [parametrisierte Filter Leistung mit Vorausberechnete Partitionen optimieren](../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md). Wenn die Veröffentlichung diese Anforderungen nicht erfüllt, sollten Sie einen erneuten Entwurf der Veröffentlichung in Betracht ziehen.  
  
-   Geben Sie die kürzestmögliche Einstellung für die Beibehaltungsdauer der Veröffentlichung an, da die Replikation keinen Cleanup der Metadaten in den Veröffentlichungs- und den Abonnementdatenbanken ausführen kann, bevor die Beibehaltungsdauer erreicht wurde. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Im Rahmen der Wartung für die Mergereplikation, überprüfen Sie gelegentlich die Vergrößerung der Systemtabellen Mergereplikation zugeordnet: **MSmerge_contents**, **MSmerge_genhistory**, und **MSmerge_tombstone**, **MSmerge_current_partition_mappings**, und **MSmerge_past_partition_mappings**. Führen Sie eine regelmäßige Neuindizierung dieser Tabellen durch. Weitere Informationen finden Sie unter [neu organisieren und Indizes neu erstellen](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Stellen Sie sicher, dass die zum Filtern verwendeten Spalten richtig indiziert sind, und erstellen Sie die entsprechenden Indizes gegebenenfalls erneut. Weitere Informationen finden Sie unter [neu organisieren und Indizes neu erstellen](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Legen Sie die **Join_unique_key** -Eigenschaft für joinsfilter, die auf eindeutigen Spalten basieren. Weitere Informationen finden Sie unter [Join Filters](../../relational-databases/replication/merge/join-filters.md).  
  
-   Begrenzen Sie die Anzahl der Tabellen in der Joinsfilterhierarchie. Wenn Sie Joinsfilter für fünf oder mehr Tabellen erstellen, sollten Sie andere Lösungen in Betracht ziehen: Kleinere Tabellen, Tabellen, die nicht geändert werden, oder Tabellen, bei denen es sich primär um Nachschlagetabellen handelt, sollten in diesem Fall nicht gefiltert werden. Verwenden Sie Joinsfilter nur zwischen Tabellen, für die eine Partitionierung auf Abonnements erfolgen muss.  
  
-   Nehmen Sie zwischen Synchronisierungen weniger Änderungen an gefilterten Tabellen vor, oder führen Sie den Merge-Agent häufiger aus. Weitere Informationen zum Angeben von Synchronisierungszeitplänen finden Sie unter [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  