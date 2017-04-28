---
title: "Momentaufnahmen für Mergeveröffentlichungen mit parametrisierten Filtern | Microsoft-Dokumentation"
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
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
- merge replication [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 246e2e5db5c3e64973c165be8b03e03b7c8226a5
ms.lasthandoff: 04/11/2017

---
# <a name="snapshots-for-merge-publications-with-parameterized-filters"></a>Momentaufnahmen für Mergeveröffentlichungen mit parametrisierten Filtern
  Wenn parametrisierte Zeilenfilter in Mergeveröffentlichungen verwendet werden, wird jedes Abonnement bei der Replikation mit einer zweiteiligen Momentaufnahme initialisiert. Zuerst wird eine Schemamomentaufnahme erstellt, die alle von der Replikation benötigten Objekte und das Schema der veröffentlichten Objekte enthält, nicht jedoch die Daten. Jedes Abonnement wird dann mit einer Momentaufnahme initialisiert, die die Objekte und das Schema aus der Schemamomentaufnahme sowie die Daten enthält, die zur Partition des Abonnements gehören. Wenn mehrere Abonnements eine bestimmte Partition erhalten (anders ausgedrückt, sie erhalten dasselbe Schema und dieselben Daten), wird die Momentaufnahme für diese Partition nur einmal erstellt. Mehrere Abonnements werden mit derselben Momentaufnahme initialisiert. Weitere Informationen zu parametrisierten Zeilenfiltern finden Sie unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Es gibt drei Methoden zum Erstellen von Momentaufnahmen für Veröffentlichungen mit parametrisierten Filtern:  
  
-   Vorabgenerieren von Momentaufnahmen für jede Partition. Bei dieser Methode können Sie steuern, wann Momentaufnahmen generiert werden.  
  
     Sie haben auch die Möglichkeit, die Momentaufnahmen nach einem Zeitplan zu aktualisieren. Wenn neue Abonnenten eine Partition abonnieren, für die eine Momentaufnahme erstellt wurde, erhalten sie eine aktuelle Momentaufnahme.  
  
-   Abonnenten das Anfordern der Momentaufnahmegenerierung und -anwendung beim erstmaligen Synchronisieren ermöglichen. Bei dieser Methode können neue Abonnenten Synchronisierungen ohne Administratoreingriff ausführen (der[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent muss auf dem Verleger ausgeführt werden, damit die Momentaufnahme generiert werden kann).  
  
    > [!NOTE]  
    >  Wenn das Filtern nach einem oder mehreren Artikeln in der Veröffentlichung nicht überlappende Partitionen ergibt, die für jedes Abonnement eindeutig sind, wird für Metadaten bei jedem Ausführen des Merge-Agents einen Cleanup ausgeführt. Das bedeutet, dass die partitionierte Momentaufnahme schneller abläuft. Bei dieser Methode sollten Sie zulassen, dass Abonnenten das Generieren und Übermitteln von Momentaufnahmen einleiten. Weitere Informationen zu den Filteroptionen finden Sie unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Manuelles Generieren einer Momentaufnahme für jeden Abonnenten mit dem Momentaufnahme-Agent. Der Abonnent muss dann einen Momentaufnahmespeicherort für den Merge-Agent bereitstellen, damit die richtige Momentaufnahme abgerufen und angewendet werden kann.  
  
    > [!NOTE]  
    >  Diese Methode wird aus Gründen der Abwärtskompatibilität unterstützt, lässt jedoch keine FTP-Momentaufnahmefreigaben zu.  
  
 Die flexibelste Vorgehensweise besteht in einer Kombination der Methoden der Vorabgenerierung und der vom Abonnenten angeforderten Momentaufnahmen: Momentaufnahmen werden vorab generiert und auf der Basis eines Terminplans (normalerweise nicht während Spitzenzeiten) aktualisiert. Falls jedoch ein Abonnement erstellt wird, das eine neue Partition erfordert, kann ein Abonnent eigene Momentaufnahmen generieren.  
  
 Beispiel: Die Außendienstmitarbeiter von [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]liefern Waren an einzelne Geschäfte aus. Jeder Vertriebsmitarbeiter erhält basierend auf seiner Anmeldung ein Abonnement, das die Daten für das vom jeweiligen Mitarbeiter bediente Geschäft abruft. Der Administrator generiert die Momentaufnahmen vorab und aktualisiert sie jeden Sonntag. Gelegentlich wird dem System ein neuer Benutzer hinzugefügt, der Daten für eine Partition benötigt, für die noch keine Momentaufnahme verfügbar ist. Um zu verhindern, dass ein Abonnent die Veröffentlichung nicht abonnieren kann, weil noch keine Momentaufnahme verfügbar ist, lässt der Administrator vom Abonnenten angeforderte Momentaufnahmen zu. Wenn der neue Abonnent erstmalig eine Verbindung herstellt, wird die Momentaufnahme für die angegebene Partition generiert und auf dem Abonnenten angewendet (der[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent muss auf dem Verleger ausgeführt werden, damit die Momentaufnahme generiert werden kann).  
  
 Informationen zum Erstellen einer Momentaufnahme für eine Veröffentlichung mit parametrisierten Filtern finden Sie unter [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="security-settings-for-the-snapshot-agent"></a>Sicherheitseinstellungen für den Momentaufnahme-Agent  
 Der Momentaufnahme-Agent erstellt für jede Partition Momentaufnahmen. Der Agent wird für vorab generierte Momentaufnahmen und Momentaufnahmen ausgeführt, die vom Abonnenten angefordert werden. Er stellt Verbindungen mit den Anmeldeinformationen her, die beim Erstellen des Auftrags des Momentaufnahme-Agents für die Veröffentlichung angegeben wurden (der Auftrag wird vom Assistenten für neue Veröffentlichung oder von **sp_addpublication_snapshot**erstellt.) Verwenden Sie **sp_changedynamicsnapshot_job**zum Ändern der Anmeldeinformationen. Weitere Informationen finden Sie unter [sp_changedynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
