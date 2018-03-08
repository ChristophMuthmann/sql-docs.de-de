---
title: "Auffüllen von Volltextindizes | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c139299c1613bb3d76328097fd1235f67ebe121a
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="populate-full-text-indexes"></a>Auffüllen von Volltextindizes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Das Erstellen und Verwalten eines Volltextindexes umfasst das Auffüllen des Indexes mithilfe eines Prozesses, der als *Auffüllung* (oder auch als *Crawl*) bezeichnet wird.  
  
##  <a name="types"></a> Types of population  
Ein Volltextindex unterstützt die folgenden Auffüllungstypen:
-   **Vollständige** Auffüllung
-   Automatische oder manuelle Auffüllung basierend auf der **Änderungsnachverfolgung**
-   Inkrementelle Auffüllung basierend auf einem **Zeitstempel**
  
## <a name="full-population"></a>Vollständige Auffüllung  
 Während einer vollständigen Auffüllung werden Indexeinträge für alle Zeilen einer Tabelle oder einer indizierten Sicht erstellt. Eine vollständige Auffüllung eines Volltextindexes erstellt Indexeinträge für alle Zeilen der Basistabelle oder der indizierten Sicht.  
  
Standardmäßig füllt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen neuen Volltextindex vollständig auf, sobald er erstellt wird.
-   Die vollständige Auffüllung kann einerseits eine deutliche Beanspruchung der Ressourcen bedeuten. Beim Erstellen eines Volltextindexes zu Zeiten mit hohen Lastwerten wird daher empfohlen, die vollständige Auffüllung bis zu einem späteren Zeitpunkt mit geringerer Auslastung zu verzögern, insbesondere, wenn die Basistabelle eines Volltextindexes sehr groß ist.
-   Der Volltextkatalog ist andererseits bis zum Abschluss der vollständigen Auffüllung der zugehörigen Volltextindizes nicht verfügbar.

Geben Sie in der `CREATE FULLTEXT INDEX`-Anweisung die `CHANGE_TRACKING OFF, NO POPULATION`-Klausel an, um einen Volltextindex zu erstellen, ohne ihn sofort aufzufüllen. Bei Angabe von `CHANGE_TRACKING MANUAL` füllt das Volltextmodul den neuen Volltextindex erst auf, wenn Sie eine `ALTER FULLTEXT INDEX`-Anweisung mithilfe der `START FULL POPULATION`- oder `START INCREMENTAL POPULATION`-Klausel ausführen. 

### <a name="example---create-a-full-text-index-without-running-a-full-population"></a>Beispiel: Erstellen eines Volltextindexes ohne Ausführung der vollständigen Auffüllung  
 Im folgenden Beispiel wird ein Volltextindex für die `Production.Document` -Tabelle der `AdventureWorks` -Beispieldatenbank erstellt. In diesem Beispiel wird `WITH CHANGE_TRACKING OFF, NO POPULATION` verwendet, um die erste vollständige Auffüllung zu verzögern.  
  
```sql
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="example---run-a-full-population-on-a-table"></a>Beispiel: Ausführen einer vollständigen Auffüllung für eine Tabelle  
 Im folgenden Beispiel wird eine vollständige Auffüllung der `Production.Document` -Tabelle der `AdventureWorks` -Beispieldatenbank ausgeführt.  
  
```sql
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
   
## <a name="population-based-on-change-tracking"></a>Auffüllung basierend auf der Änderungsnachverfolgung
 Optional können Sie die Änderungsnachverfolgung verwenden, um nach seiner ursprünglichen vollständigen Auffüllung einen Volltextindex beizubehalten. Die Änderungsnachverfolgung bedeutet einen geringen zusätzlichen Leistungsaufwand, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Tabelle verwaltet, in der Änderungen der Basistabelle seit der letzten Auffüllung verfolgt werden. Beim Verwenden der Änderungsnachverfolgung verwaltet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Aufzeichnung der Zeilen in der Basistabelle oder indizierten Sicht, die durch Updates, Löschungen oder Einfügungen geändert wurden. Datenänderungen durch WRITETEXT und UPDATETEXT werden im Volltextindex nicht wiedergegeben und bei der Änderungsnachverfolgung nicht ausgewählt.  
  
