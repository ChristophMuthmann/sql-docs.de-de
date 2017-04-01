---
title: "MSSQL_ENG020557 | Microsoft Docs"
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
  - "MSSQL_ENG020557 (Fehler)"
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# MSSQL_ENG020557
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20557|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Der Agent wird heruntergefahren. Weitere Informationen finden Sie im Auftragsverlauf des SQL Server-Agents für den Auftrag '%s'.|  
  
## Erklärung  
 Ein Replikations-Agent wurde beendet, ohne dass ein Grund in die entsprechende Verlaufstabelle geschrieben wurde, oder der Agent wurde während eines Prozesses beendet.  
  
## Benutzeraktion  
  
-   Starten Sie den Agent neu, um zu ermitteln, ob er nun fehlerfrei ausgeführt wird. Weitere Informationen finden Sie unter [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Replikations-Agent ausführbare Konzepte](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Überprüfen Sie Agent- und Auftragsverlauf auf andere Fehler, die eventuell um dieselbe Zeit aufgetreten sind. Informationen zum Anzeigen des Agentstatus und der Fehlerinformationen im Replikationsmonitor finden Sie unter folgenden Themen:  
  
    -   Der Snapshot-Agent, Protokolllese-Agent und Warteschlangenlese-Agent, finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents verknüpft sind mit einer Veröffentlichung & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
    -   Der Snapshot-Agent und Merge-Agent finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
-   Stellen Sie sicher, dass die Konnektivität zwischen den Computern, auf die der Agent zugreift, funktioniert, und stellen Sie dann mithilfe eines Hilfsprogramms eine Verbindung mit den einzelnen Computern her, z. B. mithilfe des Hilfsprogramms **sqlcmd** . Benutzen Sie zum Herstellen der Verbindungen dasselbe Konto wie der Agent. Weitere Informationen zu den erforderlichen Berechtigungen für die einzelnen Agentkonten finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Wenn der Fehler auftritt, während Sie eine Momentaufnahme erstellen oder anwenden, überprüfen Sie die Dateien im Momentaufnahmeverzeichnis auf Fehler.  
  
-   Wenn der Fehler weiterhin auftritt, erhöhen Sie die Protokollierungsstufe des Agents, und geben Sie eine Ausgabedatei für das Protokoll an. Je nach Zusammenhang, in dem der Fehler auftritt, finden Sie hier möglicherweise die Schritte, die zum Fehler führen, und weitere Fehlermeldungen. Weitere Informationen zur Konfiguration der Protokollierung für die Replikation finden Sie im Microsoft Knowledge Base-Artikel [312292](http://support.microsoft.com/kb/312292).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  