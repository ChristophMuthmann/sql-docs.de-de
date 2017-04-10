---
title: "Angeben, dass L&#246;schvorg&#228;nge f&#252;r Mergeartikel nicht nachverfolgt werden sollen (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
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
  - "Bedingte Nachverfolgung von Löschvorgängen [SQL Server-Replikation]"
  - "Mergereplikation [SQL Server-Replikation], bedingte Nachverfolgung von Löschvorgängen"
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Angeben, dass L&#246;schvorg&#228;nge f&#252;r Mergeartikel nicht nachverfolgt werden sollen (Replikationsprogrammierung mit Transact-SQL)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Standardmäßig synchronisiert die Mergereplikation DELETE-Befehle zwischen dem Verleger und dem Abonnenten. Die Mergereplikation ermöglicht Ihnen, Zeilen in der Abonnementdatenbank auch dann beizubehalten, wenn sie aus der Veröffentlichung gelöscht wurden und umgekehrt. Sie können bei der Erstellung eines neuen Artikels programmgesteuert festlegen, dass der DELETE-Befehl ignoriert wird, oder Sie können diese Funktionalität zu einem späteren Zeitpunkt mithilfe von gespeicherten Replikationsprozeduren aktivieren.  
  
> [!IMPORTANT]  
>  Die Aktivierung dieser Funktionalität führt zu Nichtkonvergenz, was bedeutet, dass die dem Abonnenten verfügbaren Daten nicht genau den Daten des Verlegers entsprechen. Sie müssen einen eigenen Mechanismus implementieren, um die gelöschten Zeilen zu entfernen.  
  
### So geben Sie an, dass Löschvorgänge für Mergeartikel ignoriert werden sollen  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie den Wert **false** für **@delete_tracking**. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung, den Wert des veröffentlicht wurde **Delete_tracking** muss für beide Artikel gleich sein.  
  
### So geben Sie an, dass Löschvorgänge für einen vorhandenen Mergeartikel ignoriert werden sollen  
  
1.  Um festzustellen, ob die fehlerkompensierung für einen Artikel aktiviert ist, führen Sie [Sp_helpmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) und beachten Sie den Wert der **Delete_tracking** im Ergebnis festlegen. Ist dieser Wert **0**, werden Löschvorgänge bereits ignoriert.  
  
2.  Wenn der Wert aus Schritt 1 **1**, führen Sie [Sp_changemergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Delete_tracking** für **@property**, und der Wert **false** für **@value**.  
  
    > [!NOTE]  
    >  Wenn die Quelltabelle eines Artikels bereits in einer anderen Veröffentlichung, den Wert des veröffentlicht wurde **Delete_tracking** muss für beide Artikel gleich sein.  
  
## Siehe auch  
 [Optimieren der Mergereplikationsleistung durch bedingtes Nachverfolgen von Löschvorgängen](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  