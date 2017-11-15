---
title: "Löschen von XML-Indizes | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing indexes
- dropping indexes
- XML indexes [SQL Server], dropping
ms.assetid: 7591ebea-34af-4925-8553-b2adb5b487c2
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 01e16ed7ef2a64f4a04af9d683247d09c8942fe2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="drop-xml-indexes"></a>Löschen von XML-Indizes
  Die [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung kann zum Löschen vorhandener primärer oder sekundärer XML-Indizes und Nicht-XML-Indizes verwendet werden. Die DROP INDEX-Optionen gelten jedoch nicht für XML-Indizes. Wenn Sie den primären XML-Index löschen, werden sämtliche vorhandenen sekundären Indizes ebenfalls gelöscht.  
  
 Die DROP-Syntax mit *TableName.IndexName* ist veraltet und wird für XML-Indizes nicht unterstützt.  
  
## <a name="example-creating-and-dropping-a-primary-xml-index"></a>Beispiel: Erstellen und Löschen eines primären XML-Index  
 Im folgenden Beispiel wird ein XML-Index für eine Spalte vom Typ **xml** erstellt:  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create Primary XML index   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Verify the index creation.   
-- Note index type is 3 for xml indexes.  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'   
-- Drop the index.  
DROP INDEX PIdx_T_XmlCol ON T  
```  
  
 Beim Löschen einer Tabelle werden auch XML-Indizes für diese automatisch gelöscht. Eine XML-Spalte kann jedoch nicht aus einer Tabelle gelöscht werden, wenn ein XML-Index für die Spalte vorhanden ist.  
  
 Im folgenden Beispiel wird ein XML-Index für eine Spalte vom Typ **xml** erstellt: Weitere Informationen finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
```  
CREATE TABLE TestTable(  
 Col1 int primary key,   
 Col2 xml (Production.ProductDescriptionSchemaCollection))   
GO  
```  
  
 Nun können Sie einen primären XML-Index für `Co12`erstellen:  
  
```  
CREATE PRIMARY XML INDEX PIdx_TestTable_Col2   
ON TestTable(Col2)  
GO  
```  
  
## <a name="example-creating-an-xml-index-by-using-the-dropexisting-index-option"></a>Beispiel: Erstellen eines XML-Index mithilfe der DROP_EXISTING-Indexoption  
 Im folgenden Beispiel wird ein XML-Index für eine Spalte (`XmlColx`) erstellt. Anschließend wird ein weiterer XML-Index mit dem gleichen Namen für eine andere Spalte (`XmlColy`) erstellt. Da die Option `DROP_EXISTING` angegeben wird, wird der vorhandene XML-Index für (`XmlColx)` gelöscht und ein neuer XML-Index für (`XmlColy`) erstellt.  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T(Col1 int primary key, XmlColx xml, XmlColy xml)  
GO  
-- Create XML index on XmlColx.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColx)  
GO  
-- Create same name XML index on XmlColy.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColy)   
WITH (DROP_EXISTING = ON)  
-- Verify the index is created on XmlColy.d.  
SELECT sc.name   
FROM   sys.xml_indexes si inner join sys.index_columns sic   
ON     sic.object_id=si.object_id and sic.index_id=si.index_id  
INNER  join sys.columns sc on sc.object_id=sic.object_id   
AND    sc.column_id=sic.column_id  
WHERE  si.name='PIdx_T_XmlCol'   
AND    si.object_id=object_id('T')  
```  
  
 Diese Abfrage gibt den Spaltennamen zurück, für den der angegebene XML-Index erstellt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
