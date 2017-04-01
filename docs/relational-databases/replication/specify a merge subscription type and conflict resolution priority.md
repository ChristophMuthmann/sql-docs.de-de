---
title: "Angeben eines Mergeabonnementtyps und einer Konfliktl&#246;sungspriorit&#228;t (Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "02/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation], Konfliktlöser für die Mergereplikation"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Angeben eines Mergeabonnementtyps und einer Konfliktl&#246;sungspriorit&#228;t (Server Management Studio)
  Auf der Seite **Abonnementtyp** des Assistenten für neue Abonnements können Sie einen Mergeabonnementtyp und eine Konfliktlösungspriorität angeben. Weitere Informationen zum Verwenden dieses Assistenten finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) und [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
 Abonnementtyp kann nicht geändert werden, nachdem ein Abonnement wird erstellt, aber die Priorität werden, für den serverabonnementtyp in geändert kann der **Abonnementeigenschaften - \< Publisher>: \< PublicationDatabase>** das Dialogfeld. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) und [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
### So geben Sie einen Mergeabonnementtyp und eine Konfliktlösungspriorität an  
  
1.  Wählen Sie auf der Seite **Abonnementtyp** des Assistenten für neue Abonnements für die Option **Abonnementtyp** entweder **Client** oder **Server** aus.  
  
2.  Wenn Sie den Abonnementtyp auswählen **Server**, geben Sie auch einen Wert (0,00 bis 99,99) für die **Priorität für Konfliktlösung** Option.  
  
### So ändern Sie die Konfliktlösungspriorität  
  
1.  In der **Abonnementeigenschaften - \< Publisher>: \< PublicationDatabase>** auf dem Verleger, geben Sie einen Wert (0,00 bis 99,99) für die **Priorität** Option.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  