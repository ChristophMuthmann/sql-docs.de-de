---
title: "XML-Indizes (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Entfernen von Indizes"
  - "Löschen von Indizes"
  - "Sekundäre Indizes [XML in SQL Server]"
  - "XML-Datentyp [SQL Server], Indizes"
  - "Verwerfen von Indizes"
  - "PATH-Index"
  - "DROP_EXISTING-Klausel"
  - "XML [SQL Server], Indizes"
  - "Primäre Indizes [XML in SQL Server]"
  - "Indizes [SQL Server], XML"
  - "XML-Indizes [SQL Server], sekundär"
  - "BLOBS, XML-Indizes"
  - "Deaktivieren von Indizes"
  - "XML-Indizes [SQL Server], ändern"
  - "XML-Indizes [SQL Server]"
  - "XML-Indizes [SQL Server], primär"
  - "Ändern von Indizes"
  - "XML-Indizes [SQL Server], löschen"
  - "VALUE-Index"
  - "XML-Indizes [SQL Server], XML-Datentyp"
  - "PROPERTY-Index"
  - "XML-Indizes [SQL Server], erstellen"
ms.assetid: f5c9209d-b3f3-4543-b30b-01365a5e7333
caps.latest.revision: 59
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 59
---
# XML-Indizes (SQL Server)
  XML-Indizes können für **xml**-Datentypspalten erstellt werden. Sie indizieren alle Tags, Werte und Pfade für die XML-Instanzen in der Spalte. Die Indizierung verbessert zudem die Abfrageleistung. Ihre Anwendung kann in folgenden Situationen von einem XML-Index profitieren:  
  
-   In Ihren Arbeitsauslastungen sind Abfragen von XML-Spalten üblich. Die Wartungskosten für den XML-Index während der Datenänderung müssen berücksichtigt werden.  
  
-   Ihre XML-Werte sind relativ groß, und die abgerufenen Teile sind relativ klein. Mit dem Erstellen eines Index wird vermieden, dass zur Laufzeit die gesamten Daten analysiert werden müssen. Davon profitieren Indexsuchen und die Abfrageverarbeitung wird effizienter.  
  
 XML-Indizes fallen in die folgenden Kategorien:  
  
-   Primärer XML-Index  
  
-   Sekundärer XML-Index  
  
 Der erste Index für die Spalte des Datentyps **xml** muss der primäre XML-Index sein. Mithilfe des primären XML-Indexes werden drei Arten sekundärer Indizes unterstützt: PATH, VALUE und PROPERTY. Abhängig vom Typ der Abfragen können diese sekundären Indizes die Abfrageleistung steigern.  
  
> [!NOTE]  
>  Sie können einen XML-Index nur dann erstellen oder bearbeiten, wenn die Datenbankoptionen korrekt für die Arbeit mit dem **xml**-Datentyp festgelegt sind. Weitere Informationen finden Sie unter [Verwenden der Volltextsuche mit XML-Spalten](../../relational-databases/xml/use-full-text-search-with-xml-columns.md).  
  
 XML-Instanzen werden in Spalten vom Typ **xml** als BLOBs (Binary Large Objects) gespeichert. Diese XML-Instanzen können groß sein, und die gespeicherte binäre Darstellung von Instanzen vom Datentyp **xml** kann bis zu 2GB groß sein. Ohne Index werden diese BLOBs zur Laufzeit aufgeteilt, um eine Abfrage auszuwerten. Diese Aufteilung kann zeitaufwändig sein. Angenommen, beispielsweise liegt die folgende Abfrage vor:  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 Um die XML-Instanzen auszuwählen, die die Bedingung in der `WHERE`-Klausel erfüllen, wird der XML-BLOB (Binary Large Object) in jeder Zeile der `Production.ProductModel`-Tabelle zur Laufzeit aufgeteilt. Dann wird der Ausdruck `(/PD:ProductDescription/@ProductModelID[.="19"]`) in der `exist()`-Methode ausgewertet. Diese Aufteilung zur Laufzeit kann abhängig von der Größe und Anzahl der in der Spalte gespeicherten Instanzen kostenintensiv sein.  
  
 Wenn das Abfragen von XML-BLOBs in Ihrer Anwendungsumgebung häufig vorkommt, ist das Indizieren der Spalten des Datentyps **xml** hilfreich. Das Verwalten des Indexes während der Datenänderung verursacht jedoch auch Kosten.  
  
