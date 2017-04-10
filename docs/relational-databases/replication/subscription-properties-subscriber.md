---
title: "Abonnementeigenschaften - Abonnent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subproperties.subscriber.f1"
helpviewer_keywords: 
  - "Abonnementeigenschaften (Dialogfeld)"
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Abonnementeigenschaften - Abonnent
  Im Dialogfeld **Abonnementeigenschaften** des Abonnenten können Sie die Eigenschaften von Pullabonnements anzeigen und festlegen.  
  
 Zu jeder im Dialogfeld **Abonnementeigenschaften** verfügbaren Eigenschaft wird auch eine Beschreibung angezeigt. Klicken Sie auf eine Eigenschaft, um die dazugehörige Beschreibung am unteren Rand des Dialogfelds anzuzeigen. Dieses Thema enthält zusätzliche Informationen zu verschiedenen Eigenschaften. Die Eigenschaften sind in folgenden Kategorien angeordnet:  
  
-   Eigenschaften, die für alle Abonnements gelten.  
  
-   Eigenschaften, die für Transaktionsabonnements gelten.  
  
-   Eigenschaften, die für Mergeabonnements gelten.  
  
 Schreibgeschützte Optionen können nur beim Erstellen des Abonnements festgelegt werden. Wenn Sie Optionen festlegen möchten, die nicht im Assistenten für neue Abonnements verfügbar sind, müssen Sie das Abonnement mithilfe von gespeicherten Prozeduren erstellen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) und [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
> [!NOTE]  
>  Wenn für das Abonnement bislang noch kein Auftrag für den Verteilungs-Agent oder den Merge-Agent erstellt wurde, werden viele Abonnementeigenschaften nicht angezeigt. Um einen Agentauftrag für ein Pullabonnement zu erstellen, führen Sie [Sp_addpullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) (für ein Abonnement für eine Momentaufnahme- oder transaktionsveröffentlichung) oder [Sp_addmergepullsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (für ein Abonnement einer Mergeveröffentlichung).  
  
## Optionen für alle Abonnements  
 **Veröffentlichte Daten von einer Momentaufnahme aus initialisieren**  
 Bestimmt, ob Abonnements mit einer Momentaufnahme (Standard) oder mithilfe einer anderen Methode initialisiert werden. Weitere Informationen zum Initialisieren von Abonnements finden Sie unter [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md).  
  
 **Momentaufnahmespeicherort**  
 Bestimmt den Speicherort, von dem aus während der Initialisierung oder der erneuten Initialisierung auf Momentaufnahmedateien zugegriffen wird. Für den Speicherort sind folgende Werte möglich:  
  
-   **Standardspeicherort**: der Standardspeicherort, der bei der Konfiguration eines Verteilers definiert wird. Weitere Informationen finden Sie unter [Geben Sie den Standard-Snapshotspeicherort & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
-   **Alternativer Ordner**: ein alternativer Speicherort, der im Dialogfeld **Veröffentlichungseigenschaften** angegeben werden kann. Weitere Informationen finden Sie unter [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
-   **Ordner für dynamische Momentaufnahme**: ein Momentaufnahmespeicherort für Mergeveröffentlichungen, für den parametrisierte Zeilenfilter verwendet werden. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
-   **FTP-Ordner**: ein Ordner auf einem Server (FTP = File Transfer Protocol) zugegriffen werden kann. Weitere Informationen finden Sie unter [Momentaufnahmen über FTP übertragen](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
 **Momentaufnahmeordner**  
 Wenn Sie einen beliebigen Wert außer auswählen **Standardspeicherort** für die **Snapshotspeicherort** Option, Sie müssen einen Pfad zum momentaufnahmeordner angeben.  
  
 **Synchronisierungsverwaltung von Windows verwenden**  
 Bestimmt, ob dieses Abonnement mithilfe von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Synchronization Manager synchronisiert werden kann.  
  
 **Sicherheit**  
 Klicken Sie auf die **Agentprozesskontos** Zeile, und klicken Sie dann auf die Eigenschaftenschaltfläche (**...**) zum Ändern des Kontos, unter dem der Snapshot-Agent oder Merge-Agent auf dem Abonnenten ausgeführt wird. Die Sicherheitsoptionen für Verbindungen sind vom Typ des Abonnements abhängig:  
  
-   Für Abonnements einer transaktionsveröffentlichung: zum Ändern des Kontos, unter dem der Verteilungsagent Verbindungen mit dem Verteiler herstellt, klicken Sie auf **Verteilerverbindung**, und klicken Sie dann auf die Eigenschaftenschaltfläche (**...**).  
  
-   Für sofort aktualisierbare Abonnements zu einer Transaktionspublikation: Zusätzlich zu den oben beschriebenen verteilerverbindung können Sie die Methode, die zum Weitergeben von Änderungen vom Abonnenten zum Verleger verwendet ändern: Klicken Sie auf **Verlegerverbindung**, und klicken Sie dann auf die Eigenschaftenschaltfläche (**...**).  
  
-   Abonnements für Mergepublikationen klicken Sie auf **Verlegerverbindung**, und klicken Sie dann auf die Eigenschaftenschaltfläche (**...**).  
  
 Weitere Informationen zu den für die einzelnen Agents erforderlichen Berechtigungen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Optionen für Transaktionsabonnements  
 **Aktualisierbares Abonnement**  
 Legt fest, ob die am Abonnenten vorgenommenen Änderungen zurück auf den Verleger repliziert werden. Änderungen können entweder mit einem sofortigen Update oder mit einem verzögerten Update über eine Warteschlange repliziert werden. Mit der Option **Updatemethode für Abonnent** wird die zu verwendende Methode festgelegt. Weitere Informationen finden Sie unter [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## Optionen für Mergeabonnements  
 **Partitionsdefinition (HOST_NAME)**  
 Für eine Veröffentlichung mit parametrisierten Filtern ausführen, wertet die Mergereplikation eine der beiden Systemfunktionen (oder beide, sofern die Filter auf beide Funktionen verweisen) während der Synchronisierung die Daten zu ermitteln, der Abonnent empfangen soll: **SUSER_SNAME()** oder **HOST_NAME()**. In der Standardeinstellung **HOST_NAME()** Gibt den Namen des Computers, auf denen der Merge-Agent ausgeführt wird, aber Sie können diesen Wert im Assistenten für neue Abonnements überschreiben. Weitere Informationen zu parametrisierten Filtern und überschreiben **HOST_NAME()**, finden Sie unter [parametrisierten Zeilenfiltern](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **Abonnementtyp** und **Priorität**  
 Zeigt an, ob es sich bei dem Abonnement um ein Client- oder Serverabonnement handelt (kann nach Erstellen des Abonnements nicht mehr geändert werden). Bei Serverabonnements können Daten erneut für andere Abonnenten veröffentlicht und eine Priorität für die Konfliktlösung festgelegt werden.  
  
 Wenn Sie im Assistenten für neue Abonnements als Abonnementtyp Server ausgewählt haben, wird dem Abonnenten eine Priorität für die Konfliktlösung zugewiesen.  
  
 **Konflikte interaktiv lösen**  
 Legt fest, ob die bei der Synchronisierung auftretenden Konflikte mit der Benutzeroberfläche des interaktiven Konfliktlösers gelöst werden sollen. Dafür ist für **Synchronisierungsverwaltung von Windows verwenden** der Wert **Aktivieren**erforderlich. Weitere Informationen finden Sie unter [Interactive Conflict Resolution](../../relational-databases/replication/merge/interactive-conflict-resolution.md).  
  
 **Websynchronisierung**  
 **Verwenden Sie die Synchronisierung von** bestimmt, ob die Verbindung mit einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] (Internet Information Services, IIS)-Server zum Synchronisieren des Abonnements. Diese Option ist nur verfügbar, wenn die Veröffentlichung für die Websynchronisierung aktiviert ist. Weitere Informationen finden Sie unter [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 Wenn Sie für **Websynchronisierung verwenden** den Wert **True**auswählen:  
  
-   Geben Sie die vollständige Adresse des IIS-Servers in **Webserveradresse**ein.  
  
-   Klicken Sie auf die **Web-Server-Verbindung** Zeile, und klicken Sie dann auf die Eigenschaftenschaltfläche (**...**) festlegen oder ändern Sie das Konto, unter dem der Abonnent eine Verbindung, auf dem IIS-Server herstellt.  
  
-   Falls erforderlich, ändern Sie **Webservertimeout** . Ein Timeout bezeichnet die Dauer in Sekunden, bevor eine Websynchronisierungsanforderung ungültig wird.  
  
 Weitere Informationen zur Konfiguration finden Sie unter [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Siehe auch  
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  