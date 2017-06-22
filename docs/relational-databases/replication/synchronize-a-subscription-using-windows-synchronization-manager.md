---
title: Synchronisieren eines Abonnements mit der Synchronisierungsverwaltung von Windows | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- synchronization [SQL Server replication], Windows Synchronization Manager
- Windows Synchronization Manager
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1c8119d5c503bdb7c40fc6af0733534093da28f6
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="synchronize-a-subscription-using-windows-synchronization-manager"></a>Synchronisieren eines Abonnements mit der Synchronisierungsverwaltung von Windows
  Die Synchronisierungsverwaltung von Windows[!INCLUDE[msCoName](../../includes/msconame-md.md)] kann nur zum Synchronisieren von Abonnements für Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Veröffentlichungen verwendet werden, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf demselben Computer ausgeführt wird wie die Synchronisierungsverwaltung. (Die Synchronisierungsverwaltung kann auch zum Synchronisieren von Offlinedateien und Webseiten verwendet werden.) So verwenden Sie die Synchronisierungsverwaltung:  
  
1.  Aktivieren Sie die Synchronisierung von Pullabonnements mithilfe der Synchronisierungsverwaltung im Dialogfeld **Abonnementeigenschaften – \<Subscriber>: \<SubscriptionDatabase>**. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
2.  Greifen Sie über das Menü **Start** von Windows auf die Synchronisierungsverwaltung zu.  
  
 Die Synchronisierungsverwaltung ermöglicht Ihnen die Verwendung des interaktiven Konfliktlösers für Mergeabonnements. In der Regel werden Konflikte, die bei der Synchronisierung entdeckt werden, automatisch gelöst. Wenn der interaktive Konfliktlöser aktiviert ist, können Konflikte jedoch während der Synchronisierung von einem Benutzer gelöst werden. Wenn die Synchronisierung nicht im Rahmen der Synchronisierungsverwaltung von Windows erfolgt (sondern als geplante Synchronisierung oder als bedarfsgesteuerte Synchronisierung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder des Replikationsmonitors), werden Konflikte ohne Benutzereingriff automatisch gemäß dem Konfliktlöser gelöst, der für den Artikel angegeben ist.  
  
> [!NOTE]  
>  Ab [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] und [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]sind 64-Bit-Versionen der Synchronisierungsverwaltung von Windows nicht in der Lage, 32-Bit-Abonnements zu erkennen.  
  
### <a name="to-enable-the-synchronization-of-pull-subscriptions-with-windows-synchronization-manager"></a>So aktivieren Sie die Synchronisierung von Pullabonnements mithilfe der Synchronisierungsverwaltung von Windows  
  
1.  Wählen Sie im Dialogfeld **Abonnementeigenschaften – \<Subscriber>: \<SubscriptionDatabase>** auf der Seite **Allgemein** für die Option **Synchronisierungsverwaltung von Windows verwenden** den Wert **Aktivieren** aus.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-synchronize-a-pull-subscription-with-synchronization-manager"></a>So synchronisieren Sie ein Pullabonnement mit der Synchronisierungsverwaltung  
  
1.  Starten Sie die Synchronisierungsverwaltung mithilfe einer der folgenden Methoden:  
  
    -   Klicken Sie in Internet Explorer auf das Menü **Extras**und anschließend auf **Synchronisieren**.  
  
    -   Klicken Sie auf **Start**, zeigen Sie auf **Programme** oder **Alle Programme**, zeigen Sie auf **Zubehör**, und klicken Sie dann auf **Synchronisieren**.  
  
    -   Klicken Sie auf **Start**und anschließend auf **Ausführen** . Geben Sie im Dialogfeld **Ausführen**  **mobsync.exe** in the **Öffnen** ein, und klicken Sie dann auf **OK**.  
  
2.  Wählen Sie im Dialogfeld **Zu synchronisierende Objekte** die Abonnements aus, die Sie synchronisieren möchten. Die Abonnements werden unter den auf dem Computer installierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen aufgeführt.  
  
3.  Klicken Sie auf **Synchronisieren**.  
  
### <a name="to-reinitialize-a-pull-subscription-with-synchronization-manager"></a>So initialisieren Sie ein Pullabonnement mit der Synchronisierungsverwaltung erneut  
  