## Primärer XML-Index  
 Der primäre XML-Index indiziert alle Tags, Werte und Pfade innerhalb der XML-Instanzen in einer XML-Spalte. Damit ein primärer XML-Index erstellt werden kann, muss die Tabelle, in der die XML-Spalte enthalten ist, einen gruppierten Index für den Primärschlüssel der Tabelle aufweisen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet diesen Primärschlüssel zum Korrelieren von Zeilen im primären XML-Index mit Zeilen in der Tabelle, in der die XML-Spalte enthalten ist.  
  
 Der primäre XML-Index ist eine aufgeteilte und persistente Darstellung der XML-BLOBs in der **xml**-Datentypspalte. Für jeden XML-BLOB in der Spalte erstellt der Index mehrere Datenzeilen. Die Anzahl der Zeilen im Index entspricht ungefähr der Anzahl der Knoten im XML-BLOB. Wenn eine Abfrage die vollständige XML-Instanz abruft, stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Instanz aus der XML-Spalte bereit. Abfragen innerhalb der XML-Instanzen verwenden den primären XML-Index und können Skalarwerte oder XML-Teilbäume zurückgeben, indem der Index selbst verwendet wird.  
  
 Jede Zeile speichert die folgenden Knoteninformationen:  
  
-   Tagname, z. B. einen Element- oder Attributnamen.  
  
-   Knotenwert.  
  
-   Knotentyp, z. B. Elementknoten, Attributknoten oder Textknoten.  
  
-   Informationen zur Dokumentreihenfolge, die durch einen internen Knotenbezeichner dargestellt wird.  
  
-   Pfad von jedem Knoten zum Stamm der XML-Struktur. Diese Spalte wird in der Abfrage nach path-Ausdrücken durchsucht.  
  
-   Primärschlüssel der Basistabelle. Der Primärschlüssel der Basistabelle wird im primären XML-Index für den Rückwärtsjoin mit der Basistabelle dupliziert, und die maximale Anzahl von Spalten im Primärschlüssel der Basistabelle ist auf 15 beschränkt.  
  
 Diese Knoteninformationen werden zum Auswerten und Erstellen der XML-Ergebnisse für eine angegebene Abfrage verwendet. Zu Optimierungszwecken werden der Tagname und die Knotentypinformationen als ganze Zahlen codiert; die Path-Spalte verwendet die gleiche Codierung. Pfade werden außerdem in umgekehrter Reihenfolge gespeichert, damit eine Pfadzuordnung erfolgen kann, wenn nur das Pfadsuffix bekannt ist. Beispiel:  
  
-   `//ContactRecord/PhoneNumber` , wobei nur die beiden letzten Schritte bekannt sind.  
  
 OR  
  
-   `/Book/*/Title` ; dabei wird das Platzhalterzeichen (`*`) in der Mitte des Ausdrucks angegeben.  
  
 Der Abfrageprozessor verwendet den primären XML-Index für Abfragen, die [xml-Datentypmethoden](../../t-sql/xml/xml-data-type-methods.md) beinhalten und entweder Skalarwerte oder die XML-Teilbäume vom primären Index selbst wiedergeben. (Dieser Index speichert alle notwendigen Informationen, um die XML-Instanz zu rekonstruieren).  
  
 Die folgende Abfrage gibt z.B. in der `CatalogDescription`-Spalte vom Typ **xml** gespeicherte Zusammenfassungsinformationen aus der `ProductModel`-Tabelle zurück. Die Abfrage gibt <`Summary`>-Informationen nur für die Produktmodelle zurück, deren Katalogbeschreibung auch die <`Features`>-Beschreibung speichert.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")SELECT CatalogDescription.query('  /PD:ProductDescription/PD:Summary') as ResultFROM Production.ProductModelWHERE CatalogDescription.exist ('/PD:ProductDescription/PD:Features') = 1  
