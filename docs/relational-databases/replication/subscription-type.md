---
title: Abonnementtyp | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cfd1ed68438aa7c79a5a6f2037cec5310fd60ce8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="subscription-type"></a>Abonnementtyp
  Die Mergereplikation umfasst zwei Abonnementtypen: Server und Client (in früheren Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als global bzw. lokal bezeichnet). Abonnenten mit einem Serverabonnement können:  
  
-   Daten für andere Abonnenten erneut veröffentlichen.  
  
-   Als alternative Synchronisierungspartner dienen.  
  
-   Konflikte entsprechend einer von Ihnen festgelegten Priorität lösen.  
  
 Die meisten Abonnenten benötigen diese Funktionalität nicht und können das Clientabonnement verwenden. Mit Clientabonnements können immer noch Konflikte erkannt und gelöst werden, Abonnenten wird jedoch keine Priorität zugeordnet: der erste Abonnent, der eine Änderung an den Verleger sendet, gewinnt in Konflikten, die durch diese Änderung auftreten können.  
  
> [!NOTE]  
>  Nach dem Erstellen eines Abonnements kann der Abonnementtyp nicht mehr geändert werden.  
  
## <a name="options"></a>Optionen  
 **Abonnementeigenschaften**  
 Wählen Sie für jeden Abonnenten aus der Dropdownliste in der **Abonnementtyp** -Spalte die Option **Client** oder **Server** aus. Geben Sie für Abonnenten mit Serverabonnements in der **Priorität für Konfliktlösung** -Spalte eine Zahl zwischen 0 und 99,99 ein (je höher die Zahl, desto höher die Priorität des Abonnenten).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
