---
title: "Suchen von ähnlichen und verwandten Dokumenten mit semantischer Suche | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: semantic search [SQL Server], document similarity queries
ms.assetid: 9f527883-031b-442f-8e95-24bc0151ecbf
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 285d172878aff387efe15941fe2312779036af0a
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="find-similar-and-related-documents-with-semantic-search"></a>Suchen von ähnlichen und verwandten Dokumenten mit semantischer Suche
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Beschreibt, wie ähnliche oder verwandte Dokumente oder Textwerte sowie Informationen zur Ähnlichkeit oder Verwandtschaft über Spalten gesucht werden, die für die statistische semantische Indizierung konfiguriert sind.  
   
##  <a name="HowToQuerySimilar"></a> Suchen von ähnlichen oder verwandten Dokumenten mit SEMANTICSIMILARITYTABLE  
 Fragen Sie zum Identifizieren ähnlicher oder verwandter Dokumente in einer bestimmten Spalte die Funktion [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md) ab.  
  
 **SEMANTICSIMILARITYTABLE** gibt eine Tabelle mit keiner Zeile, einer Zeile oder mehreren Zeilen zurück, deren Inhalt in der angegebenen Spalte dem angegebenen Dokument semantisch ähnelt. Auf diese Rowsetfunktion kann in der FROM-Klausel einer SELECT-Anweisung wie auf einen regulären Tabellennamen verwiesen werden.  
  
 Ähnliche Dokumente können nicht über Spalten hinweg abgefragt werden. Die **SEMANTICSIMILARITYTABLE**-Funktion ruft nur Ergebnisse aus derselben Spalte wie die Quellspalte ab, die durch das **source_key**-Argument identifiziert wird.  
  
 Ausführliche Informationen zu den für die **SEMANTICSIMILARITYTABLE**-Funktion erforderlichen Parametern und zu der von ihr zurückgegebenen Ergebnistabelle finden Sie unter [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md).  
  
> [!IMPORTANT]  
>  Für die Spalten, auf die Sie abzielen, muss die Volltext- und die semantische Indizierung aktiviert sein.  
  
###  <a name="HowToIdentifySimilar"></a> Example: Find the top documents that are similar to another document  
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
  
##  <a name="HowToQuerySimilarity"></a> Suchen von Informationen zur Ähnlichkeit oder Verwandtschaft von Dokumenten mit SEMANTICSIMILARITYDETAILSTABLE  
 Um weitere Informationen zu den Schlüsselausdrücken abzurufen, die bewirken, dass Dokumente ähnlich oder verwandt sind, können Sie die Funktion [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md) abfragen.  
  
 **SEMANTICSIMILARITYDETAILSTABLE** gibt eine Tabelle mit keiner, einer oder mehreren Zeilen von Schlüsselausdrücken zurück, die in zwei Dokumenten (einem Quelldokument und einem verglichenen Dokument) vorkommen, deren Inhalt semantisch ähnlich ist. Auf diese Rowsetfunktion kann in der FROM-Klausel einer SELECT-Anweisung wie auf einen regulären Tabellennamen verwiesen werden.  
  
 Ausführliche Informationen zu den für die **SEMANTICSIMILARITYDETAILSTABLE**-Funktion erforderlichen Parametern und zu der von ihr zurückgegebenen Ergebnistabelle finden Sie unter [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md).  
  
> [!IMPORTANT]  
>  Für die Spalten, auf die Sie abzielen, muss die Volltext- und die semantische Indizierung aktiviert sein.  
  
###  <a name="HowToSimilarPhrases"></a> Example: Find the top key phrases that are similar between documents  
 Im folgenden Beispiel werden die fünf Schlüsselausdrücke mit der größten Ähnlichkeit zwischen den in der **HumanResources.JobCandidate** -Tabelle angegebenen Kandidaten der AdventureWorks2012-Beispieldatenbank abgerufen.  
  
```sql  
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
  
  
