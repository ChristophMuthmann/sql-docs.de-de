---
title: Semanticsimilaritytable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- semanticsimilaritytable
- semanticsimilaritytable_TSQL
dev_langs: TSQL
helpviewer_keywords: semanticsimilaritytable function
ms.assetid: b49d40ab-7552-438b-ad67-6237dcccb75b
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2944708e70d9cc71cddcad33ff060df8a223530d
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="semanticsimilaritytable-transact-sql"></a>semanticsimilaritytable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Tabelle mit keiner, einer oder mehreren Zeilen für Dokumente zurück, deren Inhalt  in den angegebenen Spalten einem angegebenen Dokument semantisch ähnlich ist.  
  
 Auf diese Rowsetfunktion kann in der FROM-Klausel einer SELECT-Anweisung wie auf einen regulären Tabellennamen verwiesen werden.  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
SEMANTICSIMILARITYTABLE  
    (  
    table,  
    { column | (column_list) | * },  
    source_key  
    )  
```  
  
##  <a name="Arguments"></a> Argumente  
 **table**  
 Ist der Name einer Tabelle, für die die Volltext- und die semantische Indizierung aktiviert ist.  
  
 Dieser Name kann einteilig sein oder aus bis zu vier Teilen bestehen, aber ein Remoteservername ist nicht zugelassen.  
  
 **column**  
 Name der indizierten Spalte, für die Ergebnisse zurückgegeben werden sollen. Für die Spalte muss die semantische Indizierung aktiviert sein.  
  
 **column_list**  
 Gibt mehrere durch Trennzeichen getrennte Spalten an, die in Klammern eingeschlossen sind. Für alle Spalten muss die semantische Indizierung aktiviert sein.  
  
 **\***  
 Gibt an, dass alle Spalten eingeschlossen werden, für die die semantische Indizierung aktiviert ist.  
  
 **source_key**  
 Eindeutiger Schlüssel für die Zeile, um Ergebnisse für eine bestimmte Zeile anzufordern.  
  
 Der Schlüssel wird in den Typ des eindeutigen Schlüssels in der Quelltabelle möglichst Volltext-implizit konvertiert. Der Schlüssel kann als Konstante oder Variable angegeben werden. Er kann jedoch kein Ausdruck oder das Ergebnis einer skalaren Unterabfrage sein.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
 Die folgende Tabelle enthält Informationen zu ähnlichen oder verwandten Dokumenten, die diese Rowsetfunktion zurückgibt.  
  
 Passende Dokumente werden auf der Basis einzelner Spalten zurückgegeben, wenn Ergebnisse aus mehr als einer Spalte angefordert werden.  
  
|Column_name|Typ|Description|  
|------------------|----------|-----------------|  
|**source_column_id**|**int**|ID der Spalte, aus der ein Quelldokument zum Suchen von ähnlichen Dokumenten verwendet wurde.<br /><br /> Im Abschnitt über die COL_NAME-Funktion und COLUMNPROPERTY-Funktion finden Sie ausführliche Informationen zum Abrufen des Spaltennamens aus "column_id" und umgekehrt.|  
|**matched_column_id**|**int**|ID der Spalte, in der ein ähnliches Dokument gefunden wurde.<br /><br /> Im Abschnitt über die COL_NAME-Funktion und COLUMNPROPERTY-Funktion finden Sie ausführliche Informationen zum Abrufen des Spaltennamens aus "column_id" und umgekehrt.|  
|**matched_document_key**|**\***<br /><br /> Dieser Schlüssel stimmt mit dem Typ des eindeutigen Schlüssels in der Quelltabelle überein.|Eindeutiger Schlüsselwert für die Volltext- und semantische Extraktion des Dokuments oder der Zeile, das bzw. die Ähnlichkeit mit dem angegebenen Dokument in der Abfrage aufweist.|  
|**Bewertung**|**ECHTE**|Ein relativer Ähnlichkeitswert für dieses Dokument bezogen auf alle anderen ähnlichen Dokumente.<br /><br /> Der Wert ist eine Dezimalzahl im Bereich [0,0; 1,0], wobei ein höheres Ergebnis eine höhere Übereinstimmung und 1,0 ein perfektes Ergebnis darstellt.|  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Weitere Informationen finden Sie unter [Suchen von ähnlichen und verwandten Dokumenten mit Semantischer Suche](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Ähnliche Dokumente können nicht über Spalten hinweg abgefragt werden. Die **SEMANTICSIMILARITYTABLE** -Funktion ruft nur ähnliche Dokumente aus derselben Spalte wie die Quellspalte, die identifizierte ab der **Source_key** Argument.  
  
## <a name="metadata"></a>Metadaten  
 Führen Sie eine Abfrage der folgenden dynamischen Verwaltungssichten durch, um Informationen, einschließlich Statusinformationen, zur semantischen Ähnlichkeitsextraktion und Auffüllung zu erhalten:  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigungen für die Basistabelle, für die der Volltextindex und der semantische Index erstellt wurden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die ersten 10 Kandidaten abgerufen, die einem angegebenen Kandidaten aus der HumanResources.JobCandidate-Tabelle in der AdventureWorks2012-Beispieldatenbank ähneln.  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROMSEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
