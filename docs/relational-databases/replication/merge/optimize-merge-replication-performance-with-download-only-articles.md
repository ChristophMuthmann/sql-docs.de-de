---
title: Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0b82a117316022f7c30920d9174855522d374f1b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel
  Die Mergereplikation bietet zwei Artikeltypen, um die verschiedenen Anwendungsanforderungen zu erfüllen. Veröffentlichungen können der Anwendung entsprechend einen oder mehrere der Artikeltypen enthalten:  
  
-   Standardartikel  
  
-   Nur herunterladbare Artikel  
  
 Nur herunterladbare Artikel bieten eine bessere Leistung im Vergleich zu Standardartikeln und sollten stets verwendet werden, wenn sie sich eignen.  
  
> [!NOTE]  
>  Damit nur herunterladbare Artikel verwendet werden können, muss die Veröffentlichung mindestens einen Kompatibilitätsgrad von 90RTM aufweisen.  
  
## <a name="standard-articles"></a>Standardartikel  
 Standardartikel werden standardmäßig verwendet und bieten den vollen Umfang der Replikationsfunktionen, einschließlich der vielseitigen Konflikterkennung und -lösung. Standardartikel eigenen sich für Tabellen, die von mehreren Abonnenten aktualisiert werden. Andere Objekte als Tabellen, wie z. B. gespeicherte Prozeduren und Sichten, werden immer als Standardartikel veröffentlicht.  
  
## <a name="download-only-articles"></a>Nur herunterladbare Artikel  
 Nur herunterladbare Artikel sind für Anwendungen bestimmt, deren Daten nicht auf den Abonnenten aktualisiert werden, z. B. eine Gruppe von Artikeln, die in einem Produktkatalog enthalten sind. Ein Produktkatalog wird in der Regel auf dem Verleger, nicht auf den Abonnenten aktualisiert. Da nur herunterladbare Artikel nicht auf dem Abonnenten aktualisiert werden können, wird das Nachverfolgen von Metadaten nicht an die Abonnenten gesendet. Das kann den Speicher auf den Abonnenten entlasten und zu einer höheren Leistung führen, besonders bei einer langsamen Netzwerkverbindung.  
  
 Nur herunterladbare Artikel funktionieren in Verbindung mit Clientabonnements: wenn ein Artikel als nur zum Herunterladen angegeben wird, können Zeilen für diesen Artikel nicht auf Abonnenten, die Clientabonnements verwenden, eingefügt, aktualisiert oder gelöscht werden. Verleger und Abonnenten, die den Serverabonnementtyp verwenden (in der Regel Abonnenten, die Daten auf anderen Abonnenten erneut veröffentlichen), können Daten einfügen, aktualisieren und löschen. Weitere Informationen zu Clientabonnements finden Sie unter [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md).  
  
 Informationen zum Angeben eines herunterladbaren Artikels finden Sie unter [Specify That a Merge Table Article is Download-Only](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md).  
  
## <a name="using-different-article-types-in-your-applications"></a>Verwenden unterschiedlicher Artikeltypen in den Anwendungen  
 Wenn Sie die Anforderungen Ihrer Anwendung kennen, können Sie die Vor- und Nachteile zwischen einer maximalen Flexibilität und einer optimalen Leistung abwägen. Wenn z. B. bei einer Anwendung zahlreiche Konflikte und Änderungen auf dem Verleger und den Abonnenten auftreten, wird hier eine aus Standardartikeln bestehende Veröffentlichung verwendet. Einige Anwendungen, z. B. SFA-Anwendungen (Sales Force Automation), enthalten möglicherweise Artikel mit potenziellen Konflikten sowie weitere Artikel, die als Nachschlagetabellen fungieren und nur herunterladbar sind. In Anwendungen zur Dateneingabe, wie Point-of-Sale-Systeme und FFA-Anwendungen (Field Force Automation), werden Daten häufig streng partitioniert, damit keine Konflikte auftreten, und es werden in keinem Fall Daten zwischen Abonnenten ausgetauscht. In diesen Fällen bietet eine Kombination aus nicht überlappenden Partitionen, nur herunterladbare Artikeln und vorausberechneten Partitionen ein Maximum an Leistung und Skalierbarkeit. Weitere Informationen zu nicht überlappenden Partition und vorausberechneten Partitionen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Artikeloptionen für die Mergereplikation](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Optimieren der Mergereplikationsleistung durch bedingtes Nachverfolgen von Löschvorgängen](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
