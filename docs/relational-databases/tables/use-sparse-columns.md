---
title: Verwenden von Spalten mit geringer Dichte | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sparse columns, described
- null columns
- sparse columns
ms.assetid: ea7ddb87-f50b-46b6-9f5a-acab222a2ede
caps.latest.revision: "47"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7e5f2e347053a5814bc1e00365f97c2d305cc064
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="use-sparse-columns"></a>Verwenden von Spalten mit geringer Dichte
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Spalten mit geringer Dichte sind gewöhnliche Spalten, die einen optimierten Speicher für NULL-Werte haben. Spalten mit geringer Dichte reduzieren die Speicherplatzanforderungen von NULL-Werten auf Kosten eines erhöhten Aufwands, um Werte ungleich NULL abzurufen. Verwenden Sie Sparsespalten, wenn dadurch mindestens 20 Prozent bis 40 Prozent Speicherplatz eingespart werden. Spalten mit geringer Dichte und Spaltensätze werden mit der [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) -Anweisung oder der [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) -Anweisung definiert.  
  
 Spalten mit geringer Dichte können mit Spaltensätzen und gefilterten Indizes verwendet werden:  
  
-   Spaltensätze  
  
     Die Anweisungen INSERT, UPDATE und DELETE können anhand des Namens auf die Sparsespalten verweisen. Sie können jedoch auch alle Sparsespalten in einer Tabelle anzeigen und mit ihnen arbeiten, wenn sie zu einer einzelnen XML-Spalte zusammengeschlossen werden. Diese Spalte wird als Spaltensatz bezeichnet. Weitere Informationen zu Spaltensätzen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
-   Gefilterte Indizes  
  
     Da Sparsespalten viele Zeilen mit NULL-Werten haben, sind sie besonders für gefilterte Indizes geeignet. Ein gefilterter Index für eine Sparsespalte kann nur die Zeilen indizieren, die Werte enthalten. Dadurch wird ein kleinerer und effizienterer Index erstellt. Weitere Informationen finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 Mithilfe von Spalten mit geringer Dichte und von gefilterten Indizes können Anwendungen wie [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]große Mengen an benutzerdefinierten Eigenschaften mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]speichern und darauf zugreifen.  
  
## <a name="properties-of-sparse-columns"></a>Eigenschaften von Spalten mit geringer Dichte  
 Spalten mit geringer Dichte haben die folgenden Eigenschaften:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verwendet das Schlüsselwort SPARSE in einer Spaltendefinition, um die Speicherung von Werten in dieser Spalte zu optimieren. Wenn der Spaltenwert in einer Zeile der Tabelle NULL ist, belegen die Werte keinen Speicherplatz.  
  
-   Katalogsichten für eine Tabelle, die Sparsespalten aufweist, entsprechen denen einer typischen Tabelle. Diese sys.columns-Katalogsicht enthält eine Zeile für jede Spalte in der Tabelle und einen Spaltensatz, wenn einer definiert wurde.  
  
-   Spalten mit geringer Dichte sind eine Eigenschaft der Speicherebene und keine Eigenschaft der logischen Tabelle. Daher wird eine SELECT…INTO-Anweisung nicht über die Eigenschaft der Sparsespalte in eine neue Tabelle kopiert.  
  
-   Die COLUMNS_UPDATED-Funktion gibt einen **varbinary** -Wert zurück, mit dem alle Spalten, die während einer DML-Aktion aktualisiert wurden, gekennzeichnet werden. Die Bits, die von der COLUMNS_UPDATED-Funktion zurückgegeben werden, lauten folgendermaßen:  
  
    -   Wenn eine Sparsespalte explizit aktualisiert wird, wird das entsprechende Bit für diese Sparsespalte auf 1 festgelegt, und das Bit für den Spaltensatz wird auf 1 festgelegt.  
  
    -   Wenn ein Spaltensatz explizit aktualisiert wird, wird das Bit für den Spaltensatz auf 1 festgelegt, und die Bits für alle Sparsespalten in dieser Tabelle werden auf 1 festgelegt.  
  
    -   Für Einfügevorgänge werden alle Bits auf 1 festgelegt.  
  
     Weitere Informationen zu Spaltensätzen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
 Die folgenden Datentypen können nicht als SPARSE festgelegt werden:  
  
