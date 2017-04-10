---
title: "Sicherheit f&#252;r den Protokolllese-Agent (Peer-zu-Peer-Replikation) | Microsoft Docs"
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
  - "sql13.rep.p2pwizard.LRA.f1"
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Sicherheit f&#252;r den Protokolllese-Agent (Peer-zu-Peer-Replikation)
  Mithilfe der Seite **Sicherheit für den Protokolllese-Agent** können Sie Konten angeben, unter denen der Protokolllese-Agent auf jedem Peer ausgeführt wird und die Verbindungen hergestellt werden. Informationen zu Agents und bewährte Methoden für die replikationssicherheit erforderlichen Berechtigungen finden Sie unter [Sicherheitsmodell des Replikations-Agent](../../relational-databases/replication/security/replication-agent-security-model.md) und [Replikationssicherheit, bewährte Methoden](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Es gibt einen Protokolllese-Agent für jede Datenbank, die mithilfe der Transaktionsreplikation veröffentlicht wird. Wenn der Protokolllese-Agent für eine Datenbank bereits konfiguriert wurde (entweder für eine Veröffentlichung bei einer vorherigen Ausführung dieses Assistenten oder für eine andere Transaktionsveröffentlichung in derselben Datenbank), können Sie die bestehenden Anmeldeinformationen mit diesem Assistenten nicht ändern. Von Ihnen neu angegebene Anmeldeinformationen werden ignoriert. Sie können die Anmeldeinformationen im Dialogfeld **Veröffentlichungseigenschaften** ändern. Weitere Informationen finden Sie unter [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## Optionen  
 Klicken Sie auf die Eigenschaftenschaltfläche (**...**) in der Zeile für jeden Peer für den Zugriff auf die **Sicherheit für den Protokolllese-Agent** Dialogfeld. Klicken Sie im geöffneten Dialogfeld **Sicherheit für den Protokolllese-Agent** auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die von den Agents verwendeten Konten erforderlich sind.  
  
 Wenn Sie die Einstellungen im Dialogfeld eingegeben haben, werden im Raster die Verbindungsinformationen zu dem Abonnenten angezeigt.  
  
 **Agents für Verleger**  
 Der Name jeder Peerserverinstanz.  
  
 **Peerdatenbank**  
 Die Datenbank, die auf jedem Peer als Veröffentlichungs- und Abonnementdatenbank dient.  
  
 **Verbindung mit Verteiler**  
 Der Kontext, unter dem die Verbindung mit dem Verteiler hergestellt wird. Die Verbindung mit dem Verteiler wird immer hergestellt, unter dem Kontext des der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Agent ausgeführt wird, damit dieses Feld immer angezeigt **Impersonate ' \< Domäne>\\< Anmeldung\>"** oder **Impersonate ' \< Computer>\\< Anmeldung\>'**.  
  
 **Verbindung mit dem Verleger**  
 Der Kontext, unter dem die Verbindung mit dem Verleger hergestellt wird. Die Verbindung mit dem Verleger kann mithilfe einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung oder mithilfe des Windows-Kontos, unter dem der Agent ausgeführt wird, hergestellt werden. Feld zeigt eines der folgenden: **Anmeldenamen ' \< Login>'**, **Impersonate ' \< Domäne>\\< Anmeldung\>'** oder **Impersonate ' \< Computer>\\< Anmeldung\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, alle Verbindungen unter dem Kontext des Windows-Kontos herzustellen.  
  
## Siehe auch  
 [Verwalten einer Peer-to-Peer-Topologie & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  