> [!NOTE]  
>  Für Tabellen, die eine **Zeitstempel**-Spalte enthalten, können Sie die inkrementelle Auffüllung anstatt der Änderungsnachverfolgung verwenden.  
  
 Wenn Sie die Änderungsnachverfolgung während der Indexerstellung aktivieren, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die vollständige Auffüllung des neuen Volltextindexes unmittelbar nach dessen Erstellung aus. Danach werden Änderungen nachverfolgt und an den Volltextindex weitergegeben.

### <a name="enable-change-tracking"></a>Änderungsnachverfolgung aktivieren
Es gibt zwei Typen der Änderungsnachverfolgung:
-   Automatisch (Option `CHANGE_TRACKING AUTO`) Die automatische Änderungsnachverfolgung ist das Standardverhalten.
-   Manuell (Option `CHANGE_TRACKING MANUAL`)   
  
 Der Typ der Änderungsnachverfolgung bestimmt, wie der Volltextindex aufgefüllt wird, wie im Folgenden dargestellt:  
  
-   **Automatische Auffüllung**  
  
     Das Volltextmodul verwendet standardmäßig die automatische Auffüllung für den Volltextindex oder bei Angabe von `CHANGE_TRACKING AUTO`. Nachdem die ursprüngliche vollständige Auffüllung abgeschlossen wurde, werden Änderungen nachverfolgt und automatisch weitergegeben, wenn Daten in der Basistabelle geändert werden. Der Volltextindex wird im Hintergrund aktualisiert. Die so weitergegebenen Änderungen werden u. U. jedoch nicht sofort im Index wiedergegeben.  
  
     **Starten der Änderungsnachverfolgung mit automatischer Auffüllung**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING AUTO  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING AUTO  
  
    **Beispiel: Umstellen eines Volltextindexes auf die automatische Änderungsnachverfolgung**  
    Im folgenden Beispiel wird der Volltextindex für die `HumanResources.JobCandidate` -Tabelle der `AdventureWorks` -Beispieldatenbank so geändert, dass dieser die automatische Auffüllung mit Änderungsnachverfolgung verwendet.  
  
    ```sql  
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
    GO   
    ```  
  
