---
title: Erste Schritte mit der Volltextsuche | Microsoft-Dokumentation
ms.date: 08/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e87ac827013d4aa9abff8a0fb66ac3c8fc9bce62
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="get-started-with-full-text-search"></a>Erste Schritte mit der Volltextsuche
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Bei SQL Server-Datenbanken werden die Volltexte standardmäßig aktiviert. Bevor Sie Volltextabfragen jedoch ausführen können, müssen Sie einen Volltextkatalog und einen Volltextindex für die Tabellen oder indizierten Sichten, die Sie suchen möchten, erstellen.

## <a name="set-up-full-text-search-in-two-steps"></a>Volltextsuche in zwei Schritten einrichten
Es gibt zwei grundlegende Schritte zum Einrichten der Volltextsuche:  
1.  Erstellen eines Volltextkatalogs.  
2.  Erstellen eines Volltextindex für Tabellen oder eine indizierte Sicht, die Sie durchsuchen möchten. 

Jeder Volltextindex muss einem Volltextkatalog angehören. Sie können einen separaten Textkatalog für jeden Volltextindex erstellen oder einem Katalog mehrere Volltextindizes zuordnen. Ein Volltextkatalog ist ein virtuelles Objekt und gehört keiner Dateigruppe an. Der Katalog ist ein logisches Konzept, das auf eine Gruppe von Volltextindizes verweist.

> [!NOTE]
> Diese Schritte setzen voraus, dass Sie die optionalen Komponenten der Volltextsuche während der Installation von SQL Server installiert haben. Wenn dies nicht der Fall ist, müssen Sie SQL Server-Setup erneut ausführen, um sie hinzuzufügen.  

## <a name="set-up-full-text-search-with-a-wizard"></a>Einrichten der Volltextsuche mithilfe eines Assistenten 
 
Zum Einrichten der Volltextsuche mithilfe eines Assistenten finden Sie unter [Verwenden des Volltextindizierungs-Assistenten](../../relational-databases/search/use-the-full-text-indexing-wizard.md) weitere Informationen.

## <a name="set-up-full-text-search-with-transact-sql"></a>Einrichten der Volltextsuche mit Transact-SQL 
 Im folgenden zweiteiligen Beispiel wird ein Volltextkatalog mit Namen `AdvWksDocFTCat` in der AdventureWorks-Datenbank erstellt, und anschließend wird ein Volltextindex für die Tabelle `Document` in der Beispieldatenbank erstellt. Diese Anweisung erstellt den Volltextkatalog im bei der Installation angegebenen Standardverzeichnis. Der Ordner mit dem Namen `AdvWksDocFTCat` befindet sich im Standardverzeichnis.  
  
1.  Im Beispiel wird eine `AdvWksDocFTCat`CREATE FULLTEXT CATALOG [-Anweisung verwendet, um einen Volltextkatalog mit dem Namen](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) zu erstellen:  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
    Weitere Informationen finden Sie unter [Erstellen und Verwalten von Volltextkatalogen](../../relational-databases/search/create-and-manage-full-text-catalogs.md).
 
