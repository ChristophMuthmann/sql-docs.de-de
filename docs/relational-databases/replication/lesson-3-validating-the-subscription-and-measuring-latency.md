---
title: "Lektion 3: Überprüfen des Abonnements und Messen der Latenzzeit | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 93f602d096806a79f049d6c602ad92c6b16f9e26
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>Lektion 3: Überprüfen des Abonnements und Messen der Latenzzeit
In dieser Lektion verwenden Sie Überwachungstoken, um sicherzustellen, dass Änderungen auf dem Abonnenten repliziert werden, und um die Latenzzeit (die Zeit, nach der eine auf dem Verleger vorgenommene Änderung auf dem Abonnenten angezeigt wird) zu bestimmen. Diese Lektion setzt voraus, dass Sie die vorherige Lektion abgeschlossen haben: [Lektion 2: Erstellen eines Abonnements für die Transaktionsveröffentlichung](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>So fügen Sie ein Überwachungstoken ein und zeigen Informationen zum Token an  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, erweitern Sie den Serverknoten, klicken Sie mit der rechten Maustaste auf den Ordner **Replikation** , und klicken Sie anschließend auf **Replikationsmonitor starten**.  
  
    Der Replikationsmonitor wird gestartet.  
  
2.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie die Verlegerinstanz, und klicken Sie dann auf die **AdvWorksProductTrans** -Veröffentlichung.  
  
3.  Klicken Sie auf die Registerkarte **Überwachungstoken** .  
  
4.  Klicken Sie auf **Überwachung einfügen**.  
  
5.  In den folgenden Spalten sehen Sie die für das Überwachungstoken benötigte Zeit: **Verleger zu Verteiler**, **Verteiler zu Abonnent**, **Gesamtlatenzzeit**. Mit dem Wert **Ausstehend** wird angegeben, dass das Token noch nicht den Bestimmungspunkt erreicht hat.  
  
## <a name="next-steps"></a>Nächste Schritte  
In dieser Lektion haben Sie mithilfe von Überwachungstoken erfolgreich überprüft, dass Datenänderungen vom Verleger zum Abonnenten repliziert werden. Zudem können Sie Daten in der **Product** -Tabelle auf dem Verleger einfügen, aktualisieren und löschen und die **Product** -Tabelle auf dem Abonnenten abfragen, um diese Änderungen anzuzeigen, nachdem sie repliziert wurden.  
  
Damit ist das Lernprogramm Replizieren von Daten zwischen Servern mit kontinuierlicher Verbindung abgeschlossen. Ein ähnliches Lernprogramm zur Mergereplikation finden Sie unter [Tutorial: Replicating Data with Mobile Clients](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md).  
  
## <a name="see-also"></a>Siehe auch  
[Messen der Latenzzeit und Überprüfen der Verbindungen bei Transaktionsreplikationen](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
  

