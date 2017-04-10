---
title: "Momentaufnahmen f&#252;r Mergever&#246;ffentlichungen mit parametrisierten Filtern | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Parametrisierte Filter [SQL Server-Replikation], Momentaufnahmen"
  - "Momentaufnahmen [SQL Server-Replikation], parametrisierte Filter und"
  - "Filter [SQL Server-Replikation], parametrisierte"
  - "Mergereplikation [SQL Server-Replikation], Initialisieren von Abonnements"
  - "Initialisieren von Abonnements [SQL Server-Replikation], Momentaufnahmen"
ms.assetid: 99d7ae15-5457-4ad4-886b-19c17371f72c
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Momentaufnahmen f&#252;r Mergever&#246;ffentlichungen mit parametrisierten Filtern
  Wenn parametrisierte Zeilenfilter in Mergeveröffentlichungen verwendet werden, wird jedes Abonnement bei der Replikation mit einer zweiteiligen Momentaufnahme initialisiert. Zuerst wird eine Schemamomentaufnahme erstellt, die alle von der Replikation benötigten Objekte und das Schema der veröffentlichten Objekte enthält, nicht jedoch die Daten. Jedes Abonnement wird dann mit einer Momentaufnahme initialisiert, die die Objekte und das Schema aus der Schemamomentaufnahme sowie die Daten enthält, die zur Partition des Abonnements gehören. Wenn mehrere Abonnements eine bestimmte Partition erhalten (anders ausgedrückt, sie erhalten dasselbe Schema und dieselben Daten), wird die Momentaufnahme für diese Partition nur einmal erstellt. Mehrere Abonnements werden mit derselben Momentaufnahme initialisiert. Weitere Informationen zu parametrisierten Zeilenfiltern finden Sie unter [parametrisierten Zeilenfiltern](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 Es gibt drei Methoden zum Erstellen von Momentaufnahmen für Veröffentlichungen mit parametrisierten Filtern:  
  
-   Vorabgenerieren von Momentaufnahmen für jede Partition. Bei dieser Methode können Sie steuern, wann Momentaufnahmen generiert werden.  
  
     Sie haben auch die Möglichkeit, die Momentaufnahmen nach einem Zeitplan zu aktualisieren. Wenn neue Abonnenten eine Partition abonnieren, für die eine Momentaufnahme erstellt wurde, erhalten sie eine aktuelle Momentaufnahme.  
  
-   Abonnenten das Anfordern der Momentaufnahmegenerierung und -anwendung beim erstmaligen Synchronisieren ermöglichen. Bei dieser Methode können neue Abonnenten Synchronisierungen ohne Administratoreingriff ausführen (der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent muss auf dem Verleger ausgeführt werden, damit die Momentaufnahme generiert werden kann).  
  
    > [!NOTE]  
    >  Wenn das Filtern nach einem oder mehreren Artikeln in der Veröffentlichung nicht überlappende Partitionen ergibt, die für jedes Abonnement eindeutig sind, wird für Metadaten bei jedem Ausführen des Merge-Agents einen Cleanup ausgeführt. Das bedeutet, dass die partitionierte Momentaufnahme schneller abläuft. Bei dieser Methode sollten Sie zulassen, dass Abonnenten das Generieren und Übermitteln von Momentaufnahmen einleiten. Weitere Informationen zu den Filteroptionen finden Sie unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
-   Manuelles Generieren einer Momentaufnahme für jeden Abonnenten mit dem Momentaufnahme-Agent. Der Abonnent muss dann einen Momentaufnahmespeicherort für den Merge-Agent bereitstellen, damit die richtige Momentaufnahme abgerufen und angewendet werden kann.  
  
    > [!NOTE]  
    >  Diese Methode wird aus Gründen der Abwärtskompatibilität unterstützt, lässt jedoch keine FTP-Momentaufnahmefreigaben zu.  
  
 Die flexibelste Vorgehensweise besteht in einer Kombination der Methoden der Vorabgenerierung und der vom Abonnenten angeforderten Momentaufnahmen: Momentaufnahmen werden vorab generiert und auf der Basis eines Terminplans (normalerweise nicht während Spitzenzeiten) aktualisiert. Falls jedoch ein Abonnement erstellt wird, das eine neue Partition erfordert, kann ein Abonnent eigene Momentaufnahmen generieren.  
  
 Beispiel: Die Außendienstmitarbeiter von [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]liefern Waren an einzelne Geschäfte aus. Jeder Vertriebsmitarbeiter erhält basierend auf seiner Anmeldung ein Abonnement, das die Daten für das vom jeweiligen Mitarbeiter bediente Geschäft abruft. Der Administrator generiert die Momentaufnahmen vorab und aktualisiert sie jeden Sonntag. Gelegentlich wird dem System ein neuer Benutzer hinzugefügt, der Daten für eine Partition benötigt, für die noch keine Momentaufnahme verfügbar ist. Um zu verhindern, dass ein Abonnent die Veröffentlichung nicht abonnieren kann, weil noch keine Momentaufnahme verfügbar ist, lässt der Administrator vom Abonnenten angeforderte Momentaufnahmen zu. Wenn der neue Abonnent erstmalig eine Verbindung herstellt, wird die Momentaufnahme für die angegebene Partition generiert und auf dem Abonnenten angewendet (der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent muss auf dem Verleger ausgeführt werden, damit die Momentaufnahme generiert werden kann).  
  
 Informationen zum Erstellen einer Momentaufnahme für eine Veröffentlichung mit parametrisierten Filtern finden Sie unter [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## Sicherheitseinstellungen für den Momentaufnahme-Agent  
 Der Momentaufnahme-Agent erstellt für jede Partition Momentaufnahmen. Für vorab generierte und von einem Abonnenten angeforderten Momentaufnahmen, der Agent ausgeführt wird und Verbindungen mit den Anmeldeinformationen, die angegeben wurden, wenn der Snapshot-Agent-Auftrag für die Veröffentlichung erstellt wurde (der Auftrag wird erstellt, durch den Assistenten für neue Veröffentlichung oder **Sp_addpublication_snapshot**). Verwenden Sie zum Ändern der Anmeldeinformationen **Sp_changedynamicsnapshot_job**. Weitere Informationen finden Sie unter [Sp_changedynamicsnapshot_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md).  
  
## Siehe auch  
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Parametrisierte Zeilenfilter](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  