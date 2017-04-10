---
title: "Optimieren der Mergereplikationsleistung durch bedingtes Nachverfolgen von L&#246;schvorg&#228;ngen | Microsoft Docs"
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
  - "Bedingte Nachverfolgung von Löschvorgängen [SQL Server-Replikation]"
  - "Mergereplikation [SQL Server-Replikation], Nachverfolgung von bedingten Löschvorgängen"
  - "Artikel [SQL Server-Replikation], Nachverfolgung von bedingten Löschvorgängen"
ms.assetid: 58f120a3-ea3a-4e97-93f0-0eb4e580ecf2
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Optimieren der Mergereplikationsleistung durch bedingtes Nachverfolgen von L&#246;schvorg&#228;ngen
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Bei der Mergereplikation können Sie angeben, dass Löschvorgänge für einen oder mehrere Artikel nicht von Replikationstriggern oder in Systemtabellen nachverfolgt werden sollen. Wenn Sie diese Option für einen Artikel angeben, werden Löschvorgänge weder nachverfolgt, noch vom Verleger oder den Abonnenten repliziert. Diese Option steht zur Unterstützung verschiedener Anwendungsszenarien zur Verfügung, und soll dort zur Leistungsoptimierung beitragen, wo die Replikation von Löschvorgängen weder nötig noch wünschenswert ist. Die Leistung wird auf drei verschiedene Arten optimiert: die Metadaten der Löschvorgänge werden nicht gespeichert; die Löschvorgänge werden während der Synchronisierung nicht aufgezählt; die Löschvorgänge werden nicht auf dem Abonnenten repliziert oder angewendet.  
  
> [!NOTE]  
>  Damit nur herunterladbare Artikel verwendet werden können, muss die Veröffentlichung mindestens einen Kompatibilitätsgrad von 90RTM aufweisen.  
  
 Diese Option kann beim Erstellen einer Veröffentlichung angegeben werden, oder ein- bzw. ausgeschaltet werden, wenn eine Anwendung erfordert, dass bestimmte Löschvorgänge repliziert werden, andere jedoch nicht (z. B. Batchlöschvorgänge). In den folgenden Beispielen wird veranschaulicht, wie diese Option in einer Anwendung verwendet werden kann:  
  
-   In einer Anwendung für den Außendienst eines Unternehmens gibt es in der Regel Spalten wie **SalesOrderHeader**, **SalesOrderDetail** und **Product**. Die Bestellungen (Orders) werden auf dem Abonnenten eingegeben und auf den Verleger repliziert, welcher die Daten meistens an ein Fulfillment-System weitergibt. Viele Mitarbeiter im Außendienst benutzen Handheld-PCs mit begrenztem Speicherplatz; nachdem der Verleger die Bestellung erhalten hat, kann sie auf dem Abonnenten gelöscht werden. Der Löschvorgang wird nicht an den Verleger weitergegeben, da die Bestellung weiterhin im System aktiv bleiben soll.  
  
     In diesem Szenario würden die Löschvorgänge für die Tabellen **SalesOrderHeader** und **SalesOrderDetail** nicht nachverfolgt werden. Sie müssten jedoch für die **Product** -Tabelle nachverfolgt werden, denn sollte ein Produkt auf dem Verleger gelöscht werden, müsste dieser Löschvorgang an den Abonnenten gesendet werden, damit dessen Produktliste aktuell bleibt.  
  
-   Eine Anwendung könnte z. B. Vergangenheitsdaten in einer **TransactionHistory**-Tabelle speichern, aus der in regelmäßigen Abständen alle Datensätze gelöscht werden, die älter als ein Jahr sind. Die Tabelle könnte nun so gefiltert werden, dass Abonnenten nur Daten zu Transaktionen des laufenden Monats erhalten. Die monatlichen Batchlöschvorgänge zum Löschen älterer Daten auf dem Verleger sind für die Abonnenten irrelevant, würden jedoch trotzdem standardmäßig nachverfolgt und aufgelistet werden.  
  
     In diesem Szenario könnte die Aktivität auf dem System vor der Batchverarbeitung angehalten werden, damit die Anwendung die Nachverfolgung der Löschvorgänge deaktivieren kann. Ist die Batchverarbeitung abgeschlossen, kann die Nachverfolgung erneut aktiviert werden.  
  
> [!IMPORTANT]  
>  Wenn andere Prozesse weiterhin auf dem Verleger aktiv sind, müssen Sie sicherstellen, dass keine Löschvorgänge erfolgen, die an Abonnenten weitergegeben werden sollen, solange die Nachverfolgung deaktiviert ist.  
  
 **So geben Sie an, dass Löschvorgänge nicht nachverfolgt werden**  
  
-   Replikation [!INCLUDE[tsql](../../../includes/tsql-md.md)] programming: [angeben, löscht sollte nicht werden nachverfolgt für Merge Artikel und #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/publish/specify that deletes should not be tracked for merge articles.md)  
  
## Siehe auch  
 [Artikeloptionen für die Mergereplikation](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)  
  
  