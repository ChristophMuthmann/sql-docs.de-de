---
title: "Verwenden von Spaltensätzen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/30/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sparse columns, column sets
- column sets
ms.assetid: a4f9de95-dc8f-4ad8-b957-137e32bfa500
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fece12352dc2691fdab3906a00f8cb64151590b2
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="use-column-sets"></a>Verwenden von Spaltensätzen
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Für Tabellen, die Sparsespalten aufweisen, können Sie einen Spaltensatz festlegen, der alle Sparsespalten in der Tabelle zurückgibt. Bei einem Spaltensatz handelt es sich um eine nicht typisierte XML-Darstellung, die alle Sparsespalten einer Tabelle in einer strukturierten Ausgabe kombiniert. Wie auch berechnete Spalten werden Spaltensätze nicht physisch in der Tabelle gespeichert. Der Unterschied zwischen einem Spaltensatz und einer berechneten Spalte besteht darin, dass der Spaltensatz direkt aktualisiert werden kann.  
  
 Verwenden Sie Spaltensätze, wenn die Tabelle eine große Anzahl an Spalten enthält und es sehr aufwändig ist, jede Spalte einzeln zu verarbeiten. Außerdem verbessert sich die Anwendungsleistung, wenn zum Auswählen und Einfügen von Daten bei Tabellen mit sehr vielen Spalten Spaltensätze verwendet werden. Die Leistung von Spaltensätzen kann jedoch beeinträchtigt werden, wenn für die Spalten in der Tabelle sehr viele Indizes definiert werden. Das liegt daran, dass in diesem Fall für einen Ausführungsplan mehr Arbeitsspeicher erforderlich ist.  
  
 Zum Definieren eines Spaltensatzes verwenden Sie die Schlüsselwörter *<Spaltensatzname>* FOR ALL_SPARSE_COLUMNS in der [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)-Anweisung oder in der [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)-Anweisung.  
  
## <a name="guidelines-for-using-column-sets"></a>Richtlinien zum Verwenden von Spaltensätzen  
 Wenn Sie Spaltensätze verwenden, beachten Sie die folgenden Richtlinien:  
  
-   Spalten mit geringer Dichte und ein Spaltensatz können als Teil der gleichen Anweisung hinzugefügt werden.  
  
-   Sie können einer Tabelle, die bereits Sparsespalten enthält, keinen Spaltensatz hinzufügen.  
  
-   Der Spaltensatz kann nicht geändert werden. Um einen Spaltensatz zu ändern, müssen Sie die Sparsespalten und den Spaltensatz neu erstellen.  
  
-   Sie können einen Spaltensatz Tabellen hinzufügen, die keine Sparsespalten enthalten. Wenn Sie der Tabelle zu einem späteren Zeitpunkt Sparsespalten hinzufügen, werden diese im Spaltensatz angezeigt.  
  
-   Es ist nur ein Spaltensatz pro Tabelle zulässig.  
  
-   Spaltensätze sind optional, d. h. zur Verwendung von Sparsespalten nicht zwingend erforderlich.  
  
-   Für einen Spaltensatz können keine Einschränkungen oder Standardwerte definiert werden.  
  
-   Berechnete Spalten können keine Spaltensatz-Spalten enthalten.  
  
-   Verteilte Abfragen werden von Tabellen mit Spaltensätzen nicht unterstützt.  
  
-   Die Replikation unterstützt Spaltensätze nicht.  
  
-   Change Data Capture unterstützt Spaltensätze nicht.  
  
-   Ein Spaltensatz darf nicht Teil irgendeiner Art von Index sein. Dies gilt auch für XML-Indizes, Volltextindizes und indizierte Sichten. Ein Spaltensatz kann einem Index nicht als eingeschlossene Spalte hinzugefügt werden.  
  
-   Ein Spaltensatz darf nicht im Filterausdruck eines gefilterten Indexes oder einer gefilterten Statistik verwendet werden.  
  
-   Ein in einer Sicht enthaltener Spaltensatz wird als XML-Spalte angezeigt.  
  
-   Ein Spaltensatz darf nicht in einer indizierten Sichtdefinition enthalten sein.  
  
-   Partitionierte Sichten, die Tabellen mit Spaltensätzen enthalten, können aktualisiert werden, wenn die Sparsespalten in der partitionierten Sicht mit Namen angegeben sind. Eine partitionierte Sicht kann nicht aktualisiert werden, wenn sie lediglich einen Verweis auf den Spaltensatz enthält.  
  
