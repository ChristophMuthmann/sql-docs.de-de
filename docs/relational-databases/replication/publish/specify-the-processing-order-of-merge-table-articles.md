---
title: Angeben der Verarbeitungsreihenfolge von Mergetabellenartikeln | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
caps.latest.revision: "33"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa13d01bb92f37a7e7c68f0e9f7f2dbbffa1f628
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="specify-the-processing-order-of-merge-table-articles"></a>Angeben der Verarbeitungsreihenfolge von Mergetabellenartikeln
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die Mergereplikation ermöglicht Ihnen, die Reihenfolge anzugeben, in der Artikel während des Synchronisierungsprozesses vom Merge-Agent verarbeitet werden. Sie können den Artikeln bei ihrer Erstellung mithilfe gespeicherter Replikationsprozeduren programmgesteuert eine Reihenfolge zuweisen. Artikel werden in der Reihenfolge vom niedrigsten zum höchsten Wert verarbeitet. Wenn zwei Artikel denselben Wert haben, werden sie gleichzeitig verarbeitet. Weitere Informationen finden Sie unter [Angeben der Verarbeitungsreihenfolge von Mergeartikeln](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
### <a name="to-specify-the-processing-order-for-a-new-merge-article"></a>So geben Sie die Verarbeitungsreihenfolge für einen neuen Mergeartikel ein  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) aus. Geben Sie einen ganzzahligen Wert, der die Verarbeitungsreihenfolge für den Artikel darstellt, für **@processing_order**. Weitere Informationen finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Wenn Sie sortierte Artikel erstellen, sollten Sie Lücken zwischen den Werten für die Artikelreihenfolge lassen. Dadurch wird das Festlegen neuer Wert zu einem späteren Zeitpunkt erleichtert. Wenn Sie beispielsweise drei Artikel haben, für die Sie eine bestimmte Verarbeitungsreihenfolge angeben müssen, legen Sie den Wert von **@processing_order** auf 10, 20 und 30 anstatt 1, 2 und 3 fest.  
  
### <a name="to-change-the-processing-order-of-a-merge-article"></a>So ändern Sie die Verarbeitungsreihenfolge eines Mergeartikels  
  
1.  Um die Verarbeitungsreihenfolge eines Artikels zu ermitteln, führen Sie [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) aus, und betrachten den Wert von **processing_order** im Resultset.  
  
2.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) aus. Geben Sie den Wert **processing_order** für **@property** und einen ganzzahligen Wert, der die Verarbeitungsreihenfolge darstellt, für **@value**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Angeben der Verarbeitungsreihenfolge von Mergeartikeln](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)  
  
  
