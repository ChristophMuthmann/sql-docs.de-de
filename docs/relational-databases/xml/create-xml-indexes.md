---
title: Erstellen von XML-Indizes | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- indexes [XML in SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: 6ecac598-355d-4408-baf7-1b2e8d4cf7c1
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 580f5bec5834cd161d1bbe81ac17f2a26faba32b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-xml-indexes"></a>Erstellen von XML-Indizes
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie primäre und sekundäre XML-Indizes erstellt werden.  
  
## <a name="creating-a-primary-xml-index"></a>Erstellen eines primären XML-Indexes  
 Um einen primären XML-Index zu erstellen, verwenden Sie die DDL-Anweisung [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]. Nicht alle Optionen, die für Nicht-XML-Indizes verfügbar sind, werden für XML-Indizes unterstützt.  
  
 Beachten Sie beim Erstellen eines XML-Indexes Folgendes:  
  
-   Damit ein primärer XML-Index erstellt werden kann, muss die Tabelle, die die zu indizierende XML-Spalte enthält (als Basistabelle bezeichnet), einen gruppierten Index für den Primärschlüssel enthalten. Auf diese Weise wird sichergestellt, dass der primäre XML-Index mithilfe des gleichen Partitionierungsschemas und der gleichen Partitionierungsfunktion partitioniert werden kann, wenn die Basistabelle partitioniert ist.  
  
-   Wenn ein XML-Index vorhanden ist, kann der gruppierte Primärschlüssel der Tabelle nicht geändert werden. Sie müssen alle XML-Indizes für die Tabelle löschen, bevor Sie den Primärschlüssel ändern können.  
  
-   Ein primärer XML-Index kann für eine einzelne Spalte vom Typ **xml** erstellt werden. Sie können keinen anderen Indextyp mit der Spalte vom Typ XML als Schlüsselspalte erstellen. Sie können jedoch die Spalte vom Typ **xml** in einen Nicht-XML-Index einschließen. Jede Spalte vom Typ **xml** in einer Tabelle kann ihren eigenen primären XML-Index aufweisen. Es ist jedoch nur ein primärer XML-Index pro Spalte vom Typ **xml** zulässig.  
  
-   XML-Indizes werden im gleichen Namespace wie Nicht-XML-Indizes gespeichert. Aus diesem Grund dürfen ein XML-Index und ein Nicht-XML-Index für die gleiche Tabelle nicht den gleichen Namen besitzen.  
  
-   Die Optionen IGNORE_DUP_KEY- und ONLINE werden für XML-Indizes immer auf OFF festgelegt. Sie können diese Optionen mit einem Wert von OFF angeben.  
  
-   Die Dateigruppen- oder Partitionierungsinformationen der Benutzertabelle werden auf den XML-Index angewendet. Benutzer können diese nicht separat für einen XML-Index angeben.  
  
-   Die DROP_EXISTING-Indexoption kann einen primären XML-Index löschen und einen neuen primären XML-Index erstellen oder einen sekundären XML-Index löschen und einen neuen sekundären XML-Index erstellen. Mit dieser Option kann jedoch nicht ein sekundärer XML-Index gelöscht werden, um einen neuen primären XML-Index zu erstellen oder umgekehrt.  
  
-   Für die Namen primärer XML-Indizes gelten die gleichen Einschränkungen wie für Sichtnamen.  
  
 Sie können keinen XML-Index für eine Spalte vom Typ **xml** in einer Sicht für eine **Tabellen** wertvariable mit Spalten vom Typ **xml** oder Variablen vom Typ **xml** erstellen.  
  
-   Wenn Sie eine Spalte vom Typ **xml** mithilfe der Option ALTER TABLE ALTER COLUMN aus nicht typisiertem in typisiertes XML oder umgekehrt ändern möchten, sollte kein XML-Index für die Spalte vorhanden sein. Wenn ein XML-Index vorhanden ist, muss dieser gelöscht werden, bevor der Änderungsversuch des Spaltentyps unternommen wird.  
  
-   Die Option ARITHABORT muss auf ON festgelegt werden, wenn ein XML-Index erstellt wird. Zum Abfragen, Einfügen, Löschen oder Aktualisieren von Werten in der XML-Spalte mithilfe der Methoden des XML-Datentyps muss die gleiche Option für die Verbindung festgelegt werden. Wenn dies nicht der Fall ist, schlagen die Methoden des XML-Datentyps fehl.  
  
    > [!NOTE]  
    >  Informationen zu einem XML-Index finden Sie in den Katalogsichten. **sp_helpindex** wird jedoch nicht unterstützt. Beispiele weiter unten in diesem Abschnitt veranschaulichen, wie die Katalogsichten zum Ermitteln von XML-Indexinformationen abgefragt werden.  
  
 Bei Erstellen oder Neuerstellen eines primären XML-Indexes für eine Spalte des XML-Datentyps, die Werte der XML-Schematypen **xs:date** oder **xs:dateTime** (oder andere Untertypen dieser Typen) mit einer kleineren Jahresangabe als 1 enthält, kann der Index in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und späteren Versionen nicht erstellt werden. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ließ diese Werte zu. Dieses Problem kann daher auftreten, wenn Indizes in einer mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]generierten Datenbank erstellt werden. Weitere Informationen finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
