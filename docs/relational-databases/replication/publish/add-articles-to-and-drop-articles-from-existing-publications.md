---
title: "Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- removing articles
- dropping articles
- adding articles
- administering replication, articles
- publications [SQL Server replication], adding and dropping articles
- articles [SQL Server replication], adding
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0acd4302b7f996b5eae1fa4d0bd728f135e3591a
ms.lasthandoff: 04/11/2017

---
# <a name="add-articles-to-and-drop-articles-from-existing-publications"></a>Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen
  Nachdem eine Veröffentlichung erstellt wurde, können ihr Artikel hinzugefügt oder Artikel aus der Veröffentlichung gelöscht werden. Während das Hinzufügen von Artikeln jederzeit erfolgen kann, hängen die Schritte zum Löschen von Artikeln vom jeweiligen Replikationstyp und dem Zeitpunkt ab, zu dem der Artikel gelöscht wird.  
  
## <a name="adding-articles"></a>Hinzufügen von Artikeln  
 Hinzufügen eines Artikels beinhaltet Folgendes: Hinzufügen des Artikels zur Veröffentlichung; Erstellen einer neuen Momentaufnahme für die Veröffentlichung und Synchronisieren des Abonnements zum Zuweisen des Schemas und der Daten für den neuen Artikel.  
  
> [!NOTE]  
>  Wenn Sie einer Mergeveröffentlichung einen Artikel hinzufügen und ein vorhandener Artikel von diesem neuen Artikel abhängt, müssen Sie mithilfe des **@processing_order** -Parameters von [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) und [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)eine Verarbeitungsreihenfolge für die beiden Artikel angeben. Angenommen, Sie veröffentlichen eine Tabelle, aber Sie veröffentlichen keine Funktion, die auf die Tabelle verweist. Wenn Sie die Funktion nicht veröffentlichen, kann die Tabelle nicht auf dem Abonnenten erstellt werden. Wenn Sie die Funktion einer Veröffentlichung hinzufügen, geben Sie einen Wert von **1** für den **@processing_order** -Parameter von **sp_addmergearticle**an, und geben Sie einen Wert von **2** für den **@processing_order** -Parameter von **sp_changemergearticle**an. Geben Sie dann den Tabellennamen für den **@article**. Durch diese Verarbeitungsreihenfolge wird sichergestellt, dass Sie die Funktion auf dem Abonnenten vor der Tabelle erstellen, die davon abhängt. Sie können unterschiedliche Nummern für die einzelnen Artikel verwenden, dabei muss jedoch die Nummer für die Funktion kleiner als die Nummer der Tabelle sein.  
  
