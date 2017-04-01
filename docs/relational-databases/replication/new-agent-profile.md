---
title: "Neues Agentprofil | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.profiles.newperfprofile.f1"
helpviewer_keywords: 
  - "Neues Agentprofil (Dialogfeld)"
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Neues Agentprofil
  Im Dialogfeld **Neues Agentprofil** können Sie ein neues Profil erstellen. Neue Profile werden immer auf der Basis von vorhandenen Profilen erstellt. Sie können jedoch so geändert werden, dass bestimmte Anforderungen von Anwendungen erfüllt werden. Nach dem Erstellen kann das Profil auf vorhandene und zukünftige Agentaufträge im Dialogfeld **Agentprofile** angewendet werden. Agentparameterwerte können bearbeitet werden, dem \<**AgentProfileName > Eigenschaften** Dialogfeld.  
  
## Optionen  
 **Name**  
 Geben Sie einen Namen für das Profil ein.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung für das Profil ein.  
  
 **Parameter**  
 Die im Profil enthaltenen Agentparameter. In dem Profil, das als Basis für das neue Profil fungiert, müssen nicht notwendigerweise für alle Parameter Werte angegeben sein. Wenn Sie alle für einen bestimmten Agent gültigen Parameter anzeigen möchten, müssen Sie das Kontrollkästchen **Nur die in diesem Profil verwendeten Parameter anzeigen** deaktivieren. Eine Beschreibung der einzelnen Parameter finden Sie unter:  
  
-   [Replikationsmomentaufnahme-Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [Replikationsprotokolllese-Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replikationsverteilungs-Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [Replikationsmerge-Agent](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [Warteschlangenlese-Agent der Microsoft SQL Server-Replikation](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 **Standardwert**  
 Der Standardwert für jeden Agentparameter.  
  
 **Wert**  
 Der für den Parameter angegebene Wert in dem Profil, das als Basis für das neue Profil fungiert. Bearbeiten Sie dieses Feld für alle Parameterwerte, die Sie ändern möchten.  
  
 **Nur die in diesem Profil verwendeten Parameter anzeigen**  
 Deaktivieren Sie das Kontrollkästchen, um nur die für einen bestimmten Agent gültigen Parameter anzuzeigen.  
  
## Siehe auch  
 [Arbeiten mit Replikations-Agent-Profilen](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replikations-Agent-Profile](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  