1.  Wählen Sie im Dialogfeld **Zu synchronisierende Objekte** ein Abonnement aus, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **SQL Server-Abonnementeigenschaften** auf **Abonnement erneut initialisieren**.  
  
3.  Klicken Sie auf **Ja**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Beim nächsten Synchronisieren des Abonnements wird standardmäßig eine neue Momentaufnahme auf die Abonnementdatenbank angewendet. Weitere Informationen finden Sie unter [Erneutes Initialisieren von Abonnements](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
> [!NOTE]  
>  Bei der Mergereplikation können ausstehende Änderungen auf den Verleger hochgeladen werden, bevor die Momentaufnahme angewendet wird. Diese Option ist jedoch nicht in der Synchronisierungsverwaltung verfügbar. Synchronisieren Sie zum Hochladen von Änderungen das Abonnement, bevor Sie es erneut initialisieren.  
  
### <a name="to-set-properties-for-a-pull-subscription-in-synchronization-manager"></a>So legen Sie Eigenschaften für ein Pullabonnement in der Synchronisierungsverwaltung fest  
  
1.  Wählen Sie im Dialogfeld **Zu synchronisierende Objekte** ein Abonnement aus, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Sie können Eigenschaften auf den folgenden Registerkarten anzeigen und ändern:  
  
    -   **Identifikation**  
  
    -   **Abonnentenanmeldung**, **Verteileranmeldung**und **Verlegeranmeldung** (nur für die Mergereplikation)  
  
    -   **Webserverinformationen** (für Mergeabonnements auf Abonnenten, auf denen SQL Server 2005 oder höher ausgeführt wird)  
  
    -   **Andere**  
  
     Die Verwendung der Windows-Authentifizierung wird für alle Verbindungen empfohlen. Informationen zu den Berechtigungen, die der Verteilungs-Agent und der Merge-Agent benötigen, finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-pull-subscription-from-synchronization-manager"></a>So entfernen Sie ein Pullabonnement aus der Synchronisierungsverwaltung  
  
1.  Wählen Sie im Dialogfeld **Zu synchronisierende Objekte** ein Abonnement aus, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **SQL Server-Abonnementeigenschaften** auf **Abonnement entfernen**.  
  
3.  Wählen Sie im Dialogfeld **Abonnement entfernen** eine Option aus.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-interactive-resolver"></a>So verwenden Sie den interaktiven Konfliktlöser  
  
1.  Aktivieren Sie die Verwendung des interaktiven Konfliktlösers für den Artikel und das Abonnement. Weitere Informationen finden Sie unter [Angeben von interaktiver Konfliktauflösung von Mergeartikeln](../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md).  
  
2.  Mit dem Beginn der Synchronisierung des Abonnements in der Synchronisierungsverwaltung wird der interaktive Konfliktlöser automatisch gestartet, wenn der interaktive Konfliktlöser aktiviert ist und bei einem oder mehreren Artikeln Konflikte bestehen. Der interaktive Konfliktlöser zeigt die Konflikte jeweils nacheinander an und schlägt eine Lösung für jeden Konflikt vor (basierend auf dem bei der Erstellung der Veröffentlichung und des Abonnements angegebenen Konfliktlösers).  
  
3.  Sie können die im interaktiven Konfliktlöser angezeigten Spalten auch beliebig bearbeiten und dann auf eine der folgenden Schaltflächen klicken, um den Konflikt zu lösen:  
  
    -   **Vorschläge akzeptieren**  
  
    -   **Verleger akzeptieren**  
  
    -   **Abonnenten akzeptieren**  
  
    -   **Alle automatisch lösen** (alle aktuellen Konflikte werden ohne weitere Eingaben gelöst)  
  
     Die ausgewählte Zeile wird dann auf den Verleger und/oder Abonnenten angewendet. Bei folgenden Synchronisierungen wird die Zeile an andere Knoten der Topologie weitergegeben.  
  
> [!NOTE]  
>  Bearbeitungen werden nur dann angewendet, wenn sie zur Zeile gehören, die für die Lösung ausgewählt wurde. Wenn Sie z. B. Bearbeitungen unter **Verleger**vornehmen und dann auf **Abonnenten akzeptieren**klicken, werden die Bearbeitungen verworfen.  
  
## <a name="see-also"></a>Siehe auch  
 [Interaktive Konfliktlösung](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  
