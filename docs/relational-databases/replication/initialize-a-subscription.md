---
title: Initialisieren eines Abonnements | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 37e0893ec7f598c3b6ab631a4e0e2707372a5f01
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="initialize-a-subscription"></a>Initialisieren eines Abonnements
  Abonnenten in einer Replikationstopologie müssen initialisiert werden, damit sie für jeden Artikel in der Veröffentlichung, die sie abonniert haben, eine Kopie des Schemas sowie alle erforderlichen Replikationsobjekte (gespeicherte Prozeduren, Trigger, Metadatentabellen usw.) erhalten. Darüber hinaus erhält der Abonnent typischerweise einen Anfangsdatensatz. Die Standardinitialisierungsmethode verwendet eine vollständige Momentaufnahme mit Schema, Replikationsobjekten und Daten. Veröffentlichungen können aber auch ohne eine vollständige Momentaufnahme initialisiert werden.  
  
 Weitere Informationen finden Sie unter [Initialize a Subscription with a Snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) und [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
