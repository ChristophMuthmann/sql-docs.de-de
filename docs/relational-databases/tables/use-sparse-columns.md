---
title: "Verwenden von Spalten mit geringer Dichte | Microsoft Docs"
ms.custom: ""
ms.date: "03/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Spalten mit geringer Dichte, Beschreibung"
  - "NULL-Spalten"
  - "Spalten mit geringer Dichte"
ms.assetid: ea7ddb87-f50b-46b6-9f5a-acab222a2ede
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# Verwenden von Spalten mit geringer Dichte
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Spalten mit geringer Dichte sind gewöhnliche Spalten, die einen optimierten Speicher für NULL-Werte haben. Spalten mit geringer Dichte reduzieren die Speicherplatzanforderungen von NULL-Werten auf Kosten eines erhöhten Aufwands, um Werte ungleich NULL abzurufen. Verwenden Sie Spalten mit geringer Dichte, wenn dadurch mindestens 20 Prozent bis 40 Prozent Speicherplatz eingespart werden. Spalten mit geringer Dichte und Spaltensätze werden mit der [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) -Anweisung oder der [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) -Anweisung definiert.  
  
 Spalten mit geringer Dichte können mit Spaltensätzen und gefilterten Indizes verwendet werden:  
  
-   Spaltensätze  
  
     Die Anweisungen INSERT, UPDATE und DELETE können anhand des Namens auf die Spalten mit geringer Dichte verweisen. Sie können jedoch auch alle Spalten mit geringer Dichte in einer Tabelle anzeigen und mit ihnen arbeiten, wenn sie zu einer einzelnen XML-Spalte zusammengeschlossen werden. Diese Spalte wird als Spaltensatz bezeichnet. Weitere Informationen zu Spaltensätzen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
-   Gefilterte Indizes  
  
     Da Spalten mit geringer Dichte viele Zeilen mit NULL-Werten haben, sind sie besonders für gefilterte Indizes geeignet. Ein gefilterter Index für eine Spalte mit geringer Dichte kann nur die Zeilen indizieren, die Werte enthalten. Dadurch wird ein kleinerer und effizienterer Index erstellt. Weitere Informationen finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 Mithilfe von Spalten mit geringer Dichte und von gefilterten Indizes können Anwendungen wie [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] große Mengen an benutzerdefinierten Eigenschaften mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] speichern und darauf zugreifen.  
  
## Eigenschaften von Spalten mit geringer Dichte  
 Spalten mit geringer Dichte haben die folgenden Eigenschaften:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verwendet das Schlüsselwort SPARSE in einer Spaltendefinition, um die Speicherung von Werten in dieser Spalte zu optimieren. Wenn der Spaltenwert in einer Zeile der Tabelle NULL ist, belegen die Werte keinen Speicherplatz.  
  
-   Katalogsichten für eine Tabelle, die Spalten mit geringer Dichte aufweist, entsprechen denen einer typischen Tabelle. Diese sys.columns-Katalogsicht enthält eine Zeile für jede Spalte in der Tabelle und einen Spaltensatz, wenn einer definiert wurde.  
  
-   Spalten mit geringer Dichte sind eine Eigenschaft der Speicherebene und keine Eigenschaft der logischen Tabelle. Daher wird eine SELECT…INTO-Anweisung nicht über die Eigenschaft der Spalte mit geringer Dichte in eine neue Tabelle kopiert.  
  
-   Die COLUMNS_UPDATED-Funktion gibt einen **varbinary**-Wert zurück, mit dem alle Spalten, die während einer DML-Aktion aktualisiert wurden, gekennzeichnet werden. Die Bits, die von der COLUMNS_UPDATED-Funktion zurückgegeben werden, lauten folgendermaßen:  
  
    -   Wenn eine Spalte mit geringer Dichte explizit aktualisiert wird, wird das entsprechende Bit für diese Spalte mit geringer Dichte auf 1 festgelegt, und das Bit für den Spaltensatz wird auf 1 festgelegt.  
  
    -   Wenn ein Spaltensatz explizit aktualisiert wird, wird das Bit für den Spaltensatz auf 1 festgelegt, und die Bits für alle Spalten mit geringer Dichte in dieser Tabelle werden auf 1 festgelegt.  
  
    -   Für Einfügevorgänge werden alle Bits auf 1 festgelegt.  
  
     Weitere Informationen zu Spaltensätzen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
 Die folgenden Datentypen können nicht als SPARSE festgelegt werden:  
  
|||  
|-|-|  
|**geography**|**text**|  
|**Geometrie**|**timestamp**|  
|**image**|**Benutzerdefinierte Datentypen**|  
|**ntext**||  
  
