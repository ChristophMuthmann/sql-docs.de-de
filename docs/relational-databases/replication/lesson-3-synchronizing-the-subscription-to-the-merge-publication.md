---
title: "Lektion 3: Synchronisieren des Abonnements für die Mergeveröffentlichung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2309fd6c194dba691f32a1f6384b0cd9ad1ab6b0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>Lektion 3: Synchronisieren des Abonnements für die Mergeveröffentlichung
In dieser Lektion starten Sie den Merge-Agent, um das Abonnement mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]zu initialisieren. Mithilfe dieser Prozedur können Sie außerdem eine Synchronisierung mit dem Verleger ausführen. Diese Lektion setzt voraus, dass Sie die vorherige Lektion abgeschlossen haben: [Lektion 2: Erstellen eines Abonnements für die Mergeveröffentlichung](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>So starten Sie die Synchronisierung und initialisieren das Abonnement  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, und erweitern Sie dann den Serverknoten sowie den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Abonnements** mit der rechten Maustaste auf das Abonnement in der Datenbank **SalesOrdersReplica** , und klicken Sie anschließend auf **Synchronisierungsstatus anzeigen**.  
  
3.  Klicken Sie auf **Start** , um das Abonnement zu initialisieren.  
  
## <a name="next-steps"></a>Nächste Schritte  
Sie haben den Merge-Agent erfolgreich ausgeführt, um die Synchronisierung zu starten und das Abonnement zu initialisieren. Sie können auch Daten in der **SalesOrderHeader** -Tabelle oder der **SalesOrderDetail** -Tabelle auf dem Verleger oder dem Abonnenten einfügen, aktualisieren oder löschen, diese Schrittfolge wiederholen, wenn eine Netzwerkverbindung verfügbar ist, um Daten zwischen dem Verleger und dem Abonnenten zu synchronisieren, und anschließend können Sie die **SalesOrderHeader** -Tabelle oder die **SalesOrderDetail** -Tabelle auf dem anderen Server abfragen, um die replizierten Änderungen anzuzeigen.  
  
Damit ist das Lernprogramm zum Replizieren von Daten mit mobilen Clients abgeschlossen. Ein ähnliches Lernprogramm für Transaktionsreplikationen finden Sie unter [Tutorial: Replicating Data Between Continuously Connected Servers](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md).  
  
## <a name="see-also"></a>Siehe auch  
[Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)  
[Synchronisieren eines Pullabonnements](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
