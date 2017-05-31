---
title: "Veröffentlichen der Ausführung von gespeicherten Prozeduren in der Transaktionsreplikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], stored procedures and
- transactional replication, publishing stored procedure execution
ms.assetid: f4686f6f-c224-4f07-a7cb-92f4dd483158
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3417818eb5ff6f9f5afce213457828844d2912a8
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="publishing-stored-procedure-execution-in-transactional-replication"></a>Veröffentlichen der Ausführung von gespeicherten Prozeduren in der Transaktionsreplikation
  Wenn Sie gespeicherte Prozeduren verwenden, die auf dem Verleger ausgeführt werden und sich auf die veröffentlichten Tabellen auswirken, sollten Sie darüber nachdenken, diese gespeicherten Prozeduren als Artikel für die Ausführung einer gespeicherten Prozedur in Ihre Veröffentlichung aufzunehmen. Die Definition der Prozedur (die CREATE PROCEDURE-Anweisung) wird beim Initialisieren des Abonnements auf den Abonnenten repliziert. Wenn die Prozedur dann auf dem Verleger ausgeführt wird, führt die Replikation auch die entsprechende Prozedur auf dem Abonnenten aus. Dies kann in den Fällen, in denen umfangreiche Batchvorgänge ausgeführt werden, zu einer deutlichen Leistungssteigerung führen, da nur die Ausführung der Prozedur repliziert wird und sich das Replizieren der einzelnen Änderungen für jede Zeile erübrigt. Nehmen wir z. B. an, Sie erstellen in der Veröffentlichungsdatenbank die folgende gespeicherte Prozedur:  
  
```  
CREATE PROC give_raise AS  
UPDATE EMPLOYEES SET salary = salary * 1.10  
```  
  
 Mit dieser Prozedur erhält jeder der 10.000 Angestellten in Ihrem Unternehmen eine Gehaltserhöhung von 10 %. Wenn Sie diese gespeicherte Prozedur auf dem Verleger ausführen, aktualisiert sie die Gehälter aller Angestellten. Ohne die Replikation der Ausführung der gespeicherten Prozedur würde das Update an die Abonnenten als eine große Transaktion mit mehreren Schritten gesendet:  
  
```  
BEGIN TRAN  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 1'  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 2'  
```  
  
 Dieser Vorgang würde sich dann für 10.000 Updates wiederholen.  
  
 Mit der Replikation der Ausführung der gespeicherten Prozedur sendet die Replikation lediglich den Befehl zum Ausführen der gespeicherten Prozedur auf dem Abonnenten. Sie schreibt also nicht alle Updates in die Verteilungsdatenbank, um sie dann über das Netzwerk an den Abonnenten zu senden:  
  
```  
EXEC give_raise  
```  
  
> [!IMPORTANT]  
>  Die Replikation von gespeicherten Prozeduren eignet sich nicht für alle Anwendungen. Falls ein Artikel horizontal gefiltert wird, sodass auf dem Verleger andere Zeilen als auf dem Abonnenten vorhanden sind, führt das Ausführen ein und derselben gespeicherten Prozedur auf dem Abonnenten und dem Verleger zu unterschiedlichen Ergebnissen. Unterschiedliche Ergebnisse beim Ausführen ein und derselben gespeicherten Prozedur auf dem Verleger und dem Abonnenten entstehen aber auch dann, wenn das Update auf einer Unterabfrage einer anderen, nicht replizierten Tabelle basiert.  
  
 **So veröffentlichen Sie die Ausführung einer gespeicherten Prozedur**  
  
