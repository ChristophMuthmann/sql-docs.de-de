---
title: Replikations-Agentprofile | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Distribution Agent, profiles
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- Merge Agent, profiles
- agents [SQL Server replication], profiles
- Queue Reader Agent, profiles
- profiles [SQL Server], replication agents
- Snapshot Agent, profiles
- Log Reader Agent, profiles
ms.assetid: 0e980725-e42f-4283-94cb-d8a6dba5df62
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a11a7821231d4c7fa3a8719a05bdd1a7bc49ff47
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="replication-agent-profiles"></a>Replikations-Agent-Profile
  Wenn die Replikation konfiguriert wird, wird ein Satz Agentprofile auf dem Verteiler installiert. Ein Agentprofil enthält eine Reihe Parameter, die bei jeder Ausführung des Agents zur Anwendung kommen: Jeder Agent meldet sich während seines Startprozesses beim Verteiler an und fragt die Parameter in seinem Profil ab. Im Fall von Mergeabonnements, die die Websynchronisierung verwenden, werden Profile heruntergeladen und auf dem Verteiler gespeichert. Wenn das Profil geändert wird, wird das Profil auf dem Verteiler aktualisiert, wenn der Merge-Agent das nächste Mal ausgeführt wird. Weitere Informationen zur Websynchronisierung finden Sie unter [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Die Replikation stellt ein Standardprofil für jeden Agent und zusätzliche vordefinierte Profile für den Protokolllese-Agent, den Verteilungs-Agent und den Merge-Agent bereit. Neben den bereitgestellten Profilen können Sie Profile erstellen, die sich für Ihre Anwendungsanforderungen eignen. Ein Agentprofil ermöglicht ein einfaches Ändern von Schlüsselparametern für alle Agents, die dem Profil zugeordnet sind. Wenn Sie z. B. 20 Momentaufnahme-Agents haben und den Zeittimeout für Abfragen ändern müssen (den **-QueryTimeout** -Parameter), können Sie das Profil für die Momentaufnahme-Agents aktualisieren. Beim nächsten Ausführen verwenden alle Agents dieses Typs automatisch den neuen Wert.  
  
 Sie können auch verschiedene Profile für unterschiedliche Instanzen eines Agents verwenden. Ein Merge-Agent, der beispielsweise über eine DFÜ-Verbindung mit dem Verleger und dem Verteiler verbunden wird, könnte einen Satz Parameter verwenden, die sich besser für die langsamere Kommunikationsverbindung eignen, indem er das **** Profil für langsame Links verwendet.  
  
> [!NOTE]  
>  Wenn Sie einen Wert für einen Agentparameter in der Befehlszeile angeben, überschreibt dieser Wert den Wert, der für denselben Parameter im Agentprofil festgelegt wurde.  
  
 **So verwenden und ändern Sie Agentprofile**  
  
-   [Arbeiten mit Replikations-Agent-Profilen](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
## <a name="snapshot-agent-profiles"></a>Profile des Momentaufnahme-Agents  
 In der folgenden Tabelle werden die Parameter aufgeführt, die im Standardprofil für den Momentaufnahme-Agent definiert sind. Weitere Informationen zu diesen Parametern finden Sie unter [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md).  
  
||default|  
|-|-------------|  
|**-BcpBatchSize**|100000|  
|**-HistoryVerboseLevel**|2|  
|**-LoginTimeout**|15|  
|**-QueryTimeout**|1800|  
  
## <a name="log-reader-agent-profiles"></a>Profile des Protokolllese-Agents  
 In der folgenden Tabelle werden die Parameter aufgeführt, die in den Profilen für den Protokolllese-Agent definiert sind. Jede Spalte in der Tabelle steht für ein benanntes Profil. Weitere Informationen zu diesen Parametern finden Sie unter [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
||default|Ausführlicher Verlauf|  
|-|-------------|---------------------|  
|**-HistoryVerboseLevel**|1|2|  
|**-LoginTimeout**|15|15|  
|**-LogScanThreshold**|500000|500000|  
|**-PollingInterval**|5|5|  
|**-QueryTimeout**|1800|1800|  
|**-ReadBatchSize**|500|500|  
  
## <a name="distribution-agent-profiles"></a>Profile des Verteilungs-Agents  
 In der folgenden Tabelle werden die Parameter aufgeführt, die in den Profilen für den Verteilungs-Agent definiert sind. Jede Spalte in der Tabelle steht für ein benanntes Profil. Weitere Informationen zu diesen Parametern finden Sie unter [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
||default|Ausführlicher Verlauf|Synchronisierungsverwaltung von Windows|Fortsetzen bei Datenkonsistenzfehlern|Verteilungsprofil für das OLE DB-Streaming|  
|-|-------------|---------------------|-------------------------------------|-----------------------------------------|----------------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|2147473647|  
|**-CommitBatchSize**|100|100|100|100|100|  
|**-CommitBatchThreshold**|1000|1000|1000|1000|1000|  
|**-HistoryVerboseLevel**|1|2|1|1|1|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|  
|**-MaxBcpThreads**|1|1|1|1|1|  
|**-MaxDeliveredTransactions**|0|0|0|0|0|  
|**-OledbStreamThreshold**|NULL|NULL|NULL|NULL|32768|  
|**-PacketSize**|NULL|NULL|NULL|NULL|32768|  
|**-PollingInterval**|5|5|5|5|5|  
|**-QueryTimeout**|1800|1800|1800|1800|1800|  
|**-SkipErrors**|NULL|NULL|NULL|**-SkipErrors** 2601:2627:20598|NULL|  
|**-TransactionsPerHistory**|100|100|100|100|100|  
|**-UseOledbStreaming**|NULL|NULL|NULL|NULL|**-UseOledbStreaming**|  
  
## <a name="merge-agent-profiles"></a>Profile des Merge-Agents  
 In der folgenden Tabelle werden die Parameter aufgeführt, die in den Profilen für den Merge-Agent definiert sind. Jede Spalte in der Tabelle steht für ein benanntes Profil. Weitere Informationen zu diesen Parametern finden Sie unter [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
||default|Ausführlicher Verlauf|Synchronisierungsverwaltung von Windows|Zeilenanzahlüberprüfung|Überprüfung der Zeilenanzahl und Prüfsumme|Langsame Links|Server-zu-Server für hohes Volumen|  
|-|-------------|---------------------|-------------------------------------|-------------------------|--------------------------------------|---------------|------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|100000|100000|100000|  
|**-ChangesPerHistory**|100|50|50|100|100|100|1000|  
|**-DestThreads**|2|1|1|1|1|1|4|  
|**-DownloadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-DownloadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-DownloadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-FastRowCount**|1|1|1|1|1|1|1|  
|**-HistoryVerboseLevel**|2|3|1|1|2|1|2|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|15|15|  
|**-MaxDownloadChanges**|0|0|0|0|0|0|0|  
|**-MaxUploadChanges**|0|0|0|0|0|0|0|  
|**-MetadataRetentionCleanup**|1|1|1|1|1|1|1|  
|**-NumDeadlockRetries**|5|5|5|5|5|5|5|  
|**-ParallelUploadDownload**|NULL|NULL|NULL|NULL|NULL|NULL|1|  
|**-PollingInterval**|60|60|60|60|60|60|60|  
|**-QueryTimeout**|300|300|300|300|300|300|600|  
|**-QueueSizeMultiplier**|NULL|NULL|NULL|NULL|NULL|NULL|5|  
|**-SrcThreads**|2|2|2|2|2|1|3|  
|**-StartQueueTimeout**|0|0|0|0|0|0|0|  
|**-UploadGenerationsPerBatch**|50|50|50|50|50|1|500|  
|**-UploadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-UploadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-Validate**|0|0|0|1|3|0|0|  
|**-ValidateInterval**|60|60|60|60|60|60|60|  
  
## <a name="queue-reader-agent-profiles"></a>Profile des Warteschlangenlese-Agents  
 In der folgenden Tabelle werden die Parameter aufgeführt, die im Standardprofil für den Warteschlangenlese-Agent definiert sind. Weitere Informationen zu diesen Parametern finden Sie unter [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md).  
  
||default|  
|-|-------------|  
|**-HistoryVerboseLevel**|1|  
|**-LoginTimeout**|15|  
|**-PollingInterval**|5|  
|**-QueryTimeout**|1800|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Anzeigen und Ändern von Befehlszeilenparametern des Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)   
 [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