|||  
|-|-|  
|**geography**|**text**|  
|**Geometrie**|**timestamp**|  
|**image**|**Benutzerdefinierte Datentypen**|  
|**ntext**||  
  
## <a name="estimated-space-savings-by-data-type"></a>Geschätzte Speicherplatzeinsparungen nach Datentyp  
 Spalten mit geringer Dichte benötigen mehr Speicherplatz für Werte, die ungleich NULL sind, als für identische Daten benötigt wird, die nicht als SPARSE gekennzeichnet wurden. Die folgenden Tabellen geben die Speicherplatznutzung für jeden Datentyp an. Die Spalte **NULL-Prozentwert** gibt an, wie viel Prozent der Daten NULL sein müssen, um Speicherplatzeinsparungen von 40 Prozent zu erzielen.  
  
 **Datentypen fester Länge**  
  
|Datentyp|Bytes ohne geringe Dichte|Bytes mit geringer Dichte|NULL-Prozentwert|  
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
  
|Datentyp|Bytes ohne geringe Dichte|Bytes mit geringer Dichte|NULL-Prozentwert|  
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
  
|Datentyp|Bytes ohne geringe Dichte|Bytes mit geringer Dichte|NULL-Prozentwert|  
|---------------|---------------------|------------------|---------------------|  
|**sql_variant**|Ändert sich mit dem zugrunde liegenden Datentyp|||  
|**varchar** oder **char**|2*|4*|60%|  
|**nvarchar** oder **nchar**|2*|4*+|60%|  
|**varbinary** oder **binary**|2*|4*|60%|  
|**xml**|2*|4*|60%|  
|**hierarchyid**|2*|4*|60%|  
  
 *Die Länge ist gleich dem Mittelwert der im Typ enthaltenen Daten, plus 2 oder 4 Bytes.  
  
## <a name="in-memory-overhead-required-for-updates-to-sparse-columns"></a>Mehr Verarbeitungsaufwand im Arbeitsspeicher bei Aktualisierung von Spalten mit geringer Dichte  
 Beachten Sie beim Entwerfen von Tabellen mit Sparsespalten, dass beim Aktualisieren von Zeilen für jede Sparsespalte in der Tabelle, die nicht NULL ist, 2 zusätzliche Bytes Verarbeitungsaufwand entstehen. Aufgrund dieses zusätzlichen Speicherbedarfs kann bei Aktualisierungen Fehler 576 auftreten, wenn die Gesamtzeilengröße, einschließlich dieser Vergrößerung im Arbeitsspeicher, 8019 überschreitet und keine Spalten aus der Zeile geschoben werden können.  
  
 Angenommen, eine Tabelle enthält 600 Sparsespalten des Typs bigint. Wenn davon 571 Spalten nicht NULL sind, beträgt die Gesamtgröße auf dem Datenträger 571 * 12 = 6852 Bytes. Nachdem die zusätzliche Zeilengröße und der Header für Sparsespalten hinzugefügt wurden, erhöht sich dies auf etwa 6895 Bytes. Für die Seite sind immer noch etwa 1124 Bytes auf dem Datenträger verfügbar. Dadurch kann der Eindruck entstehen, dass zusätzliche Spalten erfolgreich aktualisiert werden können. Während der Aktualisierung entsteht im Arbeitsspeicher ein zusätzlicher Verarbeitungsaufwand von 2\*(Anzahl der Sparsespalten, die nicht NULL sind). In diesem Beispiel erhöht der zusätzliche Verarbeitungsaufwand – 2 \* 571 = 1.142 Bytes – die Zeilengröße auf dem Datenträger auf etwa 8.037 Bytes. Diese Größe überschreitet die maximal zulässige Größe von 8019 Bytes. Da alle Spalten Datentypen fester Länge aufweisen, können sie nicht von der Zeile geschoben werden. Als Ergebnis tritt beim Aktualisieren der Fehler 576 auf.  
  