## Geschätzte Speicherplatzeinsparungen nach Datentyp  
 Spalten mit geringer Dichte benötigen mehr Speicherplatz für Werte, die ungleich NULL sind, als für identische Daten benötigt wird, die nicht als SPARSE gekennzeichnet wurden. Die folgenden Tabellen geben die Speicherplatznutzung für jeden Datentyp an. Die Spalte **NULL-Prozentwert** gibt an, wie viel Prozent der Daten NULL sein müssen, um Speicherplatzeinsparungen von 40 Prozent zu erzielen.  
  
 **Datentypen fester Länge**  
  
|Datentyp|Bytes ohne geringe Dichte|Bytes mit geringer Dichte|NULL-Prozentsatz|  
|---------------|---------------------|------------------|---------------------|  
|**bit**|0.125|5|98%|  
|**tinyint**|1|5|86%|  
|**smallint**|2|6|76%|  
|**int**|4|8|64%|  
|**bigint**|8|12|52%|  
|**real**|4|8|64%|  
|**float**|8|12|52%|  
|**smallmoney**|4|8|64%|  
|**money**|8|12|52%|  
|**smalldatetime**|4|8|64%|  
|**datetime**|8|12|52%|  
|**uniqueidentifier**|16|20|43%|  
|**Datum**|3|7|69%|  
  
 **Datentypen präzisionsabhängiger Länge**  
  
|Datentyp|Bytes ohne geringe Dichte|Bytes mit geringer Dichte|NULL-Prozentsatz|  
|---------------|---------------------|------------------|---------------------|  
|**datetime2(0)**|6|10|57%|  
|**datetime2(7)**|8|12|52%|  
|**time(0)**|3|7|69%|  
|**time(7)**|5|9|60%|  
|**datetimetoffset(0)**|8|12|52%|  
|**datetimetoffset(7)**|10|14|49%|  
|**decimal/numeric(1,s)**|5|9|60%|  
|**decimal/numeric(38,s)**|17|21|42%|  
|**vardecimal(p,s)**|Verwenden Sie den **decimal** -Typ als konservative Schätzung.|||  
  
 **Datentypen datenabhängiger Länge**  
  
|Datentyp|Bytes ohne geringe Dichte|Bytes mit geringer Dichte|NULL-Prozentsatz|  
|---------------|---------------------|------------------|---------------------|  
|**sql_variant**|Ändert sich mit dem zugrunde liegenden Datentyp|||  
|**varchar** oder **char**|2*|4*|60%|  
|**nvarchar** oder **nchar**|2*|4*+|60%|  
|**varbinary** oder **binary**|2*|4*|60%|  
|**xml**|2*|4*|60%|  
|**hierarchyid**|2*|4*|60%|  
  
 *Die Länge ist gleich dem Mittelwert der im Typ enthaltenen Daten, plus 2 oder 4 Bytes.  
  
## Mehr Verarbeitungsaufwand im Arbeitsspeicher bei Aktualisierung von Spalten mit geringer Dichte  
 Beachten Sie beim Entwerfen von Tabellen mit Spalten mit geringer Dichte, dass beim Aktualisieren von Zeilen für jede Spalte mit geringer Dichte in der Tabelle, die nicht NULL ist, 2 zusätzliche Bytes Verarbeitungsaufwand entstehen. Aufgrund dieses zusätzlichen Speicherbedarfs kann bei Aktualisierungen Fehler 576 auftreten, wenn die Gesamtzeilengröße, einschließlich dieser Vergrößerung im Arbeitsspeicher, 8019 überschreitet und keine Spalten aus der Zeile geschoben werden können.  
  
 Angenommen, eine Tabelle enthält 600 Spalten mit geringer Dichte des Typs bigint. Wenn davon 571 Spalten nicht NULL sind, beträgt die Gesamtgröße auf dem Datenträger 571 * 12 = 6852 Bytes. Nachdem die zusätzliche Zeilengröße und der Header für Spalten mit geringer Dichte hinzugefügt wurden, erhöht sich dies auf etwa 6895 Bytes. Für die Seite sind immer noch etwa 1124 Bytes auf dem Datenträger verfügbar. Dadurch kann der Eindruck entstehen, dass zusätzliche Spalten erfolgreich aktualisiert werden können. Während der Aktualisierung entsteht im Arbeitsspeicher ein zusätzlicher Verarbeitungsaufwand von 2\*(Anzahl der Spalten mit geringer Dichte, die nicht NULL sind). In diesem Beispiel erhöht der zusätzliche Verarbeitungsaufwand – 2 \* 571 = 1.142 Bytes – die Zeilengröße auf dem Datenträger auf etwa 8.037 Bytes. Diese Größe überschreitet die maximal zulässige Größe von 8019 Bytes. Da alle Spalten Datentypen fester Länge aufweisen, können sie nicht von der Zeile geschoben werden. Als Ergebnis tritt beim Aktualisieren der Fehler 576 auf.  
  
