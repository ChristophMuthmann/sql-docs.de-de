---
title: "Hinzuf&#252;gen und L&#246;schen von Artikeln aus vorhandenen Ver&#246;ffentlichungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Artikel [SQL Server-Replikation], löschen"
  - "Löschen von Artikeln"
  - "Entfernen von Artikeln"
  - "Löschung von Artikeln"
  - "Hinzufügen von Artikeln"
  - "Verwalten der Replikations, Artikel"
  - "Veröffentlichungen [SQL Server-Replikation], Hinzufügen und Löschen von Artikeln"
  - "Artikel [SQL Server-Replikation], hinzufügen"
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# Hinzuf&#252;gen und L&#246;schen von Artikeln aus vorhandenen Ver&#246;ffentlichungen
  Nachdem eine Veröffentlichung erstellt wurde, können ihr Artikel hinzugefügt oder Artikel aus der Veröffentlichung gelöscht werden. Während das Hinzufügen von Artikeln jederzeit erfolgen kann, hängen die Schritte zum Löschen von Artikeln vom jeweiligen Replikationstyp und dem Zeitpunkt ab, zu dem der Artikel gelöscht wird.  
  
## Hinzufügen von Artikeln  
 Hinzufügen eines Artikels beinhaltet Folgendes: Hinzufügen des Artikels zur Veröffentlichung; Erstellen einer neuen Momentaufnahme für die Veröffentlichung und Synchronisieren des Abonnements zum Zuweisen des Schemas und der Daten für den neuen Artikel.  
  