## <a name="restrictions-for-using-sparse-columns"></a>Einschränkungen für die Verwendung von Spalten mit geringer Dichte  
 Spalten mit geringer Dichte können jeden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp annehmen und verhalten sich mit den folgenden Einschränkungen wie andere Spalten:  
  
-   Eine Sparsespalte muss auf NULL festlegbar sein und darf nicht über die ROWGUIDCOL-Eigenschaft oder die IDENTITY-Eigenschaft verfügen. Eine Sparsespalte darf nicht die folgenden Datentypen annehmen: **text**, **ntext**, **image**, **timestamp**, benutzerdefinierter Datentyp, **geometry**oder **geography**; sie darf auch nicht über das FILESTREAM-Attribut verfügen.  
  
-   Eine Sparsespalte kann keinen Standardwert haben.  
  
-   Eine Sparsespalte kann nicht an eine Regel gebunden sein.  
  
-   Obwohl eine berechnete Spalte eine Sparsespalte enthalten kann, kann eine berechnete Spalte nicht als SPARSE markiert werden.  
  
-   Eine Datenmaske kann für eine Sparsespalte definiert werden, jedoch nicht für eine Sparsespalte, die Teil eines Spaltensatzes ist.  
  
-   Eine Sparsespalte kann nicht Teil eines gruppierten Indexes oder eines eindeutigen Primärschlüsselindexes sein. Sowohl persistente als auch nicht persistente berechnete Spalten, die für Sparsespalten definiert wurden, können Teil eines gruppierten Schlüssels sein.  
  
-   Eine Sparsespalte kann nicht als Partitionsschlüssel eines gruppierten Indexes oder eines Heaps verwendet werden. Eine Sparsespalte kann jedoch als Partitionsschlüssel eines nicht gruppierten Indexes verwendet werden.  
  
-   Eine Sparsespalte kann nicht Teil eines benutzerdefinierten Tabellentyps sein, der in Tabellenvariablen und Tabellenwertparametern verwendet wird.  
  
-   Spalten mit geringer Dichte sind inkompatibel mit der Datenkomprimierung. Daher ist es nicht möglich, Sparsespalten komprimierten Tabellen hinzuzufügen, und Tabellen mit Sparsespalten können nicht komprimiert werden.  
  
-   Um eine Spalte mit geringer Dichte in eine ohne geringe Dichte zu ändern oder um eine Spalte ohne geringe Dichte in eine mit geringer Dichte zu ändern, muss das Speicherformat der Spalte geändert werden. Das SQL Server-Datenbankmodul verwendet die folgende Prozedur, um diese Änderung auszuführen:  
  
    1.  Fügt der Tabelle eine neue Spalte in der neuen Speichergröße und dem neuen Format hinzu.  
  
    2.  Der in der alten Spalte gespeicherte Wert wird für jede Zeile in der Tabelle in die neue Spalte aktualisiert und kopiert.  
  
    3.  Entfernt die alte Spalte aus dem Tabellenschema.  
  
    4.  Erstellt die Tabelle neu (wenn es keinen gruppierten Index gibt) oder erstellt den gruppierten Index neu, um den von der alten Spalte verwendeten Speicherplatz freizugeben.  
  
    > [!NOTE]  
    >  Schritt 2 kann fehlschlagen, wenn die Größe der Daten in der Zeile die maximal zulässige Zeilengröße überschreitet. Diese Größe enthält die Größe der in der alten Spalte gespeicherten Daten und der in der neuen Spalte gespeicherten aktualisierten Daten. Diese Grenze beträgt 8060 Bytes für Tabellen, die keine Sparsespalten enthalten, oder 8018 Bytes für Tabellen, die Sparsespalten enthalten. Dieser Fehler kann auftreten, auch wenn alle in Frage kommenden Spalten aus den Zeilen verschoben wurden.  
  
