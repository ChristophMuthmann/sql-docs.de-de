---
title: "Anzeigen von Konfliktinformationen für Mergepublikationen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- sp_helpmergeconflictrows
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
- sp_helpmergearticleconflicts
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e4ea6a407b8e79e0263c1d78ad2a192ea7253e06
ms.lasthandoff: 04/11/2017

---
# <a name="view-conflict-information-for-merge-publications"></a>Anzeigen von Konfliktinformationen für Mergepublikationen
  Wenn Konflikte während einer Mergereplikations aufgelöst werden, werden die Daten aus der verlierenden Zeile in eine Konflikttabelle geschrieben. Diese Konfliktdaten können programmgesteuert mithilfe gespeicherter Replikationsprozeduren angezeigt werden. Weitere Informationen finden Sie unter [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### <a name="to-view-conflict-information-and-losing-row-data-for-all-types-of-conflicts"></a>So zeigen Sie Konfliktinformationen und Daten zu den verlierenden Zeilen für alle Typen von Konflikten an  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)aus. Beachten Sie die Werte der folgenden Spalten im Resultset:  
  
    -   **centralized_conflicts** &ndash; 1 zeigt an, dass Konfliktzeilen auf dem Verleger gespeichert werden, und 0 zeigt an, dass Konfliktzeilen nicht auf dem Verleger gespeichert werden.  
  
    -   **decentralized_conflicts** &ndash; 1 zeigt an, dass Konfliktzeilen auf dem Abonnenten gespeichert werden, und 0 zeigt an, dass Konfliktzeilen nicht auf dem Abonnenten gespeichert werden.  
  
        > [!NOTE]  
        >  Das Konfliktprotokollierungsverhalten einer Mergeveröffentlichung wird mithilfe des **@conflict_logging** -Parameters von [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Der **@centralized_conflicts** -Parameter wurde als veraltet markiert.  
  
     In der folgenden Tabelle werden die Werte dieser Spalten in Abhängigkeit von dem für **@conflict_logging**.  
  
    |@conflict_logging-Wert|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Abonnementen für die Abonnementdatenbank [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)aus. Geben Sie einen Wert für **@publication** an, um nur Konfliktinformationen zu Artikeln zurückzugeben, die zu einer bestimmten Veröffentlichung gehören. Damit werden Konflikttabelleninformationen für Artikel mit Konflikten zurückgegeben. Notieren Sie den Wert von **conflict_table** bei allen Artikeln, die von Interesse sind. Wenn **conflict_table** für einen Artikel den Wert NULL hat, werden nur die Konflikte gelöscht, die in diesem Artikel aufgetreten sind.  
  
3.  (Optional) Überprüfen Sie die Konfliktzeilen für die Artikel, die von Interesse sind. Wählen Sie abhängig von den Werten von **centralized_conflicts** und **decentralized_conflicts** aus Schritt 1 eine der folgenden Vorgehensweisen:  
  
    -   Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)aus. Geben Sie für den Artikel (aus Schritt 1) eine Konflikttabelle für **@conflict_table**. (Optional) Geben Sie den Wert **@publication** an, um die Rückgabe von Konfliktinformationen auf eine bestimmte Veröffentlichung zu beschränken. Damit werden Zeilendaten und andere Informationen für die verlierende Zeile zurückgegeben.  
  
    -   Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)aus. Geben Sie für den Artikel (aus Schritt 1) eine Konflikttabelle für **@conflict_table**. Damit werden Zeilendaten und andere Informationen für die verlierende Zeile zurückgegeben.  
  
### <a name="to-view-information-only-on-conflicts-where-the-delete-failed"></a>So zeigen Sie nur Informationen zu Konflikten an, bei denen eine Löschung fehlschlug  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)aus. Beachten Sie die Werte der folgenden Spalten im Resultset:  
  
    -   **centralized_conflicts** &ndash; 1 zeigt an, dass Konfliktzeilen auf dem Verleger gespeichert werden, und 0 zeigt an, dass Konfliktzeilen nicht auf dem Verleger gespeichert werden.  
  
    -   **decentralized_conflicts** &ndash; 1 zeigt an, dass Konfliktzeilen auf dem Abonnenten gespeichert werden, und 0 zeigt an, dass Konfliktzeilen nicht auf dem Abonnenten gespeichert werden.  
  
        > [!NOTE]  
        >  Das Konfliktprotokollierungsverhalten einer Mergeveröffentlichung wird mithilfe des **@conflict_logging** -Parameters von [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Der **@centralized_conflicts** -Parameter wurde als veraltet markiert.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Abonnementen für die Abonnementdatenbank [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)aus. Geben Sie einen Wert für **@publication** an, um nur Konflikttabelleninformationen zu Artikeln zurückzugeben, die zu einer bestimmten Veröffentlichung gehören. Damit werden Konflikttabelleninformationen für Artikel mit Konflikten zurückgegeben. Notieren Sie den Wert von **source_object** bei allen Artikeln, die von Interesse sind. Wenn **conflict_table** für einen Artikel den Wert NULL hat, werden nur die Konflikte gelöscht, die in diesem Artikel aufgetreten sind.  
  
3.  (Optional) Überprüfen Sie die Konfliktinformationen für Löschkonflikte. Wählen Sie abhängig von den Werten von **centralized_conflicts** und **decentralized_conflicts** aus Schritt 1 eine der folgenden Vorgehensweisen:  
  
    -   Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)aus. Geben Sie den Namen der Quelltabelle (aus Schritt 1) an, in der der Konflikt bezüglich **@source_object**. (Optional) Geben Sie den Wert **@publication** an, um die Rückgabe von Konfliktinformationen auf eine bestimmte Veröffentlichung zu beschränken. Damit werden auf dem Verleger gespeicherte Informationen zu Löschkonflikten zurückgegeben.  
  
    -   Führen Sie auf dem Abonnenten für die Abonnementdatenbank [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)aus. Geben Sie den Namen der Quelltabelle (aus Schritt 1) an, in der der Konflikt bezüglich **@source_object**. (Optional) Geben Sie den Wert **@publication** an, um die Rückgabe von Konfliktinformationen auf eine bestimmte Veröffentlichung zu beschränken. Damit werden auf dem Abonnenten gespeicherte Informationen zu Löschkonflikten zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
