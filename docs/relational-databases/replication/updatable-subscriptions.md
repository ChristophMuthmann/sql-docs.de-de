---
title: "Aktualisierbare Abonnements | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.updatablesubscriptions.f1"
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Aktualisierbare Abonnements
  Für die Transaktionsreplikation sollten replizierte Daten als schreibgeschützt behandelt werden. Sie können jedoch ändern, replizierte Daten auf einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten durch Verwendung aktualisierbarer Abonnements. Wenn Sie Daten auf dem Abonnenten ändern möchten, wählen Sie in Abhängigkeit von Ihren Anforderungen eine der folgenden Optionen aus:  
  
|Aktualisierbarer Abonnementtyp|Anforderungen|  
|---------------------------------|------------------|  
|Sofortige Updates|Verleger und Abonnent müssen verbunden sein, damit Daten auf dem Abonnenten aktualisiert werden können.|  
|Verzögerte Updates über eine Warteschlange|Verleger und Abonnent müssen nicht verbunden sein, damit Daten auf dem Abonnenten aktualisiert werden können. Updates können zunächst offline vorgenommen und später dann zwischen Verleger und Abonnent synchronisiert werden.|  
  
## Optionen  
 **Abonnentenänderungen replizieren**  
 Aktivieren Sie das Kontrollkästchen in der **replizieren** -Spalte für jeden Abonnenten, die Aktualisierungen vornehmen sollten. Für die Abonnenten, die Updates vornehmen, können die entsprechende Option aus dem Dropdown-Listenfeld in der **Commit auf Verleger** Spalte:  
  
-   Für ein Abonnement mit sofortigem Update wählen Sie **Commit für Änderungen gleichzeitig ausführen** aus.  
  
-   Für ein Abonnement mit verzögertem Update über eine Warteschlange wählen Sie **Änderungen in die Warteschlange einreihen und Commit baldmöglichst ausführen** .  
  
## Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Aktualisierbare Abonnements für die Transaktionsreplikation](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  