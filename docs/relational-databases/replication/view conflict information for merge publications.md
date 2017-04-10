---
title: "Anzeigen von Konfliktinformationen zu Mergever&#246;ffentlichungen (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Konfliktlösung bei der Mergereplikation [SQL Server-Replikation], Anzeigen von Konflikten"
  - "sp_helpmergeconflictrows"
  - "Anzeigen von Konfliktinformationen"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
  - "sp_helpmergearticleconflicts"
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Anzeigen von Konfliktinformationen zu Mergever&#246;ffentlichungen (Replikationsprogrammierung mit Transact-SQL)
  Wenn Konflikte während einer Mergereplikations aufgelöst werden, werden die Daten aus der verlierenden Zeile in eine Konflikttabelle geschrieben. Diese Konfliktdaten können programmgesteuert mithilfe gespeicherter Replikationsprozeduren angezeigt werden. Weitere Informationen finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### So zeigen Sie Konfliktinformationen und Daten zu den verlierenden Zeilen für alle Typen von Konflikten an  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Beachten Sie die Werte der folgenden Spalten im Resultset:  
  
    -   **Centralized_conflicts** -1 gibt an, dass Konfliktzeilen auf dem Verleger gespeichert werden, und 0 bedeutet, dass Konfliktzeilen nicht auf dem Verleger gespeichert werden.  
  
    -   **Decentralized_conflicts** -1 gibt an, dass Konfliktzeilen auf dem Abonnenten gespeichert werden, und 0 bedeutet, dass Konfliktzeilen nicht auf dem Abonnenten gespeichert werden.  
  
        > [!NOTE]  
        >  Das konfliktprotokollierungsverhalten einer Mergeveröffentlichung wird festgelegt, mit der **@conflict_logging** Parameter [Sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Verwenden der **@centralized_conflicts** Parameter ist veraltet.  
  
     Die folgende Tabelle beschreibt die Werte dieser Spalten auf Grundlage des Werts für die angegebene **@conflict_logging**.  
  
    |@conflict_logging-Wert|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Abonnenten für die Abonnementdatenbank [Sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Geben Sie einen Wert für **@publication** an, um nur Konfliktinformationen zu Artikeln zurückzugeben, die zu einer bestimmten Veröffentlichung gehören. Damit werden Konflikttabelleninformationen für Artikel mit Konflikten zurückgegeben. Beachten Sie den Wert der **Conflict_table** bei allen Artikeln von Interesse sind. Wenn der Wert der **Conflict_table** für ein Artikel NULL ist, sind in diesem Artikel nur Löschkonflikte aufgetreten.  
  
3.  (Optional) Überprüfen Sie die Konfliktzeilen für die Artikel, die von Interesse sind. Abhängig von den Werten der **Centralized_conflicts** und **Decentralized_conflicts** aus Schritt 1, führen Sie eine der folgenden:  
  
    -   Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Geben Sie eine Konflikttabelle des Artikels (aus Schritt 1) für **@conflict_table**. (Optional) Geben Sie den Wert **@publication** Rückgabe von Konfliktinformationen auf eine bestimmte Veröffentlichung einschränken. Damit werden Zeilendaten und andere Informationen für die verlierende Zeile zurückgegeben.  
  
    -   Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Geben Sie eine Konflikttabelle des Artikels (aus Schritt 1) für **@conflict_table**. Damit werden Zeilendaten und andere Informationen für die verlierende Zeile zurückgegeben.  
  
### So zeigen Sie nur Informationen zu Konflikten an, bei denen eine Löschung fehlschlug  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Beachten Sie die Werte der folgenden Spalten im Resultset:  
  
    -   **Centralized_conflicts** -1 gibt an, dass Konfliktzeilen auf dem Verleger gespeichert werden, und 0 bedeutet, dass Konfliktzeilen nicht auf dem Verleger gespeichert werden.  
  
    -   **Decentralized_conflicts** -1 gibt an, dass Konfliktzeilen auf dem Abonnenten gespeichert werden, und 0 bedeutet, dass Konfliktzeilen nicht auf dem Abonnenten gespeichert werden.  
  
        > [!NOTE]  
        >  Das konfliktprotokollierungsverhalten einer Mergeveröffentlichung festgelegt ist, mit der **@conflict_logging** Parameter [Sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Verwenden der **@centralized_conflicts** Parameter ist veraltet.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Abonnenten für die Abonnementdatenbank [Sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Geben Sie einen Wert für **@publication** an, um nur Konflikttabelleninformationen zu Artikeln zurückzugeben, die zu einer bestimmten Veröffentlichung gehören. Damit werden Konflikttabelleninformationen für Artikel mit Konflikten zurückgegeben. Beachten Sie den Wert der **Source_object** bei allen Artikeln von Interesse sind. Wenn der Wert der **Conflict_table** für ein Artikel NULL ist, sind in diesem Artikel nur Löschkonflikte aufgetreten.  
  
3.  (Optional) Überprüfen Sie die Konfliktinformationen für Löschkonflikte. Abhängig von den Werten der **Centralized_conflicts** und **Decentralized_conflicts** aus Schritt 1, führen Sie eine der folgenden:  
  
    -   Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Geben Sie den Namen der Quelltabelle (aus Schritt 1), auf dem der Konflikt aufgetreten, für die ist **@source_object**. (Optional) Geben Sie den Wert **@publication** Rückgabe von Konfliktinformationen auf eine bestimmte Veröffentlichung einschränken. Damit werden auf dem Verleger gespeicherte Informationen zu Löschkonflikten zurückgegeben.  
  
    -   Führen Sie auf dem Abonnenten für die Abonnementdatenbank [Sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Geben Sie den Namen der Quelltabelle (aus Schritt 1), auf dem der Konflikt aufgetreten, für die ist **@source_object**. (Optional) Geben Sie den Wert **@publication** Rückgabe von Konfliktinformationen auf eine bestimmte Veröffentlichung einschränken. Damit werden auf dem Abonnenten gespeicherte Informationen zu Löschkonflikten zurückgegeben.  
  
## Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  