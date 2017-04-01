---
title: "Abonnementtyp | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.subscriptiontype.f1"
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Abonnementtyp
  Die Mergereplikation umfasst zwei abonnementtypen: Server und Client (in früheren Versionen von genannten [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als globale und lokale, bzw.). Abonnenten mit einem Serverabonnement können:  
  
-   Daten für andere Abonnenten erneut veröffentlichen.  
  
-   Als alternative Synchronisierungspartner dienen.  
  
-   Konflikte entsprechend einer von Ihnen festgelegten Priorität lösen.  
  
 Die meisten Abonnenten benötigen diese Funktionalität nicht und können das Clientabonnement verwenden. Mit Clientabonnements können immer noch Konflikte erkannt und gelöst werden, Abonnenten wird jedoch keine Priorität zugeordnet: der erste Abonnent, der eine Änderung an den Verleger sendet, gewinnt in Konflikten, die durch diese Änderung auftreten können.  
  
> [!NOTE]  
>  Nach dem Erstellen eines Abonnements kann der Abonnementtyp nicht mehr geändert werden.  
  
## Optionen  
 **Abonnementeigenschaften**  
 Wählen Sie für jeden Abonnenten **Client** oder **Server** aus dem Dropdown-Listenfeld in der **Abonnementtyp** Spalte. Für Abonnenten mit serverabonnements, geben Sie eine Zahl zwischen 0 und 99,99 in die **Priorität für Konfliktlösung** Spalte (je höher die Zahl, desto höher die Priorität für den Abonnenten).  
  
## Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  