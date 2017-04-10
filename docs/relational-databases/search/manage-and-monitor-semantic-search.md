---
title: "Verwalten und &#220;berwachen der semantischen Suche | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Semantische Suche [SQL Server], verwalten"
  - "Semantische Suche [SQL Server], überwachen"
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Verwalten und &#220;berwachen der semantischen Suche
  In diesem Thema werden der Prozess der semantischen Indizierung sowie die Tasks im Zusammenhang mit der Verwaltung und Überwachung der Indizes beschrieben.  
  
##  <a name="HowToMonitorStatus"></a> Vorgehensweise: Überprüfen des Status der semantischen Indizierung  
 **Ist die erste Phase der semantischen Indizierung abgeschlossen?**  
 Fragen Sie die dynamische Verwaltungssicht ab, [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md), und überprüfen Sie die **status**- und **status_description**-Spalten.  
  
 Die erste Phase der Indizierung umfasst die Auffüllung des Volltextschlüsselwortindexes und des semantischen Schlüsselausdruckindexes sowie die Extraktion der Dokumentähnlichkeitsdaten.  
  
```tsql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
 **Ist die zweite Phase der semantischen Indizierung abgeschlossen?**  
 Fragen Sie die dynamische Verwaltungssicht ab, [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md), und überprüfen Sie die **status**- und **status_description**-Spalten.  
  
 Die zweite Phase der Indizierung umfasst die Auffüllung des semantischen Dokumentähnlichkeitsindexes.  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a> Vorgehensweise: Überprüfen der Größe der semantischen Indizes  
 **Was ist die logische Größe eines semantischen Schlüsselausdruckindexes oder eines semantischen Dokumentähnlichkeitsindexes?**  
 Fragen Sie die dynamische Verwaltungssicht ab, [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md).  
  
 Die logische Größe wird in Anzahl von Indexseiten angezeigt.  
  
```tsql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
 **Wie groß sind die Volltext- und die semantischen Indizes für einen Volltextkatalog insgesamt?**  
 Fragen Sie die Eigenschaft **IndexSize** der Metadatenfunktion [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md) ab.  
  
```tsql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
 **Wie viele Elemente werden in den Volltext- und den semantischen Indizes für einen Volltextkatalog indiziert?**  
 Fragen Sie die Eigenschaft **ItemCount** der Metadatenfunktion [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md) ab.  
  
```tsql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a> Vorgehensweise: Erzwingen der Auffüllung der semantischen Indizes  
 Sie können die Auffüllung der Volltextindizes und semantischen Indizes mit der START/STOP/PAUSE-Klausel oder der RESUME POPULATION-Klausel mit der gleichen Syntax und dem für Volltextindizes beschriebenen Verhalten erzwingen. Weitere Informationen finden Sie unter [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md) und [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
 Da die semantische Indizierung von der Volltextindizierung abhängig ist, werden semantische Indizes nur dann aufgefüllt, wenn die zugeordneten Volltextindizes aufgefüllt werden.  
  
 **Beispiel: Starten einer vollständigen Auffüllung von Volltext- und semantischen Indizes**  
  
 Im folgenden Beispiel wird die vollständige Auffüllung von sowohl Volltext- als auch semantischen Indizes gestartet, indem ein vorhandener Volltextindex in der **Production.Document**-Tabelle in der AdventureWorks2012-Beispieldatenbank geändert wird.  
  
```vb  
USE AdventureWorks2012  
GO  
  
ALTER FULLTEXT INDEX ON Production.Document  
    START FULL POPULATION  
GO  
```  
  
##  <a name="HowToDisableIndexing"></a> Vorgehensweise: Deaktivieren oder erneutes Aktivieren der semantischen Indizierung  
 Sie können die Volltextindizierung oder semantische Indizierung mit der ENABLE/DISABLE-Klausel mit der gleichen Syntax und dem für Volltextindizes beschriebenen Verhalten deaktivieren. Weitere Informationen finden Sie unter [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
 Wenn die semantische Indizierung deaktiviert und angehalten wurde, funktionieren Abfragen über semantische Daten weiterhin und geben zuvor indizierte Daten zurück. Dieses Verhalten ist nicht konsistent mit dem Verhalten der Volltextsuche.  
  
```tsql  
-- To disable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name DISABLE  
GO  
  
-- To re-enable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name ENABLE  
GO  
```  
  
##  <a name="SemanticIndexing"></a> Phasen der semantischen Indizierung  
 Bei der semantischen Suche werden zwei Arten von Daten für jede Spalte indiziert, für die sie aktiviert wurde:  
  
1.  **Schlüsselausdrücke**  
  
2.  **Dokumentähnlichkeit**  
  
 Die semantische Indizierung erfolgt in zwei Phase, in Verbindung mit der Volltextindizierung:  
  
1.  **Phase 1**. Der Volltextschlüsselwortindex und der semantische Schlüsselausdruckindex werden zur gleichen Zeit parallel aufgefüllt. Die zur Indizierung der Dokumentähnlichkeit erforderlichen Daten werden ebenfalls zu diesem Zeitpunkt extrahiert.  
  
2.  **Phase 2**. Anschließend wird der semantische Dokumentähnlichkeitsindex aufgefüllt. Dieser Index ist von beiden Indizes abhängig, die in der vorherigen Phase aufgefüllt wurden.  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a> Problem: Semantische Indizes werden nicht aufgefüllt  
 **Werden die zugeordneten Volltextindizes aufgefüllt?**  
 Da die semantische Indizierung von der Volltextindizierung abhängig ist, werden semantische Indizes nur dann aufgefüllt, wenn die zugeordneten Volltextindizes aufgefüllt werden.  
  
 **Sind die Volltextsuche und die semantische Suche ordnungsgemäß installiert und konfiguriert?**  
 Weitere Informationen finden Sie unter [Installieren und Konfigurieren der semantischen Suche](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
 **Ist der FDHOST-Dienst nicht verfügbar, oder gibt es eine andere Bedingung, aufgrund der die Volltextindizierung fehlschlagen würde?**  
 Weitere Informationen finden Sie unter [Behandeln von Problemen mit der Volltextindizierung](../../relational-databases/search/troubleshoot-full-text-indexing.md).  
  
  