## Einschränkungen für die Verwendung von Spalten mit geringer Dichte  
 Spalten mit geringer Dichte können jeden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp annehmen und verhalten sich mit den folgenden Einschränkungen wie andere Spalten:  
  
-   Eine Spalte mit geringer Dichte muss auf NULL festlegbar sein und darf nicht über die ROWGUIDCOL-Eigenschaft oder die IDENTITY-Eigenschaft verfügen. Eine Spalte mit geringer Dichte darf nicht die folgenden Datentypen annehmen: **text**, **ntext**, **image**, **timestamp**, benutzerdefinierter Datentyp, **geometry** oder **geography**; sie darf auch nicht über das FILESTREAM-Attribut verfügen.  
  
-   Eine Spalte mit geringer Dichte kann keinen Standardwert haben.  
  
-   Eine Spalte mit geringer Dichte kann nicht an eine Regel gebunden sein.  
  
-   Obwohl eine berechnete Spalte eine Spalte mit geringer Dichte enthalten kann, kann eine berechnete Spalte nicht als SPARSE markiert werden.  
  
-   Eine Datenmaske kann für eine Spalte mit geringer Dichte definiert werden, jedoch nicht für eine Spalte mit geringer Dichte, die Teil eines Spaltensatzes ist.  
  
-   Eine Spalte mit geringer Dichte kann nicht Teil eines gruppierten Indexes oder eines eindeutigen Primärschlüsselindexes sein. Sowohl persistente als auch nicht persistente berechnete Spalten, die für Spalten mit geringer Dichte definiert wurden, können Teil eines gruppierten Schlüssels sein.  
  
-   Eine Spalte mit geringer Dichte kann nicht als Partitionsschlüssel eines gruppierten Indexes oder eines Heaps verwendet werden. Eine Spalte mit geringer Dichte kann jedoch als Partitionsschlüssel eines nicht gruppierten Indexes verwendet werden.  
  
-   Eine Spalte mit geringer Dichte kann nicht Teil eines benutzerdefinierten Tabellentyps sein, der in Tabellenvariablen und Tabellenwertparametern verwendet wird.  
  
-   Spalten mit geringer Dichte sind inkompatibel mit der Datenkomprimierung. Daher ist es nicht möglich, Spalten geringer Dichte komprimierten Tabellen hinzuzufügen, und Tabellen mit Spalten mit geringer Dichte können nicht komprimiert werden.  
  
-   Um eine Spalte mit geringer Dichte in eine ohne geringe Dichte zu ändern oder um eine Spalte ohne geringe Dichte in eine mit geringer Dichte zu ändern, muss das Speicherformat der Spalte geändert werden. Das SQL Server-Datenbankmodul verwendet die folgende Prozedur, um diese Änderung auszuführen:  
  
    1.  Fügt der Tabelle eine neue Spalte in der neuen Speichergröße und dem neuen Format hinzu.  
  
    2.  Der in der alten Spalte gespeicherte Wert wird für jede Zeile in der Tabelle in die neue Spalte aktualisiert und kopiert.  
  
    3.  Entfernt die alte Spalte aus dem Tabellenschema.  
  
    4.  Erstellt die Tabelle neu (wenn es keinen gruppierten Index gibt) oder erstellt den gruppierten Index neu, um den von der alten Spalte verwendeten Speicherplatz freizugeben.  
  
    > [!NOTE]  
    >  Schritt 2 kann fehlschlagen, wenn die Größe der Daten in der Zeile die maximal zulässige Zeilengröße überschreitet. Diese Größe enthält die Größe der in der alten Spalte gespeicherten Daten und der in der neuen Spalte gespeicherten aktualisierten Daten. Diese Grenze beträgt 8060 Bytes für Tabellen, die keine Spalten mit geringer Dichte enthalten, oder 8018 Bytes für Tabellen, die Spalten mit geringer Dichte enthalten. Dieser Fehler kann auftreten, auch wenn alle in Frage kommenden Spalten aus den Zeilen verschoben wurden.  
  
