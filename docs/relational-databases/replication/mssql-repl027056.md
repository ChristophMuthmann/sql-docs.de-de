---
title: "MSSQL_REPL027056 | Microsoft Docs"
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
  - "MSSQL_REPL027056 (Fehler)"
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_REPL027056
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|27056|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Vom Mergeprozess konnte der Generierungsverlauf auf '%1' nicht geändert werden. Führen Sie zur Problembehandlung einen Neustart der Synchronisierung mit ausführlicher Verlaufsprotokollierung aus, und geben Sie eine Ausgabedatei an, in die geschrieben werden soll.|  
  
## Erklärung  
 Dieser Fehler wird in der Regel als Folge eine Konflikts in Systemtabellen der Mergereplikation ausgelöst, die extrem groß geworden sind. Meistens entstehen große Systemtabellen aufgrund einer langen Beibehaltungsdauer von Veröffentlichungen, da Metadaten bis zum Ablauf der Beibehaltungsdauer gespeichert werden müssen.  
  
## Benutzeraktion  
 **So lösen Sie das Problem:**  
  
1.  Verringern Sie den Wert des-**DownloadGenerationsPerBatch** und **- UploadGenerationsPerBatch** Parameter für den Merge-Agent, damit die Verarbeitung fortgesetzt werden, während Sie die zugrunde liegende Behandeln des Fehlers widmen. Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
    -   [Arbeiten mit Replikations-Agent-Profilen](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Anzeigen und Ändern von Replikations-Agent-Befehlszeilenparameter & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Replikations-Agent ausführbare Konzepte](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
2.  Geben Sie die Beibehaltungsdauer für die Veröffentlichung so niedrig wie möglich an. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
3.  Im Rahmen der Wartung für die Mergereplikation, überprüfen Sie gelegentlich die Vergrößerung der Systemtabellen Mergereplikation zugeordnet: **MSmerge_contents**, **MSmerge_genhistory**, und **MSmerge_tombstone**, **MSmerge_current_partition_mappings**, und **MSmerge_past_partition_mappings**. Führen Sie eine regelmäßige Neuindizierung dieser Tabellen durch. Weitere Informationen finden Sie unter [neu organisieren und Indizes neu erstellen](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  