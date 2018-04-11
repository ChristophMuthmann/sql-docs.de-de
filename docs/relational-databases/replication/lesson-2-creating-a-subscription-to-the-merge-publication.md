---
title: 'Lektion 2: Erstellen eines Abonnements für die Mergeveröffentlichung | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff899aa93ddedd959cdbe70a0a292752d851c92b
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="lesson-2-creating-a-subscription-to-the-merge-publication"></a>Lektion 2: Erstellen eines Abonnements für die Mergeveröffentlichung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In dieser Lektion erstellen Sie das Abonnement mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Anschließend erstellen Sie Berechtigungen für die Abonnementdatenbank und generieren die gefilterte Datenmomentaufnahme für das neue Abonnement manuell. Für diese Lektion wird vorausgesetzt, dass Sie die vorherige Lektion abgeschlossen haben: [Lektion 1: Veröffentlichen von Daten mithilfe der Mergereplikation](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md).  
  
### <a name="to-create-the-subscription"></a>So erstellen Sie das Abonnement  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, erweitern Sie den Serverknoten und den Ordner **Replikation** . Klicken Sie mit der rechten Maustaste auf den Ordner **Lokale Abonnements** , und klicken Sie anschließend auf **Neue Abonnements**.  
  
    Der Assistent für neue Abonnements wird gestartet.  
  
2.  Klicken Sie auf der Seite **Veröffentlichung** in der Liste **Verleger** auf **SQL Server-Verleger suchen** .  
  
3.  Geben Sie im Dialogfeld **Verbindung mit Server herstellen** im Feld **Servername** den Namen der Verlegerinstanz ein, und klicken Sie auf **Verbinden**.  
  
4.  Klicken Sie auf **AdvWorksSalesOrdersMerge**, und klicken Sie auf **Weiter**.  
  
5.  Klicken Sie auf der Seite Speicherort des Merge-Agents auf **Jeden Agent auf seinem Abonnenten ausführen**, und klicken Sie anschließend auf **Weiter**.  
  
6.  Wählen Sie auf der Seite Abonnenten den Instanznamen des Abonnentenservers aus, und wählen Sie unter **Abonnementdatenbank**aus der Liste die Option **<New Database>** aus.  
  
7.  Geben Sie im Dialogfeld **Neue Datenbank** den Namen **SalesOrdersReplica** in das Feld **Datenbankname** ein, klicken Sie auf **OK**, und klicken Sie anschließend auf **Weiter**.  
  
8.  Klicken Sie auf der Seite Sicherheit für den Merge-Agent auf die Schaltfläche mit den Auslassungspunkten (**…**), geben Sie im Feld **Prozesskonto** das Konto \<*Computername>***\repl_merge** ein, und geben Sie das Kennwort für dieses Konto ein. Klicken Sie auf **OK** und anschließend auf **Weiter** und dann erneut auf **Weiter**.  
  
9. Wählen Sie auf der Seite Abonnements initialisieren aus der Liste **Initialisierungszeitpunkt** die Option **Bei der ersten Synchronisierung** aus, klicken Sie auf **Weiter**, und klicken Sie erneut auf **Weiter** .  
  
10. Geben Sie auf der Seite HOST_NAME-Werte im Feld **HOST_NAME-Wert** den Wert **adventure-works\pamela0** ein, und klicken Sie anschließend auf **Fertig stellen**.  
  
11. Klicken Sie erneut auf **Fertig stellen** , und klicken Sie nach dem Erstellen des Abonnements auf **Schließen**.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Festlegen der Datenbankberechtigungen auf dem Abonnenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, erweitern Sie **Datenbanken**, **SalesOrdersReplica**und **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Benutzer**, und wählen Sie anschließend **Neuer Benutzer**aus.  
  
2.  Geben Sie auf der Seite **Allgemein** im Feld **Benutzername** den Namen \<*Computername>***\repl_merge** ein, klicken Sie auf die Schaltfläche mit den Auslassungspunkten (**…**), und klicken Sie auf **Durchsuchen**. Wählen Sie \<*Computername>***\repl_merge** aus, klicken Sie auf **OK** und dann auf **Namen überprüfen**, und klicken Sie anschließend auf **OK**.  
  
3.  Wählen Sie unter **Mitgliedschaft in Datenbankrollen**die **db_owner**-Rolle aus, und klicken Sie anschließend auf **OK** , um den Benutzer zu erstellen.  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>So erstellen Sie die gefilterte Datenmomentaufnahme für das Abonnement  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Veröffentlichungen** mit der rechten Maustaste auf die **AdvWorksSalesOrdersMerge** -Veröffentlichung, und klicken Sie anschließend auf **Eigenschaften**.  
  
    Das Dialogfeld **Veröffentlichungseigenschaften** wird angezeigt.  
  
3.  Wählen Sie die Seite **Datenpartitionen** aus, und klicken Sie auf **Hinzufügen**.  
  
4.  Geben Sie im Dialogfeld **Datenpartition hinzufügen** im Feld **HOST_NAME-Wert** den Wert **adventure-works\pamela0** ein, und klicken Sie anschließend auf **OK**.  
  
5.  Wählen Sie die neu hinzugefügte Partition aus, klicken Sie auf **Die ausgewählten Momentaufnahmen jetzt generieren**, und klicken Sie anschließend auf **OK**.  
  
## <a name="next-steps"></a>Next Steps  
Sie haben erfolgreich ein Abonnement für die Mergeveröffentlichung erstellt und die gefilterte Momentaufnahme für die Datenpartition des neuen Abonnements generiert, damit diese verfügbar ist, wenn das Abonnement initialisiert wird. Als Nächstes gewähren Sie dem Merge-Agent Rechte für die Abonnementdatenbank und führen den Merge-Agent aus, um die Synchronisierung zu starten und das Abonnement zu initialisieren. Weitere Informationen finden Sie unter [Lektion 3: Synchronisieren des Abonnements für die Mergeveröffentlichung](../../relational-databases/replication/lesson-3-synchronizing-the-subscription-to-the-merge-publication.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
[Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)  
[Momentaufnahmen für Mergeveröffentlichungen mit parametrisierten Filtern](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
