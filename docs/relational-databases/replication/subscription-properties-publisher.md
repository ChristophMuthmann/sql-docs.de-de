---
title: "Abonnementeigenschaften - Verleger | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subproperties.publisher.f1"
helpviewer_keywords: 
  - "Abonnementeigenschaften (Dialogfeld)"
ms.assetid: d4b2bc8b-0431-4331-8305-8992c96d0d34
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Abonnementeigenschaften - Verleger
  Im Dialogfeld **Abonnementeigenschaften** des Verlegers können Sie die Eigenschaften von Pushabonnements anzeigen und festlegen. Sie können auch bestimmte Eigenschaften von Pullabonnements anzeigen. Die übrigen Eigenschaften sind jedoch nur über das Dialogfeld **Abonnementeigenschaften** des Abonnenten verfügbar und können auch nur dort geändert werden.  
  
 Zu jeder im Dialogfeld **Abonnementeigenschaften** verfügbaren Eigenschaft wird auch eine Beschreibung angezeigt. Klicken Sie auf eine Eigenschaft, um die dazugehörige Beschreibung am unteren Rand des Dialogfelds anzuzeigen. In diesem Thema werden zusätzliche Informationen zu einer Reihe von Eigenschaften bereitgestellt. Die meisten dieser Eigenschaften sind auf dem Verleger nur für Pushabonnements verfügbar. Die Eigenschaften sind in folgenden Kategorien angeordnet:  
  
-   Eigenschaften, die für alle Abonnements gelten.  
  
-   Eigenschaften, die für Transaktionsabonnements gelten.  
  
-   Eigenschaften, die für Mergeabonnements gelten.  
  
 Schreibgeschützte Optionen können nur beim Erstellen des Abonnements festgelegt werden. Wenn Sie Optionen festlegen möchten, die nicht im Assistenten für neue Abonnements verfügbar sind, müssen Sie das Abonnement mithilfe von gespeicherten Prozeduren erstellen. Weitere Informationen finden Sie unter [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) und [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
## Optionen für alle Abonnements  
 **Sicherheit**  
 Klicken Sie auf die **Agentprozesskontos** Zeile, und klicken Sie dann auf die Eigenschaftenschaltfläche (**...**) zum Ändern des Kontos, unter dem der Snapshot-Agent oder Merge-Agent auf dem Verteiler ausgeführt wird. Klicken Sie zum Ändern des Kontos, unter dem der Snapshot-Agent oder Merge-Agent Verbindungen mit dem Abonnenten stellt, auf **abonnentenverbindung**, und klicken Sie dann auf die Eigenschaftenschaltfläche (**...**).  
  
 Weitere Informationen zu den für die einzelnen Agents erforderlichen Berechtigungen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Optionen für Transaktionsabonnements  
 **Transaktionsschleifen verhindern**  
 Legt fest, ob der Verteilungs-Agent Transaktionen des Abonnenten zurück an den Abonnenten sendet. Diese Option wird bei der bidirektionalen Transaktionsreplikation verwendet. Weitere Informationen finden Sie unter [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).  
  
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
  
## Siehe auch  
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  