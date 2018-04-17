---
title: Semantickeyphrasetable (Transact-SQL) | Microsoft Docs
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
- semantickeyphrasetable
- semantickeyphrasetable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semantickeyphrasetable function
ms.assetid: d33b973a-2724-4d4b-aaf7-67675929c392
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 621ecbfde7150cfba17f910a092ec894825362a8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="semantickeyphrasetable-transact-sql"></a>semantickeyphrasetable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Tabelle mit keiner, einer oder mehreren Zeilen für die Schlüsselausdrücke zurück, die den angegebenen Spalten in der angegebenen Tabelle zugeordnet sind.  
  
 Auf diese Rowsetfunktion kann in der FROM-Klausel einer SELECT-Anweisung so verwiesen werden, als handelte es sich dabei um einen regulären Tabellennamen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
SEMANTICKEYPHRASETABLE  
    (  
    table,  
    { column | (column_list) | * }  
     [ , source_key ]  
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
  
 Der Schlüssel wird in den Typ des eindeutigen Schlüssels in der Quelltabelle möglichst Volltext-implizit konvertiert. Der Schlüssel kann als Konstante oder Variable angegeben werden. Er kann jedoch kein Ausdruck oder das Ergebnis einer skalaren Unterabfrage sein. Wird "source_key" nicht angegeben, werden Ergebnisse für alle Zeilen zurückgegeben.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
 In der folgenden Tabelle werden die Schlüsselausdrücke beschrieben, die von dieser Rowset-Funktion zurückgegeben werden.  
  
|Column_name|Typ|Description|  
|------------------|----------|-----------------|  
|**column_id**|**int**|Die ID der Spalte, aus der der aktuelle Schlüsselausdruck extrahiert und indiziert wurde.<br /><br /> Im Abschnitt über die COL_NAME-Funktion und COLUMNPROPERTY-Funktion finden Sie ausführliche Informationen zum Abrufen des Spaltennamens aus "column_id" und umgekehrt.|  
|**document_key**|**\***<br /><br /> Dieser Schlüssel stimmt mit dem Typ des eindeutigen Schlüssels in der Quelltabelle überein.|Eindeutiger Schlüsselwert des Dokuments oder der Zeile, anhand dem der aktuelle Schlüsselausdruck indiziert wurde.|  
|**keyphrase**|**NVARCHAR**|Der Schlüsselausdruck in der durch "column_id" angegebenen Spalte, der dem durch "document_key" angegebenen Dokument zugeordnet ist.|  
|**score**|**REAL**|Ein relativer Wert für diesen Schlüsselausdruck in der Beziehung mit allen anderen Schlüsselausdrücken im gleichen Dokument in der indizierten Spalte.<br /><br /> Der Wert ist eine Dezimalzahl im Bereich [0,0; 1,0], wobei ein höheres Ergebnis eine höhere Gewichtung und 1,0 ein perfektes Ergebnis darstellt.|  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Weitere Informationen finden Sie unter [Suchen von Schlüsselausdrücken in Dokumenten mit Semantischer Suche](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md).  
  
## <a name="metadata"></a>Metadaten  
 Führen Sie eine Abfrage der folgenden dynamischen Verwaltungssichten durch, um Informationen, einschließlich Statusinformationen, zur semantischen Schlüsselausdruckextraktion und Auffüllung zu erhalten:  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigungen für die Basistabelle, für die der Volltextindex und der semantische Index erstellt wurden.  
  
## <a name="examples"></a>Beispiele  
  
###  <a name="HowToTopPhrases"></a>Beispiel 1: Suchen der wichtigsten Schlüsselausdrücke in einem bestimmten Dokument  
 Im folgenden Beispiel werden die obersten 10 Schlüsselausdrücke aus dem von der @DocumentId-Variable in der Spalte "Dokument" der Production.Document-Tabelle der AdventureWorks-Beispieldatenbank angegebenen Dokument abgerufen. Die @DocumentId-Variable stellt einen Wert aus der Schlüsselspalte des Volltextindexes dar. Die **SEMANTICKEYPHRASETABLE** -Funktion ruft diese Ergebnisse effizient mithilfe eines Indexsuchvorgangs anstelle eines Tabellenscans ab. In diesem Beispiel wird davon ausgegangen, dass die Spalte für die Volltextindizierung und die semantische Indizierung konfiguriert wurde.  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
  
```  
  
###  <a name="HowToTopDocuments"></a>Beispiel 2: Suchen der wichtigsten Dokumente, die einen bestimmten Schlüsselausdruck enthalten  
 Im folgenden Beispiel werden die obersten 25 Dokumente mit dem Schlüsselausdruck "Klammer" in der Spalte "Dokument" der Production.Document-Tabelle der AdventureWorks-Beispieldatenbank abgerufen. In diesem Beispiel wird davon ausgegangen, dass die Spalte für die Volltextindizierung und die semantische Indizierung konfiguriert wurde.  
  
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
  
```  
  
  
