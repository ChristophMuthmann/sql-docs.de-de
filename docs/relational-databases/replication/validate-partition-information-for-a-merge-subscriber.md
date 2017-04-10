---
title: "&#220;berpr&#252;fen von Partitionsinformationen f&#252;r einen Mergeabonnenten | Microsoft Docs"
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
  - "Überprüfen von Daten der Mergereplikation [SQL Server-Replikation], Partitionen"
  - "Parametrisierte Filter [SQL Server-Replikation], Überprüfen von Partitionsinformationen"
  - "Überprüfen von Partitionsinformationen"
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# &#220;berpr&#252;fen von Partitionsinformationen f&#252;r einen Mergeabonnenten
  Beim Definieren eines parametrisierten Zeilenfilters für eine Mergeveröffentlichung kommt eine Funktion zum Einsatz, die die Abonnenteninformationen, wie z. B. den Benutzernamen des Abonnenten, referenziert. Standardmäßig überprüft die Replikation die Abonnenteninformationen auf der Basis dieser Funktion. Erst dann erfolgt die jeweilige Synchronisierung. Die Überprüfung erfolgt auch immer dann, wenn eine Momentaufnahme auf den Abonnenten angewendet wird. Mit der Überprüfung wird sichergestellt, dass die Daten ordnungsgemäß für die einzelnen Abonnenten partitioniert sind. Überprüfungsverhalten wird gesteuert, indem die **Validate_subscriber_info** veröffentlichungseigenschaft, die mit geändert werden kann [Sp_changemergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) oder auf die **Abonnementoptionen** auf der Seite der **Veröffentlichungseigenschaften** Dialogfeld. Weitere Informationen zum Ändern der Veröffentlichungseigenschaften finden Sie unter [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
## Funktionsweise der Partitionsüberprüfung  
 Wenn eine Veröffentlichung mithilfe der Funktion gefiltert wird, z. B. **SUSER_SNAME()**, der Merge-Agent wendet den Anfangssnapshot an jeden Abonnenten basierend auf Daten, die für die **SUSER_SNAME()** Ausdruck.  
  
 Wenn die Überprüfung aktiviert ist und der Abonnent für die nächste Synchronisierung erneut eine Verbindung mit dem Verleger herstellt, überprüft der Merge-Agent die Informationen auf dem Abonnenten und stellt sicher, dass die Partition auf den Abonnenten mit der Partition identisch ist, die in der Anfangsmomentaufnahme gesendet wurde. Bei allen nachfolgenden Merge- bzw. Momentaufnahmeanwendungen überprüft der Merge-Agent die Partition der einzelnen Abonnenten.  
  
 Wenn der Merge-Agent feststellt, dass die im Filterausdruck verwendete Funktion einen anderen Wert zurückgibt als in der Anfangsmomentaufnahme, schlägt die Merge- bzw. Momentaufnahmeanwendung fehl, und das Abonnement des Abonnenten muss möglicherweise erneut initialisiert werden. Diese erneute Initialisierung kann nötig werden, um Probleme zu vermeiden, die sich aus der Änderung der Mergeeinstellungen eines Abonnenten ergeben können. Es reicht möglicherweise aber auch aus, die Informationen auf dem Abonnenten, wie z. B. den Benutzernamen, auf den Wert zum Zeitpunkt der ursprünglichen Momentaufnahme zurückzusetzen.  
  
 Beim Überprüfen einer Partition gleicht der Merge-Agent aber nicht nur die Partition mit den Werten ab, die von den in den Filterausdrücken verwendeten Funktionen zurückgegeben werden, sondern er kontrolliert auch, ob die Momentaufnahme generiert wurde, bevor Änderungen vorgenommen wurden, durch die sie ungültig geworden ist. Solche Änderungen können z. B. Metadaten-Cleanupoperationen oder Schemaänderungen sein. Wenn eine partitionierte Momentaufnahme zu alt ist, gibt der Merge-Agent einen Fehler zurück. In diesem Fall müssen Sie auf der Grundlage einer aktuellen regulären Momentaufnahme eine neue partitionierte Momentaufnahme für diesen Abonnenten generieren.  
  
## Siehe auch  
 [Verwaltung & #40; Replikation & #41;](../../relational-databases/replication/administration/administration-replication.md)   
 [Bewährte Methoden für die Replikationsverwaltung](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Erneutes Initialisieren von Abonnements](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md)  
  
  