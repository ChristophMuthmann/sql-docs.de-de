---
title: "Lektion 2: Erstellen eines Abonnements für die Transaktionsveröffentlichung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bc5e6abed8f9d92532e186377b85396b711f290d
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>Lektion 2: Erstellen eines Abonnements für die Transaktionsveröffentlichung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In dieser Lektion erstellen Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ein Abonnement. Für diese Lektion wird vorausgesetzt, dass Sie die vorherige Lektion abgeschlossen haben: [Lektion 1: Veröffentlichen von Daten mithilfe der Transaktionsreplikation](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md).  
  
### <a name="to-create-the-subscription"></a>So erstellen Sie das Abonnement  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Klicken Sie im Ordner **Lokale Veröffentlichungen** mit der rechten Maustaste auf die **AdvWorksProductTrans** -Veröffentlichung und anschließend auf **Neue Abonnements**.  
  
    Der Assistent für neue Abonnements wird gestartet.  
  
3.  Wählen Sie auf der Seite Veröffentlichung die **AdvWorksProductTrans**-Veröffentlichung aus, und klicken Sie dann auf **Weiter**.  
  
4.  Wählen Sie auf der Seite Speicherort des Verteilungs-Agents die Option **Alle Agents auf dem Verteiler ausführen**aus, und klicken Sie dann auf **Weiter**.  
  
5.  Wenn der Name der Abonnenteninstanz auf der Seite Abonnenten nicht angezeigt wird, klicken Sie auf **Abonnent hinzufügen**, klicken Sie auf **SQL Server-Abonnenten hinzufügen**, geben Sie den Namen der Abonnenteninstanz im Dialogfeld **Verbindung mit Server herstellen** ein, und klicken Sie dann auf **Verbinden**.  
  
6.  Wählen Sie auf der Seite Abonnenten den Instanzennamen des Abonnentenservers aus, und wählen Sie **<New Database>** unter der Option **Abonnementdatenbank**aus.  
  
7.  Geben Sie im Dialogfeld **Neue Datenbank** den Namen **ProductReplica** in das Feld **Datenbankname** ein, klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
8.  Klicken Sie im Dialogfeld **Sicherheit für den Verteilungs-Agent** auf die Schaltfläche mit den Auslassungspunkten (**…**), geben Sie im Feld **Prozesskonto** das Konto \<*Computername>***\repl_distribution** ein, geben Sie das Kennwort für dieses Konto ein, klicken Sie auf **OK** und anschließend auf **Weiter**.  
  
9. Klicken Sie auf **Fertig stellen** , um auf den verbleibenden Seiten die Standardwerte zu übernehmen und den Assistenten zu beenden.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Festlegen der Datenbankberechtigungen auf dem Abonnenten  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Abonnenten her, erweitern Sie **Datenbanken**, **ProductReplica**und **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Benutzer**, und wählen Sie anschließend **Neuer Benutzer**aus.  
  
2.  Klicken Sie auf der Seite **Allgemein** in der Liste **Benutzertyp** auf **Windows-Benutzer**.  
  
3.  Wählen sie das Feld **Benutzername** aus, und klicken Sie auf die Schaltfläche mit den Auslassungspunkten (...). **Geben Sie die den Objektnamen ein**, um den Feldtyp <Machine_Name>**\repl_distribution** auszuwählen, klicken Sie auf **Namen überprüfen** und anschließend auf **OK**.  
  
4.  Wählen Sie auf der Seite **Mitgliedschaft** im Bereich **Mitgliedschaft in Datenbankrollen** die **db_owner**-Rolle aus, und klicken Sie anschließend auf **OK**, um den Benutzer zu erstellen.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>So zeigen Sie den Synchronisierungsstatus des Abonnements an  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Erweitern Sie im Ordner **Lokale Veröffentlichungen** die **AdvWorksProductTrans** -Veröffentlichung, klicken Sie mit der rechten Maustaste auf das Abonnement in der **ProductReplica** -Datenbank und anschließend auf **Synchronisierungsstatus anzeigen**.  
  
    Der aktuelle Synchronisierungsstatus des Abonnements wird angezeigt.  
  
3.  Wenn das Abonnement unter **AdvWorksProductTrans**nicht angezeigt wird, drücken Sie F5, um die Liste zu aktualisieren.  
  
## <a name="next-steps"></a>Next Steps  
Sie haben erfolgreich ein Abonnement für die Transaktionsveröffentlichung erstellt. Da der Verteilungs-Agent für dieses Abonnement ständig ausgeführt wird, wird das Abonnement initialisiert, wenn es erstellt wird. Als Nächstes verwenden Sie Überwachungstoken, um zu überprüfen, ob die Änderungen auf dem Abonnenten repliziert werden, und um die Latenzzeit zu ermitteln. Siehe [Lesson 3: Validating the Subscription and Measuring Latency](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)  
[Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
