---
title: "Erste Schritte mit der Volltextsuche | Microsoft Docs"
ms.date: "08/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Volltextkataloge [SQL Server], erstellen"
  - "Volltextindizes [SQL Server], erstellen"
  - "Volltextsuche [SQL Server], Informationen zu"
  - "Volltextsuche [SQL Server], einrichten"
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
caps.latest.revision: 76
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 72
---
# Erste Schritte mit der Volltextsuche
Die Volltextsuche unterstützt mehrere Sprachen durch die Verwendung der folgenden *linguistischen Komponenten*: Wörtertrennungen und Wortstammerkennungen, Stopplisten mit Stoppwörtern (auch als Füllwörter bezeichnet) und Thesaurusdateien. Für Thesaurusdateien (und in einigen Fällen auch für Stopplisten) ist die Konfiguration durch den Datenbankadministrator erforderlich. Eine bestimmte Thesaurusdatei unterstützt alle Volltextindizes, die die entsprechende Sprache verwenden, und eine bestimmte Stopliste kann einer beliebigen Anzahl von Volltextindizes zugeordnet werden.  
 
Für SQL Server-Datenbanken ist die Volltextsuche standardmäßig aktiviert, aber Sie müssen zuerst einen [Volltextkatalog erstellen](https://msdn.microsoft.com/library/bb326035.aspx) sowie einen Volltextindex für Tabellen oder indizierte Sichten erstellen, die Sie durchsuchen möchten.
 
 ## Schrittweise Anweisungen 
 
 Wechseln Sie zum Thema [Verwenden des Volltextindizierungs-Assistenten](https://msdn.microsoft.com/library/ms180091.aspx), wenn Sie schrittweise Anweisungen erhalten möchten.

In diesem Thema werden Aspekte, Beispiele und Links zu anderen Themen behandelt.
##  <a name="configure"></a> Planen des Setups

Es gibt zwei grundlegende Schritte zum Konfigurieren von Tabellenspalten in einer Datenbank für die Volltextsuche:  
  
- Erstellen eines Volltextkatalogs.  
  
- Erstellen eines Volltextindex für Tabellen oder eine indizierte Sicht, die Sie durchsuchen möchten. 

     Ein Volltextindex ist ein besonderer Typ eines tokenbasierten funktionellen Index, der durch das Volltextmodul erstellt und verwaltet wird. Um eine Volltextsuche für eine Tabelle oder Sicht erstellen zu können, muss ein eindeutiger, einspaltiger Index vorhanden sein, der keine NULL-Werte zulässt. Das Volltextmodul benötigt diesen eindeutigen Index, um jeder Zeile in der Tabelle einen eindeutigen, komprimierbaren Schlüssel zuzuordnen. Ein Volltextindex kann Spalten vom Typ **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** und **varbinary(max)** enthalten. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md).   
  
     Jeder Volltextindex muss einem Volltextkatalog angehören. Sie können einen separaten Textkatalog für jeden Volltextindex erstellen oder einem Katalog mehrere Volltextindizes zuordnen. Ein Volltextkatalog ist ein virtuelles Objekt und gehört keiner Dateigruppe an. Der Katalog ist ein logisches Konzept, das auf eine Gruppe von Volltextindizes verweist.  
  

 Unterschiede zwischen Volltextindizes und regulären SQL Server-Indizes:.  
  
|Volltextindizes|Reguläre SQL Server-Indizes|  
|------------------------|--------------------------------|  
|Nur ein Volltextindex pro Tabelle zulässig.|Mehrere reguläre Indizes pro Tabelle zulässig.|  
|Das Hinzufügen von Daten zu Volltextindizes, *Auffüllen* genannt, muss angefordert werden. Dies erfolgt entweder mithilfe eines Zeitplans bzw. mithilfe einer speziellen Anforderung oder automatisch beim Hinzufügen neuer Daten.|Automatisches Update, wenn die Daten, auf denen der Index basiert, eingefügt, aktualisiert oder gelöscht werden.|  
|Gruppiert innerhalb derselben Datenbank zu einem oder mehreren Volltextkatalogen.|Nicht gruppiert.|  
    
##  <a name="options"></a> enthalten  
  
### Sprache für Spalte  
 Weitere Informationen zum Auswählen der Sprache für die Spalte finden Sie unter [Auswählen einer Sprache beim Erstellen eines Volltextindex](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
### Auswählen einer Dateigruppe für einen Volltextindex  
 Die Erstellung eines Volltextindex ist ein ziemlich E/A-intensiver Vorgang (grob gesprochen besteht es aus dem Lesen von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und dem anschließenden Weitergeben der gefilterten Daten an den Volltextindex). Die beste Vorgehensweise besteht darin, einen Volltextindex in der Datenbankdateigruppe anzuordnen, die am besten für die Optimierung der E/A-Leistung geeignet ist, oder ordnen Sie die Volltextindizes in einer anderen Dateigruppe auf einem anderen Volume an.  
  
 Es wird empfohlen, Tabellendaten und alle zugehörigen Volltextkataloge in derselben Dateigruppe zu speichern. Aus Leistungsgründen kann es in einigen Fällen auch ratsam sein, die Tabellendaten und den Volltextindex in verschiedenen Dateigruppen auf unterschiedlichen Volumes anzuordnen, um die E/A-Parallelität zu erhöhen.  

  
### Zuweisen des Volltextindex   
 
 Es ist zu empfehlen, Tabellen mit denselben Updatemerkmalen (z. B. geringe Anzahl an Änderungen gegenüber einer großen Anzahl an Änderungen oder Tabellen, die regelmäßig zu bestimmten Tageszeiten geändert werden) zu gruppieren und demselben Volltextkatalog zuzuweisen. Indem Sie Zeitpläne für Volltextkataloge einrichten, bleiben Volltextindizes mit den Tabellen synchronisiert, ohne dass sich dies in Phasen umfangreicher Datenbankaktivitäten negativ auf die Ressourcenverwendung des Datenbankservers auswirkt.  
  
 Beachten Sie die folgenden Richtlinien:  
  
-   Wählen Sie stets den kleinsten eindeutigen Index, der verfügbar ist, als eindeutigen Volltextschlüssel aus (ein 4 Byte umfassender, auf dem integer-Datentyp basierender Index ist am besten geeignet). Hierdurch können Sie den Umfang der Ressourcen, die vom [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search-Dienst im Dateisystem benötigt werden, erheblich reduzieren. Wenn Sie einen breiten Primärschlüssel verwenden (mehr als 100 Byte), sollten Sie erwägen, als eindeutigen Volltextschlüssel einen anderen eindeutigen Index in der Tabelle auszuwählen (oder einen anderen eindeutigen Index zu erstellen). Andernfalls kann die Volltextauffüllung nicht mehr fortgesetzt werden, wenn der eindeutige Volltextschlüssel die maximal zulässige Größe erreicht (900 Byte).  
  
-   Wenn Sie eine Tabelle mit mehreren Millionen Zeilen indizieren, sollten Sie die Tabelle einem eigenen Volltextkatalog zuweisen.  
  
-   Berücksichtigen Sie sowohl den Umfang der Änderungen in den Tabellen, die mit einem Volltextindex indiziert werden, als auch die Gesamtzahl der Tabellenzeilen. Wenn die Gesamtzahl der geänderten Zeilen zusammen mit der Anzahl an Zeilen, die während der letzten Volltextauffüllung in der Tabelle enthalten waren, mehrere Millionen umfasst, sollten Sie die Tabelle einem eigenen Volltextkatalog zuweisen.  

  
### Zuordnen einer Stoppliste   
  Eine *Stoppliste* ist eine Liste von Stoppwörtern. Stoppwörter werden auch als Füllwörter bezeichnet. Jedem Volltextindex ist eine Stoppliste zugeordnet, und die Wörter der Stoppliste werden auf Volltextabfragen des Indexes angewendet. Standardmäßig ist der Systemstoppliste ein neuer Volltextindex zugeordnet. Sie können auch eine eigene Stoppliste erstellen und verwenden. Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 Die folgende [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung erstellt z. B. durch Kopieren der Systemstoppliste eine neue Volltext-Stoppliste mit dem Namen „myStoplist3“:  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 Die folgende [-Anweisung](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] ändert eine Stoppliste mit dem Namen „myStoplist“, indem zuerst für Spanisch und dann für Französisch das Wort „en“ hinzugefügt wird:  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
    
## Aktualisieren eines Index  
 Volltextindizes können wie reguläre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Indizes automatisch aktualisiert werden, sobald Daten in den zugeordneten Tabellen geändert werden. Dies ist das Standardverhalten. Alternativ dazu können Sie die Volltextindizes auch manuell auf dem aktuellen Stand halten oder in bestimmten Abständen aktualisieren lassen. Das Auffüllen eines Volltextindex kann zeitaufwändig und ressourcenintensiv sein. Aus diesem Grund wird das Indexupdate meist als asynchroner Vorgang durchgeführt, der im Hintergrund ausgeführt wird und den Volltextindex jeweils nach Änderungen in der Basistabelle aktualisiert. 
 
 Das sofortige Aktualisieren eines Volltextindex nach jeder Änderung in der Basistabelle kann ressourcenintensiv sein. Bei sehr hohen Update-, Einfügungs- und Löschungsraten kann es deshalb zu einer Verringerung der Abfrageleistung kommen. In diesem Fall sollten Sie erwägen, eine manuelle Änderungsnachverfolgung und entsprechende Updates zu planen, um die zahlreichen Änderungen von Zeit zu Zeit zu bearbeiten, anstatt mit den Abfragen um Ressourcen zu wetteifern.  
  
 Überwachen Sie den Auffüllungsstatus mithilfe der Funktion FULLTEXTCATALOGPROPERTY oder OBJECTPROPERTYEX. Führen Sie die folgende Anweisung aus, um den Auffüllungsstatus des Katalogs zu ermitteln:  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 In der Regel ist das zurückgegebene Ergebnis 1, während ein vollständiges Auffüllen ausgeführt wird.  
 

##  <a name="example"></a> Beispiel: Einrichten der Volltextsuche  
 Im folgenden zweiteiligen Beispiel wird ein Volltextkatalog mit dem Namen `AdvWksDocFTCat` in der AdventureWorks-Datenbank erstellt, und anschließend wird ein Volltextindex für die Tabelle `Document` in [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] erstellt. Diese Anweisung erstellt den Volltextkatalog im bei der Installation angegebenen Standardverzeichnis. Der Ordner mit dem Namen `AdvWksDocFTCat` befindet sich im Standardverzeichnis.  
  
1.  Im Beispiel wird eine [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)-Anweisung verwendet, um einen Volltextkatalog mit dem Namen `AdvWksDocFTCat` zu erstellen:  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  Bevor Sie einen Volltextindex für die Document-Tabelle erstellen können, müssen Sie sicherstellen, dass die Tabelle über einen eindeutigen, einspaltigen Index verfügt, der keine NULL-Werte zulässt. Die folgende [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)-Anweisung erstellt in der DocumentID-Spalte der Document-Tabelle den eindeutigen `ui_ukDoc`-Index:  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  Nachdem Sie einen eindeutigen Schlüssel erstellt haben, können Sie in der `Document`-Tabelle einen Volltextindex erstellen, indem Sie die folgende [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md)-Anweisung verwenden.  
  
    ```  
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
  
     Die in diesem Beispiel definierte TYPE COLUMN gibt die Typspalte in der Tabelle an, die den Typ des Dokuments in der Spalte Document (binäre Spalte) enthält. In der Typspalte wird die vom Benutzer angegebene Dateierweiterung für das Dokument der betreffenden Zeile gespeichert: ".doc", ".xls" usw. Das Volltextmodul verwendet die Erweiterung einer Zeile, um den richtigen Filter für die Analyse der Daten in dieser Zeile aufzurufen. Nachdem der Filter die binären Daten der Zeile analysiert hat, analysiert die angegebene Wörtertrennung den Inhalt (in diesem Beispiel wird die Wörtertrennung für britisches Englisch verwendet). Beachten Sie, dass der Filtervorgang nur zur Indizierungszeit ausgeführt wird bzw. wenn ein Benutzer eine Spalte in der Basistabelle einfügt oder aktualisiert, während für den Volltextindex die automatische Änderungsnachverfolgung aktiviert ist. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
   
## Erstellen eines Volltextkatalogs  
  
-   [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
-   [Erstellen und Verwalten von Volltextkatalogen](../../relational-databases/search/create-and-manage-full-text-catalogs.md)  
  
## Anzeigen der Indizes  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
## Erstellen eines eindeutigen Indexes  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [Öffnen des Tabellen-Designers &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-table-designer-visual-database-tools.md)  
  
## Erstellen eines Volltextindexes  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
-   [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md)  
  
## Anzeigen von Informationen zu einem Volltextindex  
  
|Katalogsicht oder dynamische Verwaltungssicht|Beschreibung|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)|Gibt eine Zeile für jeden Verweis zwischen Volltextkatalog und Volltextindex zurück.|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|Enthält eine Zeile für jede Spalte, die Teil eines Volltextindexes ist.|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)|Ein Volltextindex verwendet interne Tabellen, die als Volltextindexfragmente bezeichnet werden, um die umgekehrten Indexdaten zu speichern. Diese Sicht kann verwendet werden, um die Metadaten zu diesen Fragmenten abzufragen. Diese Sicht enthält eine Zeile für jedes Volltextindexfragment in jeder Tabelle, die einen Volltextindex enthält.|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)|Enthält eine Zeile pro Volltextindex eines Tabellenobjekts.|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)|Gibt Informationen zum Inhalt eines Volltextindex für die angegebene Tabelle zurück.|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)|Gibt Informationen zum Inhalt auf Dokumentebene eines Volltextindex für die angegebene Tabelle zurück. Ein Schlüsselwort kann in mehreren Dokumenten angezeigt werden.|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|Gibt Informationen zu den aktuell ausgeführten Volltextindexauffüllungen zurück.|  
  

  
## Und weitere Informationen 
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  