-   Abfragebenachrichtigungen, die auf Spaltensätze verweisen, sind nicht zulässig.  
  
-   Für XML-Daten gilt eine Größenbeschränkung von 2 GB. Wenn die gesamte Datengröße aller Sparsespalten ungleich NULL in einer Zeile diesen Wert überschreitet, wird für die Abfrage bzw. den DML-Vorgang ein Fehler ausgegeben.  
  
-   Informationen zu den Daten, die von der Funktion COLUMNS_UPDATED zurückgegeben werden, finden Sie unter [Verwenden von Spalten mit geringer Dichte](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="guidelines-for-selecting-data-from-a-column-set"></a>Richtlinien zum Auswählen von Daten aus einem Spaltensatz  
 Beim Auswählen von Daten aus einem Spaltensatz sind die folgenden Richtlinien zu beachten:  
  
-   Grundsätzlich handelt es sich bei einem Spaltensatz um eine aktualisierbare, berechnete XML-Spalte, die einen Satz zugrunde liegender relationaler Spalten in einer XML-Darstellung zusammenfasst. Der Spaltensatz unterstützt nur die ALL_SPARSE_COLUMNS-Eigenschaft. Diese Eigenschaft dient zur Zusammenfassung aller Werte ungleich NULL in allen Sparsespalten für eine bestimmte Zeile.  
  
-   Im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Tabellen-Editor werden Spaltensätze als bearbeitbare XML-Felder angezeigt. Definieren Sie Spaltensätze im folgenden Format:  
  
    ```  
    <column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...  
    ```  
  
     Beispiele für Spaltensatzwerte:  
  
    -   `<sparseProp1>10</sparseProp1><sparseProp3>20</sparseProp3>`  
  
    -   `<DocTitle>Bicycle Parts List</DocTitle><Region>West</Region>`  
  
-   Spalten mit geringer Dichte, die NULL-Werte enthalten, werden in der XML-Darstellung des Spaltensatzes nicht berücksichtigt.  
  
> [!WARNING]  
>  Durch das Hinzufügen eines Spaltensatzes ändert sich das Verhalten von SELECT *-Abfragen. Statt der einzelnen Sparsespalten wird der Spaltensatz als XML-Spalte zurückgegeben. Schema-Designer und Softwareentwickler müssen darauf achten, dass der Code vorhandener Anwendungen hierdurch nicht gestört wird.  
  
## <a name="inserting-or-modifying-data-in-a-column-set"></a>Einfügen und Ändern von Daten in einem Spaltensatz  
 Zur Änderung von Daten in einem Spaltensatz verwenden Sie die Namen der einzelnen Spalten. Sie können auch auf den Namen des Spaltensatzes verweisen und die Werte des Spaltensatzes angeben, indem Sie das XML-Format des Spaltensatzes verwenden. Spalten mit geringer Dichte können in der XML-Spalte in beliebiger Reihenfolge angezeigt werden.  
  
 Wenn Sie die Werte von Sparsespalten mit dem XML-Spaltensatz einfügen bzw. aktualisieren, werden die Werte, die in die zugrunde liegenden Sparsespalten eingefügt werden, automatisch vom **xml** -Datentyp konvertiert. Bei numerischen Spalten werden leere Werte im XML-Format in leere Zeichenfolgen konvertiert. Hierdurch wird der Wert 0 in die numerische Spalte eingefügt, wie im folgenden Beispiel gezeigt.  
  
```  
CREATE TABLE t (i int SPARSE, cs xml column_set FOR ALL_SPARSE_COLUMNS);  
GO  
INSERT t(cs) VALUES ('<i/>');  
GO  
SELECT i FROM t;  
GO  
```  
  
 In diesem Beispiel wurde kein Wert für die Spalte `i`angegeben, und der Wert `0` wurde eingefügt.  
  
## <a name="using-the-sqlvariant-data-type"></a>Verwenden des sql_variant-Datentyps  
 Der **sql_variant** -Datentyp kann mehrere unterschiedliche Datentypen speichern, z.B. **int**, **char**und **date**. Spaltensätze geben Datentypinformationen zu Dezimalstellen, Genauigkeit und Gebietsschema, die mit einem **sql_variant** -Wert verknüpft sind, in der generierten XML-Spalte als Attribute aus. Wenn Sie versuchen, diese Attribute in einer benutzerdefinierten XML-Anweisung als Eingabe für einen INSERT- oder UPDATE-Vorgang für einen Spaltensatz bereitzustellen, sind einige dieser Attribute obligatorisch, und anderen wird ein Standardwert zugewiesen. In der folgenden Tabelle sind die Datentypen und die Standardwerte aufgeführt, die vom Server generiert werden, wenn der Wert nicht angegeben wird.  
  
|Datentyp|localeID*|sqlCompareOptions|sqlCollationVersion|SqlSortId|Maximale Länge|Genauigkeit|Dezimalstellen|  
|---------------|----------------|-----------------------|-------------------------|---------------|--------------------|---------------|-----------|  
|**char**, **varchar**, **binary**|-1|'Standardwert'|0|0|8000|Nicht zutreffend**|Nicht verfügbar|  
|**nvarchar**|-1|'Standardwert'|0|0|4000|Nicht verfügbar|Nicht verfügbar|  
|**decimal**, **float**, **real**|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|18|0|  
|**integer**, **bigint**, **tinyint**, **smallint**|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|  
|**datetime2**|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|7|  
|**datetime offset**|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|7|  
|**datetime**, **date**, **smalldatetime**|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|  
|**money**, **smallmoney**|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|  
|**Uhrzeit**|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|Nicht verfügbar|7|  
  
 \*  „localeID -1“ ist das Standardgebietsschema. Das englischsprachige Gebietsschema ist 1033.  
  
 **  Nicht zutreffend = Bei einem SELECT-Vorgang für den Spaltensatz werden für diese Attribute keine Werte ausgegeben. Gibt eine Fehlermeldung zurück, wenn für dieses Attribut von dem Aufrufer in der für einen Spaltensatz in einem INSERT- oder UPDATE-Vorgang bereitgestellten XML-Darstellung ein Wert angegeben wird.  
  
## <a name="security"></a>Security  
 Das Sicherheitsmodell für Spaltensätze funktioniert ähnlich wie das Sicherheitsmodell zwischen Tabellen und Spalten. Spaltensätze können als Minitabellen visualisiert werden, und die SELECT-Vorgänge entsprechen den SELECT *-Vorgängen für diese Minitabellen. Bei der Beziehung zwischen Spaltensatz und Sparsespalten handelt es sich jedoch nicht um einen Container, sondern um eine Gruppenbeziehung. Das Sicherheitsmodell prüft die Sicherheit der Spaltensatz-Spalte, wobei die DENY-Vorgänge für die zugrunde liegenden Sparsespalten berücksichtigt werden. Für das Sicherheitsmodell gelten die folgenden zusätzlichen Eigenschaften:  
  
-   Wie bei anderen Spalten in der Tabelle können Sicherheitsberechtigungen für den Spaltensatz erteilt und aufgehoben werden.  
  
-   Der GRANT- bzw. REVOKE-Vorgang für SELECT-, INSERT-, UPDATE-, DELETE- und REFERENCES-Berechtigungen für einen Spaltensatz wirkt sich nicht auf die zugrunde liegenden Spalten aus. Dieser Vorgang gilt nur für die Verwendung der Spaltensatz-Spalte. Die DENY-Berechtigung für einen Spaltensatz gilt jedoch auch für die zugrunde liegenden Sparsespalten.  
  
-   Zur Ausführung von SELECT-, INSERT-, UPDATE- und DELETE-Anweisungen für den Spaltensatz muss der Benutzer über die entsprechenden Berechtigungen für den Spaltensatz und über die entsprechenden Berechtigungen für alle Sparsespalten in der Tabelle verfügen. Da der Spaltensatz alle Sparsespalten in der Tabelle darstellt, müssen Sie über Berechtigungen für alle diese Spalten verfügen, einschließlich Spalten, die Sie nicht ändern.  
  
-   Durch die Ausführung einer REVOKE-Anweisung für eine Sparsespalte bzw. einen Spaltensatz wird die Sicherheitseinstellung auf die Einstellung des übergeordneten Objekts zurückgesetzt.  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen enthält eine Dokumenttabelle die gemeinsamen Spalten `DocID` und `Title`. Die Produktionsgruppe möchte eine `ProductionSpecification` -Spalte und eine `ProductionLocation` -Spalte für alle Produktionsdokumente. Die Marketinggruppe möchte eine `MarketingSurveyGroup` -Spalte für Marketingdokumente.  
  
### <a name="a-creating-a-table-that-has-a-column-set"></a>A. Erstellen einer Tabelle mit einem Spaltensatz  
 Im folgenden Beispiel wird eine Tabelle erstellt, die Sparsespalten und den Spaltensatz `SpecialPurposeColumns` enthält. Im Beispiel werden zwei Zeilen in die Tabelle eingefügt, und anschließend werden Daten aus der Tabelle ausgewählt.  
  
> [!NOTE]  
>  Diese Tabelle hat nur fünf Spalten, um die Anzeige und das Lesen zu erleichtern.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStoreWithColumnSet  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL,  
     MarketingProgramID int SPARSE NULL,  
     SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS);  