1.  Zum Hinzufügen einzelner oder mehrerer Artikel stehen die folgenden Methoden zur Verfügung:  
  
    -   [Hinzufügen von Artikeln zu einer Veröffentlichung und Löschen von Artikeln aus einer Veröffentlichung &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  Nachdem Sie einer Veröffentlichung einen Artikel hinzugefügt haben, müssen Sie eine neue Momentaufnahme für die Veröffentlichung (sowie – bei Mergeveröffentlichungen mit parametrisierten Filtern – für alle Partitionen) erstellen. Der Verteilungs-Agent oder der Merge-Agent kopiert dann das Schema und die Daten für den neuen Artikel auf den Abonnenten (ohne dabei die gesamte Veröffentlichung neu zu initialisieren).  
  
    -   Informationen zum Erstellen einer Momentaufnahme finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Informationen zum Erstellen einer neuen Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern finden Sie unter [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
3.  Synchronisieren Sie nach Abschluss der Momentaufnahmeerstellung das Abonnement, um das Schema und die Daten für den neuen Artikel zu kopieren.  
  
    -   Informationen zum Synchronisieren eines Pushabonnements finden Sie unter [Synchronisieren eines Pushabonnements](../../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
    -   Informationen zum Synchronisieren eines Pullabonnements finden Sie unter [Synchronisieren eines Pullabonnements](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## <a name="dropping-articles"></a>Löschung von Artikeln  
 Artikel können jederzeit aus einer Veröffentlichung gelöscht werden, wobei jedoch Folgendes zu beachten ist:  
  
-   Durch das Löschen eines Artikels aus einer Veröffentlichung wird weder das Objekt aus der Veröffentlichungsdatenbank noch das zugehörige Objekt aus der Abonnementdatenbank entfernt. Verwenden Sie DROP \<Objekt>, um diese Objekte ggf. zu entfernen. Wenn Sie einen Artikel löschen möchten, der über Fremdschlüsseleinschränkungen mit anderen veröffentlichten Artikeln verknüpft ist, sollten Sie die Tabelle auf dem Abonnenten manuell oder mithilfe einer bedarfsgesteuerten Skriptausführung löschen. Geben Sie ein Skript an, dass die entsprechenden DROP \<Objekt>-Anweisungen enthält. Weitere Informationen finden Sie unter [Ausführen von Skripts während der Synchronisierung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Bei Mergeveröffentlichungen mit einem Kompatibilitätsgrad von 90RTM oder höher können Artikel jederzeit gelöscht werden. Es ist jedoch eine neue Momentaufnahme erforderlich. Darüber hinaus gilt:  
  
    -   Wenn der Artikel ein übergeordneter Artikel in einer Joinfilter- oder logischen Datensatzbeziehung ist, müssen zunächst die Beziehungen gelöscht werden, was eine erneute Initialisierung erforderlich macht.  
  
    -   Wenn der Artikel den letzten parametrisierten Filter in einer Veröffentlichung hat, müssen die Abonnements erneut initialisiert werden.  
  
-   Bei Mergeveröffentlichungen mit einem Kompatibilitätsgrad von unter 90RTM können Artikel ohne weiteres gelöscht werden, solange die Abonnements noch nicht zum ersten Mal synchronisiert wurden. Wird ein Artikel nach der Synchronisierung von Abonnements gelöscht, müssen die Abonnements gelöscht, neu erstellt und dann synchronisiert werden.  
  
-   Bei Momentaufnahme- oder Transaktionsveröffentlichungen können Artikel ohne weiteres gelöscht werden, solange noch keine Abonnements erstellt wurden. Wird ein Artikel nach der Erstellung von Abonnements gelöscht, müssen die Abonnements gelöscht, neu erstellt und dann synchronisiert werden. Weitere Informationen zum Löschen von Abonnements finden Sie unter [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md) und [sp_dropsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Mit**sp_dropsubscription** können Sie einen einzelnen Artikel aus dem Abonnement löschen, statt das gesamte Abonnement zu löschen.  
  
1.  Das Löschen eines Artikels aus einer Veröffentlichung umfasst das eigentliche Löschen des Artikels und das Erstellen einer neuen Momentaufnahme für die Veröffentlichung. Durch das Löschen eines Artikels wird die aktuelle Momentaufnahme ungültig, sodass eine neue Momentaufnahme erstellt werden muss.  
  
    -   Informationen zum Löschen eines Artikels aus einer Veröffentlichung finden Sie unter [Hinzufügen und Löschen von Artikeln aus einer Veröffentlichung &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) oder [Löschen eines Artikels](../../../relational-databases/replication/publish/delete-an-article.md).  
  
2.  Nachdem Sie einen Artikel aus einer Veröffentlichung gelöscht haben, müssen Sie eine neue Momentaufnahme für die Veröffentlichung (sowie – bei Mergeveröffentlichungen mit parametrisierten Filtern – für alle Partitionen) erstellen.  
  
    -   Informationen zum Erstellen einer Momentaufnahme finden Sie unter [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Informationen zum Erstellen einer neuen Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern finden Sie unter [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Wie oben bereits erwähnt, müssen die Abonnements in einigen Fällen nach dem Löschen eines Artikels gelöscht und dann neu erstellt sowie synchronisiert werden. Weitere Informationen finden Sie unter [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md) und [Synchronisieren von Daten](../../../relational-databases/replication/synchronize-data.md).  
 
 > [!NOTE]
 > **[!INCLUDE[ssSQL15](../../../includes/sssql14-md.md)]Service Pack 2** oder höher und **[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] Service Pack 1** oder höher unterstützen das Löschen einer Tabelle mit dem **DROP TABLE**-DLL-Befehl für Artikel, die an einer Transaktionsreplikation beteiligt sind. Wenn eine DROP TABLE-DDL durch die Publikation(en) unterstützt wird, löscht der DROP TABLE-Vorgang die Tabelle aus der Veröffentlichung und der Datenbank. Der Protokollleseagent wird einen Bereinigungsbefehl für die Verteilungsdatenbank für die gelöschte Tabelle posten und die Bereinigung der Metadaten des Verlegers durchführen. Wenn der Protokollleser noch nicht alle Protokolleinträge verarbeitet hat, die auf die gelöschte Tabelle verweisen, wird er neue Befehle ignorieren, die der gelöschten Tabelle zugeordnet sind. Bereits verarbeitete Datensätze werden an die Verteilungsdatenbank übermittelt. Sie können auf die Abonnentendatenbank angewendet werden, wenn der Verteilungs-Agent sie verarbeitet, bevor der Protokollleser veraltete (gelöschte) Artikel bereinigt. Die **Standard**-Einstellung für alle Veröffentlichungen für Transaktionsreplikationen unterstützt keine DROP TABLE-DLL. [KB 3170123](https://support.microsoft.com/en-us/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1) enthält weitere detaillierte Informationen zu dieser Verbesserung.

  
## <a name="see-also"></a>Siehe auch  
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Erneutes Initialisieren von Abonnements](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
