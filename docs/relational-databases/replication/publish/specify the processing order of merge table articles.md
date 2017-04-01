---
title: "Angeben der Verarbeitungsreihenfolge von Mergetabellenartikeln (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
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
  - "Artikel [SQL Server-Replikation], Verarbeitungsreihenfolge"
  - "Mergereplikation [SQL Server-Replikation], Verarbeitungsreihenfolge von Artikeln"
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Angeben der Verarbeitungsreihenfolge von Mergetabellenartikeln (Replikationsprogrammierung mit Transact-SQL)
  Die Mergereplikation ermöglicht es Ihnen, die Reihenfolge anzugeben, in der Artikel während des Synchronisierungsprozesses vom Merge-Agent verarbeitet werden. Sie können den Artikeln bei ihrer Erstellung mithilfe gespeicherter Replikationsprozeduren programmgesteuert eine Reihenfolge zuweisen. Artikel werden in der Reihenfolge vom niedrigsten zum höchsten Wert verarbeitet. Wenn zwei Artikel denselben Wert haben, werden sie gleichzeitig verarbeitet. Weitere Informationen finden Sie unter [Geben Sie die Verarbeitung Reihenfolge von Merge Artikel](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
### So geben Sie die Verarbeitungsreihenfolge für einen neuen Mergeartikel ein  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie einen Ganzzahlwert, der die Verarbeitungsreihenfolge des Artikels für **@processing_order**. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Wenn Sie sortierte Artikel erstellen, sollten Sie Lücken zwischen den Werten für die Artikelreihenfolge lassen. Dadurch wird das Festlegen neuer Wert zu einem späteren Zeitpunkt erleichtert. Z. B. Wenn Sie drei Artikel Sie für die eine bestimmte Verarbeitungsreihenfolge angeben müssen haben, legen Sie den Wert der **@processing_order** 10, 20 und 30 anstatt 1, 2 und 3, bzw..  
  
### So ändern Sie die Verarbeitungsreihenfolge eines Mergeartikels  
  
1.  Um die Verarbeitungsreihenfolge eines Artikels zu bestimmen, führen [Sp_helpmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) und beachten Sie den Wert der **Processing_order** im Ergebnis festlegen.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_changemergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Geben Sie den Wert **Processing_order** für **@property** und einen ganzzahligen Wert, der die Verarbeitungsreihenfolge für **@value**.  
  
## Siehe auch  
 [Angeben der Verarbeitungsreihenfolge von Mergeartikeln](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)  
  
  