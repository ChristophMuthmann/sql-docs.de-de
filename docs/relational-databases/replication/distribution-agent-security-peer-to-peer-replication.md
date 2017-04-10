---
title: "Sicherheit f&#252;r den Verteilungs-Agent (Peer-zu-Peer-Replikation) | Microsoft Docs"
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
  - "sql13.rep.p2pwizard.DA.f1"
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Sicherheit f&#252;r den Verteilungs-Agent (Peer-zu-Peer-Replikation)
  Die **Sicherheit für den Verteilungs-Agent** Seite können Sie die Konten angeben, unter dem der Verteilungsagent ausgeführt wird und Verbindungen mit den Computern in einer Peer-to-Peer-Topologie. Informationen zu Agents und bewährte Methoden für die replikationssicherheit erforderlichen Berechtigungen finden Sie unter [Sicherheitsmodell des Replikations-Agent](../../relational-databases/replication/security/replication-agent-security-model.md) und [Replikationssicherheit, bewährte Methoden](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Wenn der Verteilungs-Agent für ein Abonnement bereits in einer früheren Ausführung dieses Assistenten konfiguriert wurde, können Sie die entsprechenden in diesem Assistenten verwendeten Anmeldeinformationen nicht ändern. Von Ihnen neu angegebene Anmeldeinformationen werden ignoriert. Sie können die Anmeldeinformationen im Dialogfeld **Abonnementeigenschaften** ändern. Weitere Informationen finden Sie unter [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## Optionen  
 Klicken Sie auf die Eigenschaftenschaltfläche (**...**) in der Zeile für jeden Abonnenten Zugriff auf die **Verteilungs-Agent-Sicherheit** Dialogfeld. Klicken Sie im geöffneten Dialogfeld **Sicherheit für den Verteilungs-Agent** auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die von den Agents verwendeten Konten erforderlich sind.  
  
 Wenn Sie die Einstellungen in einem der beiden Dialogfelder eingegeben haben, werden im Raster die Verbindungsinformationen zu dem Abonnenten angezeigt.  
  
 **Agent für Abonnent**  
 Der Name der einzelnen Peers.  
  
 **Peerdatenbank**  
 Die Datenbank auf dem Peer, der sowohl als Veröffentlichungs- als auch als Abonnementdatenbank dient.  
  
 **Verbindung mit Verteiler**  
 Der Kontext, unter dem die Verbindung mit dem Verteiler hergestellt wird. Lokale Verbindungen werden immer unter dem Kontext des Windows-Kontos hergestellt, das zum Ausführen der Agents verwendet wird. Dieser Assistent erstellt Pushabonnements (die lokale Verbindung ist die Verbindung mit dem Verteiler), dieses Feld immer angezeigt werden: **Impersonate ' \< Domäne>\\< Anmeldung\>"** oder **Impersonate ' \< Computer>\\< Anmeldung\>'**.  
  
 **Verbindung mit Abonnent**  
 Der Kontext, unter dem die Verbindung mit dem Abonnenten hergestellt wird. Die Verbindung kann entweder mithilfe des Kontexts des Windows-Kontos hergestellt werden, unter dem der Agent ausgeführt wird, oder mithilfe des Kontexts einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung. Feld zeigt eines der folgenden: **Anmeldenamen ' \< Login>'**, **Impersonate ' \< Domäne>\\< Anmeldung\>'** oder **Impersonate ' \< Computer>\\< Anmeldung\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, alle Verbindungen unter dem Kontext des Windows-Kontos herzustellen.  
  
## Siehe auch  
 [Verwalten einer Peer-to-Peer-Topologie & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  