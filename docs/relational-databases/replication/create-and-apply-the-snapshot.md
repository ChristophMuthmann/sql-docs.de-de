---
title: "Erstellen und Anwenden der Momentaufnahme | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Momentaufnahmen [SQL Server-Replikation], anwenden"
  - "Momentaufnahmen [SQL Server-Replikation], erstellen"
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Erstellen und Anwenden der Momentaufnahme
  Momentaufnahmen werden nach dem Erstellen einer Veröffentlichung vom Momentaufnahme-Agent generiert. Sie können folgendermaßen generiert werden:  
  
-   Sofort. Standardmäßig wird eine Momentaufnahme für eine Mergeveröffentlichung sofort nach dem Erstellen der Veröffentlichung im Assistenten für neue Veröffentlichung generiert.  
  
-   Zu einem geplanten Zeitpunkt. Geben Sie einen Zeitplan für die **Snapshot-Agent** Seite des Assistenten für neue Veröffentlichung oder mithilfe von gespeicherten Prozeduren oder Replikationsverwaltungsobjekten (RMO).  
  
-   Manuell. Führen Sie den Momentaufnahme-Agent von der Eingabeaufforderung oder in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus. Weitere Informationen zum Ausführen von Agents finden Sie unter [Replikations-Agent ausführbare Konzepte](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) und [Starten und Beenden eines Replikations-Agents & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
 Bei der Mergereplikation wird jedes Mal eine Momentaufnahme generiert, wenn der Momentaufnahme-Agent ausgeführt wird. Für die Transaktionsreplikation, momentaufnahmegenerierung hängt von der Einstellung der Eigenschaft der Veröffentlichung **Immediate_sync**. Ist die Eigenschaft auf TRUE festgelegt (die Standardeinstellung bei der Verwendung des Assistenten für neue Veröffentlichung), wird bei jedem Ausführen des Momentaufnahme-Agents eine Momentaufnahme generiert, der jederzeit auf einen Abonnenten angewendet werden kann. Wenn die Eigenschaft auf FALSE festgelegt ist (die Standardeinstellung bei Verwendung **Sp_addpublication**), die Momentaufnahme wird nur generiert, wenn ein neues Abonnement hinzugefügt wurde, seit der letzten Snapshot-Agent ausgeführt wird. Abonnenten müssen warten, für den Snapshot-Agent durchführen, bevor sie synchronisiert werden können.  
  
 Generierte Momentaufnahmen werden im Standardmomentaufnahmeordner auf dem Verteiler gespeichert. Sie können Momentaufnahmedateien aber auch auf Wechselmedien wie z. B. Wechseldatenträgern, CD-ROMs oder an anderen Speicherorten als dem Standardmomentaufnahmeordner speichern. Darüber hinaus können Sie die Momentaufnahmedateien komprimieren, sodass sie leichter zu speichern und zu übertragen sind, und Skripts vor oder nach der Anwendung der Momentaufnahme auf den Abonnenten ausführen. Weitere Informationen zu diesen Optionen finden Sie unter [Snapshot Options](../../relational-databases/replication/snapshot-options.md).  
  
 Handelt es sich um eine Momentaufnahme für eine Mergeveröffentlichung, die parametrisierte Filter verwendet, wird die Momentaufnahme mit einem zweiteiligen Prozess erstellt. Zuerst wird eine Schemamomentaufnahme erstellt, die die Replikationsskripts und das Schema der veröffentlichten Objekte enthält, nicht jedoch die Daten. Jedes Abonnement wird dann mit einer Momentaufnahme initialisiert, die die aus der Schemamomentaufnahme kopierten Skripts und das Schema sowie die Daten enthält, die zur Partition des Abonnements gehören. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Nachdem die Momentaufnahme auf dem Verleger erstellt und am standardmäßigen bzw. einem anderen Momentaufnahmespeicherort gespeichert wurde, kann sie an den Abonnenten übertragen und auf diesen angewendet werden. Der Verteilungs-Agent (bei Momentaufnahme- oder Transaktionsreplikation) bzw. der Merge-Agent (bei Mergereplikation) überträgt die Momentaufnahme und wendet die Schema- und Datendateien während der Erstsynchronisierung auf die Abonnement-Datenbank auf dem Abonnenten an. Standardmäßig erfolgt die Erstsynchronisierung unmittelbar nach dem Erstellen einer Abonnements, wenn Sie den Assistenten für neue Veröffentlichung verwenden. Dieses Verhalten wird von der Option **Initialisierungszeitpunkt** auf der Seite **Abonnements initialisieren** des Assistenten gesteuert. Wenn Momentaufnahmen generiert werden, nachdem ein Abonnement initialisiert wurde, werden sie nicht auf den Abonnenten angewendet, es sei denn, ein Abonnement ist für die erneute Initialisierung markiert. Weitere Informationen finden Sie unter [Abonnements erneut initialisieren](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
 Nachdem der Verteilungs- bzw. der Merge-Agent die Anfangsmomentaufnahme angewendet hat, gibt er nachfolgende Updates und andere Datenänderungen weiter. Wenn Momentaufnahmen an Abonnenten verteilt und auf ihnen angewendet werden, sind nur die Abonnenten betroffen, die auf eine Anfangsmomentaufnahme oder neue Momentaufnahmen warten. Andere Abonnenten dieser Veröffentlichung (diejenigen, die bereits Einfügungen, Updates, Löschungen oder andere Änderungen der veröffentlichten Daten empfangen) sind nicht betroffen.  
  
 Informationen zum Erstellen und Anwenden der Anfangsmomentaufnahme finden Sie unter [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
 Informationen zum Anzeigen oder Ändern des Standardspeicherorts für den Momentaufnahmeordner finden Sie im entsprechenden Abschnitt.  
  
-   [! INCLUDE [SsManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [Specify the Default Snapshot Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)  
  
-   Replikations- und RMO-Programmierung: [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
## Siehe auch  
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md)   
 [Sp_addpublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)  
  
  