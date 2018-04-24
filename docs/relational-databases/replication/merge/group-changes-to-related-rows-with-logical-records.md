---
title: Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ad76799c-4486-4b98-9705-005433041321
caps.latest.revision: 55
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c9fad4059dd0e027d521404ab55b889270f5126
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="group-changes-to-related-rows-with-logical-records"></a>Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Standardmäßig werden Datenänderungen beim Mergereplikationsprozess auf Zeilenbasis verarbeitet. In vielen Fällen ist das zweckmäßig, jedoch müssen bei einigen Anwendungen verknüpfte Zeilen als Einheit verarbeitet werden. Mit der Funktion logischer Datensätze der Mergereplikation können Sie eine Beziehung zwischen verknüpften Zeilen in verschiedenen Tabellen definieren, sodass Zeilen als Einheit verarbeitet werden.  
  
> [!NOTE]  
>  Logische Datensätze können allein oder in Verbindung mit Joinfiltern verwendet werden. Weitere Informationen zu Joinfiltern finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md). Zum Verwenden logischer Datensätze muss die Veröffentlichung mindestens einen Kompatibilitätsgrad von 90RTM aufweisen.  
  
 Nehmen Sie die folgenden drei verknüpften Tabellen als Beispiel:  
  
 ![Logischer Datensatz für drei Tabellen für nur Spaltennamen](../../../relational-databases/replication/merge/media/logical-records-01.gif "Three table logical record, with column names only")  
  
 Die **Customers** -Tabelle ist die übergeordnete Tabelle in dieser Beziehung und enthält eine **CustID**-Primärschlüsselspalte. Die **Orders** -Tabelle enthält eine **OrderID**-Primärschlüsselspalte sowie eine FOREIGN KEY-Einschränkung für die **CustID** -Spalte, die auf die **CustID** -Spalte in der **Customers** -Tabelle verweist. Dementsprechend enthält die **OrderItems** -Tabelle eine **OrderItemID**-Primärschlüsselspalte sowie eine FOREIGN KEY-Einschränkung für die **OrderID** -Spalte, die auf die **OrderID** -Spalte in der **Orders** -Tabelle verweist.  
  
 In diesem Beispiel besteht ein logischer Datensatz aus allen Zeilen in der **Orders** -Tabelle, die sich auf einen einzelnen **CustID** -Wert beziehen, und allen Zeilen der **OrderItems** -Tabelle, die sich auf jene Zeilen in der **Orders** -Tabelle beziehen. Das Diagramm zeigt alle Zeilen in den drei Tabellen, die im logischen Datensatz für Customer 2 enthalten sind:  
  
 ![Logischer Datensatz mit Werten für drei Tabellen](../../../relational-databases/replication/merge/media/logical-records-02.gif "Three table logical record with values")  
  
 Informationen zum Definieren einer logischen Datensatzbeziehung zwischen Artikeln finden Sie unter [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
## <a name="benefits-of-logical-records"></a>Vorteile logischer Datensätze  
 Logische Datensätze bieten zwei entscheidende Vorteile:  
  
-   Datenänderungen werden als Einheit angewendet.  
  
-   Gleichzeitige Erkennung und Lösung von Konflikten in mehreren Zeilen aus mehreren Tabellen.  
  
### <a name="the-application-of-changes-as-a-unit"></a>Anwendung von Änderungen als Einheit  
 Falls die Mergeverarbeitung unterbrochen wird, wie z. B. bei einer gelöschten Verbindung, wird bei Verwendung logischer Datensätze für die teilweise abgeschlossene Gruppe verknüpfter replizierter Änderungen ein Rollback ausgeführt. Beispiel: Ein Abonnent fügt einen neuen Auftrag mit **OrderID** = 6 und zwei neue Zeilen in der **OrderItems** -Tabelle mit **OrderItemID** = 10 und **OrderItemID** = 11 für **OrderID** = 6 hinzu.  
  
 ![Logischer Datensatz mit Werten für drei Tabellen](../../../relational-databases/replication/merge/media/logical-records-04.gif "Three table logical record with values")  
  
 Wenn der Replikationsprozess unterbrochen wird, nachdem die **Orders** -Zeile für **OrderID** = 6 abgeschlossen wurde, jedoch bevor die **OrderItems** 10 und 11 abgeschlossen wurden, ist der **OrderTotal** -Wert für **OrderID** = 6 ohne Verwendung logischer Datensätze nicht mit der Summe der **OrderAmount** -Werte für die **OrderItems** -Zeilen konsistent. Bei Verwendung logischer Datensätze wird für die **Orders** -Zeile für **OrderID** = 6 erst dann ein Commit ausgeführt, wenn die verknüpften **OrderItems** -Änderungen repliziert wurden.  
  
 Ein anderes Szenario bei der Verwendung logischer Datensätze wäre folgendes: Jemand fragt Datensätze ab, während Änderungen vom Mergeprozess angewendet werden. Der Benutzer sieht dann die teilweise replizierten Änderungen erst, wenn sie abgeschlossen sind. Beispiel: Die Orders-Zeile für **OrderID** = 6 wurde vom Replikationsprozess hochgeladen. Jedoch fragt ein Benutzer die Tabellen ab, bevor der Replikationsprozess die **OrderItems** -Zeilen repliziert hat. Der **OrderTotal** -Wert wäre nun nicht mit der Summe der **OrderAmount** -Werte identisch. Bei der Verwendung logischer Datensätze wäre die **Orders** -Zeile erst dann zu sehen, wenn die **OrderItems** -Zeilen abgeschlossen wurden und ein Commit für die Transaktion als Einheit ausgeführt wurde.  
  
### <a name="the-application-of-conflict-handling-to-more-than-one-table"></a>Anwendung der Konfliktbehandlung auf mehrere Tabellen  
 Nehmen Sie als Beispiel den Fall, dass zwei Abonnenten das obige Dataset verwenden:  
  
-   Ein Benutzer ändert auf dem ersten Abonnenten den **OrderAmount** -Wert von **OrderItemID** 5 von 100 auf 150 und den **OrderTotal** -Wert von **OrderID** 3 von 200 auf 250.  
  
-   Ein Benutzer ändert auf dem zweiten Abonnenten den **OrderAmount** -Wert von **OrderItemID** 6 von 25 auf 125 und den **OrderTotal** -Wert von **OrderID** 3 von 200 auf 300.  
  
 Würden diese Änderungen ohne Verwendung logischer Datensätze repliziert werden, ergäben die unterschiedlichen **OrderTotal** -Werte einen Konflikt, und nur einer der Werte würde repliziert. Die nicht in Konflikt stehenden Änderungen in der **OrderItems** -Tabelle würden problemlos repliziert. Das würde dazu führen, dass die endgültigen **OrderTotal** -Werte in Bezug auf die **OrderItems** -Zeilen inkonsistent wären. Werden logische Datensätze in diesem Szenario verwendet, würde auch für die Änderung von **OrderItems** , die mit der verlierenden Änderung der **Orders** -Tabelle verbunden ist, ein Rollback ausgeführt. Die endgültigen **OrderTotal** -Werte entsprächen dann einer genauen Zusammenfassung der **OrderItems** -Zeilen.  
  
 Weitere Informationen zur Konflikterkennung und -lösung bei logischen Datensätzen finden Sie unter [Ermitteln und Lösen von Konflikten in logischen Datensätzen](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
## <a name="considerations-for-using-logical-records"></a>Überlegungen zum Verwenden logischer Datensätze  
 Beachten Sie bei der Verwendung von logischen Datensätzen Folgendes:  
  
### <a name="general-considerations"></a>Allgemeine Überlegungen  
  
-   Halten Sie die Anzahl der Tabellen in einem logischen Datensatz so gering wie möglich: Empfohlen werden maximal fünf Tabellen.  
  
-   Logische Datensätze können nicht auf Spalten verweisen, die folgende Datentypen enthalten:  
  
    -   **varchar(max)** und **nvarchar(max)**  
  
    -   **varbinary(max)**  
  
    -   **text** und **ntext**  
  
    -   **image**  
  
    -   **XML**  
  
    -   **UDT**  
  
-   Fremdschlüsselbeziehungen in veröffentlichten Tabellen können nicht mit der Option CASCADE definiert werden. Weitere Informationen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql.md) und [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md).  
  
-   Sie können keine Spalten aktualisieren, die in der Klausel der logischen Beziehung verwendet werden.  
  
-   Eine benutzerdefinierte Konfliktlösung mit Geschäftslogikhandlern oder benutzerdefinierte Konfliktlöser werden nicht für Artikel unterstützt, die in einen logischen Datensatz eingeschlossen sind.  
  
-   Wenn logische Datensätze in einer Veröffentlichung verwendet werden, die parametrisierte Filter enthält, müssen Sie jeden Abonnenten mit einer Momentaufnahme für dessen Partition initialisieren. Falls Sie einen Abonnenten mit einer anderen Methode initialisieren, schlägt der Merge-Agent fehl. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
-   Konflikte, die logische Datensätze einschließen, werden im Konflikt-Viewer nicht angezeigt. Mit den gespeicherten Replikationsprozeduren können Informationen zu diesen Konflikten angezeigt werden. Weitere Informationen finden Sie unter [Anzeigen von Konfliktinformationen zu Mergeveröffentlichungen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
### <a name="publication-settings"></a>Veröffentlichungseinstellungen  
  
-   Die Veröffentlichung muss mindestens einen Kompatibilitätsgrad von 90RTM aufweisen. Weitere Informationen finden Sie im Abschnitt „Kompatibilitätsgrad von Veröffentlichungen“ [Abwärtskompatibilität von Replikationen](../../../relational-databases/replication/replication-backward-compatibility.md).  
  
-   Die Veröffentlichung muss den systemeigenen Momentaufnahmemodus verwenden. Dies ist die Standardeinstellung, es sei denn, Sie replizieren in [!INCLUDE[ssEW](../../../includes/ssew-md.md)]. Logische Datensätze werden von diesem Programm nicht unterstützt.  
  
-   Die Veröffentlichung kann eine Websynchronisierung nicht zulassen. Weitere Informationen zur Websynchronisierung finden Sie unter [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
-   Gehen Sie folgendermaßen vor, wenn Sie logische Datensätze für eine gefilterte Veröffentlichung verwenden möchten:  
  
    -   Vorausberechnete Partitionen müssen ebenfalls verwendet werden. Die Anforderungen für vorausberechnete Partitionen treffen auch auf logische Datensätze zu. Weitere Informationen finden Sie unter [Optimieren Parametrisierter Filter-Leistung mit Vorausberechneten Partitionen ](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
    -   Sie können keine nicht überlappenden parametrisierten Filter verwenden. Weitere Informationen finden Sie im Abschnitt zum Festlegen von Partitionsoptionen unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Wenn die Veröffentlichung Joinfilter verwendet, muss die **join unique key** -Eigenschaft für alle Joinfilter, die an Beziehungen logischer Datensätze beteiligt sind, auf **true** festgelegt werden. Weitere Informationen finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
### <a name="relationships-between-tables"></a>Beziehungen zwischen Tabellen  
  
-   Tabellen, die über logische Datensätze verknüpft sind, müssen Primärschlüssel/Fremdschlüssel-Beziehungen aufweisen.  
  
-   Die Option NOT FOR REPLICATION kann für FOREIGN KEY-Einschränkungen nicht festgelegt werden.  
  
-   Untergeordnete Tabellen können nur eine übergeordnete Tabelle aufweisen.  
  
     Eine Datenbank, in der z. B. Kurse und Studenten nachverfolgt werden, könnte folgendermaßen aufgebaut sein:  
  
     ![Untergeordnete Tabelle mit mehr als einer übergeordneten Tabelle](../../../relational-databases/replication/merge/media/logical-records-03.gif "Child table with more than one parent table")  
  
     Sie können keinen logischen Datensatz verwenden, der die drei Tabellen in dieser Beziehung darstellt, da die Zeilen in **ClassMembers** keiner einzelnen Primärschlüsselzeile zugewiesen sind. Die Tabellen **Classes** und **ClassMembers** könnten jedoch einen logischen Datensatz bilden, ebenso die Tabellen **ClassMembers** und **Students**, aber nicht alle drei zusammen.  
  
-   Die Veröffentlichung kann keine kreisförmigen Joinfilterbeziehungen enthalten.  
  
     Nehmen Sie das Beispiel **Customers**, **Orders**und **OrderItems**: Sie könnten keine logischen Datensätze verwenden, wenn die **Orders** -Tabelle auch eine FOREIGN KEY-Einschränkung aufweisen würde, die auf die **OrderItems** -Tabelle verweist.  
  
## <a name="performance-implications-of-logical-records"></a>Leistungseinschränkungen logischer Datensätze  
 Logische Datensätze wirken sich auf die Leistung aus. Ohne logische Datensätze kann der Replikations-Agent alle Änderungen für einen bestimmten Artikel gleichzeitig verarbeiten. Da die Änderungen zeilenweise erfolgen, bestehen außerdem nur minimale Sperr- und Transaktionsprotokollanforderungen für die Anwendung von Änderungen.  
  
 Werden logische Datensätzen verwendet, muss der Merge-Agent die Änderungen für jeden vollständigen logischen Datensatz auf einmal verarbeiten. Das wirkt sich auf die Dauer aus, die der Merge-Agent zum Replizieren der Zeilen benötigt. Darüber hinaus können sich die Sperranforderungen erhöhen, da der Agent eine separate Transaktion für jeden logischen Datensatz öffnet.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Artikeloptionen für die Mergereplikation](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
  