-   Wenn Sie eine Nicht-Sparsespalte in eine Sparsespalte ändern, belegt die Sparsespalte mehr Speicherplatz für Werte ungleich NULL. Wenn eine Zeile die maximale Zeilengrößenbeschränkung fast erreicht hat, kann der Vorgang fehlschlagen.  
  
## <a name="sql-server-technologies-that-support-sparse-columns"></a>SQL Server-Technologien, die Spalten mit geringer Dichte unterstützen  
 In diesem Abschnitt wird beschrieben, wie Sparsespalten in den folgenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Technologien unterstützt werden:  
  
-   Transaktionsreplikation  
  
     Transaktionsreplikation unterstützt die Sparsespalten. Spaltensätze, die zusammen mit Sparsespalten verwendet werden können, werden jedoch nicht unterstützt. Weitere Informationen zu Spaltensätzen finden Sie unter [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md).  
  
     Die Replikation des SPARSE-Attributs wird durch eine Schemaoption bestimmt, die mit [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) oder über das Dialogfeld **Artikeleigenschaften** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]festgelegt wird. Frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen keine Sparsespalten. Wenn Sie Daten für eine frühere Version replizieren müssen, legen Sie fest, dass das SPARSE-Attribut nicht repliziert werden sollte.  
  
     Veröffentlichten Tabellen können Sie keine neuen Sparsespalten hinzufügen; Sie können auch nicht die SPARSE-Eigenschaft einer vorhandenen Spalte ändern. Wenn ein solcher Vorgang erforderlich ist, löschen Sie die Veröffentlichung, und erstellen Sie sie erneut.  
  
-   Mergereplikation  
  
     Mergereplikation unterstützt keine Sparsespalten und keine Spaltensätze.  
  
-   Änderungsnachverfolgung  
  
     Änderungsnachverfolgung unterstützt Sparsespalten und Spaltensätze. Wenn ein Spaltensatz in einer Tabelle aktualisiert wird, behandelt die Änderungsnachverfolgung diese als Update für die gesamte Zeile. Es steht keine detaillierte Änderungsnachverfolgung zur Verfügung, um den exakten Satz an Sparsespalten abzurufen, die über den Spaltensatz-Updatevorgang aktualisiert werden. Wenn die Sparsespalten explizit über eine DML-Anweisung aktualisiert werden, arbeitet die Änderungsnachverfolgung wie gewohnt und identifiziert den exakten Satz an geänderten Spalten.  
  
-   Change Data Capture  
  
     Change Data Capture unterstützt Sparsespalten, aber keine Spaltensätze.  
  
-   Die SPARSE-Eigenschaft einer Spalte wird beim Kopieren der Tabelle nicht beibehalten.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel enthält eine Dokumenttabelle einen allgemeinen Satz mit der `DocID` -Spalte und der `Title`-Spalte. Die Produktionsgruppe möchte eine `ProductionSpecification` -Spalte und eine `ProductionLocation` -Spalte für alle Produktionsdokumente. Die Marketinggruppe möchte eine `MarketingSurveyGroup` -Spalte für Marketingdokumente. Mit dem Code in diesem Beispiel wird eine Tabelle ausgegeben, in der Sparsespalten verwendet werden. Es werden Zeilen in die Tabelle eingefügt und Daten aus der Tabelle ausgewählt.  
  
> [!NOTE]  
>  Diese Tabelle hat nur fünf Spalten, um die Anzeige und das Lesen zu erleichtern. Sie können optional die Sparsespalten so deklarieren, dass NULL-Werte zulässig sind, wenn die ANSI_NULL_DFLT_ON-Option festgelegt wurde.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwenden von Spaltensätzen](../../relational-databases/tables/use-column-sets.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
