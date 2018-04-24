---
title: CREATE XML INDEX (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- XML_TSQL
- CREATE_XML_INDEX_TSQL
- XML INDEX
- CREATE_XML_TSQL
- XML
- CREATE XML
- CREATE XML INDEX
- XML_INDEX_TSQL
- FOR_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- CREATE INDEX statement
- index creation [SQL Server], XML indexes
- XML indexes [SQL Server], creating
ms.assetid: c510cfbc-68be-4736-b3cc-dc5b7aa51f14
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f91e623d31626fa1063dd525f06e137ace751bc9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-xml-index-transact-sql"></a>CREATE XML INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt einen XML-Index für eine angegebene Tabelle. Ein Index kann erstellt werden, bevor Daten in der Tabelle enthalten sind. XML-Indizes können für Tabellen in einer anderen Datenbank durch Angabe eines gekennzeichneten Datenbanknamens erstellt werden.  
  
> [!NOTE]  
>  Informationen zum Erstellen eines relationalen Indexes finden Sie unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md). Informationen zum Erstellen eines räumlichen Indexes finden Sie unter [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Create XML Index   
CREATE [ PRIMARY ] XML INDEX index_name   
    ON <object> ( xml_column_name )  
    [ USING XML INDEX xml_index_name   
        [ FOR { VALUE | PATH | PROPERTY } ] ]  
    [ WITH ( <xml_index_option> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_name  
}  
  
<xml_index_option> ::=  
{   
    PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 [PRIMARY] XML  
 Erstellt einen XML-Index für die angegebene **xml**-Spalte. Wenn PRIMARY angegeben ist, wird ein gruppierter Index mit dem gruppierten Schlüssel erstellt, der aus dem Gruppierungsschlüssel der Benutzertabelle und dem Bezeichner für einen XML-Knoten besteht. Jede Tabelle kann bis zu 249 XML-Indizes enthalten. Beachten Sie beim Erstellen eines XML-Indexes Folgendes:  
  
-   Für den Primärschlüssel der Benutzertabelle muss ein gruppierter Index vorhanden sein.  
  
-   Der Gruppierungsschlüssel der Benutzertabelle ist auf 15 Spalten begrenzt.  
  
-   Für jede **xml**-Spalte in einer Tabelle können ein primärer XML-Index und mehrere sekundäre XML-Indizes vorhanden sein.  
  
-   Für eine **xml**-Spalte muss ein primärer XML-Index vorhanden sein, bevor ein sekundärer XML-Index für die Spalte erstellt werden kann.  
  
-   Ein XML-Index kann nur für eine einzige **xml**-Spalte erstellt werden. Sie können keinen XML-Index für eine Nicht-**xml**-Spalte erstellen. Außerdem können Sie keinen relationalen Index für eine **xml**-Spalte erstellen.  
  
-   Sie können weder einen primären noch einen sekundären XML-Index für eine **xml**-Spalte in einer Sicht, für eine Tabellenwertvariable mit **xml**-Spalten oder für Variablen des Typs **xml** erstellen.  
  
-   Sie können keinen primären XML-Index für eine berechnete **xml**-Spalte erstellen.  
  
-   Die SET-Optionseinstellungen müssen mit den Einstellungen übereinstimmen, die für indizierte Sichten und berechnete Spaltenindizes erforderlich sind. Insbesondere muss die Option ARITHABORT auf ON festgelegt sein, wenn ein XML-Index erstellt und Werte in der **xml**-Spalte eingefügt, gelöscht oder aktualisiert werden.  
  
 Weitere Informationen finden Sie unter [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
 *index_name*  
 Der Name des Indexes. Indexnamen müssen für eine Tabelle eindeutig sein, können aber innerhalb einer Datenbank mehrfach vorkommen. Indexnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
  
 Primäre XML-Indexnamen dürfen nicht mit den folgenden Zeichen beginnen: **#**, **##**, **@** oder **@@**.  
  
 *xml_column_name*  
 Gibt die **xml**-Spalte an, auf der der Index basiert. Für eine einzige XML-Indexdefinition kann nur eine **xml**-Spalte angegeben werden. Allerdings können für eine **xml**-Spalte mehrere sekundäre XML-Indizes erstellt werden.  
  
 USING XML INDEX *xml_index_name*  
 Gibt den primären XML-Index an, der beim Erstellen eines sekundären XML-Indexes verwendet werden soll.  
  
 FOR { VALUE | PATH | PROPERTY }  
 Gibt den Typ des sekundären XML-Indexes an.  
  
 Value  
 Erstellt einen sekundären XML-Index für Spalten, bei denen die Schlüsselspalten (Knotenwert und Pfad) vom primären XML-Index stammen.  
  
 PATH  
 Erstellt einen sekundären XML-Index für Spalten, die auf Pfad- und Knotenwerten im primären XML-Index basieren. Im sekundären Index von PATH handelt es sich bei den Pfad- und Knotenwerten um Schlüsselspalten, die ein effizientes Suchen nach Pfaden ermöglichen.  
  
 PROPERTY  
 Erstellt einen sekundären XML-Index für Spalten (PS, Pfad und Knotenwert) des primären XML-Indexes. Dabei steht PS für den Primärschlüssel der Basistabelle.  
  
 **\<object>::=**  
  
 Gibt das vollqualifizierte oder nicht vollqualifizierte Objekt an, das indiziert werden soll.  
  
 *database_name*  
 Der Name der Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle gehört.  
  
 *table_name*  
 Der Name der Tabelle, die indiziert werden soll.  
  
 **\<xml_index_option> ::=** 
  
 Gibt die Optionen an, die beim Erstellen des Indexes verwendet werden sollen.  
  
 PAD_INDEX **=** { ON | **OFF** }  
 Gibt die Auffüllung von Indizes an. Der Standardwert ist OFF.  
  
 ON  
 Der Prozentsatz des mit *fillfactor* angegebenen freien Speicherplatzes wird für die Zwischenebenenseiten des Indexes angewendet.  
  
 OFF oder *fillfactor* ist nicht angegeben  
 Die Zwischenebenenseiten sind nahezu vollständig aufgefüllt. Allerdings ist ausreichend Speicherplatz vorhanden, um mindestens eine Zeile in der maximal für den Index möglichen Größe aufzunehmen, wenn der Schlüsselsatz auf den Zwischenseiten berücksichtigt wird.  
  
 Die Option PAD_INDEX ist nur dann hilfreich, wenn FILLFACTOR angegeben ist, da PAD_INDEX den durch FILLFACTOR angegebenen Prozentsatz verwendet. Wenn der für FILLFACTOR angegebene Prozentsatz nicht groß genug ist, um eine Zeile aufzunehmen, überschreibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] diesen Prozentsatz intern, um das Minimum zuzulassen. Auf jeder Zwischenindexseite befinden sich unabhängig vom angegebenen *fillfactor*-Wert nie weniger als zwei Zeilen.  
  
 FILLFACTOR **=***fillfactor*  
 Gibt einen Prozentsatz an, der angibt, wie weit das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Blattebene jeder Indexseite während der Indexerstellung oder -neuerstellung füllen soll. *fillfactor* muss ein ganzzahliger Wert zwischen 1 und 100 sein. Die Standardeinstellung ist 0. Wenn *fillfactor* 100 oder 0 entspricht, werden von [!INCLUDE[ssDE](../../includes/ssde-md.md)] Indizes mit vollständig aufgefüllten Blattseiten erstellt.  
  
> [!NOTE]  
>  Die Füllfaktorwerte 0 und 100 sind in jeder Hinsicht identisch.  
  
 Die FILLFACTOR-Einstellung gilt nur, wenn der Index erstellt oder neu erstellt wird. [!INCLUDE[ssDE](../../includes/ssde-md.md)] hält den angegebenen Prozentsatz des Speicherplatzes nicht dynamisch auf den Seiten frei. Zum Anzeigen der Füllfaktoreinstellung verwenden Sie die Katalogsicht [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
> [!IMPORTANT]  
>  Das Erstellen eines gruppierten Indexes mit einem FILLFACTOR-Wert unter 100 wirkt sich auf den Speicherplatz aus, den die Daten belegen, da [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Daten beim Erstellen des gruppierten Indexes neu verteilt.  
  
 Weitere Informationen finden Sie unter [Angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).  
  
 SORT_IN_TEMPDB **=** { ON | **OFF** }  
 Gibt an, ob temporäre Ergebnisse des Sortierens in **tempdb** gespeichert werden sollen. Der Standardwert ist OFF.  
  
 ON  
 Die Zwischenergebnisse von Sortierungen, mit denen der Index erstellt wird, werden in **tempdb** gespeichert. Dadurch kann sich die zum Erstellen eines Index erforderliche Zeit verringern, wenn sich **tempdb** in anderen Datenträgersätzen befindet als die Benutzerdatenbank. Sie erhöht jedoch den Betrag an Speicherplatz, der während der Indexerstellung verwendet wird.  
  
 OFF  
 Die Zwischenergebnisse der Sortierung werden in derselben Datenbank gespeichert wie der Index.  
  
 Zusätzlich zu dem Speicherplatz, der in der Benutzerdatenbank zum Erstellen des Index erforderlich ist, muss **tempdb** ungefähr die gleiche Menge an zusätzlichem Speicherplatz aufweisen, um die Zwischenergebnisse der Sortierung zu speichern. Weitere Informationen finden Sie unter [SORT_IN_TEMPDB-Optionen für Indizes](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 IGNORE_DUP_KEY **=OFF**  
 Hat keine Auswirkungen für XML-Indizes, da der Indextyp nie eindeutig ist. Legen Sie diese Option nicht auf ON fest, oder es wird ein Fehler ausgelöst.  
  
 DROP_EXISTING **=** { ON | **OFF** }  
 Gibt an, dass der benannte, bereits vorhandene XML-Index gelöscht und neu erstellt wird. Der Standardwert ist OFF.  
  
 ON  
 Der vorhandene Index wird gelöscht und neu erstellt. Der angegebene Indexname muss mit dem Namen eines derzeit vorhandenen Index übereinstimmen. Die Indexdefinition kann jedoch geändert werden. Sie können beispielsweise andere Spalten, eine andere Sortierreihenfolge, ein anderes Partitionsschema oder andere Indexoptionen angeben.  
  
 OFF  
 Es wird ein Fehler angezeigt, wenn der angegebene Indexname bereits vorhanden ist.  
  
 Der Indextyp kann nicht mithilfe von DROP_EXISTING geändert werden. Es ist auch nicht möglich, einen primären XML-Index als sekundären XML-Index neu zu definieren oder umgekehrt.  
  
 ONLINE **=OFF**  
 Gibt an, dass zugrunde liegende Tabellen oder zugehörige Indizes für Abfragen und Datenänderungen während des Indexvorgangs nicht zur Verfügung stehen. In dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Onlineindexerstellungen für XML-Indizes nicht unterstützt. Wenn diese Option für einen XML-Index auf ON festgelegt ist, wird ein Fehler ausgelöst. Lassen Sie die ONLINE-Option weg, oder legen Sie ONLINE auf OFF fest.  
  
 Ein Offlineindexvorgang, der einen XML-Index erstellt, neu erstellt oder löscht, aktiviert eine Schemaänderungssperre (Sch-M) für die Tabelle. Dadurch wird verhindert, dass Benutzer für die Dauer des Vorgangs auf die zugrunde liegende Tabelle zugreifen können.  
  
> [!NOTE]  
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 Gibt an, ob Zeilensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Zeilensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Zeilensperren verwendet werden.  
  
 OFF  
 Zeilensperren werden nicht verwendet.  
  
 ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
 Gibt an, ob Seitensperren zulässig sind. Der Standardwert ist ON.  
  
 ON  
 Seitensperren sind beim Zugriff auf den Index zulässig. Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] bestimmt, wann Seitensperren verwendet werden.  
  
 OFF  
 Seitensperren werden nicht verwendet.  
  
 MAXDOP **=***max_degree_of_parallelism*  
 Überschreibt die Konfigurationsoption [Max. Grad an Parallelität](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) für die Dauer des Indexvorgangs. Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.  
  
> [!IMPORTANT]  
>  Obwohl die MAXDOP-Option syntaktisch für alle XML-Indizes unterstützt wird, verwendet CREATE XML INDEX für einen primären XML-Index nur einen einzelnen Prozessor.  
  
 *max_degree_of_parallelism* kann folgende Werte haben:  
  
 1  
 Unterdrückt das Generieren paralleler Pläne.  
  
 \>1  
 Beschränkt die maximale Anzahl der Prozessoren, die bei einem parallelen Indexvorgang verwendet werden, je nach aktueller Systemauslastung auf die angegebene Zahl oder einen niedrigeren Wert.  
  
 0 (Standard)  
 Verwendet abhängig von der aktuellen Systemarbeitsauslastung die tatsächliche Anzahl von Prozessoren oder weniger Prozessoren.  
  
 Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Parallele Indexvorgänge sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für den SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="remarks"></a>Remarks  
 Berechnete Spalten, die von **xml**-Datentypen abgeleitet wurden, können als Schlüsselspalten oder als eingeschlossene Nichtschlüsselspalten indiziert werden, vorausgesetzt, der Datentyp der berechneten Spalte ist als Indexschlüsselspalte oder -nichtschlüsselspalte zulässig. Sie können keinen primären XML-Index für eine berechnete **xml**-Spalte erstellen.  
  
 Zum Anzeigen von Informationen zu XML-Indizes verwenden Sie die Katalogsicht [sys.xml_indexes](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md).  
  
 Weitere Informationen zu XML-Indizes finden Sie unter [XML Indexes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md).  
  
## <a name="additional-remarks-on-index-creation"></a>Weitere Hinweise zum Erstellen von Indizes  
 Weitere Informationen zum Erstellen von Indizes finden Sie in den Hinweisen unter [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-primary-xml-index"></a>A. Erstellen eines primären XML-Indexes  
 Im folgenden Beispiel wird ein primärer XML-Index für die Spalte `CatalogDescription` in der Tabelle `Production.ProductModel` erstellt.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT * FROM sys.indexes  
            WHERE name = N'PXML_ProductModel_CatalogDescription')  
    DROP INDEX PXML_ProductModel_CatalogDescription   
        ON Production.ProductModel;  
GO  
CREATE PRIMARY XML INDEX PXML_ProductModel_CatalogDescription  
    ON Production.ProductModel (CatalogDescription);  
GO  
```  
  
### <a name="b-creating-a-secondary-xml-index"></a>B. Erstellen eines sekundären XML-Indexes  
 Im folgenden Beispiel wird ein sekundärer XML-Index für die Spalte `CatalogDescription` in der Tabelle `Production.ProductModel` erstellt.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.indexes  
            WHERE name = N'IXML_ProductModel_CatalogDescription_Path')  
    DROP INDEX IXML_ProductModel_CatalogDescription_Path  
        ON Production.ProductModel;  
GO  
CREATE XML INDEX IXML_ProductModel_CatalogDescription_Path   
    ON Production.ProductModel (CatalogDescription)  
    USING XML INDEX PXML_ProductModel_CatalogDescription FOR PATH ;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [XML-Indizes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  

