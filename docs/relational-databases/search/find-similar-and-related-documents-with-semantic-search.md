---
title: "Suchen von &#228;hnlichen und verwandten Dokumenten mit semantischer Suche | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Semantische Suche [SQL Server], Dokumentähnlichkeitsabfragen"
ms.assetid: 9f527883-031b-442f-8e95-24bc0151ecbf
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Suchen von &#228;hnlichen und verwandten Dokumenten mit semantischer Suche
  Beschreibt, wie ähnliche oder verwandte Dokumente oder Textwerte sowie Informationen zur Ähnlichkeit oder Verwandtschaft über Spalten gesucht werden, die für die statistische semantische Indizierung konfiguriert sind.  
  
##  <a name="BasicsQuerySimilar"></a> Suchen von ähnlichen oder verwandten Dokumenten  
  
###  <a name="HowToQuerySimilar"></a> Vorgehensweise: Suchen von ähnlichen oder verwandten Dokumenten mit SEMANTICSIMILARITYTABLE  
 Fragen Sie zum Identifizieren ähnlicher oder verwandter Dokumente in einer bestimmten Spalte die Funktion [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md) ab.  
  
 **SEMANTICSIMILARITYTABLE** gibt eine Tabelle mit keiner Zeile, einer Zeile oder mehreren Zeilen zurück, deren Inhalt in der angegebenen Spalte dem angegebenen Dokument semantisch ähnelt. Auf diese Rowsetfunktion kann in der FROM-Klausel einer SELECT-Anweisung wie auf einen regulären Tabellennamen verwiesen werden.  
  
 Ähnliche Dokumente können nicht über Spalten hinweg abgefragt werden. Die **SEMANTICSIMILARITYTABLE**-Funktion ruft nur Ergebnisse aus derselben Spalte wie die Quellspalte ab, die durch das **source_key**-Argument identifiziert wird.  
  
 Ausführliche Informationen zu den für die **SEMANTICSIMILARITYTABLE**-Funktion erforderlichen Parametern und zu der von ihr zurückgegebenen Ergebnistabelle finden Sie unter [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md).  
  
> [!IMPORTANT]  
>  Für die Spalten, auf die Sie abzielen, muss die Volltext- und die semantische Indizierung aktiviert sein.  
  
###  <a name="HowToIdentifySimilar"></a> Beispiel: Suchen der wichtigsten Dokumente, die einem anderen Dokument ähnlich sind  
 Im folgenden Beispiel werden die ersten zehn Kandidaten abgerufen, die dem mit *@CandidateID* angegebenen Kandidaten aus der HumanResources.JobCandidate-Tabelle in der AdventureWorks2012-Beispieldatenbank ähneln.  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROM SEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
##  <a name="BasicsQuerySimilarity"></a> Suchen von Informationen zur Ähnlichkeit oder Verwandtschaft von Dokumenten  
  
###  <a name="HowToQuerySimilarity"></a> Vorgehensweise: Suchen von Informationen zur Ähnlichkeit oder Verwandtschaft von Dokumenten mit SEMANTICSIMILARITYDETAILSTABLE  
 Um weitere Informationen zu den Schlüsselausdrücken abzurufen, die bewirken, dass Dokumente ähnlich oder verwandt sind, können Sie die Funktion [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md) abfragen.  
  
 **SEMANTICSIMILARITYDETAILSTABLE** gibt eine Tabelle mit keiner, einer oder mehreren Zeilen von Schlüsselausdrücken zurück, die in zwei Dokumenten (einem Quelldokument und einem verglichenen Dokument) vorkommen, deren Inhalt semantisch ähnlich ist. Auf diese Rowsetfunktion kann in der FROM-Klausel einer SELECT-Anweisung wie auf einen regulären Tabellennamen verwiesen werden.  
  
 Ausführliche Informationen zu den für die **SEMANTICSIMILARITYDETAILSTABLE**-Funktion erforderlichen Parametern und zu der von ihr zurückgegebenen Ergebnistabelle finden Sie unter [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md).  
  
> [!IMPORTANT]  
>  Für die Spalten, auf die Sie abzielen, muss die Volltext- und die semantische Indizierung aktiviert sein.  
  
###  <a name="HowToSimilarPhrases"></a> Beispiel: Suchen der wichtigsten Schlüsselausdrücke, die zwischen Dokumenten ähnlich sind  
 Im folgenden Beispiel werden die fünf Schlüsselausdrücke mit der größten Ähnlichkeit zwischen den in der **HumanResources.JobCandidate** -Tabelle angegebenen Kandidaten der AdventureWorks2012-Beispieldatenbank abgerufen.  
  
```tsql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROM SEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
  