-   **Manuelle Auffüllung**  
  
     Wenn Sie CHANGE_TRACKING MANUAL angeben, verwendet das Volltextmodul die manuelle Auffüllung für den Volltextindex. Nachdem die ursprüngliche vollständige Auffüllung abgeschlossen wurde, werden Änderungen nachverfolgt, wenn Daten in der Basistabelle geändert werden. Sie werden jedoch nicht an den Volltextindex weitergegeben, bis Sie eine ALTER FULLTEXT INDEX … START UPDATE POPULATION -Anweisung anwenden. Sie können den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent verwenden, um die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung in regelmäßigen Abständen aufzurufen.  
  
     **So beginnen Sie die Änderungsnachverfolgung mit manueller Auffüllung**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING MANUAL  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING MANUAL  
  
    **Beispiel: Erstellen eines Volltextindexes mit manueller Änderungsnachverfolgung**  
    Im folgenden Beispiel wird ein Volltextindex mit Änderungsnachverfolgung und manueller Auffüllung für die `HumanResources.JobCandidate` -Tabelle der `AdventureWorks` -Beispieldatenbank erstellt.  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
    CREATE FULLTEXT CATALOG ft AS DEFAULT;  
    CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
       KEY INDEX ui_ukJobCand   
       WITH CHANGE_TRACKING=MANUAL;  
    GO  
    ```  
  
    **Beispiel: Ausführen einer manuellen Auffüllung**  
    Im folgenden Beispiel wird eine manuelle Auffüllung des Volltextindexes mit Änderungsnachverfolgung für die `HumanResources.JobCandidate` -Tabelle der `AdventureWorks` -Beispieldatenbank ausgeführt.  
  
    ```sql 
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
    GO  
    ```
   
### <a name="disable-change-tracking"></a>Deaktivieren der Änderungsnachverfolgung 
  
-   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING OFF  
  
-   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING OFF  
   
  
## <a name="incremental-population-based-on-a-timestamp"></a>Inkrementelle Auffüllung basierend auf einem Zeitstempel  
 Eine inkrementelle Auffüllung ist ein alternativer Mechanismus zum manuellen Auffüllen eines Volltextindexes. Wenn in einer Tabelle sehr viele Einfügungen stattfinden, ist die inkrementelle Auffüllung ggf. effizienter als die manuelle Auffüllung.
 
 Sie können eine inkrementelle Auffüllung für einen Volltextindex ausführen, für den CHANGE_TRACKING auf den Wert MANUAL oder OFF festgelegt ist. 
  
 Voraussetzung für die inkrementelle Auffüllung ist, dass die indizierte Tabelle eine Spalte vom Datentyp **timestamp** aufweist. Ist keine **timestamp** -Spalte vorhanden, kann die inkrementelle Auffüllung nicht ausgeführt werden.   

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die Spalte **timestamp** , um Zeilen zu identifizieren, die sich seit der letzten Auffüllung geändert haben. Bei der inkrementellen Auffüllung wird der Volltextindex bezüglich der Zeilen aktualisiert, die seit der letzten Auffüllung oder während des letzten Auffüllungsvorgangs hinzugefügt, gelöscht oder geändert wurden. Am Ende einer Auffüllung wird vom Volltextsuchmodul ein neuer **timestamp** -Wert aufgezeichnet. Dieser Wert entspricht dem größten in SQL Gatherer gefundenen **Zeitstempel**-Wert. Der Wert wird verwendet, wenn die nachfolgende inkrementelle Auffüllung gestartet wird.  
 
In einigen Fällen führt die Anforderung für eine inkrementelle Auffüllung zu einer vollständigen Auffüllung.
-   Eine Anforderung für eine inkrementelle Auffüllung für eine Tabelle ohne **timestamp** -Spalte führt zu einer vollständigen Auffüllung.
-   Wenn es sich bei der ersten Auffüllung eines Volltextindexes um eine inkrementelle Auffüllung handelt, werden alle Zeilen indiziert. Damit entspricht die Auffüllung einer vollständigen Auffüllung. 
-   Anforderungen für eine inkrementelle Auffüllung werden als vollständige Auffüllung implementiert, wenn sich Metadaten, die sich auf den Volltextindex für die Tabelle auswirken, seit der letzten Auffüllung geändert haben. Dies umfasst Metadatenänderungen durch Spalten-, Index- oder Volltextindexdefinitionen. 

### <a name="run-an-incremental-population"></a>Ausführen einer inkrementellen Auffüllung
  
 Führen Sie mithilfe der `START INCREMENTAL POPULATION`-Klausel eine `ALTER FULLTEXT INDEX`-Anweisung aus, um eine inkrementelle Auffüllung auszuführen.  
  
###  <a name="create"></a> Erstellen oder Ändern eines Zeitplans für die inkrementelle Auffüllung   
  
1.  Erweitern Sie in Management Studio im Objekt-Explorer den Server.  
  
2.  Erweitern Sie **Datenbanken**, und erweitern Sie dann die Datenbank, die den Volltextindex enthält.  
  
3.  Erweitern Sie **Tabellen**.  
  
    Klicken Sie mit der rechten Maustaste auf die Tabelle, für die der Volltextindex definiert ist. Wählen Sie **Volltextindex**, und klicken Sie dann im Kontextmenü **Volltextindex** auf **Eigenschaften**. Das Dialogfeld **Volltextindexeigenschaften** wird geöffnet.  

    > [!IMPORTANT]  
    >  Wenn die Basistabelle oder Sicht keine Spalte für den Datentyp **Zeitstempel** enthält, ist eine inkrementelle Auffüllung nicht möglich.
      
1.  Wählen Sie im Bereich **Seite auswählen** **Zeitpläne** aus.  
  
     Verwenden Sie diese Seite, um Zeitpläne für einen SQL Server-Agent-Auftrag zu erstellen oder zu verwalten, der eine inkrementelle Tabellenauffüllung für die Basistabelle oder indizierte Sicht eines Volltextindex beginnt.  

     Folgende Optionen stehen zur Verfügung:  
  
    -   Um einen neuen Zeitplan zu **erstellen**, klicken Sie auf **Neu**.  
  
        Das Dialogfeld **Neuer Zeitplan für Tabellen-Volltextindizierung** wird geöffnet und erlaubt das Erstellen eines neuen Zeitplans. Klicken Sie auf **OK**, um den Zeitplan zu speichern.  
  
        > [!IMPORTANT]  
        >  Einem neuen Zeitplan wird ein SQL Server-Agent-Auftrag (Start Incremental Table Population on *database_name*.*table_name*) zugeordnet, sobald Sie das Dialogfeld **Volltextindexeigenschaften** schließen. Wenn Sie mehrere Zeitpläne für denselben Volltextindex erstellen, verwenden alle denselben Auftrag.  
  
    -   Um einen vorhandenen Zeitplan zu **ändern**, wählen Sie den vorhandenen Zeitplan aus, und klicken Sie auf **Bearbeiten**.  
  
         Das Dialogfeld **Neuer Zeitplan für Tabellen-Volltextindizierung** wird geöffnet und erlaubt das Bearbeiten des Zeitplans.  
  
        > [!NOTE]  
        >  Informationen zum Ändern eines Auftrags des SQL Server-Agents finden Sie unter [Ändern eines Auftrags](http://msdn.microsoft.com/library/dd5e5f20-20c4-4ab9-a19a-db87577dcd43).  
  
    -   Um einen vorhandenen Zeitplan zu **entfernen**, wählen Sie den vorhandenen Zeitplan aus, und klicken Sie auf **Löschen**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]   
  
##  <a name="crawl"></a> Beheben von Fehlern in einer Volltextauffüllung (Durchforstung)  
Tritt während eines Durchforstungsvorgangs ein Fehler auf, wird von der Durchforstungsprotokollfunktion der Volltextsuche ein Durchforstungsprotokoll erstellt und gewartet. Dabei handelt es sich um eine Nur-Text-Datei. Jedes Durchforstungsprotokoll gehört zu einem bestimmten Volltextkatalog. Standardmäßig befinden sich Durchforstungsprotokolle für eine bestimmte Instanz (in diesem Beispiel die Standardinstanz) im Ordner `%ProgramFiles%\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\LOG`.
 
Das Benennungsschema für Durchforstungsprotokolldateien lautet folgendermaßen:  
  
`SQLFT<DatabaseID><FullTextCatalogID>.LOG[<n>]`
  
Die variablen Teile des Durchforstungsprotokolldatei-Namens sind die folgenden.
-   <**DatabaseID**>: Die ID einer Datenbank. <**dbid**> ist eine fünfstellige Zahl mit führenden Nullen.  
-   <**Volltext-Katalog-ID**>: Die ID eines Volltextkatalogs. <**catid**> ist eine fünfstellige Zahl mit führenden Nullen.  
-   <**n**> ist eine ganze Zahl, die angibt, dass mindestens ein Durchforstungsprotokoll desselben Volltextkatalogs vorhanden ist.  
  
 `SQLFT0000500008.2` ist z.B. die Durchforstungsprotokolldatei für eine Datenbank mit der Datenbank-ID = 5 und der Volltextkatalog-ID = 8. Die 2 am Ende des Dateinamens gibt an, dass zwei Durchforstungsprotokolldateien für dieses Datenbank-Katalog-Paar vorhanden sind.  

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)   
 [Erste Schritte mit der Volltextsuche](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
