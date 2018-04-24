---
title: Veröffentlichen von Daten und Datenbankobjekten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- user-defined types [SQL Server replication]
- articles [SQL Server replication], dropping
- objects [SQL Server replication]
- publications [SQL Server replication], creating
- merge replication [SQL Server replication], publications
- schema-only articles [SQL Server replication]
- publishing [SQL Server replication], database objects
- articles [SQL Server replication], defining
- publishing [SQL Server replication], functions
- replication [SQL Server], publications
- publishing [SQL Server replication], views
- tables [SQL Server replication]
- schemas [SQL Server replication]
- publishing [SQL Server replication], data
- schemas [SQL Server replication], publishing
- articles [SQL Server replication], stored procedures and
- publishing [SQL Server replication], tables
- alias data types [SQL Server replication]
- publications [SQL Server replication], deleting
- snapshot replication [SQL Server], publications
- articles [SQL Server replication], modifying
- transactional replication, publications
- publishing [SQL Server replication], stored procedures
- publishing [SQL Server replication]
- views [SQL Server replication]
- stored procedures [SQL Server replication], publishing
- publications [SQL Server replication], schema options
- articles [SQL Server replication], adding
- publications [SQL Server replication], modifying
- user-defined functions [SQL Server replication]
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
caps.latest.revision: 83
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 615c392f7b34d775a9e1115d655819c13d75469b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="publish-data-and-database-objects"></a>Veröffentlichen von Daten und Datenbankobjekten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Wenn Sie eine Veröffentlichung erstellen möchten, können Sie die Tabellen und anderen Datenbankobjekte auswählen, die Sie veröffentlichen möchten. Mit einer Replikation können die folgenden Datenbankobjekte veröffentlicht werden:  
  
|Datenbankobjekt|Momentaufnahmereplikation und Transaktionsreplikation|Mergereplikation|  
|---------------------|--------------------------------------------------------|-----------------------|  
|Tabellen|X|X|  
|Partitionierte Tabellen|X|X|  
|Gespeicherte Prozeduren – Definition ([!INCLUDE[tsql](../../../includes/tsql-md.md)] und CLR)|X|X|  
|Gespeicherte Prozeduren – Ausführung ([!INCLUDE[tsql](../../../includes/tsql-md.md)] und CLR)|X|nein|  
|Sichten|X|X|  
|Indizierte Sichten|X|X|  
|Indizierte Sichten als Tabellen|X|nein|  
|Benutzerdefinierte Typen (CLR)|X|X|  
|Benutzerdefinierte Funktionen ([!INCLUDE[tsql](../../../includes/tsql-md.md)] und CLR)|X|X|  
|Aliasdatentypen|X|X|  
|Volltextindizes|X|X|  
|Schemaobjekte (Einschränkungen, Indizes, Benutzer-DML-Trigger, erweiterte Eigenschaften und Sortierung)|X|X|  
  
## <a name="creating-publications"></a>Erstellen von Veröffentlichungen  
 Beim Erstellen einer Veröffentlichung sind die folgenden Informationen bereitzustellen:  
  
-   Verteiler  
  
-   Speicherort der Momentaufnahmedateien  
  
-   Veröffentlichungsdatenbank  
  
-   Typ der zu erstellenden Veröffentlichung (Momentaufnahmeveröffentlichung, Transaktionsveröffentlichung, Transaktionsveröffentlichung mit aktualisierbaren Abonnements oder Mergeveröffentlichung)  
  
-   Daten und Datenbankobjekte (Artikel), die in die Veröffentlichung aufgenommen werden sollen  
  
-   statische Zeilenfilter und Spaltenfilter (alle Veröffentlichungstypen) sowie parametrisierte Zeilenfilter und Joinfilter (Mergeveröffentlichungen)  
  
-   Zeitplan für den Momentaufnahme-Agent  
  
