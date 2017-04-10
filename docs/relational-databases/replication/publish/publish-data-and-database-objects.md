---
title: "Ver&#246;ffentlichen von Daten und Datenbankobjekten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Benutzerdefinierte Typen [SQL Server-Replikation]"
  - "Artikel [SQL Server-Replikation], löschen"
  - "Objekte [SQL Server-Replikation]"
  - "Veröffentlichungen [SQL Server-Replikation], erstellen"
  - "Mergereplikation [SQL Server-Replikation], Veröffentlichungen"
  - "Artikel vom Typ schema only [SQL Server-Replikation]"
  - "Veröffentlichen [SQL Server-Replikation], Datenbankobjekte"
  - "Artikel [SQL Server-Replikation], definieren"
  - "Veröffentlichen [SQL Server-Replikation], Funktionen"
  - "Replikation [SQL Server], Veröffentlichungen"
  - "Veröffentlichen [SQL Server-Replikation], Ansichten"
  - "Tabellen [SQL Server-Replikation]"
  - "Schemas [SQL Server-Replikation]"
  - "Veröffentlichen [SQL Server-Replikation], Daten"
  - "Schemas [SQL Server-Replikation], veröffentlichen"
  - "Artikel [SQL Server-Replikation], gespeicherte Prozeduren und"
  - "Veröffentlichen [SQL Server-Replikation], Tabellen"
  - "Aliasdatentypen [SQL Server-Replikation]"
  - "Veröffentlichungen [SQL Server-Replikation], löschen"
  - "Momentaufnahmereplikation [SQL Server], Veröffentlichungen"
  - "Artikel [SQL Server-Replikation], ändern"
  - "Transaktionsreplikation, Veröffentlichungen"
  - "Veröffentlichen [SQL Server-Replikation], gespeicherte Prozeduren"
  - "Veröffentlichen [SQL Server-Replikation]"
  - "Sichten [SQL Server-Replikation]"
  - "Gespeicherte Prozeduren [SQL Server-Replikation], veröffentlichen"
  - "Veröffentlichungen [SQL Server-Replikation], Schemaoptionen"
  - "Artikel [SQL Server-Replikation], hinzufügen"
  - "Veröffentlichungen [SQL Server-Replikation], ändern"
  - "Benutzerdefinierte Funktionen [SQL Server-Replikation]"
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
caps.latest.revision: 83
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 83
---
# Ver&#246;ffentlichen von Daten und Datenbankobjekten
  Wenn Sie eine Veröffentlichung erstellen möchten, können Sie die Tabellen und anderen Datenbankobjekte auswählen, die Sie veröffentlichen möchten. Mit einer Replikation können die folgenden Datenbankobjekte veröffentlicht werden:  
  
|Datenbankobjekt|Momentaufnahmereplikation und Transaktionsreplikation|Mergereplikation|  
|---------------------|--------------------------------------------------------|-----------------------|  
|Tabellen|X|X|  
|Partitionierte Tabellen|X|X|  
|Gespeicherte Prozeduren – Definition ([!INCLUDE[tsql](../../../includes/tsql-md.md)] und CLR)|X|X|  
|Gespeicherte Prozeduren – Ausführung ([!INCLUDE[tsql](../../../includes/tsql-md.md)] und CLR)|X|Nein|  
|Sichten|X|X|  
|Indizierte Sichten|X|X|  
|Indizierte Sichten als Tabellen|X|Nein|  
|Benutzerdefinierte Typen (CLR)|X|X|  
|Benutzerdefinierte Funktionen ([!INCLUDE[tsql](../../../includes/tsql-md.md)] und CLR)|X|X|  
|Aliasdatentypen|X|X|  
|Volltextindizes|X|X|  
|Schemaobjekte (Einschränkungen, Indizes, Benutzer-DML-Trigger, erweiterte Eigenschaften und Sortierung)|X|X|  
  