GO  
```  
  
### <a name="b-inserting-data-to-a-table-by-using-the-names-of-the-sparse-columns"></a>B. Einfügen von Daten in eine Tabelle anhand der Namen der Sparsespalten  
 In den folgenden Beispielen werden zwei Zeilen in die in Beispiel A erstellte Tabelle eingefügt. Hierzu werden die Namen der Sparsespalten verwendet, und auf den Spaltensatz wird nicht verwiesen.  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStoreWithColumnSet (DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
### <a name="c-inserting-data-to-a-table-by-using-the-name-of-the-column-set"></a>C. Einfügen von Daten in eine Tabelle anhand des Spaltensatznamens  
 Im folgenden Beispiel wird eine dritte Zeile in die in Beispiel A erstellte Tabelle eingefügt. Diesmal werden die Namen der Sparsespalten nicht verwendet. Stattdessen wird der Name des Spaltensatzes verwendet, und der INSERT-Vorgang gibt die Werte für zwei der vier Sparsespalten im XML-Format zurück.  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, SpecialPurposeColumns)  
VALUES (3, 'Tire Spec 2', '<ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>');  
GO  
```  
  
### <a name="d-observing-the-results-of-a-column-set-when-select--is-used"></a>D. Prüfen der Ergebnisse eines Spaltensatzes bei Verwendung von SELECT *  
 Im folgenden Beispiel werden alle Spalten der Tabelle ausgewählt, die einen Spaltensatz enthält. Es wird eine XML-Spalte mit den kombinierten Werten der Sparsespalten zurückgegeben. Die Sparsespalten werden nicht einzeln zurückgegeben.  
  
