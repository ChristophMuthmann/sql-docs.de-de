---
title: "Lektion 1: Veröffentlichen von Daten mithilfe der Transaktionsreplikation | Microsoft-Dokumentation"
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
ms.assetid: 9c55aa3c-4664-41fc-943f-e817c31aad5e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 021ff6838de18ea03a50aae661d543061088ae87
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-1-publishing-data-using-transactional-replication"></a>Lektion 1: Veröffentlichen von Daten mithilfe der Transaktionsreplikation
In dieser Lektion erstellen Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Transaktionsveröffentlichung, um eine gefilterte Teilmenge der **Product** -Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank zu veröffentlichen. Außerdem fügen Sie der Veröffentlichungszugriffsliste (Publication Access List, PAL) die vom Verteilungs-Agent verwendete SQL Server-Anmeldung hinzu. Bevor Sie dieses Tutorial starten, sollten Sie das vorherige Tutorial ( [Vorbereiten des Servers für die Replikation](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)) abgeschlossen haben.  
  
### <a name="to-create-a-publication-and-define-articles"></a>So erstellen Sie eine Veröffentlichung und definieren Artikel  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** und klicken Sie mit der rechten Maustaste auf den Ordner **Lokale Veröffentlichungen** . Klicken Sie anschließend auf **Neue Veröffentlichung**.  
  
    Der Assistent für neue Veröffentlichung wird gestartet.  
  
3.  Wählen Sie auf der Seite Veröffentlichungsdatenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]aus, und klicken Sie anschließend auf **Weiter**.  
  
4.  Wählen Sie auf der Seite Veröffentlichungstyp **Transaktionsveröffentlichung**aus, und klicken Sie anschließend auf **Weiter**.  
  
5.  Erweitern Sie auf der Seite Artikel den Knoten **Tabellen** , aktivieren Sie das Kontrollkästchen **Product** , erweitern Sie anschließend **Product** und deaktivieren Sie die Kontrollkästchen **ListPrice** und **StandardCost** . Klicken Sie auf **Weiter**.  
  
6.  Klicken Sie auf der Seite Tabellenzeilen filtern auf **Hinzufügen**.  
  
7.  Klicken Sie im Dialogfeld **Filter hinzufügen** auf die Spalte **SafetyStockLevel** , klicken Sie auf den Pfeil nach rechts, um der WHERE-Klausel der Filteranweisung die Spalte hinzuzufügen, und ändern Sie die WHERE-Klausel wie folgt:  
  
    ```  
    WHERE [SafetyStockLevel] < 500  
    ```  
  
8.  Klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
9. Aktivieren Sie das Kontrollkästchen **Momentaufnahme sofort erstellen und zum Initialisieren von Abonnements verfügbar halten** und klicken Sie auf **Weiter**.  
  
10. Deaktivieren Sie auf der Seite „Agentsicherheit“ das Kontrollkästchen **Sicherheitseinstellungen des Momentaufnahme-Agents verwenden** .  
  
11. Klicken Sie für den Momentaufnahme-Agent auf **Sicherheitseinstellungen**, geben Sie \<*Machine_Name>***\repl_snapshot** im Feld **Prozesskonto** ein, geben Sie das Kennwort für dieses Konto ein und klicken Sie anschließend auf **OK**.  
  
12. Wiederholen Sie den vorherigen Schritt, um repl_logreader als Prozesskonto für den Protokolllese-Agenten festzulegen, und klicken Sie anschließend auf **Fertig stellen**.  
  
13. Geben Sie auf der Seite „Assistenten abschließen“ im Feld **Veröffentlichungsname** den Namen **AdvWorksProductTrans** ein und klicken Sie auf **Fertig stellen**.  
  
14. Klicken Sie auf **Schließen** , um den Assistenten zu beenden, nachdem die Veröffentlichung erstellt wurde.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>So zeigen Sie den Status der Momentaufnahmegenerierung an  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Veröffentlichungen** mit der rechten Maustaste auf **AdvWorksProductTrans**und anschließend auf **Status des Momentaufnahme-Agents anzeigen**.  
  
3.  Der aktuelle Status des Auftrags des Momentaufnahme-Agents für die Veröffentlichung wird angezeigt. Prüfen Sie, ob der Momentaufnahmeauftrag erfolgreich war, bevor Sie zur nächsten Lektion wechseln.  
  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>So fügen Sie der PAL die Anmeldung des Verteilungs-Agents hinzu  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Veröffentlichungen** mit der rechten Maustaste auf **AdvWorksProductTrans**und anschließend auf **Eigenschaften**.  
  
    Das Dialogfeld **Veröffentlichungseigenschaften** wird angezeigt.  
  
3.  Wählen Sie die Seite **Veröffentlichungszugriffsliste** aus und klicken Sie auf **Hinzufügen**.  
  
4.  Wählen Sie im Dialogfeld **Veröffentlichungszugriff hinzufügen** die Anmeldung *<Computername>***\repl_distribution** aus und klicken Sie auf **OK**. Klicken Sie auf **OK**.  
  
## <a name="next-steps"></a>Nächste Schritte  
Sie haben die Transaktionsveröffentlichung erfolgreich erstellt. Als Nächstes abonnieren Sie diese Veröffentlichung. Siehe [Lektion 2: Erstellen eines Abonnements für die Transaktionsveröffentlichung](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
## <a name="see-also"></a>Siehe auch  
[Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md)  
[Definieren eines Artikels](../../relational-databases/replication/publish/define-an-article.md)  
[Erstellen und Anwenden der Momentaufnahme](../../relational-databases/replication/create-and-apply-the-snapshot.md)  
  
  
  