### <a name="example-creating-a-primary-xml-index"></a>Beispiel: Erstellen eines primären XML-Indexes  
 In den meisten Beispielen wird Tabelle T (pk INT PRIMARY KEY, xCol XML) mit einer nicht typisierten XML-Spalte verwendet. Diese können auf einfache Weise zu typisiertem XML erweitert werden. Aus Gründen der Vereinfachung werden die Abfragen für XML-Dateninstanzen beschrieben, wie das im folgenden Beispiel gezeigt wird:  
  
```  
<book genre="security" publicationdate="2002" ISBN="0-7356-1588-2">  
   <title>Writing Secure Code</title>  
   <author>  
      <first-name>Michael</first-name>  
      <last-name>Howard</last-name>  
   </author>  
   <author>  
      <first-name>David</first-name>  
      <last-name>LeBlanc</last-name>  
   </author>  
   <price>39.99</price>  
</book>  
```  
  
 Die folgende Anweisung erstellt einen XML-Index mit der Bezeichnung idx_xCol für die XML-Spalte xCol der Tabelle T:  
  
```  
CREATE PRIMARY XML INDEX idx_xCol on T (xCol)  
```  
  
## <a name="creating-a-secondary-xml-index"></a>Erstellen eines sekundären XML-Indexes  
 Verwenden Sie die DDL-Anweisung [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)], um sekundäre XML-Indizes zu erstellen und den Typ des gewünschten sekundären XML-Indexes anzugeben.  
  
 Beachten Sie beim Erstellen sekundärer XML-Indizes Folgendes:  
  
-   Alle Indizierungsoptionen, die für einen nicht gruppierten Index gelten, sind mit Ausnahme von IGNORE_DUP_KEY und ONLINE für sekundäre XML-Indizes zulässig. Die beiden Optionen müssen für sekundäre XML-Indizes immer auf OFF festgelegt sein.  
  
-   Die sekundären Indizes werden ebenso wie der primäre XML-Index partitioniert.  
  
-   DROP_EXISTING kann einen sekundären Index für die Benutzertabelle löschen und einen anderen sekundären Index für die Benutzertabelle erstellen.  
  
 Sie können die **sys.xml_indexes** -Katalogsicht abfragen, um XML-Indexinformationen abzurufen. Beachten Sie, dass die **secondary_type_desc** -Spalte in der **sys.xml_indexes** -Katalogsicht den Typ des sekundären Indexes bereitstellt:  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 Der zurückgegebene Wert in der **secondary_type_desc** -Spalte kann NULL, PATH, VALUE oder PROPERTY sein. Für den primären Index lautet der zurückgegebene Wert NULL.  
  
### <a name="example-creating-secondary-xml-indexes"></a>Beispiel: Erstellen sekundärer XML-Indizes  
 Das folgende Beispiel zeigt, wie sekundäre XML-Indizes erstellt werden. Im Beispiel werden außerdem Informationen zu den von Ihnen erstellten XML-Indizes bereitgestellt.  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML);  
GO  
-- Create primary index.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol);  
GO  
-- Create secondary indexes (PATH, VALUE, PROPERTY).  
CREATE XML INDEX PIdx_T_XmlCol_PATH ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PATH;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_VALUE ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR VALUE;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_PROPERTY ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PROPERTY;  
GO  
```  
  
 Sie können die `sys.xml_indexes` -Katalogsicht abfragen, um XML-Indexinformationen abzurufen. Der Typ wird in der `secondary_type_desc` -Spalte des zweiten Indizes bereitgestellt.  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 Sie können auch die Katalogsicht nach Indexinformationen abfragen.  
  
```  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T');  
```  
  
 Sie können Beispieldaten hinzufügen und anschließend die XML-Indexinformationen überprüfen.  
  
```  
INSERT INTO T VALUES (1,  
'<doc id="123">  
<sections>  
<section num="2">  
<heading>Background</heading>  
</section>  
<section num="3">  
<heading>Sort</heading>  
</section>  
<section num="4">  
<heading>Search</heading>  
</section>  
</sections>  
</doc>');  
GO  
-- Check XML index information.  
SELECT *  
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, NULL, 'DETAILED');  
GO  
-- Space usage of primary XML index  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id  
FROM    sys.xml_indexes i   
WHERE   i.name = 'PIdx_T_XmlCol' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
--- Space usage of secondary XML index (for example PATH secondary index)  PIdx_T_XmlCol_PATH  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id   
FROM    sys.xml_indexes i   
WHERE  i.name = 'PIdx_T_XmlCol_PATH' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
  
-- Space usage of all secondary XML indexes for a particular table  
SELECT i.name, object_name(i.object_id), stats.*   
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, DEFAULT, 'DETAILED') stats  
JOIN sys.xml_indexes i ON (stats.object_id = i.object_id and stats.index_id = i.index_id)  
WHERE secondary_type is not null;  
-- Drop secondary indexes.  
DROP INDEX PIdx_T_XmlCol_PATH ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_VALUE ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_PROPERTY ON T;  
GO  
-- Drop primary index.  
DROP INDEX PIdx_T_XmlCol ON T;  
-- Drop table T.  
DROP TABLE T;  
Go  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