2.  Bevor Sie einen Volltextindex für die Document-Tabelle erstellen können, müssen Sie sicherstellen, dass die Tabelle über einen eindeutigen, einspaltigen Index verfügt, der keine NULL-Werte zulässt. Die folgende [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) -Anweisung erstellt in der DocumentID-Spalte der Document-Tabelle den eindeutigen `ui_ukDoc`-Index:  
  
    ```sql 
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  

3.  Nachdem Sie einen eindeutigen Schlüssel erstellt haben, können Sie in der `Document` -Tabelle einen Volltextindex erstellen, indem Sie die folgende [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) -Anweisung verwenden.  
  
    ```sql  
    CREATE FULLTEXT INDEX ON Production.Document  
    (  
        Document                         --Full-text index column name   
            TYPE COLUMN FileExtension    --Name of column that contains file type information  
            Language 2057                 --2057 is the LCID for British English  
    )  
    KEY INDEX ui_ukDoc ON AdvWksDocFTCat --Unique index  
    WITH CHANGE_TRACKING AUTO            --Population type;  
    GO  
  
    ```  
  
     Die in diesem Beispiel definierte TYPE COLUMN gibt die Typspalte in der Tabelle an, die den Typ des Dokuments in der Spalte Document (binäre Spalte) enthält. In der Typspalte wird die vom Benutzer angegebene Dateierweiterung – „.doc“, „.xls“ usw. – für das Dokument der betreffenden Zeile gespeichert. Das Volltextmodul verwendet die Erweiterung einer Zeile, um den richtigen Filter für die Analyse der Daten in dieser Zeile aufzurufen. Nachdem der Filter die binären Daten der Zeile analysiert hat, analysiert die angegebene Worttrennung den Inhalt. (In diesem Beispiel wird die Worttrennung für britisches Englisch verwendet.) Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md).  

    Weitere Informationen finden Sie unter [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md).

##  <a name="options"></a> Wählen Sie Optionen für einen Volltextindex aus 
  
### <a name="choose-a-language"></a>Wählen Sie eine Sprache  
 Weitere Informationen zum Auswählen der Sprache für die Spalte finden Sie unter [Auswählen einer Sprache beim Erstellen eines Volltextindex](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
### <a name="choose-a-filegroup"></a>Wählen Sie eine Dateigruppe  
 Das Erstellen eines Volltextindex ist ziemlich E/A-intensiv. Zusammenfassend besteht es aus dem Lesen von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und dem anschließenden Weitergeben der gefilterten Daten an den Volltextindex. Die beste Vorgehensweise besteht darin, einen Volltextindex in der Datenbankdateigruppe anzuordnen, die am besten für die Optimierung der E/A-Leistung geeignet ist, oder ordnen Sie die Volltextindizes in einer anderen Dateigruppe auf einem anderen Volume an.
  
### <a name="choose-a-full-text-catalog"></a>Wählen Sie einen Volltextkatalog   
 
 Es ist zu empfehlen, Tabellen mit denselben Updatemerkmalen (z. B. geringe Anzahl an Änderungen gegenüber einer großen Anzahl an Änderungen oder Tabellen, die regelmäßig zu bestimmten Tageszeiten geändert werden) zu gruppieren und demselben Volltextkatalog zuzuweisen. Indem Sie Zeitpläne für Volltextkataloge einrichten, bleiben Volltextindizes mit den Tabellen synchronisiert, ohne dass sich dies in Phasen umfangreicher Datenbankaktivitäten negativ auf die Ressourcenverwendung des Datenbankservers auswirkt.  
  
 Beachten Sie die folgenden Richtlinien:  
  
-   Wenn Sie eine Tabelle mit mehreren Millionen Zeilen indizieren, sollten Sie die Tabelle einem eigenen Volltextkatalog zuweisen.  
  
-   Berücksichtigen Sie sowohl den Umfang der Änderungen in den Tabellen, die mit einem Volltextindex indiziert werden, als auch die Gesamtzahl der Tabellenzeilen. Wenn die Gesamtzahl der geänderten Zeilen zusammen mit der Anzahl an Zeilen, die während der letzten Volltextauffüllung in der Tabelle enthalten waren, mehrere Millionen umfasst, sollten Sie die Tabelle einem eigenen Volltextkatalog zuweisen.  

### <a name="associate-a-unique-index"></a>Ordnen Sie einen eindeutigen Index zu
Wählen Sie stets den kleinsten eindeutigen Index, der verfügbar ist, als eindeutigen Volltextschlüssel aus (ein 4 Byte umfassender, auf dem integer-Datentyp basierender Index ist am besten geeignet). Hierdurch können Sie den Umfang der Ressourcen, die vom [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search-Dienst im Dateisystem benötigt werden, erheblich reduzieren. Wenn Sie einen breiten Primärschlüssel verwenden (mehr als 100 Byte), sollten Sie erwägen, als eindeutigen Volltextschlüssel einen anderen eindeutigen Index in der Tabelle auszuwählen (oder einen anderen eindeutigen Index zu erstellen). Andernfalls kann die Volltextauffüllung nicht mehr fortgesetzt werden, wenn der eindeutige Volltextschlüssel die maximal zulässige Größe erreicht (900 Byte).  
 
### <a name="associate-a-stoplist"></a>Zuordnen einer Stoppliste   
  Eine *Stoppliste* ist eine Liste von Stoppwörtern. Stoppwörter werden auch als Füllwörter bezeichnet. Jedem Volltextindex ist eine Stoppliste zugeordnet, und die Wörter der Stoppliste werden auf Volltextabfragen des Indexes angewendet. Standardmäßig ist der Systemstoppliste ein neuer Volltextindex zugeordnet. Sie können auch eine eigene Stoppliste erstellen und verwenden.   
  
 Die folgende [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung erstellt z.B. durch Kopieren aus der Systemstoppliste eine neue Volltext-Stoppliste mit dem Namen „myStoplist3“:  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 Die folgende [-Anweisung](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] ändert eine Stoppliste mit dem Namen „myStoplist“, indem zuerst für Spanisch und dann für Französisch das Wort „en“ hinzugefügt wird:  
  
```sql  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).

## <a name="update-a-full-text-index"></a>Aktualisieren Sie einen Volltextindex  
 Volltextindizes können wie reguläre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Indizes automatisch aktualisiert werden, sobald Daten in den zugeordneten Tabellen geändert werden. Dies ist das Standardverhalten. Alternativ dazu können Sie die Volltextindizes auch manuell auf dem aktuellen Stand halten oder in bestimmten Abständen aktualisieren lassen. Auffüllen eines Volltextindex kann zeitaufwändig und ressourcenintensiv sein. Aus diesem Grund wird das Indexupdate meist als asynchroner Vorgang durchgeführt, der im Hintergrund ausgeführt wird und den Volltextindex jeweils nach Änderungen in der Basistabelle aktualisiert. 
 
Das sofortige Aktualisieren eines Volltextindex nach jeder Änderung in der Basistabelle ist auch ressourcenintensiv. Bei sehr hohen Update-, Einfügungs- und Löschungsraten kann es deshalb zu einer Verringerung der Abfrageleistung kommen. In diesem Fall sollten Sie erwägen, eine manuelle Änderungsnachverfolgung und entsprechende Updates zu planen, um die zahlreichen Änderungen von Zeit zu Zeit zu bearbeiten, anstatt mit den Abfragen um Ressourcen zu wetteifern.  
  
Weitere Informationen finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md). 

## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie die SQL Server-Volltextsuche eingerichtet haben, können Sie mit dem Ausführen von Volltextabfragen beginnen. Weitere Informationen finden Sie unter [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md).