-   SQL Server Management Studio: [Veröffentlichen der Ausführung einer gespeicherten Prozedur in einer Transaktionsveröffentlichung &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
-   Replikationsprogrammierung mit Transact-SQL: Führen Sie [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) aus, und geben Sie anschließend für den **@type**-Parameter den Wert 'serializable proc exec' (empfohlen) oder 'proc exec' an. Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="modifying-the-procedure-at-the-subscriber"></a>Ändern der Prozedur auf dem Abonnenten  
 Standardmäßig wird die Definition der gespeicherten Prozedur auf dem Verleger an jeden Abonnenten weitergegeben. Sie können aber auch die gespeicherte Prozedur auf dem Abonnenten ändern. Dies ist dann sinnvoll, wenn auf dem Verleger und dem Abonnenten eine unterschiedliche Logik ausgeführt werden soll. Gehen wir als Beispiel von **sp_big_delete**aus, einer gespeicherten Prozedur auf dem Verleger mit zwei Funktionen: Zum einen löscht die Prozedur 1.000.000 Zeilen aus der replizierten **big_table1** -Tabelle, zum anderen aktualisiert sie die nicht replizierte **big_table2**-Tabelle. Um den Bedarf an Netzwerkressourcen zu reduzieren, sollten Sie das Löschen der 1 Million Zeilen als gespeicherte Prozedur weitergeben, indem Sie **sp_big_delete**veröffentlichen. Auf dem Abonnenten können Sie **sp_big_delete** so ändern, dass nur die 1 Million Zeilen gelöscht werden, ohne ein nachfolgendes Update von **big_table2**auszuführen.  
  
> [!NOTE]  
>  Standardmäßig werden alle Änderungen, die mithilfe von ALTER PROCEDURE auf dem Verleger vorgenommen werden, an den Abonnenten weitergegeben. Wenn Sie dies verhindern möchten, deaktivieren Sie die Weitergabe der Schemaänderungen, bevor Sie ALTER PROCEDURE ausführen. Weitere Informationen zu Schemaänderungen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="types-of-stored-procedure-execution-articles"></a>Typen von Artikeln für die Ausführung einer gespeicherter Prozedur  
 Es gibt zwei verschiedene Möglichkeiten, mit denen die Ausführung einer gespeicherten Prozedur veröffentlicht werden kann: serialisierbare Prozedurausführungsartikel und Prozedurausführungsartikel.  
  
-   Die Verwendung der ersten Option wird empfohlen, weil dabei die Prozedurausführung nur dann repliziert wird, wenn die Prozedur im Kontext einer serialisierbaren Transaktion ausgeführt wird. Falls die gespeicherte Prozedur von außerhalb einer serialisierbaren Transaktion ausgeführt wird, werden Änderungen an den Daten in den veröffentlichten Tabellen als eine Reihe von DML-Anweisungen repliziert. Dieses Verhalten trägt dazu bei, dass die Daten auf dem Abonnenten mit den Daten auf dem Verleger konsistent sind. Dies erweist sich vor allem für Batchvorgänge, wie z. B. umfangreiche Cleanupvorgänge, als hilfreich.  
  
-   Bei der Option zum Ausführen von Prozeduren kann die Prozedurausführung auf alle Abonnenten repliziert werden, und zwar unabhängig davon, ob die einzelnen Anweisungen in der gespeicherten Prozedur erfolgreich waren. Da Änderungen, die von der gespeicherten Prozedur an den Daten vorgenommen wurden, innerhalb mehrerer Transaktionen auftreten können, ist außerdem nicht sichergestellt, dass die Daten auf den Abonnenten mit den Daten auf dem Verleger konsistent sind. Zur Behebung dieser Probleme müssen Abonnenten schreibgeschützt sein. Außerdem ist es erforderlicht, dass Sie eine Isolationsstufe verwenden, die größer ist als READ UNCOMMITTED. Wenn Sie READ UNCOMMITTED verwendet, werden Änderungen an Daten in veröffentlichten Tabellen als Reihe von DML-Anweisungen repliziert.  
  
 Im folgenden Beispiel werden die Gründe veranschaulicht, warum das Replizieren von Prozeduren als serialisierbare Prozedurartikel empfehlenswert ist.  
  
```  
BEGIN TRANSACTION T1  
SELECT @var = max(col1) FROM tableA  
UPDATE tableA SET col2 = <value>   
   WHERE col1 = @var   
  
BEGIN TRANSACTION T2  
INSERT tableA VALUES <values>  
COMMIT TRANSACTION T2  
```  
  
 Im vorhergehenden Beispiel wurde davon ausgegangen, dass die SELECT-Anweisung in der T1-Transaktion vor der INSERT-Anweisung in der T2-Transaktion stattfindet.  
  
 Wird die Prozedur nicht in einer serialisierbaren Transaktion ausgeführt (beispielsweise mit einer auf SERIALIZABLE festgelegten Isolationsstufe), kann die T2-Transaktion innerhalb des Bereichs der SELECT-Anweisung in T1 eine neue Zeile einfügen und vor T1 ein Commit ausführen. Das bedeutet auch, dass sie vor T1 auf den Abonnenten angewendet wird. Wird T1 auf den Abonnenten angewendet, könnte die SELECT-Anweisung einen anderen Wert auf dem Verleger zurückgeben und zu einem unterschiedlichen Ergebnis der UPDATE-Anweisung führen.  
  
 Wenn die Prozedur in einer serialisierbaren Transaktion ausgeführt wird, darf die T2-Transaktion keine Zeile innerhalb des von der SELECT-Anweisung in T2 liegenden Bereichs einfügen. Sie wird dann so lange blockiert, bis T1 einen Commit ausführt und so dieselben Ergebnisse auf dem Abonnenten sichergestellt sind.  
  
 Sperren werden länger aufrecht erhalten, wenn Sie die Prozedur in einer serialisierbaren Transaktion ausführen, und können zu reduzierter Parallelität führen.  
  
## <a name="the-xactabort-setting"></a>Die XACT_ABORT-Einstellung  
 Beim Replizieren der Ausführung einer gespeicherten Prozedur sollte die Einstellung XACT_ABORT für die Sitzung, die die gespeicherte Prozedur ausführt, ON angeben. Wenn für XACT_ABORT die Einstellung OFF festgelegt ist und während der Ausführung der Prozedur auf dem Verleger ein Fehler auftritt, kommt es auch auf dem Abonnenten zum selben Fehler, was wiederum zum Ausfall des Verteilungs-Agents führt. Durch Angeben von ON für XACT_ABORT wird sichergestellt, dass alle Fehler, zu denen es bei der Ausführung auf dem Verleger kommt, ein Rollback der gesamten Ausführung auslösen, sodass der Ausfall des Verteilungs-Agents vermieden wird. Weitere Informationen zum Festlegen von XACT_ABORT finden Sie unter [SET XACT_ABORT &#40;Transact-SQL&#41;](../../../t-sql/statements/set-xact-abort-transact-sql.md).  
  
 Wenn für XACT_ABORT OFF angegeben werden muss, geben Sie den **-SkipErrors** -Parameter für den Verteilungs-Agent an. Auf diese Weise kann der Agent auch dann die Änderungen auf den Abonnenten anwenden, wenn es zu einem Fehler kommt.  
  
## <a name="see-also"></a>Siehe auch  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
