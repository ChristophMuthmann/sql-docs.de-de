---
title: Semanticsimilaritydetailstable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 376c644ebeab414cc9f3cf93a56b449f2669be5b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Tabelle mit keiner, einer oder mehreren Zeilen von Schlüsselausdrücken zurück, die in zwei Dokumenten (einem Quelldokument und einem übereinstimmenden Dokument) vorkommen, deren Inhalt semantisch ähnlich ist.  
  
 Auf diese Rowsetfunktion kann in der FROM-Klausel einer SELECT-Anweisung verwiesen werden 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
SEMANTICSIMILARITYDETAILSTABLE  
    (  
    table,  
    source_column,  
    source_key,  
    matched_column,  
    matched_key  
    )  
```  
  
##  <a name="Arguments"></a> Argumente  
 **table**  
 Ist der Name einer Tabelle, für die die Volltext- und die semantische Indizierung aktiviert ist.  
  
 Dieser Name kann einteilig sein oder aus bis zu vier Teilen bestehen, aber ein Remoteservername ist nicht zugelassen.  
  
 **source_column**  
 Name der Spalte in der Quellzeile, deren Inhalt auf Ähnlichkeit überprüft werden soll.  
  
 **source_key**  
 Der eindeutige Schlüssel, der die Zeile des Quelldokuments angibt.  
  
 Dieser Schlüssel wird nach Möglichkeit immer implizit in den Typ des eindeutigen Volltextschlüssels in der Quelltabelle konvertiert. Der Schlüssel kann als Konstante oder Variable angegeben werden. Er kann jedoch kein Ausdruck oder das Ergebnis einer skalaren Unterabfrage sein. Wenn ein ungültiger Schlüssel angegeben wird, werden keine Zeilen zurückgegeben.  
  
 **matched_column**  
 Name der Spalte in der übereinstimmenden Zeile, deren Inhalt auf Ähnlichkeit überprüft werden soll.  
  
 **matched_key**  
 Der eindeutige Schlüssel, der die Zeile des übereinstimmenden Dokuments angibt.  
  
 Dieser Schlüssel wird nach Möglichkeit immer implizit in den Typ des eindeutigen Volltextschlüssels in der Quelltabelle konvertiert. Der Schlüssel kann als Konstante oder Variable angegeben werden. Er kann jedoch kein Ausdruck oder das Ergebnis einer skalaren Unterabfrage sein.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
 In der folgenden Tabelle werden die Schlüsselausdrücke beschrieben, die von dieser Rowset-Funktion zurückgegeben werden.  
  
|Column_name|Typ|Description|  
|------------------|----------|-----------------|  
|**keyphrase**|**NVARCHAR**|Der Schlüsselausdruck, der zur Ähnlichkeit zwischen Quelldokument und übereinstimmendem Dokument beiträgt.|  
|**score**|**REAL**|Ein relativer Wert für diesen Schlüsselausdruck in der Beziehung mit allen anderen Schlüsselausdrücken, die in den beiden Dokumenten ähnlich sind.<br /><br /> Der Wert ist eine Dezimalzahl im Bereich [0,0; 1,0], wobei ein höheres Ergebnis eine höhere Gewichtung und 1,0 ein perfektes Ergebnis darstellt.|  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Weitere Informationen finden Sie unter [Suchen von ähnlichen und verwandten Dokumenten mit Semantischer Suche](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
## <a name="metadata"></a>Metadaten  
 Führen Sie eine Abfrage der folgenden dynamischen Verwaltungssichten durch, um Informationen, einschließlich Statusinformationen, zur semantischen Ähnlichkeitsextraktion und Auffüllung zu erhalten:  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigungen für die Basistabelle, für die der Volltextindex und der semantische Index erstellt wurden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die fünf Schlüsselausdrücke mit der größten Ähnlichkeit zwischen den in der **HumanResources.JobCandidate** -Tabelle angegebenen Kandidaten der AdventureWorks2012-Beispieldatenbank abgerufen. Die @CandidateId und @MatchedID Variablen Werte aus der Schlüsselspalte des Volltextindex-darstellen.  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROMSEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