-   Die Konten, unter denen die folgenden Agents ausgeführt werden: Momentaufnahme-Agent für alle Veröffentlichungen; Protokolllese-Agent für alle Transaktionsveröffentlichungen; Warteschlangenlese-Agent für Transaktionsveröffentlichungen mit aktualisierbaren Abonnements.  
  
-   Name und Beschreibung der Veröffentlichung.  
  
 Informationen zum Arbeiten mit Veröffentlichungen finden Sie in den folgenden Themen:  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [Anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [Löschen einer Veröffentlichung](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [Löschen eines Artikels](../../../relational-databases/replication/publish/delete-an-article.md)  
  
> [!NOTE]  
>  Beim Löschen eines Artikels oder einer Veröffentlichung werden die Objekte nicht vom Abonnenten entfernt.  
  
## <a name="publishing-tables"></a>Veröffentlichen von Tabellen  
 Tabellen sind die Objekte, die am häufigsten veröffentlicht werden. In den folgenden Themen finden Sie weiterführende Informationen zu Fragen im Zusammenhang mit dem Veröffentlichen von Tabellen:  
  
-   [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md)  
  
-   [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
-   [Article Options for Merge Replication](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
-   [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
 Beim Veröffentlichen einer Tabelle für die Replikation können Sie angeben, welche Schemaobjekte auf den Abonnenten kopiert werden sollen, z. B. deklarierte referenzielle Integrität (PRIMARY KEY-Einschränkungen, Referenzeinschränkungen, eindeutige Einschränkungen), Indizes, Benutzer-DML-Trigger (DDL-Trigger können nicht repliziert werden), erweiterte Eigenschaften und Sortierungen. Erweiterte Eigenschaften werden nur in der ersten Synchronisierung zwischen dem Verleger und dem Abonnenten repliziert. Wenn Sie eine erweiterte Eigenschaft nach der ersten Synchronisierung hinzufügen oder ändern, wird die Änderung nicht repliziert.  
  
 Informationen zum Angeben von Schemaoptionen finden Sie unter [Angeben von Schemaoptionen](../../../relational-databases/replication/publish/specify-schema-options.md) oder <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>.  
  
### <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes  
 Die Replikation unterstützt das Veröffentlichen von Tabellen und Indizes. Das Maß an Unterstützung hängt vom verwendeten Replikationstyp und den Optionen ab, die für die Veröffentlichung und die mit den partitionierten Tabellen verbundenen Artikel angegeben werden. Weitere Informationen finden Sie unter [Replicate Partitioned Tables and Indexes](../../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
## <a name="publishing-stored-procedures"></a>Veröffentlichen gespeicherter Prozeduren  
 Das Replizieren von Definitionen für gespeicherte Prozeduren ist bei allen Replikationstypen möglich: CREATE PROCEDURE wird auf jeden Abonnenten kopiert. Bei CLR-gespeicherten Prozeduren (Common Language Runtime) wird auch die zugehörige Assembly kopiert. Änderungen an den Prozeduren werden auf die Abonnenten repliziert, während Änderungen an den zugehörigen Assemblys nicht repliziert werden.  
  
 Bei der Transaktionsreplikation ist jedoch nicht nur die Definition einer gespeicherten Prozedur replizierbar, sondern Sie können auch die Ausführung der gespeicherten Prozeduren replizieren. Dies ist bei der Replikation der Ergebnisse von wartungsorientierten gespeicherten Prozeduren hilfreich, die sich möglicherweise auf große Datenmengen auswirken. Weitere Informationen finden Sie unter [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## <a name="publishing-views"></a>Veröffentlichen von Sichten  
 Das Replizieren von Sichten ist bei allen Replikationstypen möglich. Dabei kann die Sicht (und der zugehörige Index, sofern es sich um eine indizierte Sicht handelt) auf den Abonnenten kopiert werden, in jedem Fall muss aber auch die Basistabelle repliziert werden.  
  
 Bei indizierten Sichten ist es bei der Transaktionsreplikation auch möglich, die indizierte Sicht als Tabelle und nicht als Sicht zu replizieren. Dadurch entfällt die Notwendigkeit, die Basistabelle mit zu replizieren. Geben Sie dazu eine der "indexed view logbased"-Optionen für den *@type*-Parameter von [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) an. Weitere Informationen zum Verwenden von **sp_addarticle** finden Sie unter [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="publishing-user-defined-functions"></a>Veröffentlichen benutzerdefinierter Funktionen  
 Die CREATE FUNCTION-Anweisungen für CLR-Funktionen und [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Funktionen werden auf alle Abonnenten kopiert. Bei CLR-Funktionen wird auch die zugehörige Assembly kopiert. Änderungen an den Funktionen werden auf die Abonnenten repliziert, während Änderungen an den zugehörigen Assemblys nicht repliziert werden.  
  
## <a name="publishing-user-defined-types-and-alias-data-types"></a>Veröffentlichen von benutzerdefinierten Typen und Aliasdatentypen  
 Spalten, die benutzerdefinierte Typen oder Aliasdatentypen verwenden, werden genauso wie alle anderen Spalten auf die Abonnenten repliziert. Auf dem Abonnenten wird für jeden replizierten Typ die CREATE TYPE-Anweisung ausgeführt, bevor die Tabelle erstellt wird. Bei benutzerdefinierten Typen wird auch die zugehörige Assembly auf alle Abonnenten kopiert. Änderungen an benutzerdefinierten Typen oder Aliasdatentypen werden nicht auf die Abonnenten repliziert.  
  
 Wenn ein Typ in einer Datenbank definiert, beim Erstellen einer Veröffentlichung aber nicht in einer Spalte referenziert ist, wird der Typ nicht auf die Abonnenten kopiert. Wenn Sie später in der Datenbank eine Spalte dieses Typs erstellen und diesen Typ replizieren möchten, müssen Sie zunächst manuell den Typ (und bei benutzerdefiniertem Typ die zugehörige Assembly) auf alle Abonnenten kopieren.  
  
## <a name="publishing-full-text-indexes"></a>Veröffentlichen von Volltextindizes  
 Die CREATE FULLTEXT INDEX-Anweisung wird auf alle Abonnenten kopiert, und der Volltextindex wird auf dem Abonnenten erstellt. Änderungen an Volltextindizes, die mit ALTER FULLTEXT INDEX vorgenommen wurden, werden nicht repliziert.  
  
## <a name="making-schema-changes-to-published-objects"></a>Ausführen von Schemaänderungen an veröffentlichten Objekten  
 Die Replikation unterstützt eine breite Palette von Schemaänderungen an veröffentlichten Objekten. Bei den folgenden Schemaänderungen an veröffentlichten Objekten auf einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verleger werden die Änderungen standardmäßig an alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten weitergegeben:  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="considerations-for-publishing"></a>Überlegungen zum Veröffentlichen  
 Beachten Sie beim Veröffentlichen von Datenbankobjekten Folgendes:  
  
-   Die Benutzer können während der Erstellung der Veröffentlichung und der Anfangsmomentaufnahme weiter auf die Datenbank zugreifen. Es empfiehlt sich aber, für das Erstellen von Veröffentlichungen Zeiten mit geringerem Verkehrsaufkommen auf dem Verleger auszuwählen.  
  
-   Datenbanken können nicht mehr umbenannt werden, nachdem in ihnen eine Veröffentlichung erstellt wurde. Wenn eine solche Datenbank umbenannt werden soll, müssen Sie zunächst die Replikation aus der Datenbank entfernen.  
  
-   Wenn Sie ein Datenbankobjekt veröffentlichen, das von mindestens einem weiteren Datenbankobjekt abhängt, müssen Sie alle Objekte veröffentlichen, auf die verwiesen wird. Wenn Sie beispielsweise eine Sicht veröffentlichen, die von einer Tabelle abhängt, muss auch die Tabelle veröffentlicht werden.  
  
    > [!NOTE]  
    >  Wenn Sie einer Mergeveröffentlichung einen Artikel hinzufügen und ein vorhandener Artikel von diesem neuen Artikel abhängt, müssen Sie mithilfe des **@processing_order** -Parameter von [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) und [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Angenommen, Sie veröffentlichen eine Tabelle, aber Sie veröffentlichen keine Funktion, die auf die Tabelle verweist. Wenn Sie die Funktion nicht veröffentlichen, kann die Tabelle nicht auf dem Abonnenten erstellt werden. Wenn Sie die Funktion einer Veröffentlichung hinzufügen, geben Sie einen Wert von **1** für den **@processing_order** -Parameter von **sp_addmergearticle**an, und geben Sie einen Wert von **2** für den **@processing_order** -Parameter von **sp_changemergearticle**an. Geben Sie dann den Tabellennamen für den **@article**. Durch diese Verarbeitungsreihenfolge wird sichergestellt, dass Sie die Funktion auf dem Abonnenten vor der Tabelle erstellen, die davon abhängt. Sie können unterschiedliche Nummern für jeden Artikel verwenden, solange die Nummer für die Funktion niedriger ist als die Nummer für die Tabelle.  
  
-   Veröffentlichungsnamen dürfen die folgenden Zeichen nicht enthalten: % * [ ] | : " ? \ / < >.  
  
### <a name="limitations-on-publishing-objects"></a>Beschränkungen für das Veröffentlichen von Objekten  
  
-   Die maximale Anzahl von Artikeln und Spalten, die veröffentlicht werden können, ist je nach Veröffentlichungstyp unterschiedlich. Weitere Informationen finden Sie im Abschnitt „Replikationsobjekte“ [Spezifikationen der maximalen Kapazität für SQL Server](../../../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
-   Gespeicherte Prozeduren, Sichten, Trigger und benutzerdefinierte Funktionen, die mit WITH ENCRYPTION definiert wurden, können nicht als Teil der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikation veröffentlicht werden.  
  
-   Es ist möglich, XML-Schemaauflistungen zu replizieren, Änderungen werden aber nach der Anfangsmomentaufnahme nicht mehr repliziert.  
  
-   Für die Transaktionsreplikation veröffentlichte Tabellen müssen einen Primärschlüssel haben. Befindet sich eine Tabelle in einer Transaktionsreplikationsveröffentlichung, können die Indizes, die mit Primärschlüsselspalten verknüpft sind, nicht deaktiviert werden, weil diese Indizes von der Replikation benötigt werden. Wenn Sie einen Index deaktivieren möchten, müssen Sie zuerst die Tabelle aus der Veröffentlichung löschen.  
  
-   Mit [sp_bindefault &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) erstellte gebundene Standardwerte werden nicht repliziert (gebundene Standardwerte werden als veraltet markiert und stattdessen Standardwerte verwendet, die mit dem DEFAULT-Schlüsselwort von ALTER TABLE bzw. CREATE TABLE erstellt wurden).  
  
-   Funktionen, die den **NOEXPAND** -Hinweis für indizierte Sichten enthalten, können nicht in derselben Veröffentlichung wie die Tabellen, auf die verwiesen wird, und die indizierten Sichten veröffentlicht werden. Dies liegt an der Reihenfolge, in der sie vom Verteilungs-Agent übermittelt werden. Um dieses Problem zu umgehen, fügen Sie die Erstellung der Tabelle und indizierten Sichten in eine erste Veröffentlichung ein, während Sie Funktionen, die den **NOEXPAND** -Hinweis für die indizierten Sichten enthalten, einer zweiten Veröffentlichung hinzufügen, die Sie veröffentlichen, nachdem die erste Veröffentlichung abgeschlossen ist. Alternativ können Sie Skripts für diese Funktionen erstellen und mit dem *@post_snapshot_script* -Parameter von **sp_addpublication**.  
  
### <a name="schemas-and-object-ownership"></a>Schemas und Objektbesitz  
 Im Assistenten für neue Veröffentlichung weist die Replikation in Bezug auf Schemas und den Objektbesitz das folgende Standardverhalten auf:  
  
-   Für Artikel in Mergeveröffentlichungen mit einem Kompatibilitätsgrad von mindestens 90, Momentaufnahmeveröffentlichungen und Transaktionsveröffentlichungen gilt: Standardmäßig entspricht der Objektbesitzer auf dem Abonnenten dem Besitzer des entsprechenden Objekts auf dem Verleger. Wenn die Schemas, die Besitzer von Objekten sind, auf dem Abonnenten nicht vorhanden sind, werden sie automatisch erstellt.  
  
-   Für Artikel in Mergeveröffentlichungen mit einem Kompatibilitätsgrad von unter 90: Standardmäßig wird der Besitzer leer gelassen und während der Erstellung des Objekts auf dem Abonnenten mit **dbo** angeben.  
  
-   Für Artikel in Oracle-Veröffentlichungen: Standardmäßig wird der Besitzer mit **dbo**angegeben.  
  
-   Für Artikel in Veröffentlichungen, die Zeichenmodus-Momentaufnahmen verwenden (werden für Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten und [!INCLUDE[ssEW](../../../includes/ssew-md.md)] -Abonnenten verwendet): Standardmäßig wird der Besitzer leer gelassen. Als Besitzer wird standardmäßig der Besitzer verwendet, der mit dem vom Verteilungs- oder Merge-Agent zum Herstellen einer Verbindung mit dem Abonnenten verwendeten Konto verknüpft ist.  
  
 Der Objektbesitzer kann im Dialogfeld **Artikeleigenschaften\<***Artikel***>** und über folgende gespeicherte Prozeduren festgelegt werden: **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle** und **sp_changemergearticle**. Weitere Informationen finden Sie unter [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md) und [Anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
### <a name="publishing-data-to-subscribers-running-previous-versions-of-sql-server"></a>Veröffentlichen von Daten auf Abonnenten, auf denen eine frühere Version von SQL Server ausgeführt wird  
  
-   Wenn Sie Daten auf einem Abonnenten veröffentlichen, auf dem eine frühere Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ausgeführt wird, steht nur die Funktionalität dieser früheren Version zur Verfügung, und zwar sowohl hinsichtlich der replikationsspezifischen Funktionalität als auch der Funktionalität des Produkts als Ganzes.  
  
-   Bei Mergeveröffentlichungen richten sich die Funktionen, die in einer Veröffentlichung verwendet werden können, nach dem Kompatibilitätsgrad. Dank dieses Veröffentlichungstyps können auch Abonnenten unterstützt werden, auf denen eine frühere Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ausgeführt wird.  
  
### <a name="publishing-tables-in-more-than-one-publication"></a>Veröffentlichen von Tabellen in mehreren Veröffentlichungen  
 Die Replikation unterstützt das Veröffentlichen von Artikeln in mehreren Veröffentlichungen (darunter auch das erneute Veröffentlichen von Daten), wobei die folgenden Einschränkungen gelten:  
  
-   Wenn ein Artikel in einer Transaktionsveröffentlichung und in einer Mergeveröffentlichung veröffentlicht wird, müssen Sie sicherstellen, dass für den Mergeartikel für die *@published_in_tran_pub* -Eigenschaft TRUE festgelegt ist. Weitere Informationen über Einstellungseigenschaften finden Sie unter [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md) und [Anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
     Sie sollten außerdem die *@published_in_tran_pub* -Eigenschaft festlegen, wenn ein Artikel Bestandteil eines Transaktionsabonnements und in einer Mergeveröffentlichung enthalten ist. Beachten Sie in diesem Fall, dass bei der Transaktionsreplikation Tabellen auf dem Abonnenten standardmäßig als schreibgeschützt behandelt werden. Werden bei der Mergereplikation Datenänderungen an einer Tabelle in einem Transaktionsabonnement vorgenommen, kann es zu einer Nichtkonvergenz der Daten kommen. Um dies zu vermeiden, empfiehlt es sich, solche Tabellen in der Mergeveröffentlichung als "nur herunterladbar" zu kennzeichnen. Dadurch wird verhindert, dass ein Mergeabonnent Datenänderungen in die Tabelle hochlädt. Weitere Informationen finden Sie unter [Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Ein Artikel kann nicht gleichzeitig in einer Mergeveröffentlichung und in einer Transaktionsveröffentlichung mit Abonnements mit verzögertem Update über eine Warteschlange veröffentlicht werden.  
  
-   Artikel in Transaktionsveröffentlichungen, die Abonnements mit Update unterstützen, können nicht erneut veröffentlicht werden.  
  
-   Wenn ein Artikel in mehreren Transaktionsveröffentlichungen veröffentlicht wird, die Abonnements mit verzögertem Update über eine Warteschlage unterstützen, müssen die folgenden Eigenschaften für den Artikel in allen Veröffentlichungen denselben Wert aufweisen:  
  
    |Eigenschaft|Parameter in sp_addarticle|  
    |--------------|---------------------------------|  
    |Identitätsbereichsverwaltung|**@auto_identity_range** (als veraltet markiert) und **@identityrangemangementoption**|  
    |Identitätsbereich des Verlegers|**@pub_identity_range**|  
    |Identitätsbereich|**@identity_range**|  
    |Identitätsbereich-Schwellenwert|**@threshold**|  
  
     Weitere Informationen zu diesen Parametern finden Sie unter [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Wenn ein Artikel in mehreren Mergeveröffentlichungen veröffentlicht wird, müssen die folgenden Eigenschaften für den Artikel in allen Veröffentlichungen denselben Wert aufweisen:  
  
    |Eigenschaft|Parameter in sp_addmergearticle|  
    |--------------|--------------------------------------|  
    |Spaltennachverfolgung|**@column_tracking**|  
    |Schemaoptionen|**@schema_option**|  
    |Spaltenfilterung|**@vertical_partition**|  
    |Abonnentenuploadoptionen|**@subscriber_upload_options**|  
    |Bedingtes Nachverfolgen von Löschvorgängen|**@delete_tracking**|  
    |Fehlerkompensierung|**@compensate_for_errors**|  
    |Identitätsbereichsverwaltung|**@auto_identity_range** (als veraltet markiert) und **@identityrangemangementoption**|  
    |Identitätsbereich des Verlegers|**@pub_identity_range**|  
    |Identitätsbereich|**@identity_range**|  
    |Identitätsbereich-Schwellenwert|**@threshold**|  
    |Partitionsoptionen|**@partition_options**|  
    |BLOB-Spaltenstreaming|**@stream_blob_columns**|  
    |Filtertyp|**@filter_type** (Parameter in **sp_addmergefilter**)|  
  
     Weitere Informationen zu diesen Parametern finden Sie unter [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) und [sp_addmergefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md).  
  
-   Die Transaktionsreplikation und die ungefilterte Mergereplikation unterstützen das Veröffentlichen einer Tabelle in mehreren Veröffentlichungen und das anschließende Abonnieren innerhalb einer einzelnen Tabelle in der Abonnementdatenbank (üblicherweise als Rollupszenario bezeichnet). Rollup wird häufig zum Aggregieren von Teilsätzen von Daten aus mehreren Speicherorten in einer Tabelle auf einem zentralen Abonnenten verwendet. Gefilterte Mergeveröffentlichungen unterstützen das Szenario mit einem zentralen Abonnenten nicht. Bei der Mergereplikation wird das Rollup typischerweise über eine einzelne Veröffentlichung mit parametrisierten Zeilenfiltern implementiert. Weitere Informationen zu parametrisierten Zeilenfiltern finden Sie unter [Parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Verteilung konfigurieren](../../../relational-databases/replication/configure-distribution.md)   
 [Initialize a Subscription](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Skripterstellung für die Replikation](../../../relational-databases/replication/scripting-replication.md)   
 [Sichern des Verlegers](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
