---
title: "Sicherheit f&#252;r den &lt;Agentname-&gt;-Agent | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.agentnameagentsecurity.f1"
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Sicherheit f&#252;r den &lt;Agentname-&gt;-Agent
  Die **\< AgentName> -Agent-Sicherheit** auf der Seite können Sie angeben, die Konten, unter denen Verteilungs-Agent (für Transaktions- und momentaufnahmereplikation) oder Merge-Agent (bei Mergereplikation) ausführen und Verbindungen mit den Computern in einer Replikationstopologie. Informationen zu Agents und bewährte Methoden für die replikationssicherheit erforderlichen Berechtigungen finden Sie unter [Sicherheitsmodell des Replikations-Agent](../../relational-databases/replication/security/replication-agent-security-model.md) und [Replikationssicherheit, bewährte Methoden](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## Optionen  
 Klicken Sie auf die Eigenschaftenschaltfläche (**...**) in der Zeile für jeden Abonnenten Zugriff auf die **Verteilungs-Agent-Sicherheit** oder **Sicherheit für den Merge-Agent** Dialogfeld. Klicken Sie in dem geöffneten Dialogfeld auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die von den Agents verwendeten Konten erforderlich sind.  
  
 Wenn Sie die Einstellungen in einem der beiden Dialogfelder eingegeben haben, werden im Raster die Verbindungsinformationen zu dem Abonnenten angezeigt.  
  
 **Agent für Abonnent**  
 Die Namen aller Abonnenten.  
  
 **Verbindung mit Verteiler**  
 Wird bei der Transaktions- und Momentaufnahmereplikation angezeigt. Der Kontext, unter dem die Verbindung mit dem Verteiler hergestellt wird. Lokale Verbindungen werden immer unter dem Kontext des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Kontos hergestellt, das zum Ausführen der Agents verwendet wird:  
  
-   Bei Pushabonnements ist die lokale Verbindung die Verbindung mit dem Verteiler, dieses Feld immer angezeigt werden: **Impersonate ' \< Domäne>\\< Anmeldung\>"** oder **Impersonate ' \< Computer>\\< Anmeldung\>'** für Pushabonnements.  
  
-   Bei Pullabonnements kann die Verbindung auch unter dem Kontext einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung hergestellt werden. Feld zeigt eines der folgenden: **Anmeldenamen ' \< Login>'**, **Impersonate ' \< Domäne>\\< Anmeldung\>'** oder **Impersonate ' \< Computer>\\< Anmeldung\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, alle Verbindungen unter dem Kontext des Windows-Kontos herzustellen.  
  
 **Verbindung mit Verleger &Verteiler**  
 Wird bei Mergereplikation angezeigt. Der Kontext, unter dem die Verbindung mit dem Verleger und Verteiler hergestellt wird. Lokale Verbindungen werden immer unter dem Kontext des Windows-Kontos hergestellt, das zum Ausführen der Agents verwendet wird.  
  
-   Bei Pushabonnements ist die lokale Verbindung die Verbindung mit dem Verleger und Verteiler, damit immer in diesem Feld angezeigt wird: **Impersonate ' \< Domäne>\\< Anmeldung\>"** oder **Impersonate ' \< Computer>\\< Anmeldung\>'** für Pushabonnements.  
  
-   Bei Pullabonnements kann die Verbindung auch unter dem Kontext einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung hergestellt werden. Feld zeigt eines der folgenden: **Anmeldenamen ' \< Login>'**, **Impersonate ' \< Domäne>\\< Anmeldung\>'** oder **Impersonate ' \< Computer>\\< Anmeldung\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, alle Verbindungen unter dem Kontext des Windows-Kontos herzustellen.  
  
 **Verbindung mit Abonnent**  
 Der Kontext, unter dem die Verbindung mit dem Abonnenten hergestellt wird. Lokale Verbindungen werden immer unter dem Kontext des Windows-Kontos hergestellt, das zum Ausführen der Agents verwendet wird.  
  
-   Bei Pullabonnements ist die lokale Verbindung die Verbindung mit dem Abonnenten, dieses Feld immer angezeigt werden: **Impersonate ' \< Domäne>\\< Anmeldung\>"** oder **Impersonate ' \< Computer>\\< Anmeldung\>'** für Pushabonnements.  
  
-   Bei Pushabonnements kann die Verbindung auch unter dem Kontext einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung hergestellt werden. Feld zeigt eines der folgenden: **Anmeldenamen ' \< Login>'**, **Impersonate ' \< Domäne>\\< Anmeldung\>'** oder **Impersonate ' \< Computer>\\< Anmeldung\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, alle Verbindungen unter dem Kontext des Windows-Kontos herzustellen.  
  
## Siehe auch  
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Sicherheit und Schutz & #40; Replikation & #41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  