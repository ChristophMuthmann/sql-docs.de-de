---
title: "Suchen von Schlüsselausdrücken in Dokumenten mit der semantischen Suche | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server], key phrase queries
ms.assetid: 6ee3676e-ed5d-43ec-aeca-1eed78967111
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe02dd662836bec41032e4715171c1b016590a81
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="find-key-phrases-in-documents-with-semantic-search"></a>Suchen von Schlüsselausdrücken in Dokumenten mit der semantischen Suche
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Beschreibt, wie Schlüsselausdrücke in Dokumenten oder Textspalten gesucht werden, die für die statistische semantische Indizierung konfiguriert sind.  

##  <a name="howtofind"></a> Suchen der Schlüsselausdrücke in Dokumenten mit SEMANTICKEYPHRASETABLE  
 Um die Schlüsselausdrücke in bestimmten Dokumenten bzw. Dokumente zu identifizieren, die bestimmte Schlüsselausdrücke enthalten, fragen Sie die Funktion [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md) ab.  
  
 SEMANTICKEYPHRASETABLE gibt eine Tabelle mit keiner, einer oder mehreren Zeilen für die Schlüsselausdrücke zurück, die in der angegebenen Tabelle Spalten zugeordnet sind. Auf diese Rowsetfunktion kann in der FROM-Klausel einer SELECT-Anweisung so verwiesen werden, als handelte es sich dabei um einen regulären Tabellennamen.  
  
> [!NOTE]  
>  In dieser Release werden nur einzelne Wörter für die semantische Suche in den Index aufgenommen. Multiwortausdrücke (ngrams) werden nicht indiziert. Auch werden verschiedene Formen des gleichen Wortes getrennt indiziert. Beispielsweise werden "Agent" und "Agents" getrennt indiziert.  
  
 Ausführliche Informationen zu den für die SEMANTICKEYPHRASETABLE-Funktion erforderlichen Parametern und zu der von ihr zurückgegebenen Ergebnistabelle finden Sie unter [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md).  
  
> [!IMPORTANT]  
>  Für die Spalten, auf die Sie abzielen, muss die Volltext- und die semantische Indizierung aktiviert sein.  
  
###  <a name="HowToTopPhrases"></a> Beispiel 1: Suchen der wichtigsten Schlüsselausdrücke in einem bestimmten Dokument  
 Im folgenden Beispiel werden die obersten 10 Schlüsselausdrücke aus dem von der @DocumentId-Variable in der Spalte "Dokument" der Production.Document-Tabelle der AdventureWorks-Beispieldatenbank angegebenen Dokument abgerufen. Die @DocumentId-Variable stellt einen Wert aus der Schlüsselspalte des Volltextindexes dar.  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
GO  
```  
  
 Die **SEMANTICKEYPHRASETABLE** -Funktion ruft diese Ergebnisse effizient mithilfe eines Indexsuchvorgangs anstelle eines Tabellenscans ab.  
  
###  <a name="HowToTopDocuments"></a> Example 2: Find the top documents that contain a specific key phrase  
 Im folgenden Beispiel werden die obersten 25 Dokumente mit dem Schlüsselausdruck "Klammer" in der Spalte "Dokument" der Production.Document-Tabelle der AdventureWorks-Beispieldatenbank abgerufen.  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
GO  
```  
  
  