```  
  
 Hinsichtlich des primären XML-Indexes werden die einzelnen XML-BLOB-Instanzen in der Basistabelle nicht aufgeteilt, sondern die Zeilen in dem Index, der dem jeweiligen XML-BLOB entspricht, werden sequenziell nach dem in der `exist()`-Methode angegebenen Ausdruck durchsucht. Wenn der Pfad in der Path-Spalte im Index gefunden wird, wird das <`Summary`>-Element mit seinen Unterstrukturen aus dem primären XML-Index abgerufen und in einen XML-BLOB als Ergebnis der `query()`-Methode konvertiert.  
  
 Beachten Sie, dass der primäre XML-Index beim Abrufen einer vollständigen XML-Instanz nicht verwendet wird. Die folgende Abfrage ruft z. B. die gesamte XML-Instanz aus der Tabelle ab, die die Produktionsanweisungen für ein bestimmtes Produktmodell beschreibt.  
  
```  
USE AdventureWorks2012;SELECT InstructionsFROM Production.ProductModel WHERE ProductModelID=7;  
```  
  
## Sekundäre XML-Indizes  
 Wenn Sie die Suchleistung verbessern möchten, können Sie sekundäre XML-Indizes erstellen. Ein primärer XML-Index muss zuerst beendet werden, bevor Sie sekundäre Indizes erstellen können. Die folgenden Typen werden unterschieden:  
  
-   Sekundärer XML PATH-Index  
  
-   Sekundärer XML VALUE-Index  
  
-   Sekundärer XML PROPERTY-Index  
  
 Es folgen einige Richtlinien zum Erstellen eines oder mehrerer sekundärer Indizes:  
  
-   Wenn bei Ihrer Arbeitsauslastung im erheblichen Ausmaß Pfadausdrücke für XML-Spalten verwendet werden, führt der sekundäre XML-Index des Typs PATH wahrscheinlich zu einer Beschleunigung Ihrer Arbeitsauslastung. Der häufigste Fall ist das Verwenden der **exist()**-Methode für XML-Spalten in der WHERE-Klausel von Transact-SQL.  
  
-   Wenn bei Ihrer Arbeitsauslastung mehrere Werte aus einzelnen XML-Instanzen mithilfe von Pfadausdrucken abgerufen werden, kann das Gruppieren der Pfade innerhalb jeder XML-Instanz im PROPERTY-Index nützlich sein. Diese Situation tritt üblicherweise in einem Eigenschaftsbehälterszenario auf, wenn die Eigenschaften eines Objekts abgerufen werden und dessen Primärschlüsselwert bekannt ist.  
  
-   Wenn bei Ihrer Arbeitsauslastung das Abfragen von Werten innerhalb von XML-Instanzen vorkommt, ohne dass dabei die Element- oder Attributnamen bekannt sind, die diese Werte enthalten, können Sie den VALUE-Index erstellen. Diese Situation kommt üblicherweise beim Durchsuchen von descendant-Achsen vor, z.B. bei //author[last-name="Howard"], wo die \<author>-Elemente in jeder beliebigen Ebene der Hierarchie auftreten können. Sie kommt auch bei Abfragen mit Platzhaltern vor, z.B. bei /book [@* = "novel"], wobei die Abfrage nach \<book>-Elementen sucht, die über irgendein Attribut verfügen, das den Wert „novel“ aufweist.  
  
### Sekundärer XML PATH-Index  
 Wenn Ihre Abfragen im Allgemeinen path-Ausdrücke für Spalten des Typs **xml** angeben, beschleunigt ein sekundärer PATH-Index möglicherweise die Suche. Wie bereits zuvor in diesem Thema beschrieben, ist der primäre Index hilfreich, wenn Sie Abfragen verwenden, die die **exist()**-Methode in der WHERE-Klausel angeben. Wenn Sie einen sekundären PATH-Index hinzufügen, können Sie die Suchleistung in solchen Abfragen möglicherweise verbessern.  
  
 Zwar vermeidet ein primärer XML-Index das Aufteilen des XML-BLOBs zur Laufzeit, er bietet jedoch möglicherweise nicht die optimale Leistung für Abfragen, die auf path-Ausdrücken basieren. Da alle Zeilen im primären XML-Index, die einem XML-BLOB entsprechen, sequenziell nach großen XML-Instanzen durchsucht werden, kann diese sequenzielle Suche langsam sein. In diesem Fall kann ein sekundärer Index, der auf den Pfad- und Knotenwerten im primären Index aufbaut, die Indexsuche erheblich beschleunigen. Im sekundären PATH-Index sind die path- und node-Werte Schlüsselspalten, die effizientere Suchläufe beim Suchen nach Pfaden ermöglichen. Der Abfrageoptimierer kann den PATH-Index für Ausdrücke wie die im folgenden Beispiel gezeigten verwenden:  
  
-   `/root/Location` ; gibt nur den Pfad an.  
  
 OR  
  
-   `/root/Location/@LocationID[.="10"]` ; gibt den Pfad- und Knotenwert an.  
  
 Die folgende Abfrage zeigt, in welchen Fällen der PATH-Index hilfreich ist:  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 In der Abfrage entsprechen der path-Ausdruck `/PD:ProductDescription/@ProductModelID` und der Wert `"19"` in der `exist()`-Methode den Schlüsselfeldern des PATH-Indexes. Auf diese Weise wird die direkte Suche im PATH-Index ermöglicht und eine bessere Suchleistung als bei einer sequenziellen Suche nach path-Werten im primären Index bereitgestellt.  
  
### Sekundärer XML VALUE-Index  
 Wenn Abfragen wertbasiert sind, z.B. `/Root/ProductDescription/@*[. = "Mountain Bike"]` oder `//ProductDescription[@Name = "Mountain Bike"]`, und der Pfad nicht vollständig angegeben wird oder einen Platzhalter enthält, erzielen Sie möglicherweise schnellere Ergebnisse, indem Sie einen sekundären XML-Index erstellen, der auf Knotenwerten im primären XML-Index basiert.  
  
 Die Schlüsselspalten des VALUE-Indexes sind der Knotenwert und der Pfad des primären XML-Indexes. Wenn die Arbeitslast das Abfragen von Werten aus XML-Instanzen umfasst, ohne dass die Element- oder Attributnamen bekannt sind, die die Werte enthalten, kann der VALUE-Index hilfreich sein. Der folgende Ausdruck profitiert z. B. vom Vorhandensein eines VALUE-Indexes:  
  
