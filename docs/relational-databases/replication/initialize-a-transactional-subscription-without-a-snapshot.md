---
title: Initialisieren eines Transaktionsabonnements ohne Momentaufnahme | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactional replication, initializing
- replication [SQL Server], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 75c8c1f8-60bc-44a8-944b-d18d1f6bda11
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8406d41eeb1e02d06f6a745e13129717fdcbf916
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="initialize-a-transactional-subscription-without-a-snapshot"></a>Initialisieren eines Transaktionsabonnements ohne Momentaufnahme
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Standardmäßig wird ein Abonnement für eine Transaktionsveröffentlichung mithilfe einer Momentaufnahme initialisiert, die vom Momentaufnahme-Agent generiert und vom Verteilungs-Agent angewendet wird. In einigen Szenarien, wenn z. B. große Anfangsdatasets eine Rolle spielen, ist es vorteilhafter, ein Abonnement mit einer anderen Methode zu initialisieren. Folgende weitere Methoden stehen zum Initialisieren eines Abonnements zur Verfügung:  
  
-   Angeben einer Sicherung. Stellen Sie die Sicherung auf dem Abonnenten her. Der Verteilungs-Agent kopiert dann alle erforderlichen Replikationsmetadaten und gespeicherten Prozeduren. Mit der Initialisierung über eine Sicherung können Daten am schnellsten und bequemsten auf den Abonnenten übertragen werden. Das liegt daran, dass jede neuere Sicherung verwendet werden kann, die nach dem Aktivieren einer Veröffentlichung für das Initialisieren mit einer Sicherung vorgenommen wurde.  
  
-   Kopieren eines Anfangsdatensatzes auf den Abonnenten mithilfe eines anderen Mechanismus, wie z. B. Anfügen einer Datenbank. Stellen Sie sicher, dass die Daten und das Schema auf dem Abonnenten stimmen. Der Verteilungs-Agent kopiert dann alle erforderlichen Metadaten und gespeicherten Prozeduren.  
  
## <a name="initializing-a-subscription-with-a-backup"></a>Initialisieren eines Abonnements mit einer Sicherung  
 Eine Sicherung enthält eine gesamte Datenbank. Deshalb enthält jede Abonnementdatenbank bei ihrer Initialisierung eine vollständige Kopie der Veröffentlichungsdatenbank.  
  
-   Die Sicherung enthält Tabellen, die nicht als Artikel für die Veröffentlichung angegeben sind.  
  
-   Die Sicherung enthält auch dann alle Daten, wenn Zeilen oder Spaltenfilter für eine Tabelle angegeben sind.  
  
 Es ist Aufgabe des Administrators oder der Anwendung, alle unerwünschten Objekte oder Daten nach der Wiederherstellung der Sicherung zu entfernen. In folgenden Synchronisierungen werden Datenänderungen nur repliziert, wenn sie sich auf Tabellen beziehen, die als Artikel angeben sind, und die Änderungen allen von Ihnen angegebenen Filterkriterien entsprechen.  
  
> [!NOTE]  
>  Beim Wiederherstellen einer Sicherung müssen Sie sicherstellen, dass die Sicherung vom Verleger stammt, wenn der Abonnent automatisch synchronisiert werden soll. Die LNS-Werte (Log Sequence Number, Protokollfolgenummer) in der Sicherung (mit denen der Startpunkt für die Synchronisierung festgelegt wird) beziehen sich immer auf den speziellen Verleger.  
  
 **So initialisieren Sie ein Abonnement mit einer Sicherung**  
  
 Zum Initialisieren eines Abonnements mit einer Sicherung muss diese Option beim Erstellen einer Veröffentlichung zuerst aktiviert werden. Anschließend geben Sie Werte für eine Reihe von Optionen an, wenn Sie ein Abonnement erstellen. Veröffentlichungen können über den Assistenten für neue Veröffentlichung oder programmgesteuert aktiviert werden. Die Werte, die für die Abonnementoptionen erforderlich sind, können jedoch nur programmgesteuert angegeben werden.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Aktivieren der Initialisierung mit einer Sicherung für Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/enable-initialization-with-backup-for-transactional-publications.md)  
  
