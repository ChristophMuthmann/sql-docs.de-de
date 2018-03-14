---
title: 'Entwicklerhandbuch: Themen zur Vorgehensweise (Replikation) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c6c15ae6-da52-4638-93d3-61c7242e8a0b
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a6f7342fe198add76b574366ca4a4f78c822facf
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="developer39s-guide-how-to-topics-replication"></a>Entwicklerhandbuch: Themen zur Vorgehensweise (Replikation)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieses Thema enthält Links zu Informationen über die programmgesteuerte Ausführung replikationsbezogener Tasks.  
  
## <a name="securing-a-replication-topology"></a>Sichern einer Replikationstopologie  
  
-   [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
-   [Verwalten von Anmeldungen in der Veröffentlichungszugriffsliste](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="configuring-modifying-and-disabling-publishing-and-distribution-replication"></a>Konfigurieren, Ändern und Deaktivieren der Veröffentlichung und Verteilung (Replikation)  
  
-   [Konfigurieren der Veröffentlichung und der Verteilung](../../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [Deaktivieren der Veröffentlichung und Verteilung](../../../relational-databases/replication/disable-publishing-and-distribution.md)  
  
## <a name="creating-modifying-and-deleting-publications-and-articles"></a>Erstellen, Ändern und Löschen von Veröffentlichungen und Artikeln  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [Anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [Löschen einer Veröffentlichung](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [Löschen eines Artikels](../../../relational-databases/replication/publish/delete-an-article.md)  
  
-   [Erstellen einer Veröffentlichung aus einer Oracle-Datenbank](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)  
  
-   [Festlegen des Ablaufdatums für Abonnements](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [Angeben von Schemaoptionen](../../../relational-databases/replication/publish/specify-schema-options.md)  
  
-   [Replizieren von Schemaänderungen](../../../relational-databases/replication/publish/replicate-schema-changes.md)  
  
-   [Verwalten von Identitätsspalten](../../../relational-databases/replication/publish/manage-identity-columns.md)  
  
-   [Festlegen des Kompatibilitätsgrads von Mergeveröffentlichungen](../../../relational-databases/replication/publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>Momentaufnahmeoptionen  
  
-   [Konfigurieren von Momentaufnahmeeigenschaften &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [Übermitteln einer Momentaufnahme über FTP](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
### <a name="filtering-data"></a>Filtern von Daten  
  
-   [Definieren und Ändern eines Spaltenfilters](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [Definieren und Ändern eines statischen Zeilenfilters](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [Definieren und Ändern eines parametrisierten Zeilenfilters für einen Mergeartikel](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [Optimieren von parametrisierten Zeilenfiltern](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [Definieren und Ändern eines Verknüpfungsfilters zwischen Mergeartikeln](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>Transaktionsreplikationsoptionen  
  
-   [Festlegen der Propagierungsmethode für Datenänderungen an Transaktionsartikeln](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [Aktivieren des Aktualisierens von Abonnements für Transaktionsveröffentlichungen](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>Mergereplikationsoptionen  
  
-   [Definieren einer logischen Datensatzbeziehung zwischen Mergetabellenartikeln](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [Angeben der Verarbeitungsreihenfolge von Mergetabellenartikeln &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [Angeben, dass ein neuer Mergetabellenartikel nur herunterladbar ist](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [Angeben, dass Löschvorgänge für Mergeartikel nicht nachverfolgt werden sollen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [Angeben der Konfliktnachverfolgungs- und -lösungsebene für Mergeartikel](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [Angeben eines Mergeartikelkonfliktlösers](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [Angeben interaktiver Konfliktauflösung von Mergeartikeln](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="creating-modifying-and-deleting-subscriptions"></a>Erstellen, Ändern und Löschen von Abonnements  
  
-   [Erstellen eines Pullabonnements](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
-   [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
-   [Löschen eines Pullabonnements](../../../relational-databases/replication/delete-a-pull-subscription.md)  
  
-   [Erstellen eines Pushabonnements](../../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
-   [Löschen eines Pushabonnements](../../../relational-databases/replication/delete-a-push-subscription.md)  
  
-   [Angeben von Synchronisierungszeitplänen](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
-   [Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md)
  
-   [Erstellen eines Abonnements für einen Nicht-SQL Server-Abonnenten](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronizing-subscriptions"></a>Synchronisieren von Abonnements  
  
-   [Erstellen und Anwenden der Anfangsmomentaufnahme](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Initialisieren eines Transaktionsabonnements von einer Sicherung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [Manuelles Initialisieren eines Abonnements](../../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [Synchronisieren eines Pullabonnements](../../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Synchronisieren eines Pushabonnements](../../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [Erneutes Initialisieren eines Abonnements](../../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [Ausführen von Skripts während der Synchronisierung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [Implementieren eines Geschäftslogikhandlers für einen Mergeartikel](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [Debuggen eines Geschäftslogikhandlers &#40;Replikationsprogrammierung&#41;](../../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [Kontrollieren des Verhaltens von Triggern und Einschränkungen während der Synchronisierung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [Implementieren eines benutzerdefinierten Konfliktlösers für einen Mergeartikel](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administering-a-replication-topology"></a>Verwalten einer Replikationstopologie  
  
-   [Arbeiten mit Replikations-Agent-Profilen](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [Überprüfen der Daten am Abonnenten](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
-   [Verwalten von Partitionen für eine Mergeveröffentlichung mit parametrisierten Filtern](../../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [Massenladen von Daten in Tabellen in einer Mergeveröffentlichung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/bulk-load-data-into-tables-in-a-merge-publication.md)  
  
-   [Cleanup von Mergemetadaten &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/clean-up-merge-metadata-replication-transact-sql-programming.md)  
  
-   [Ausführen eines Pseudoupdates für einen Mergeartikel &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)  
  
-   [Anzeigen replizierter Befehle und anderer Informationen in der Verteilungsdatenbank &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [Aktivieren koordinierter Sicherungen für die Transaktionsreplikation &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
-   [Verwalten einer Peer-zu-Peer-Topologie &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)  
  
-   [Versetzen einer Replikationstopologie in einen inaktiven Status &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)  
  
-   [Konfigurieren des Transaktionssatzauftrags für einen Oracle-Verleger &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)  
  
-   [Aktualisieren von Replikationsskripts &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitoring-a-replication-topology"></a>Überwachen einer Replikationstopologie  
  
-   [Zulassen, dass Nichtadministratoren den Replikationsmonitor verwenden](../../../relational-databases/replication/monitor/allow-non-administrators-to-use-replication-monitor.md)  
  
-   [Programmgesteuertes Überwachen der Replikation](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
-   [Anzeigen replizierter Befehle und anderer Informationen in der Verteilungsdatenbank &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [Anzeigen von Konfliktinformationen zu Mergeveröffentlichungen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
-   [Messen der Latenzzeit und Überprüfen der Verbindungen bei Transaktionsreplikationen](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
