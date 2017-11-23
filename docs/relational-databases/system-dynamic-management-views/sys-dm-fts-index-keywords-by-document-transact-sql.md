---
title: dm_fts_index_keywords_by_document (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_by_document_TSQL
- dm_fts_index_keywords_by_document_TSQL
- sys.dm_fts_index_keywords_by_document
- dm_fts_index_keywords_by_document
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- sys.dm_fts_index_keywords_by_document dynamic management function
- full-text search [SQL Server], viewing keywords
ms.assetid: 793b978b-c8a1-428c-90c2-a3e49d81b5c9
caps.latest.revision: "40"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5db2c784b48c6a1c9ef97f11fb0fbb7903bc85e4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmftsindexkeywordsbydocument-transact-sql"></a>sys.dm_fts_index_keywords_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Gibt Informationen über den Inhalt auf Dokumentebene von einem Volltextindex zurück, der der angegebenen Tabelle zugeordnet ist.  
  
 sys.dm_fts_index_keywords_by_document ist eine dynamische Verwaltungsfunktion.  
  
 **Auf höherer Ebene Volltextindex Informationen anzeigen**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
 **So zeigen Sie Informationen zu Inhalten auf Eigenschaftenebene an, der sich auf eine Dokumenteigenschaft beziehen**  
  
-   [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_fts_index_keywords_by_document  
(   
    DB_ID('database_name'),     OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argumente  
 Db_id ("*Database_name*")  
 Ein Aufruf der [DB_ID()](../../t-sql/functions/db-id-transact-sql.md) Funktion. Diese Funktion akzeptiert einen Datenbanknamen und gibt die Datenbank-ID zurück, die von sys.dm_fts_index_keywords_by_document für die Suche nach der angegebenen Datenbank verwendet wird. Wenn *Database_name* wird weggelassen wird, wird die aktuelle Datenbank-ID zurückgegeben.  
  
 Object_id ("*Table_name*")  
 Ein Aufruf der [OBJECT_ID()](../../t-sql/functions/object-id-transact-sql.md) Funktion. Diese Funktion akzeptiert einen Tabellennamen und gibt die Tabellen-ID der Tabelle zurück, die den zu überprüfenden Volltextindex enthält.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Column|Datentyp|Description|  
|------------|---------------|-----------------|  
|Schlüsselwort (keyword)|**nvarchar(4000)**|Die hexadezimale Darstellung des Schlüsselworts, das im Volltextindex gespeichert ist.<br /><br /> Hinweis: OxFF stellt das Sonderzeichen, das das Ende einer Datei oder das Dataset anzeigt.|  
|display_term|**nvarchar(4000)**|Die Klartextform des Schlüsselworts. Dieses Format wird vom internen Format abgeleitet, das im Volltextindex gespeichert ist.<br /><br /> Hinweis: OxFF stellt das Sonderzeichen, das das Ende einer Datei oder das Dataset anzeigt.|  
|column_id|**int**|Die ID der Spalte für die Volltextindizierung des aktuellen Schlüsselworts.|  
|document_id|**int**|Die ID des Dokuments bzw. der Zeile für die Volltextindizierung des aktuellen Ausdrucks. Diese ID entspricht dem Volltextschlüsselwert dieses Dokuments bzw. dieser Zeile.|  
|occurrence_count|**int**|Anzahl der Vorkommen des aktuellen Schlüsselworts in das Dokument oder die Zeile, die vom angegebenen **Document_id**. Wenn "*Search_property_name*" angegeben ist, Occurrence_count zeigt nur die Anzahl der Vorkommen des aktuellen Schlüsselworts in der angegebenen Sucheigenschaft im Dokument oder in der Zeile.|  
  
## <a name="remarks"></a>Hinweise  
 Die von sys.dm_fts_index_keywords_by_document zurückgegebenen Informationen dienen u. a. zum Abrufen der folgenden Ergebnisse:  
  
-   Die Gesamtzahl der Schlüsselwörter in einem Volltextindex  
  
-   Ob ein Schlüsselwort Teil eines bestimmten Dokuments bzw. einer Zeile ist  
  
-   Wie oft ein Schlüsselwort im gesamten Volltextindex vorkommt, d. h.:  
  
     ([Summe](../../t-sql/functions/sum-transact-sql.md)(**Occurrence_count**), in denen **Schlüsselwort**=*Keyword_value* )  
  
-   Wie oft ein Schlüsselwort in einem bestimmten Dokument bzw. in einer Zeile vorkommt  
  
-   Wie viele Schlüsselwörter ein bestimmtes Dokument bzw. eine Zeile enthält  
  
 Darüber hinaus können Sie anhand der von sys.dm_fts_index_keywords_by_document zurückgegebenen Informationen alle Schlüsselwörter eines gegebenen Dokuments oder einer gegebenen Zeile abrufen.  
  
 Wenn die Volltextschlüsselspalte wie empfohlen mit dem integer-Datentyp definiert ist, kann die document_id direkt dem Volltextschlüsselwert in der Basistabelle zugeordnet werden.  
  
 Wenn als Datentyp für die Volltextschlüsselspalte jedoch ein anderer Typ als Integer festgelegt ist, stellt document_id nicht den Volltextschlüsselwert in der Basistabelle dar. In diesem Fall um die Zeile in der Basistabelle zu identifizieren, die von Dm_fts_index_keywords_by_document zurückgegeben wird, müssen Sie auf diese Sicht mit den Ergebnissen zurückgegeben, die durch Verknüpfen [Sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md). Speichern Sie jedoch zuvor die Ausgabe der gespeicherten Prozedur in eine temporäre Tabelle. Anschließend können Sie die Spalte document_id von dm_fts_index_keywords_by_document mit der von der gespeicherten Prozedur zurückgegebenen Spalte DOCID verknüpfen. Beachten Sie, dass eine **Zeitstempel** Spalte kann nicht empfangen, Werte zum Zeitpunkt des Einfügens, da von automatisch generierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aus diesem Grund die **Zeitstempel** Spalte konvertiert werden muss, um **varbinary(8)** Spalten. Das folgende Beispiel zeigt die erforderlichen Schritte: In diesem Beispiel *Table_id* ist die ID der Tabelle, *Database_name* ist der Name Ihrer Datenbank und *Table_name* ist der Name der Tabelle.  
  
```  
USE database_name;  
GO  
CREATE TABLE #MyTempTable   
   (  
      docid INT PRIMARY KEY ,  
      [key] INT NOT NULL  
   );  
DECLARE @db_id int = db_id(N'database_name');  
DECLARE @table_id int = OBJECT_ID(N'table_name');  
INSERT INTO #MyTempTable EXEC sp_fulltext_keymappings @table_id;  
SELECT * FROM sys.dm_fts_index_keywords_by_document   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert CREATE FULLTEXT CATALOG-Berechtigungen und die SELECT-Berechtigung für die vom Volltextindex abgedeckten Spalten.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-displaying-full-text-index-content-at-the-document-level"></a>A. Anzeigen des Inhalts eines Volltextindexes auf Dokumentebene  
 Im folgenden Beispiel wird der Inhalt des Volltextindexes auf Dokumentebene in der `HumanResources.JobCandidate`-Tabelle der `AdventureWorks2012`-Beispieldatenbank angezeigt.  
  
> [!NOTE]  
>  Sie können diesen Index erstellen, durch das Ausführen der im Beispiels für die `HumanResources.JobCandidate` in Tabelle [CREATE FULLTEXT INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_by_document(db_id('AdventureWorks'),   
object_id('HumanResources.JobCandidate'));  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Volltextsuche und semantische Suche dynamische Verwaltungssichten und Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)   
 [dm_fts_index_keywords &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [dm_fts_index_keywords_by_property &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [Sp_fulltext_keymappings &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [Verbessern der Leistung von Volltextindizes](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
  