-   Replikationsprogrammierung mit Transact-SQL: [Initialisieren eines Transaktionsabonnements von einer Sicherung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
> [!NOTE]  
>  Wenn ein Abonnement ohne Verwendung einer Momentaufnahme initialisiert wird, muss das Konto, unter dem der SQL Server-Dienst auf dem Verleger ausgeführt wird, Schreibberechtigung für den Momentaufnahmeordner auf dem Verteiler besitzen. Weitere Informationen zu Berechtigungen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
### <a name="ensuring-the-suitability-of-a-backup"></a>Sicherstellen der Eignung einer Sicherung  
 Eine Sicherung eignet sich zum Initialisieren eines Abonnenten, wenn alle Transaktionen, die nach dem Erstellen der Sicherung auftreten, auf dem Verteiler gespeichert werden. Die Replikation zeigt eine Fehlermeldung an, falls sich die Sicherung nicht eignet.  
  
 Beachten Sie die folgenden Richtlinien, um sicherzustellen, dass sich eine Sicherung eignet:  
  
-   Verwenden Sie die neueste verfügbare Sicherung. Falls die neueste Sicherung die maximalen Beibehaltungsdauer der Verteilung überschritten hat, erstellen Sie eine neue Sicherung, und führen Sie erst dann die Initialisierung mit einer Sicherung durch. Weitere Informationen zu Beibehaltungsdauer finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Der Replikationsauftrag Verteilungscleanup löscht Transaktionen, die älter als 72 Stunden sind, aus der Verteilungsdatenbank. Der Cleanup basiert auf der für die Veröffentlichung festgelegten Beibehaltungsdauer. Wenn Sie eine Synchronisierung mit älteren Sicherungen ausführen, sollten Sie den Auftrag vorübergehend deaktivieren, bevor Sie die Sicherung wiederherstellen. Nachdem das Abonnement erfolgreich erstellt wurde, können Sie den Auftrag wieder aktivieren. Dadurch verhindern Sie, dass Transaktionen aus der Verteilungsdatenbank entfernt werden, die für eine erfolgreiche Synchronisierung aus der Sicherung erforderlich sind. Informationen zum Ausführen von Cleanupaufträgen finden Sie unter [Ausführen von Aufträgen zur Replikationswartung &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md).  
  
 In einigen Fällen müssen Sie Anpassungen nach dem Einrichten von Abonnements, die mit einer Sicherung initialisiert wurden, in der wiederhergestellten Abonnentendatenbank manuell ausführen. In der Regel sind manuelle Änderungen an der wiederhergestellten Abonnentendatenbank erforderlich, wenn die Definition der Veröffentlichung voraussichtlich dazu führt, dass sich der Inhalt der Abonnentendatenbank von dem Inhalt der Verlegerdatenbank unterscheidet.  
  
-   Indizierte Sichten in der wiederhergestellten Datenbank müssen in Tabellen konvertiert werden, wenn sie als Artikel vom Typ log-based indexed-view-to-table veröffentlicht werden.  
  
-   Abonnierte timestamp-Spalten in wiederhergestellten Datenbanken müssen in **binary(8)** -Spalten konvertiert werden: Kopieren Sie den Inhalt der Tabellen, die timestamp-Spalten enthalten, in neue Tabellen, die übereinstimmende Schemas, jedoch anstelle der timestamp-Spalten **binary(8)** -Spalten aufweisen. Löschen Sie die ursprünglichen Tabellen, und geben Sie den neuen Tabellen jeweils denselben Namen wie den ursprünglichen Tabellen.  
  
## <a name="initializing-a-subscription-with-an-alternative-method"></a>Initialisieren eines Abonnements mit einer alternativen Methode  
 Abonnements können mit jeder beliebigen Methode initialisiert werden, die das Kopieren des Veröffentlichungsdatenbankschemas und der Daten auf den Abonnenten zulässt, wie z. B. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Wenn Sie zum Initialisieren des Abonnenten eine alternative Methode verwenden, werden Unterstützungsobjekte der Replikation auf den Abonnenten kopiert.  
  
 Im Unterschied zur Sicherung muss durch Sie oder die Anwendung sichergestellt werden, dass die Daten und das Schema beim Hinzufügen des Abonnements ordnungsgemäß synchronisiert werden. Wenn es zwischen dem Zeitpunkt, zu dem die Daten und das Schema auf den Abonnenten kopiert wurden, und dem Zeitpunkt, zu dem das Abonnement hinzugefügt wird, beispielsweise auf dem Verleger zu einer Aktivität gekommen ist, kann es passieren, dass Änderungen, die sich aus dieser Aktivität ergeben, nicht auf den Abonnenten repliziert werden.  
  
 Informationen zum Initialisieren eines Abonnements mit einer alternativen Methode finden Sie unter [Initialize a Subscription Manually](../../relational-databases/replication/initialize-a-subscription-manually.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md)  
  
  