> [!NOTE]  
>  Wenn Sie eine Mergepublikation einen Artikel hinzufügen und ein vorhandener Artikel, die die neuen Artikel abhängt, müssen Sie angeben, dass eine Verarbeitungsreihenfolge für beide Artikel mithilfe der **@processing_order** Parameter [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) und [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Angenommen, Sie veröffentlichen eine Tabelle, aber Sie veröffentlichen keine Funktion, die auf die Tabelle verweist. Wenn Sie die Funktion nicht veröffentlichen, kann die Tabelle nicht auf dem Abonnenten erstellt werden. Beim Hinzufügen der Funktion für die Veröffentlichung: Geben Sie den Wert **1** für die **@processing_order** Parameter **Sp_addmergearticle**; und geben Sie den Wert **2** für die **@processing_order** Parameter **Sp_changemergearticle**, geben Sie den Tabellennamen für den Parameter **@article**. Durch diese Verarbeitungsreihenfolge wird sichergestellt, dass Sie die Funktion auf dem Abonnenten vor der Tabelle erstellen, die davon abhängt. Sie können unterschiedliche Nummern für die einzelnen Artikel verwenden, dabei muss jedoch die Nummer für die Funktion kleiner als die Nummer der Tabelle sein.  
  
1.  Zum Hinzufügen einzelner oder mehrerer Artikel stehen die folgenden Methoden zur Verfügung:  
  
    -   [Fügen Sie und Löschen von Artikeln aus einer Veröffentlichung & #40 hinzu; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  Nachdem Sie einer Veröffentlichung einen Artikel hinzugefügt haben, müssen Sie eine neue Momentaufnahme für die Veröffentlichung (sowie – bei Mergeveröffentlichungen mit parametrisierten Filtern – für alle Partitionen) erstellen. Der Verteilungs-Agent oder der Merge-Agent kopiert dann das Schema und die Daten für den neuen Artikel auf den Abonnenten (ohne dabei die gesamte Veröffentlichung neu zu initialisieren).  
  
    -   Informationen zum Erstellen einer Momentaufnahme finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   So erstellen eine neue Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern finden Sie unter [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
3.  Synchronisieren Sie nach Abschluss der Momentaufnahmeerstellung das Abonnement, um das Schema und die Daten für den neuen Artikel zu kopieren.  
  
    -   Informationen zum Synchronisieren eines Pushabonnements finden Sie unter [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
    -   Informationen zum Synchronisieren eines Pullabonnements finden Sie unter [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## Löschen von Artikeln  
 Artikel können jederzeit aus einer Veröffentlichung gelöscht werden, wobei jedoch Folgendes zu beachten ist:  
  
-   Durch das Löschen eines Artikels aus einer Veröffentlichung wird weder das Objekt aus der Veröffentlichungsdatenbank noch das zugehörige Objekt aus der Abonnementdatenbank entfernt. Verwenden Sie DROP \< Object> auf diese Objekte zu entfernen. Wenn Sie einen Artikel, die mit anderen veröffentlichten Artikeln über foreign Key-Einschränkungen verknüpft ist löschen, wird empfohlen, dass Sie die Tabelle auf dem Abonnenten manuell oder mithilfe einer bedarfsgesteuerten skriptausführung löschen: Geben Sie ein Skript, das die entsprechenden Dropdownliste enthält \< Objekt> Anweisungen. Weitere Informationen finden Sie unter [Ausführen von Skripts während der Synchronisierung & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Bei Mergeveröffentlichungen mit einem Kompatibilitätsgrad von 90RTM oder höher können Artikel jederzeit gelöscht werden. Es ist jedoch eine neue Momentaufnahme erforderlich. Darüber hinaus gilt:  
  
    -   Wenn der Artikel ein übergeordneter Artikel in einer Joinfilter- oder logischen Datensatzbeziehung ist, müssen zunächst die Beziehungen gelöscht werden, was eine erneute Initialisierung erforderlich macht.  
  
    -   Wenn der Artikel den letzten parametrisierten Filter in einer Veröffentlichung hat, müssen die Abonnements erneut initialisiert werden.  
  
-   Bei Mergeveröffentlichungen mit einem Kompatibilitätsgrad von unter 90RTM können Artikel ohne weiteres gelöscht werden, solange die Abonnements noch nicht zum ersten Mal synchronisiert wurden. Wird ein Artikel nach der Synchronisierung von Abonnements gelöscht, müssen die Abonnements gelöscht, neu erstellt und dann synchronisiert werden.  
  
-   Bei Momentaufnahme- oder Transaktionsveröffentlichungen können Artikel ohne weiteres gelöscht werden, solange noch keine Abonnements erstellt wurden. Wird ein Artikel nach der Erstellung von Abonnements gelöscht, müssen die Abonnements gelöscht, neu erstellt und dann synchronisiert werden. Weitere Informationen zum Löschen von Abonnements finden Sie unter [Publikationen abonnieren,](../../../relational-databases/replication/subscribe-to-publications.md) und [Sp_dropsubscription & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). **Sp_dropsubscription** ermöglicht es Ihnen, einzelne Artikel aus dem Abonnement, statt das gesamte Abonnement zu löschen.  
  
1.  Das Löschen eines Artikels aus einer Veröffentlichung umfasst das eigentliche Löschen des Artikels und das Erstellen einer neuen Momentaufnahme für die Veröffentlichung. Durch das Löschen eines Artikels wird die aktuelle Momentaufnahme ungültig, sodass eine neue Momentaufnahme erstellt werden muss.  
  
    -   Zum Löschen eines Artikels aus einer Veröffentlichung finden Sie unter [Hinzufügen und löschen Artikeln aus einer Veröffentlichung & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) oder [Löschen eines Artikels](../../../relational-databases/replication/publish/delete-an-article.md).  
  
2.  Nachdem Sie einen Artikel aus einer Veröffentlichung gelöscht haben, müssen Sie eine neue Momentaufnahme für die Veröffentlichung (sowie – bei Mergeveröffentlichungen mit parametrisierten Filtern – für alle Partitionen) erstellen.  
  
    -   Informationen zum Erstellen einer Momentaufnahme finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   So erstellen eine neue Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern finden Sie unter [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Wie oben bereits erwähnt, müssen die Abonnements in einigen Fällen nach dem Löschen eines Artikels gelöscht und dann neu erstellt sowie synchronisiert werden. Weitere Informationen finden Sie unter [Publikationen abonnieren,](../../../relational-databases/replication/subscribe-to-publications.md) und [Daten synchronisieren](../../../relational-databases/replication/synchronize-data.md).  
  
## Siehe auch  
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Erneutes Initialisieren von Abonnements](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  