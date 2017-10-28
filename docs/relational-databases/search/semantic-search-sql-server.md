---
title: Semantische Suche (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca60c4ada6bd908d5401784db74a9b8b0c93396b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="semantic-search-sql-server"></a>Semantische Suche (SQL Server)
Die statistische semantische Suche liefert einen tiefen Einblick in unstrukturierte Dokumente, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken gespeichert sind, indem statistisch relevante *Schlüsselausdrücke*extrahiert und indiziert werden. Anschließend werden diese Schlüsselausdrücke verwendet, um *ähnliche oder verwandte Dokumente* zu identifizieren und zu indizieren.  
  
##  <a name="whatcanido"></a> Was ist mit der semantischen Suche alles möglich?  
 Die semantische Suche basiert auf der vorhandenen Volltextsuchfunktion in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ermöglicht jedoch neue Szenarien, die über Schlüsselwortsuchen hinausgehen. Während Sie bei der Volltextsuche *Wörter* in einem Dokument abfragen können, können Sie bei der *semantischen* Suche die Bedeutung des Dokuments abfragen. Die jetzt möglichen Lösungen umfassen die automatische Tagextraktion, die Ermittlung von verwandten Inhalten sowie die hierarchische Navigation über ähnlichen Inhalt. Sie können beispielsweise den Index von Schlüsselausdrücken abfragen, um die Taxonomie für eine Organisation oder für einen Korpus von Dokumenten zu erstellen. Oder sie können den Dokumentähnlichkeitsindex abfragen, um Lebensläufe zu identifizieren, die einer Arbeitsplatzbeschreibung entsprechen.  
  
 In den folgenden Beispielen sind die Funktionen der semantischen Suche dargestellt. Gleichzeitig veranschaulichen diese Beispiele die drei Transact-SQL-Rowsetfunktionen, die Sie zum Abfragen der semantischen Indizes und zum Abrufen der Ergebnisse als strukturierte Daten verwenden.  
  
###  <a name="find1"></a> Find the key phrases in a document  
 Die folgende Abfrage ruft die Schlüsselausdrücke ab, die im Beispieldokument identifiziert wurden. Sie präsentiert die Ergebnisse in absteigender Reihenfolge nach dem Grad der statistischen Bedeutung der einzelnen Schlüsselausdrücke.
 
 Diese Abfrage ruft die Funktion [semantickeyphrasetable](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md) auf.  
  
```tsql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
###  <a name="find2"></a> Find similar or related documents  
 Die folgende Abfrage ruft die Dokumente ab, die als dem Beispieldokument ähnlich oder damit verwandt identifiziert wurden. Sie präsentiert die Ergebnisse in absteigender Reihenfolge nach dem Grad der Ähnlichkeit von zwei Dokumenten.
 
 Diese Abfrage ruft die Funktion [semanticsimilaritytable](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md) auf.  
  
```vb  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS SourceTitle, DocumentTitle AS MatchedTitle,  
        DocumentID, score  
    FROM SEMANTICSIMILARITYTABLE(Documents, *, @DocID)  
    INNER JOIN Documents ON DocumentID = matched_document_key  
    ORDER BY score DESC  
  
```  
  
###  <a name="find3"></a> Find the key phrases that make documents similar or related  
 Die folgende Abfrage ruft die Schlüsselausdrücke ab, die zwei Beispieldokumente ähnlich oder verwandt machen. Sie präsentiert die Ergebnisse in absteigender Reihenfolge nach dem Grad, der die Gewichtung der einzelnen Schlüsselausdrücke angibt.
 
 Diese Abfrage ruft die Funktion [semanticsimilaritydetailstable](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md) auf.  
  
```tsql  
SET @SourceTitle = 'first.docx'  
SET @MatchedTitle = 'second.docx'  
  
SELECT @SourceDocID = DocumentID FROM Documents WHERE DocumentTitle = @SourceTitle  
SELECT @MatchedDocID = DocumentID FROM Documents WHERE DocumentTitle = @MatchedTitle  
  
SELECT @SourceTitle AS SourceTitle, @MatchedTitle AS MatchedTitle, keyphrase, score  
    FROM semanticsimilaritydetailstable(Documents, DocumentContent,  
        @SourceDocID, DocumentContent, @MatchedDocID)  
    ORDER BY score DESC  
  
```  
  
##  <a name="store"></a> Speichern von Dokumenten in SQL Server  
 Bevor Sie Dokumente mit der semantischen Suche indizieren können, müssen Sie die Dokumente in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank speichern.  
  
 Die FileTable-Funktion in SQL Server macht unstrukturierte Dateien und Dokument zu so genannten „First Class Citizens“ (FCCs) der relationalen Datenbank. Folglich können Datenbankentwickler Dokumente zusammen mit strukturierten Daten in Transact-SQL-basierten Vorgängen bearbeiten.  
  
 Weitere Informationen zu der FileTable-Funktion finden Sie unter [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md). Informationen zur FILESTREAM-Funktion, die eine andere Option zum Speichern von Dokumenten in der Datenbank ist, finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
##  <a name="reltasks"></a> Related tasks  
 [Installieren und Konfigurieren der semantischen Suche](../../relational-databases/search/install-and-configure-semantic-search.md)  
 Beschreibt die erforderlichen Komponenten für die statistische semantische Suche und wie diese Komponenten installiert oder überprüft werden.  
  
 [Aktivieren der semantischen Suche in Tabellen und Spalten](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)  
 Beschreibt, wie die statistische semantische Indizierung für ausgewählte Spalten, die Dokumente oder Text enthalten, aktiviert bzw. deaktiviert wird.  
  
 [Suchen von Schlüsselausdrücken in Dokumenten mit der semantischen Suche](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)  
 Beschreibt, wie Schlüsselausdrücke in Dokumenten oder Textspalten gesucht werden, die für die statistische semantische Indizierung konfiguriert sind.  
  
 [Suchen von ähnlichen und verwandten Dokumenten mit semantischer Suche](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)  
 Beschreibt, wie ähnliche oder verwandte Dokumente oder Textwerte sowie Informationen zur Ähnlichkeit oder Verwandtschaft über Spalten gesucht werden, die für die statistische semantische Indizierung konfiguriert sind.  
  
 [Verwalten und Überwachen der semantischen Suche](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
 Beschreibt den Prozess der semantischen Indizierung sowie die Tasks im Zusammenhang mit der Überwachung und Verwaltung der Indizes.  
  
##  <a name="relcontent"></a> Related content  
 [Semantische Such-DDL, Funktionen, gespeicherte Prozeduren und Sichten](../../relational-databases/search/semantic-search-ddl-functions-stored-procedures-and-views.md)  
 Führt die zur Unterstützung der semantischen Suche hinzugefügten oder geänderten Transact-SQL-Anweisungen und SQL Server-Datenbankobjekte auf.  
  
  