## Erstellen von Veröffentlichungen  
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
  
-   [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [Anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [Löschen einer Veröffentlichung](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [Löschen eines Artikels](../../../relational-databases/replication/publish/delete-an-article.md)  
  
> [!NOTE]  
>  Beim Löschen eines Artikels oder einer Veröffentlichung werden die Objekte nicht vom Abonnenten entfernt.  
  
## Veröffentlichen von Tabellen  
 Tabellen sind die Objekte, die am häufigsten veröffentlicht werden. In den folgenden Themen finden Sie weiterführende Informationen zu Fragen im Zusammenhang mit dem Veröffentlichen von Tabellen:  
  
-   [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md)  
  
-   [Artikeloptionen für die Transaktionsreplikation](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
-   [Artikeloptionen für die Mergereplikation](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
-   [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
 Beim Veröffentlichen einer Tabelle für die Replikation können Sie angeben, welche Schemaobjekte auf den Abonnenten kopiert werden sollen, z. B. deklarierte referenzielle Integrität (PRIMARY KEY-Einschränkungen, Referenzeinschränkungen, eindeutige Einschränkungen), Indizes, Benutzer-DML-Trigger (DDL-Trigger können nicht repliziert werden), erweiterte Eigenschaften und Sortierungen. Erweiterte Eigenschaften werden nur in der ersten Synchronisierung zwischen dem Verleger und dem Abonnenten repliziert. Wenn Sie eine erweiterte Eigenschaft nach der ersten Synchronisierung hinzufügen oder ändern, wird die Änderung nicht repliziert.  
  
 Angeben von Schemaoptionen finden Sie unter [Schemaoptionen angeben](../../../relational-databases/replication/publish/specify-schema-options.md) oder <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>.  
  
### Partitionierte Tabellen und Indizes  
 Die Replikation unterstützt das Veröffentlichen von Tabellen und Indizes. Das Maß an Unterstützung hängt vom verwendeten Replikationstyp und den Optionen ab, die für die Veröffentlichung und die mit den partitionierten Tabellen verbundenen Artikel angegeben werden. Weitere Informationen finden Sie unter [replizieren partitionierter Tabellen und Indizes](../../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
## Veröffentlichen gespeicherter Prozeduren  
 Das Replizieren von Definitionen für gespeicherte Prozeduren ist bei allen Replikationstypen möglich: CREATE PROCEDURE wird auf jeden Abonnenten kopiert. Bei CLR-gespeicherten Prozeduren (Common Language Runtime) wird auch die zugehörige Assembly kopiert. Änderungen an den Prozeduren werden auf die Abonnenten repliziert, während Änderungen an den zugehörigen Assemblys nicht repliziert werden.  
  
 Bei der Transaktionsreplikation ist jedoch nicht nur die Definition einer gespeicherten Prozedur replizierbar, sondern Sie können auch die Ausführung der gespeicherten Prozeduren replizieren. Dies ist bei der Replikation der Ergebnisse von wartungsorientierten gespeicherten Prozeduren hilfreich, die sich möglicherweise auf große Datenmengen auswirken. Weitere Informationen finden Sie unter [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## Veröffentlichen von Sichten  
 Das Replizieren von Sichten ist bei allen Replikationstypen möglich. Dabei kann die Sicht (und der zugehörige Index, sofern es sich um eine indizierte Sicht handelt) auf den Abonnenten kopiert werden, in jedem Fall muss aber auch die Basistabelle repliziert werden.  
  
 Bei indizierten Sichten ist es bei der Transaktionsreplikation auch möglich, die indizierte Sicht als Tabelle und nicht als Sicht zu replizieren. Dadurch entfällt die Notwendigkeit, die Basistabelle mit zu replizieren. Geben Sie dazu eine der Optionen "indexed View Logbased" für die *@type* Parameter [Sp_addarticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Weitere Informationen zur Verwendung von **Sp_addarticle**, finden Sie unter [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Veröffentlichen benutzerdefinierter Funktionen  
 Die CREATE FUNCTION-Anweisungen für CLR-Funktionen und [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Funktionen werden auf alle Abonnenten kopiert. Bei CLR-Funktionen wird auch die zugehörige Assembly kopiert. Änderungen an den Funktionen werden auf die Abonnenten repliziert, während Änderungen an den zugehörigen Assemblys nicht repliziert werden.  
  
## Veröffentlichen von benutzerdefinierten Typen und Aliasdatentypen  
 Spalten, die benutzerdefinierte Typen oder Aliasdatentypen verwenden, werden genauso wie alle anderen Spalten auf die Abonnenten repliziert. Die TYPEstatement erstellen für jeden replizierten Typ wird auf dem Abonnenten ausgeführt, bevor die Tabelle erstellt wird. Bei benutzerdefinierten Typen wird auch die zugehörige Assembly auf alle Abonnenten kopiert. Änderungen an benutzerdefinierten Typen oder Aliasdatentypen werden nicht auf die Abonnenten repliziert.  
  
 Wenn ein Typ in einer Datenbank definiert, beim Erstellen einer Veröffentlichung aber nicht in einer Spalte referenziert ist, wird der Typ nicht auf die Abonnenten kopiert. Wenn Sie später in der Datenbank eine Spalte dieses Typs erstellen und diesen Typ replizieren möchten, müssen Sie zunächst manuell den Typ (und bei benutzerdefiniertem Typ die zugehörige Assembly) auf alle Abonnenten kopieren.  
  
## Veröffentlichen von Volltextindizes  
 Die CREATE FULLTEXT INDEX-Anweisung wird auf alle Abonnenten kopiert, und der Volltextindex wird auf dem Abonnenten erstellt. Änderungen an Volltextindizes, die mit ALTER FULLTEXT INDEX vorgenommen wurden, werden nicht repliziert.  
  
## Ausführen von Schemaänderungen an veröffentlichten Objekten  
 Die Replikation unterstützt eine breite Palette von Schemaänderungen an veröffentlichten Objekten. Bei den folgenden Schemaänderungen an veröffentlichten Objekten auf einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verleger werden die Änderungen standardmäßig an alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Abonnenten weitergegeben:  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Weitere Informationen finden Sie unter [vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## Überlegungen zum Veröffentlichen  
 Beachten Sie beim Veröffentlichen von Datenbankobjekten Folgendes:  
  
-   Die Benutzer können während der Erstellung der Veröffentlichung und der Anfangsmomentaufnahme weiter auf die Datenbank zugreifen. Es empfiehlt sich aber, für das Erstellen von Veröffentlichungen Zeiten mit geringerem Verkehrsaufkommen auf dem Verleger auszuwählen.  
  
-   Datenbanken können nicht mehr umbenannt werden, nachdem in ihnen eine Veröffentlichung erstellt wurde. Wenn eine solche Datenbank umbenannt werden soll, müssen Sie zunächst die Replikation aus der Datenbank entfernen.  
  
-   Wenn Sie ein Datenbankobjekt veröffentlichen, das von mindestens einem weiteren Datenbankobjekt abhängt, müssen Sie alle Objekte veröffentlichen, auf die verwiesen wird. Wenn Sie beispielsweise eine Sicht veröffentlichen, die von einer Tabelle abhängt, muss auch die Tabelle veröffentlicht werden.  
  
    > [!NOTE]  
    >  Wenn Sie eine Mergepublikation einen Artikel hinzufügen und ein vorhandener Artikel, die die neuen Artikel abhängt, müssen Sie angeben, dass eine Verarbeitungsreihenfolge für beide Artikel mithilfe der **@processing_order** Parameter [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) und [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Angenommen, Sie veröffentlichen eine Tabelle, aber Sie veröffentlichen keine Funktion, die auf die Tabelle verweist. Wenn Sie die Funktion nicht veröffentlichen, kann die Tabelle nicht auf dem Abonnenten erstellt werden. Beim Hinzufügen der Funktion für die Veröffentlichung: Geben Sie den Wert **1** für die **@processing_order** Parameter **Sp_addmergearticle**; und geben Sie den Wert **2** für die **@processing_order** Parameter **Sp_changemergearticle**, geben Sie den Tabellennamen für den Parameter **@article**. Durch diese Verarbeitungsreihenfolge wird sichergestellt, dass Sie die Funktion auf dem Abonnenten vor der Tabelle erstellen, die davon abhängt. Sie können unterschiedliche Nummern für jeden Artikel verwenden, solange die Nummer für die Funktion niedriger ist als die Nummer für die Tabelle.  
  
-   Veröffentlichungsnamen dürfen die folgenden Zeichen nicht enthalten: % * [ ] | : " ? \ / \< >.  
  
### Beschränkungen für das Veröffentlichen von Objekten  
  
-   Die maximale Anzahl von Artikeln und Spalten, die veröffentlicht werden können, ist je nach Veröffentlichungstyp unterschiedlich. Weitere Informationen finden Sie im Abschnitt "Replikationsobjekte" [Spezifikationen der maximalen Kapazität für SQL Server](../../../sql-server/maximum-capacity-specifications-for-sql-server.md).  
  
-   Gespeicherte Prozeduren, Sichten, Trigger und benutzerdefinierte Funktionen, die mit WITH ENCRYPTION definiert wurden, können nicht als Teil der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Replikation veröffentlicht werden.  
  
-   Es ist möglich, XML-Schemaauflistungen zu replizieren, Änderungen werden aber nach der Anfangsmomentaufnahme nicht mehr repliziert.  
  
-   Für die Transaktionsreplikation veröffentlichte Tabellen müssen einen Primärschlüssel haben. Befindet sich eine Tabelle in einer Transaktionsreplikationsveröffentlichung, können die Indizes, die mit Primärschlüsselspalten verknüpft sind, nicht deaktiviert werden, weil diese Indizes von der Replikation benötigt werden. Wenn Sie einen Index deaktivieren möchten, müssen Sie zuerst die Tabelle aus der Veröffentlichung löschen.  
  
-   Mit erstellte gebundene Standardwerte [Sp_bindefault & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) werden nicht repliziert (gebundene Standardwerte werden als veraltet markiert und stattdessen Standardwerte verwendet, die mit dem DEFAULT-Schlüsselwort von ALTER TABLE oder CREATE TABLE erstellt).  
  
-   Funktionen, die die **NOEXPAND** -Hinweis für indizierte Sichten nicht in der Reihenfolge, in der der Verteilungs-Agent werden übermittelt, bald in derselben Veröffentlichung wie die referenzierten Tabellen und indizierten Sichten veröffentlicht werden. Um dieses Problem zu umgehen, fügen Sie der Tabelle und die Erstellung von indizierten Sichten in eine erste Veröffentlichung, und Hinzufügen von Funktionen, die die **NOEXPAND** Hinweis für die indizierten Sichten, einer zweiten Veröffentlichung, die Sie, nachdem die erste Veröffentlichung veröffentlichen abgeschlossen ist. Oder, Skripts für diese Funktionen erstellen und übermitteln Sie das Skript mithilfe der *@post_snapshot_script* Parameter **Sp_addpublication**.  
  
### Schemas und Objektbesitz  
 Im Assistenten für neue Veröffentlichung weist die Replikation in Bezug auf Schemas und den Objektbesitz das folgende Standardverhalten auf:  
  
-   Für Artikel in Mergeveröffentlichungen mit einem Kompatibilitätsgrad von mindestens 90, Momentaufnahmeveröffentlichungen und Transaktionsveröffentlichungen gilt: Standardmäßig entspricht der Objektbesitzer auf dem Abonnenten dem Besitzer des entsprechenden Objekts auf dem Verleger. Wenn die Schemas, die Besitzer von Objekten sind, auf dem Abonnenten nicht vorhanden sind, werden sie automatisch erstellt.  
  
-   Für Artikel in Mergeveröffentlichungen mit einem Kompatibilitätsgrad von unter 90: Standardmäßig wird der Besitzer leer gelassen und während der Erstellung des Objekts auf dem Abonnenten mit **dbo** angeben.  
  
-   Für Artikel in Oracle-Veröffentlichungen: Standardmäßig wird der Besitzer mit **dbo**angegeben.  
  
-   Für Artikel in Veröffentlichungen, die Zeichenmodus-Momentaufnahmen verwenden (werden für Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Abonnenten und [!INCLUDE[ssEW](../../../includes/ssew-md.md)]-Abonnenten verwendet): Standardmäßig wird der Besitzer leer gelassen. Als Besitzer wird standardmäßig der Besitzer verwendet, der mit dem vom Verteilungs- oder Merge-Agent zum Herstellen einer Verbindung mit dem Abonnenten verwendeten Konto verknüpft ist.  
  
 Der Besitzer des Objekts geändert werden kann, über die **Artikeleigenschaften - \<***Artikel***>** Dialogfeld und über die folgenden gespeicherten Prozeduren: **Sp_addarticle**, **Sp_addmergearticle**, **Sp_changearticle**, und **Sp_changemergearticle**. Weitere Informationen finden Sie unter [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md), und [anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
### Veröffentlichen von Daten auf Abonnenten, auf denen eine frühere Version von SQL Server ausgeführt wird  
  
-   Wenn Sie Daten auf einem Abonnenten veröffentlichen, auf dem eine frühere Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt wird, steht nur die Funktionalität dieser früheren Version zur Verfügung, und zwar sowohl hinsichtlich der replikationsspezifischen Funktionalität als auch der Funktionalität des Produkts als Ganzes.  
  
-   Bei Mergeveröffentlichungen richten sich die Funktionen, die in einer Veröffentlichung verwendet werden können, nach dem Kompatibilitätsgrad. Dank dieses Veröffentlichungstyps können auch Abonnenten unterstützt werden, auf denen eine frühere Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt wird.  
  
### Veröffentlichen von Tabellen in mehreren Veröffentlichungen  
 Die Replikation unterstützt das Veröffentlichen von Artikeln in mehreren Veröffentlichungen (darunter auch das erneute Veröffentlichen von Daten), wobei die folgenden Einschränkungen gelten:  
  
-   Wenn ein Artikel in einer Transaktionspublikation und einer Mergeveröffentlichung veröffentlicht wird, stellen Sie sicher, dass die *@published_in_tran_pub* Eigenschaft auf TRUE festgelegt ist, für den Mergeartikel. Weitere Informationen zum Festlegen von Eigenschaften finden Sie unter [anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md) und [anzeigen und Ändern von Artikeleigenschaften](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
     Sie sollten auch festlegen, die *@published_in_tran_pub* -Eigenschaft, wenn ein Artikel Bestandteil eines Transaktionsabonnements und in einer Mergeveröffentlichung enthalten ist. Beachten Sie in diesem Fall, dass bei der Transaktionsreplikation Tabellen auf dem Abonnenten standardmäßig als schreibgeschützt behandelt werden. Werden bei der Mergereplikation Datenänderungen an einer Tabelle in einem Transaktionsabonnement vorgenommen, kann es zu einer Nichtkonvergenz der Daten kommen. Um dies zu vermeiden, empfiehlt es sich, solche Tabellen in der Mergeveröffentlichung als "nur herunterladbar" zu kennzeichnen. Dadurch wird verhindert, dass ein Mergeabonnent Datenänderungen in die Tabelle hochlädt. Weitere Informationen finden Sie unter [Merge Replikationsleistung mit Download-Only Artikeln optimieren](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Ein Artikel kann nicht gleichzeitig in einer Mergeveröffentlichung und in einer Transaktionsveröffentlichung mit Abonnements mit verzögertem Update über eine Warteschlange veröffentlicht werden.  
  
-   Artikel in Transaktionsveröffentlichungen, die Abonnements mit Update unterstützen, können nicht erneut veröffentlicht werden.  
  
-   Wenn ein Artikel in mehreren Transaktionsveröffentlichungen veröffentlicht wird, die Abonnements mit verzögertem Update über eine Warteschlage unterstützen, müssen die folgenden Eigenschaften für den Artikel in allen Veröffentlichungen denselben Wert aufweisen:  
  
    |Eigenschaft|Parameter in sp_addarticle|  
    |--------------|---------------------------------|  
    |Identitätsbereichsverwaltung|**@auto_identity_range** (veraltet) und **@identityrangemangementoption**|  
    |Identitätsbereich des Verlegers|**@pub_identity_range**|  
    |Identitätsbereich|**@identity_range**|  
    |Identitätsbereich-Schwellenwert|**@threshold**|  
  
     Weitere Informationen zu diesen Parametern finden Sie unter [Sp_addarticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Wenn ein Artikel in mehreren Mergeveröffentlichungen veröffentlicht wird, müssen die folgenden Eigenschaften für den Artikel in allen Veröffentlichungen denselben Wert aufweisen:  
  
    |Eigenschaft|Parameter in sp_addmergearticle|  
    |--------------|--------------------------------------|  
    |Spaltennachverfolgung|**@column_tracking**|  
    |Schemaoptionen|**@schema_option**|  
    |Spaltenfilterung|**@vertical_partition**|  
    |Abonnentenuploadoptionen|**@subscriber_upload_options**|  
    |Bedingtes Nachverfolgen von Löschvorgängen|**@delete_tracking**|  
    |Fehlerkompensierung|**@compensate_for_errors**|  
    |Identitätsbereichsverwaltung|**@auto_identity_range** (veraltet) und **@identityrangemangementoption**|  
    |Identitätsbereich des Verlegers|**@pub_identity_range**|  
    |Identitätsbereich|**@identity_range**|  
    |Identitätsbereich-Schwellenwert|**@threshold**|  
    |Partitionsoptionen|**@partition_options**|  
    |BLOB-Spaltenstreaming|**@stream_blob_columns**|  
    |Filtertyp|**@filter_type** (Parameter in **Sp_addmergefilter**)|  
  
     Weitere Informationen zu diesen Parametern finden Sie unter [Sp_addmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) und [Sp_addmergefilter & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md).  
  
-   Die Transaktionsreplikation und die ungefilterte Mergereplikation unterstützen das Veröffentlichen einer Tabelle in mehreren Veröffentlichungen und das anschließende Abonnieren innerhalb einer einzelnen Tabelle in der Abonnementdatenbank (üblicherweise als Rollupszenario bezeichnet). Rollup wird häufig zum Aggregieren von Teilsätzen von Daten aus mehreren Speicherorten in einer Tabelle auf einem zentralen Abonnenten verwendet. Gefilterte Mergeveröffentlichungen unterstützen das Szenario mit einem zentralen Abonnenten nicht. Bei der Mergereplikation wird das Rollup typischerweise über eine einzelne Veröffentlichung mit parametrisierten Zeilenfiltern implementiert. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
## Siehe auch  
 [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Konfigurieren der Verteilung](../../../relational-databases/replication/configure-distribution.md)   
 [Initialisieren eines Abonnements](../../../relational-databases/replication/initialize-a-subscription.md)   
 [Erstellen von Skripts für die Replikation](../../../relational-databases/replication/scripting-replication.md)   
 [Sichern des Verlegers](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  