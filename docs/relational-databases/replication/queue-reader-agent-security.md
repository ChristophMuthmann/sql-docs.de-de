---
title: "Sicherheit f&#252;r den Warteschlangenlese-Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.security.QRA.f1"
helpviewer_keywords: 
  - "Sicherheit für den Warteschlangenlese-Agent (Dialogfeld)"
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Sicherheit f&#252;r den Warteschlangenlese-Agent
  Im Dialogfeld **Sicherheit für den Warteschlangenlese-Agent** können Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto angeben, unter dem der Warteschlangenlese-Agent ausgeführt wird und Verbindungen mit dem Verteiler herstellt. Der Agent stellt eine Verbindung mit dem Verleger über das angegebene Konto die **Verlegereigenschaften** im Dialogfeld (verfügbar über die **Verteilereigenschaften** im Dialogfeld); der Agent stellt eine Verbindung mit dem Abonnenten mithilfe desselben Kontexts wie der Verteilungs-Agent für das Abonnement. Weitere Informationen finden Sie unter [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Das Konto muss für das angegebene Kennwort gültig sein. Konten und Kennwörter werden erst bei der Ausführung eines Agents überprüft.  
  
## Optionen  
 **Prozesskonto**  
 Geben Sie das Windows-Konto ein, unter dem der Warteschlangenlese-Agent auf dem Verteiler ausgeführt wird. Das Windows-Konto, das Sie angeben, muss mindestens Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.  
  
 **Das Kennwort** und **Kennwort bestätigen**  
 In diese Felder geben Sie das Kennwort für das Windows-Konto ein.  
  
## Siehe auch  
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  