---
title: Verbessern der Leistung von Volltextabfragen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0658dc74-25eb-4486-bbd6-e85c1f92c272
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ec53c06cb92a31b0488d2f6c4ef1f294e43c0a1
ms.lasthandoff: 04/11/2017

---
# <a name="improve-the-performance-of-full-text-queries"></a>Verbessern der Leistung von Volltextabfragen
  Die folgenden Empfehlungen sollen Ihnen dabei helfen, die Leistung von Volltextabfragen zu erhöhen.  
  
 Die Leistung bei Volltextabfragen wird auch von den Hardwareressourcen wie Arbeitsspeicher, Datenträgergeschwindigkeit, CPU-Geschwindigkeit und Computerarchitektur beeinflusst.  
  
-   Defragmentieren Sie den Index der Basistabelle mithilfe von [ALTER INDEX REORGANIZE](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   Organisieren Sie den Volltextkatalog mithilfe von [ALTER FULLTEXT CATALOG REORGANIZE](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)neu. Stellen Sie sicher, dass dies vor dem Leistungstest erfolgt, da das Ausführen dieser Anweisung zu einer Masterzusammenführung der Volltextindizes im Katalog führt.  
  
-   Beschränken Sie die Auswahl von Volltextschlüsselspalten auf eine kleine Spalte. Es wird zwar eine 900-Byte-Spalte unterstützt, aber es ist ratsam, in einem Volltextindex eine kleinere Schlüsselspalte zu verwenden. **int** und **bigint** bieten die beste Leistung.  
  
-   Durch die Verwendung eines Volltextschlüssels mit ganzen Zahlen können Sie einen Join mit der Zuordnungstabelle **docid** vermeiden. Deshalb verbessert ein ganzzahliger Volltextschlüssel die Abfrageleistung erheblich und optimiert außerdem die Durchforstungsleistung. Es können sich weitere Leistungsvorteile ergeben, wenn der Volltextschlüssel auch der Schlüssel des gruppierten Index ist.  
  
-   Fassen Sie mehrere [CONTAINS](../../t-sql/queries/contains-transact-sql.md) -Prädikate zu einem CONTAINS-Prädikat zusammen. Sie können in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Liste von Spalten in der CONTAINS-Abfrage angeben.  
  
-   Verwenden Sie [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) oder [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) statt CONTAINS bzw. FREETEXT, wenn Sie nur Volltextschlüssel- oder Ranginformationen benötigen.  
  
-   Verwenden Sie den *top_n_by_rank* -Parameter der Funktionen FREETEXTTABLE und CONTAINSTABLE, um die Ergebnisse einzuschränken und die Leistung zu erhöhen. Mit*top_n_by_rank* können Sie nur die relevantesten Treffer aufrufen. Verwenden Sie diesen Parameter nur, wenn es beim vorliegenden Geschäftsmodell nicht erforderlich ist, alle möglichen Ergebnisse zurückzugeben (d.h., es wird kein *Gesamtrückruf*benötigt).  
  
    > [!NOTE]  
    >  Gesamtrückrufe werden i d. R. in juristischen Szenarios verlangt. In anderen Geschäftsszenarios, z. B. für das E-Business, sind Leistungsaspekte meist vorrangig.  
  
-   Prüfen Sie den Volltextabfrageplan, um sicherzustellen, dass der entsprechende Joinplan ausgewählt ist. Verwenden Sie ggf. einen Joinhinweis oder einen Abfragehinweis. Wenn ein Parameter in der Volltextabfrage verwendet wird, bestimmt der erste Wert dieses Parameters den Abfrageplan. Sie können den OPTIMIZE FOR- [Abfragehinweis](../../t-sql/queries/hints-transact-sql-query.md) verwenden, um die Abfrage zu zwingen, einen von Ihnen ausgewählten Wert zu kompilieren. Dadurch wird ein deterministischer Abfrageplan und bessere Leistung erzielt.  
  
-   Zu viele Volltextindexfragmente im Volltextindex können zu einer beträchtlichen Verringerung der Abfrageleistung führen. Um die Anzahl der Fragmente zu reduzieren, organisieren Sie den Volltextkatalog neu, indem Sie die Option REORGANIZE der [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung verwenden. Diese Anweisung führt im Wesentlichen alle Fragmente zu einem einzelnen großen Fragment zusammen und entfernt alle veralteten Einträge aus dem Volltextindex.  
  
-   Bei der Volltextsuche in  können die unter CONTAINSTABLE (AND, OR) angegebenen logischen Operatoren entweder als SQL-Joins oder innerhalb der Streaming-Tabellenwertfunktionen (STVF) der Volltextausführung implementiert werden. Normalerweise werden Abfragen, die nur über einen Typ von logischen Operatoren verfügen, ausschließlich über die Volltextausführung implementiert, während Abfragen mit gemischten logischen Operatoren auch SQL-Joins aufweisen. Bei der Implementierung eines logischen Operators innerhalb der Volltextausführung STVF werden einige spezielle Indexeigenschaften verwendet, die gegenüber SQL-Joins Geschwindigkeitsvorteile aufweisen. Aus diesem Grund ist es ratsam, für Frames von Abfragen möglichst nur einen Typ von logischem Operator zu verwenden.  
  
-   Bei Anwendungen, die Prädikate mit selektiver Beziehung enthalten, funktionieren Abfragen, die selektive relationale Prädikate und nicht selektive Volltextprädikate verwenden, ggf. am besten, wenn sie für die Verwendung des Abfrageoptimierers geschrieben werden. Dann kann der Abfrageoptimierer entscheiden, ob ein Prädikats- oder Bereichs-Pushdown verwendet werden kann, um einen effektiven Abfrageplan aufzustellen. Dieser Ansatz ist einfacher und häufig auch effizienter als das Indizieren von relationalen Daten als Volltextdaten.  
  
## <a name="related-resources"></a>Verwandte Ressourcen  
 [SQL Server 2008-Volltextsuche: Internes und Erweiterungen](http://go.microsoft.com/fwlink/?LinkId=129544)  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
  