```  
SELECT DocID, Title, SpecialPurposeColumns FROM DocumentStoreWithColumnSet ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1      Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `2      Survey 2142  <MarketingSurveyGroup>Men 25 - 35</MarketingSurveyGroup>`  
  
 `3      Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### <a name="e-observing-the-results-of-selecting-the-column-set-by-name"></a>E. Prüfen der Ergebnisse der Auswahl des Spaltensatzes nach Name  
 Da die Produktionsabteilung nicht an den Marketingdaten interessiert ist, wird in diesem Beispiel eine `WHERE` -Klausel zur Einschränkung der Ausgabe hinzugefügt. In diesem Beispiel wird der Name des Spaltensatzes verwendet.  
  
```  
SELECT DocID, Title, SpecialPurposeColumns  
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1     Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `3     Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### <a name="f-observing-the-results-of-selecting-sparse-columns-by-name"></a>F. Prüfen der Ergebnisse der Auswahl von Sparsespalten nach Name  
 Auch wenn eine Tabelle einen Spaltensatz enthält, können Sie eine Abfrage anhand der einzelnen Spaltennamen durchführen, wie im folgenden Beispiel gezeigt.  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        ProductionSpecification ProductionLocation`  
  
 `1     Tire Spec 1  AXZZ217                 27`  
  
 `3     Tire Spec 2  AXW9R411                38`  
  
### <a name="g-updating-a-table-by-using-a-column-set"></a>G. Aktualisieren einer Tabelle mithilfe eines Spaltensatzes  
 Im folgenden Beispiel wird der dritte Datensatz mit neuen Werten für beide Sparsespalten aktualisiert, die von der Zeile verwendet werden.  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification><ProductionLocation>38</ProductionLocation>'  
WHERE DocID = 3 ;  
GO  
```  
  
> [!IMPORTANT]  
>  Mit einer UPDATE-Anweisung, die einen Spaltensatz verwendet, werden alle Sparsespalten in der Tabelle aktualisiert. Spalten mit geringer Dichte, auf die nicht verwiesen wird, werden auf NULL festgelegt.  
  
 Im folgenden Beispiel wird der dritte Datensatz aktualisiert, es wird jedoch nur der Wert für eine der beiden Spalten mit Werten angegeben. Die zweite Spalte `ProductionLocation` ist nicht in der `UPDATE` -Anweisung enthalten und wird auf NULL aktualisiert.  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification>'  
WHERE DocID = 3 ;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwenden von Spalten mit geringer Dichte](../../relational-databases/tables/use-sparse-columns.md)  
  
  