-   `//author[LastName="someName"]` , wobei der Wert des <`LastName`>-Elements bekannt ist, das übergeordnete <`author`>-Element jedoch an beliebiger Position auftreten kann.  
  
-   `/book[@* = "someValue"]` , wobei die Abfrage nach dem <`book`>-Element sucht, das ein Attribut mit dem Wert `"someValue"` aufweist.  
  
 Die folgende Abfrage gibt `ContactID` aus der `Contact`-Tabelle zurück. Die `WHERE`-Klausel gibt einen Filter an, der nach Werten in der `AdditionalContactInfo`-Spalte vom Typ **xml** sucht. Die Kontakt-IDs werden nur zurückgegeben, wenn der entsprechende XML-BLOB mit den zusätzlichen Kontaktinformationen eine bestimmte Rufnummer enthält. Da das <`telephoneNumber`>-Element an beliebiger Position im XML auftreten kann, gibt der path-Ausdruck die descendant-or-self-Achse an.  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS CI,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.exist('//ACT:telephoneNumber/ACT:number[.="111-111-1111"]') = 1  
```  
  
 In dieser Situation ist der Suchwert für <`number`> bekannt, kann jedoch an beliebiger Position in der XML-Instanz als untergeordnetes Element des <`telephoneNumber`>-Elements angezeigt werden. Diese Art der Abfrage kann möglicherweise von einer Indexsuche profitieren, die auf einem bestimmten Wert basiert.  
  
### Sekundärer PROPERTY-Index  
 Abfragen, die einen oder mehrere Werte aus einzelnen XML-Instanzen abrufen, können möglicherweise von einem PROPERTY-Index profitieren. Dieses Szenario tritt ein, wenn Sie Objekteigenschaften mithilfe der **value()**-Methode des Datentyps **xml** abrufen, und der Wert des Primärschlüssels des Objekts bekannt ist.  
  
 Der PROPERTY-Index basiert auf Spalten (PK, Pfad- und Knotenwert) des primären XML-Indexes, wobei PK der Primärschlüssel der Basistabelle ist.  
  
 Die folgende Abfrage ruft z. B. für Produktmodell `19` die folgenden `ProductModelID`- und `ProductModelName`-Attributwerte mithilfe der `value()`-Methode ab. Der PROPERTY-Index kann eine schnellere Ausführung als die Verwendung des primären XML-Indexes oder der anderen sekundären XML-Indizes bereitstellen.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.value('(/PD:ProductDescription/@ProductModelID)[1]', 'int') as ModelID,  
       CatalogDescription.value('(/PD:ProductDescription/@ProductModelName)[1]', 'varchar(30)') as ModelName          
FROM Production.ProductModel     
WHERE ProductModelID = 19  
```  
  
 Mit Ausnahme der Unterschiede, die weiter unten in diesem Thema beschrieben werden, gleicht das Erstellen eines XML-Indexes für eine **xml**-Spalte dem Erstellen eines Indexes für eine Spalte, die nicht den Typ **xml** aufweist. Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-DDL-Anweisungen können zum Erstellen und Verwalten von XML-Indizes verwendet werden:  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
## Abrufen von Informationen zu XML-Indizes  
 XML-Indexeinträge erscheinen in der Katalogsicht sys.indexes, wobei der Index den "Typ" 3 besitzt Die Namensspalte enthält den Namen des XML-Index.  
  
 XML-Indizes sind auch in der Katalogsicht sys.xml_indexes aufgezeichnet. Diese enthält alle Spalten von sys.indexes und einige spezielle Spalten, die für XML-Indizes nützlich sind. Der Wert NULL in der Spalte secondary_type zeigt einen primären XML-Index an; die Werte 'P', 'R' und 'V' stehen für sekundäre PATH-, PROPERTY- bzw. VALUE-XML-Indizes.  
  
 Der von XML-Indizes verwendete Speicherplatz kann in der Tabellenwertfunktion [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) gefunden werden. Sie stellt für alle Indextypen Informationen bereit, wie z. B. zur Anzahl der belegten Datenträgerseiten, zur durchschnittlichen Zeilengröße in Byte und zur Anzahl der Datensätze. Dieses schließt auch XML-Indizes ein. Diese Informationen sind für jede Datenbankpartition verfügbar. XML-Indizes verwenden das Partitionierungsschema und die Partitionierungsfunktion der Basistabelle.  
  
## Siehe auch  
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [XML-Daten &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  