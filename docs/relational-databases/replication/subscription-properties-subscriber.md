---
title: Abonnementeigenschaften - Abonnent | Microsoft Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.subproperties.subscriber.f1
helpviewer_keywords:
- Subscription Properties dialog box
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0983dafd2e95edbec342c7a885c1182f6dc053a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="subscription-properties---subscriber"></a>Abonnementeigenschaften - Abonnent
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Im Dialogfeld **Abonnementeigenschaften** des Abonnenten können Sie die Eigenschaften von Pullabonnements anzeigen und festlegen.  
  
 Zu jeder im Dialogfeld **Abonnementeigenschaften** verfügbaren Eigenschaft wird auch eine Beschreibung angezeigt. Klicken Sie auf eine Eigenschaft, um die dazugehörige Beschreibung am unteren Rand des Dialogfelds anzuzeigen. Dieses Thema enthält zusätzliche Informationen zu verschiedenen Eigenschaften. Die Eigenschaften sind in folgenden Kategorien angeordnet:  
  
-   Eigenschaften, die für alle Abonnements gelten.  
  
-   Eigenschaften, die für Transaktionsabonnements gelten.  
  
-   Eigenschaften, die für Mergeabonnements gelten.  
  
 Schreibgeschützte Optionen können nur beim Erstellen des Abonnements festgelegt werden. Wenn Sie Optionen festlegen möchten, die nicht im Assistenten für neue Abonnements verfügbar sind, müssen Sie das Abonnement mithilfe von gespeicherten Prozeduren erstellen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) und [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
> [!NOTE]  
>  Wenn für das Abonnement bislang noch kein Auftrag für den Verteilungs-Agent oder den Merge-Agent erstellt wurde, werden viele Abonnementeigenschaften nicht angezeigt. Um einen Agentauftrag für ein Pullabonnement zu erstellen, führen Sie [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) (für ein Abonnement einer Momentaufnahme- oder Transaktionsveröffentlichung) oder [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) aus (für ein Abonnement einer Mergeveröffentlichung).  
  
## <a name="options-for-all-subscriptions"></a>Optionen für alle Abonnements  
 **Veröffentlichte Daten von einer Momentaufnahme aus initialisieren**  
 Bestimmt, ob Abonnements mit einer Momentaufnahme (Standard) oder mithilfe einer anderen Methode initialisiert werden. Weitere Informationen zum Initialisieren von Abonnements finden Sie unter [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md).  
  
 **Momentaufnahmespeicherort**  
 Bestimmt den Speicherort, von dem aus während der Initialisierung oder der erneuten Initialisierung auf Momentaufnahmedateien zugegriffen wird. Für den Speicherort sind folgende Werte möglich:  
  
-   **Standardspeicherort**: der Standardspeicherort, der bei der Konfiguration eines Verteilers definiert wird. Weitere Informationen finden Sie unter [Angeben des standardmäßigen Momentaufnahmespeicherorts &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
-   **Alternativer Ordner**: ein alternativer Speicherort, der im Dialogfeld **Veröffentlichungseigenschaften** angegeben werden kann. Weitere Informationen finden Sie unter [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
-   **Ordner für dynamische Momentaufnahme**: ein Momentaufnahmespeicherort für Mergeveröffentlichungen, für den parametrisierte Zeilenfilter verwendet werden. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
-   **FTP-Ordner**: ein Ordner, auf den ein FTP-Server (File Transfer Protocol) zugreifen kann. Weitere Informationen finden Sie unter [Übertragen von Momentaufnahmen über FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
 **Momentaufnahmeordner**  
 Wenn Sie für die Option **Momentaufnahmespeicherort** einen anderen Wert als **Standardspeicherort** auswählen, müssen Sie einen Pfad zum Momentaufnahmeordner angeben.  
  
 **Synchronisierungsverwaltung von Windows verwenden**  
 Bestimmt, ob dieses Abonnement mithilfe von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Synchronization Manager synchronisiert werden kann.  
  
 **Security**  
 Klicken Sie auf die Zeile **Agentprozesskonto** , und klicken Sie dann auf die **Schaltfläche mit den drei Punkten**, um das Konto zu ändern, unter dem der Verteilungs-Agent oder der Merge-Assistent auf dem Abonnenten ausgeführt werden. Die Sicherheitsoptionen für Verbindungen sind vom Typ des Abonnements abhängig:  
  
-   Für Abonnements einer Transaktionsveröffentlichung: Sie können das Konto, unter dem der Verteilungs-Agent Verbindungen mit dem Verteiler erstellt, ändern, indem Sie auf **Verteilerverbindung**und anschließend auf die **Schaltfläche mit den drei Punkten**klicken.  
  
-   Für Abonnements mit sofortigem Update von Transaktionsveröffentlichungen: zusätzlich zur oben beschriebenen Verteilerverbindung können Sie die Methode ändern, mit der Änderungen vom Abonnenten zum Verleger übermittelt werden: klicken Sie auf **Verlegerverbindung**und anschließend auf die **Schaltfläche mit den drei Punkten**.  
  
-   Für Abonnements von Mergeveröffentlichungen, klicken Sie auf **Verlegerverbindung**und anschließend auf die **Schaltfläche mit den drei Punkten**.  
  
 Weitere Informationen zu den für die einzelnen Agents erforderlichen Berechtigungen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="options-for-transactional-subscriptions"></a>Optionen für Transaktionsabonnements  
 **Aktualisierbares Abonnement**  
 Legt fest, ob die am Abonnenten vorgenommenen Änderungen zurück auf den Verleger repliziert werden. Änderungen können entweder mit einem sofortigen Update oder mit einem verzögerten Update über eine Warteschlange repliziert werden. Mit der Option **Updatemethode für Abonnent** wird die zu verwendende Methode festgelegt. Weitere Informationen finden Sie unter [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="options-for-merge-subscriptions"></a>Optionen für Mergeabonnements  
 **Partitionsdefinition (HOST_NAME)**  
 Wenn Sie eine Mergereplikation für eine Veröffentlichung mit parametrisierten Filtern ausführen, wird bei der Synchronisierung eine der beiden Systemfunktionen, **SUSER_SNAME()** oder **HOST_NAME()**(oder beide, sofern die Filter auf beide Funktionen verweisen) ausgewertet, um festzulegen, welche Daten der Abonnent empfangen soll. **HOST_NAME()** gibt standardmäßig den Namen des Computers zurück, auf dem der Merge-Agent ausgeführt wird. Sie können diesen Wert jedoch im Assistenten für neue Abonnements überschreiben. Weitere Informationen zu parametrisierten Filtern und zum Überschreiben von **HOST_NAME()**finden Sie unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Abonnementtyp** und **Priorität**  
 Zeigt an, ob es sich bei dem Abonnement um ein Client- oder Serverabonnement handelt (kann nach Erstellen des Abonnements nicht mehr geändert werden). Bei Serverabonnements können Daten erneut für andere Abonnenten veröffentlicht und eine Priorität für die Konfliktlösung festgelegt werden.  
  
 Wenn Sie im Assistenten für neue Abonnements als Abonnementtyp Server ausgewählt haben, wird dem Abonnenten eine Priorität für die Konfliktlösung zugewiesen.  
  
 **Konflikte interaktiv lösen**  
 Legt fest, ob die bei der Synchronisierung auftretenden Konflikte mit der Benutzeroberfläche des interaktiven Konfliktlösers gelöst werden sollen. Dafür ist für **Synchronisierungsverwaltung von Windows verwenden** der Wert **Aktivieren**erforderlich. Weitere Informationen finden Sie unter [Interactive Conflict Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
 **Websynchronisierung**  
 Durch**Websynchronisierung verwenden** wird bestimmt, ob für die Synchronisierung des Abonnements eine Verbindung mit einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] IIS-Server (Internetinformationsdienste) hergestellt wird. Diese Option ist nur verfügbar, wenn die Veröffentlichung für die Websynchronisierung aktiviert ist. Weitere Informationen finden Sie unter [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Wenn Sie für **Websynchronisierung verwenden** den Wert **True**auswählen:  
  
-   Geben Sie die vollständige Adresse des IIS-Servers in **Webserveradresse**ein.  
  
-   Klicken Sie auf die Zeile **Webserververbindung**, und klicken Sie anschließend auf die Schaltfläche mit den **drei Punkten**, um das Konto festzulegen oder zu ändern, unter dem der Abonnent eine Verbindung mit dem IIS-Server herstellt.  
  
-   Falls erforderlich, ändern Sie **Webservertimeout** . Ein Timeout bezeichnet die Dauer in Sekunden, bevor eine Websynchronisierungsanforderung ungültig wird.  
  
 Weitere Informationen zur Konfiguration finden Sie unter [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