-   Wenn Sie eine Spalte ohne geringe Dichte in eine Spalte mit geringer Dichte ändern, belegt die Spalte mit geringer Dichte mehr Speicherplatz für Werte ungleich NULL. Wenn eine Zeile die maximale Zeilengrößenbeschränkung fast erreicht hat, kann der Vorgang fehlschlagen.  
  
## SQL Server-Technologien, die Spalten mit geringer Dichte unterstützen  
 In diesem Abschnitt wird beschrieben, wie Spalten mit geringer Dichte in den folgenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Technologien unterstützt werden:  
  
-   Transaktionsreplikation  
  
     Transaktionsreplikation unterstützt die Spalten mit geringer Dichte. Spaltensätze, die zusammen mit Spalten mit geringer Dichte verwendet werden können, werden jedoch nicht unterstützt. Weitere Informationen zu Spaltensätzen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
     Die Replikation des SPARSE-Attributs wird durch eine Schemaoption bestimmt, die mit [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) oder über das Dialogfeld **Artikeleigenschaften** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] festgelegt wird. Frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen keine Spalten mit geringer Dichte. Wenn Sie Daten für eine frühere Version replizieren müssen, legen Sie fest, dass das SPARSE-Attribut nicht repliziert werden sollte.  
  
     Veröffentlichten Tabellen können Sie keine neuen Spalten mit geringer Dichte hinzufügen; Sie können auch nicht die SPARSE-Eigenschaft einer vorhandenen Spalte ändern. Wenn ein solcher Vorgang erforderlich ist, löschen Sie die Veröffentlichung, und erstellen Sie sie erneut.  
  
-   Mergereplikation  
  
     Mergereplikation unterstützt keine Spalten mit geringer Dichte und keine Spaltensätze.  
  
-   Änderungsnachverfolgung  
  
     Änderungsnachverfolgung unterstützt Spalten mit geringer Dichte und Spaltensätze. Wenn ein Spaltensatz in einer Tabelle aktualisiert wird, behandelt die Änderungsnachverfolgung diese als Update für die gesamte Zeile. Es steht keine detaillierte Änderungsnachverfolgung zur Verfügung, um den exakten Satz an Spalten mit geringer Dichte abzurufen, die über den Spaltensatz-Updatevorgang aktualisiert werden. Wenn die Spalten mit geringer Dichte explizit über eine DML-Anweisung aktualisiert werden, arbeitet die Änderungsnachverfolgung wie gewohnt und identifiziert den exakten Satz an geänderten Spalten.  
  
-   Change Data Capture  
  
     Change Data Capture unterstützt Spalten mit geringer Dichte, aber keine Spaltensätze.  
  
-   Die SPARSE-Eigenschaft einer Spalte wird beim Kopieren der Tabelle nicht beibehalten.  
  
## Beispiele  
 In diesem Beispiel enthält eine Dokumenttabelle einen allgemeinen Satz mit der `DocID` -Spalte und der `Title`-Spalte. Die Produktionsgruppe möchte eine `ProductionSpecification` -Spalte und eine `ProductionLocation` -Spalte für alle Produktionsdokumente. Die Marketinggruppe möchte eine `MarketingSurveyGroup` -Spalte für Marketingdokumente. Mit dem Code in diesem Beispiel wird eine Tabelle ausgegeben, in der Spalten mit geringer Dichte verwendet werden. Es werden Zeilen in die Tabelle eingefügt und Daten aus der Tabelle ausgewählt.  
  
> [!NOTE]  
>  Diese Tabelle hat nur fünf Spalten, um die Anzeige und das Lesen zu erleichtern. Sie können optional die Spalten mit geringer Dichte so deklarieren, dass NULL-Werte zulässig sind, wenn die ANSI_NULL_DFLT_ON-Option festgelegt wurde.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStore  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL ) ;  
GO  
  
INSERT DocumentStore(DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStore(DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
 Wenn Sie alle Spalten in der Tabelle auswählen, wird ein herkömmlicher Ergebnissatz zurückgegeben.  
  
```  
SELECT * FROM DocumentStore ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID  Title        ProductionSpecification  ProductionLocation  MarketingSurveyGroup`  
  
 `1      Tire Spec 1  AXZZ217                  27                  NULL`  
  
 `2      Survey 2142  NULL                     NULL                Men 25-35`  
  
 Da die Produktionsabteilung nicht an den Marketingdaten interessiert ist, möchte sie eine Spaltenliste verwenden, die nur die für sie wichtigen Spalten zurückgibt, wie in der folgenden Abfrage gezeigt.  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStore   
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID  Title        ProductionSpecification  ProductionLocation`  
  
 `1      Tire Spec 1  AXZZ217                  27`  
  
## Siehe auch  
 [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  