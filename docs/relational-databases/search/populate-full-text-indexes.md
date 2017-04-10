---
title: "Auff&#252;llen von Volltextindizes | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Indexauffüllungen [Volltextsuche]"
  - "Inkrementelle Auffüllungen [Volltextsuche]"
  - "Auffüllungen [Volltextsuche]"
  - "Volltextsuche [SQL Server], Eigenschaften"
  - "Crawls [Volltextsuche]"
  - "Automatische Updates des Volltextindexes"
  - "Auffüllungen mithilfe der Änderungsnachverfolgung [Volltextsuche]"
  - "Manuelle Updates [Volltextsuche]"
  - "Manuelle Auffüllungen [Volltextsuche]"
  - "Automatische Auffüllungen [Volltextsuche]"
  - "Volltextindizes [SQL Server], Schlüsselspalte"
  - "Vollständige Auffüllungen [Volltextsuche]"
  - "Volltextindizes [SQL Server], Auffüllungen"
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
caps.latest.revision: 78
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 75
---
# Auff&#252;llen von Volltextindizes
  Das Erstellen und Verwalten eines Volltextindexes umfasst das Auffüllen des Indexes mithilfe eines Prozesses, der als *Auffüllung* (oder auch als *Crawl*) bezeichnet wird.  
  
##  <a name="types"></a> Typen der Auffüllung  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die folgenden Auffüllungstypen: vollständige Auffüllung, auf der Änderungsnachverfolgung basierende automatische oder manuelle Auffüllung sowie inkrementelle zeitstempelbasierte Auffüllung.  
  
### Vollständige Auffüllung  
 Während einer vollständigen Auffüllung werden Indexeinträge für alle Zeilen einer Tabelle oder einer indizierten Sicht erstellt. Eine vollständige Auffüllung eines Volltextindexes erstellt Indexeinträge für alle Zeilen der Basistabelle oder der indizierten Sicht.  
  
 Standardmäßig füllt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen neuen Volltextindex vollständig auf, sobald er erstellt wird. Die vollständige Auffüllung kann jedoch eine deutliche Beanspruchung der Ressourcen bedeuten. Beim Erstellen eines Volltextindexes zu Zeiten mit hohen Lastwerten wird daher empfohlen, die vollständige Auffüllung bis zu einem späteren Zeitpunkt mit geringerer Auslastung zu verzögern, insbesondere, wenn die Basistabelle eines Volltextindexes sehr groß ist. Der Volltextkatalog ist dann allerdings bis zum Abschluss der vollständigen Auffüllung der zugehörigen Volltextindizes nicht verfügbar. Um einen Volltextindex zu erstellen, ohne ihn sofort aufzufüllen, geben Sie die Klausel CHANGE_TRACKING OFF, NO POPULATION in der CREATE FULLTEXT INDEX-Anweisung an. Wenn Sie CHANGE_TRACKING MANUAL angeben, verwendet das Volltextmodul die Anweisung. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] füllt den neuen Volltextindex erst auf, wenn Sie eine ALTER FULLTEXT INDEX-Anweisung mithilfe der START FULL POPULATION- oder START INCREMENTAL POPULATION-Klausel ausführen. Weitere Informationen finden Sie unter den Beispielen "A. Erstellen eines Volltextindexes ohne Ausführung der vollständigen Auffüllung" und "B. Ausführen einer vollständigen Auffüllung einer Tabelle " weiter unten in diesem Thema.  
  
 [In diesem Thema](#top)NACH OBEN  
  
### Auffüllung mithilfe von Änderungsnachverfolgung  
 Optional können Sie die Änderungsnachverfolgung verwenden, um nach seiner ursprünglichen vollständigen Auffüllung einen Volltextindex beizubehalten. Die Änderungsnachverfolgung bedeutet einen geringen zusätzlichen Leistungsaufwand, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Tabelle verwaltet, in der Änderungen der Basistabelle seit der letzten Auffüllung verfolgt werden. Beim Verwenden der Änderungsnachverfolgung registriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Zeilen in der Basistabelle oder indizierten Sicht, die durch Updates, Löschungen oder Einfügungen geändert wurden. Datenänderungen durch WRITETEXT und UPDATETEXT werden im Volltextindex nicht wiedergegeben und bei der Änderungsnachverfolgung nicht ausgewählt.  
  
> [!NOTE]  
>  Für Tabellen, die eine **timestamp**-Spalte enthalten, können Sie inkrementelle Auffüllungen verwenden.  
  
 Wenn die Änderungsnachverfolgung während der Indexerstellung aktiviert ist, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die vollständige Auffüllung des neuen Volltextindexes unmittelbar nach dessen Erstellung aus. Danach werden Änderungen nachverfolgt und an den Volltextindex weitergegeben. Es gibt zwei Typen der Änderungsnachverfolgung, automatisch (Option CHANGE_TRACKING AUTO) und manuell (Option CHANGE_TRACKING MANUAL). Die automatische Änderungsnachverfolgung ist das Standardverhalten.  
  
 Der Typ der Änderungsnachverfolgung bestimmt, wie der Volltextindex aufgefüllt wird, wie im Folgenden dargestellt:  
  
-   Automatische Auffüllung  
  
     Wenn Sie CHANGE_TRACKING AUTO angeben, verwendet das Volltextmodul automatische Auffüllung für den Volltextindex. Nachdem die ursprüngliche vollständige Auffüllung abgeschlossen wurde, werden Änderungen nachverfolgt und automatisch weitergegeben, wenn Daten in der Basistabelle geändert werden. Der Volltextindex wird im Hintergrund aktualisiert. Die so weitergegebenen Änderungen werden u. U. jedoch nicht sofort im Index wiedergegeben.  
  
     **So richten Sie die Nachverfolgung von Änderungen mit automatischer Auffüllung ein**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING AUTO  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING AUTO  
  
     Weitere Informationen finden Sie unter Beispiel "E. Änderung eines Volltextindexes zur Verwendung der automatischen Änderungsnachverfolgung" weiter unten in diesem Thema.  
  
-   Manuelle Auffüllung  
  
     Wenn Sie CHANGE_TRACKING MANUAL angeben, verwendet das Volltextmodul die manuelle Auffüllung für den Volltextindex. Nachdem die ursprüngliche vollständige Auffüllung abgeschlossen wurde, werden Änderungen nachverfolgt, wenn Daten in der Basistabelle geändert werden. Sie werden jedoch nicht an den Volltextindex weitergegeben, bis Sie eine ALTER FULLTEXT INDEX … START UPDATE POPULATION -Anweisung anwenden. Sie können den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent verwenden, um die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung in regelmäßigen Abständen aufzurufen.  
  
     **So beginnen Sie die Änderungsnachverfolgung mit manueller Auffüllung**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING MANUAL  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING MANUAL  
  
     Weitere Informationen finden Sie unter den Beispielen "C. Erstellen eines Volltextindexes mit manueller Änderungsnachverfolgung" und "D. Ausführung einer manuellen Auffüllung" weiter unten in diesem Thema.  
  
 **So schalten Sie die Änderungsnachverfolgung aus**  
  
-   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) … WITH CHANGE_TRACKING OFF  
  
-   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) … SET CHANGE_TRACKING OFF  
  
 [In diesem Thema](#top)NACH OBEN  
  
### Inkrementelle, auf Timestamps basierende Auffüllung  
 Eine inkrementelle Auffüllung ist ein alternativer Mechanismus zum manuellen Auffüllen eines Volltextindexes. Sie können eine inkrementelle Auffüllung für einen Volltextindex ausführen, für den CHANGE_TRACKING auf den Wert MANUAL oder OFF festgelegt ist. Wenn es sich bei der ersten Auffüllung eines Volltextindexes um eine inkrementelle Auffüllung handelt, werden alle Zeilen indiziert. Damit entspricht die Auffüllung einer vollständigen Auffüllung.  
  
 Voraussetzung für die inkrementelle Auffüllung ist, dass die indizierte Tabelle eine Spalte vom Datentyp **timestamp** aufweist. Ist keine **timestamp**-Spalte vorhanden, kann die inkrementelle Auffüllung nicht ausgeführt werden. Eine Anforderung für eine inkrementelle Auffüllung für eine Tabelle ohne **timestamp**-Spalte führt zu einer vollständigen Auffüllung. Anforderungen für eine inkrementelle Auffüllung werden als vollständige Auffüllung implementiert, wenn sich Metadaten, die sich auf den Volltextindex für die Tabelle auswirken, seit der letzten Auffüllung geändert haben. Dies umfasst Metadatenänderungen durch Spalten-, Index- oder Volltextindexdefinitionen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die Spalte **timestamp**, um Zeilen zu identifizieren, die sich seit der letzten Auffüllung geändert haben. Bei der inkrementellen Auffüllung wird der Volltextindex bezüglich der Zeilen aktualisiert, die seit der letzten Auffüllung oder während des letzten Auffüllungsvorgangs hinzugefügt, gelöscht oder geändert wurden. Wenn in einer Tabelle sehr viele Einfügungen stattfinden, ist die inkrementelle Auffüllung ggf. effizienter als die manuelle Auffüllung.  
  
 Am Ende einer Auffüllung wird vom Volltextsuchmodul ein neuer **timestamp**-Wert aufgezeichnet. Dieser Wert entspricht dem größten in SQL Gatherer aufgetretenen **timestamp**-Wert. Der Wert wird verwendet, wenn eine nachfolgende inkrementelle Auffüllung gestartet wird.  
  
 Um eine inkrementelle Auffüllung auszuführen, führen Sie eine ALTER FULLTEXT INDEX-Anweisung mit der Klausel START INCREMENTAL POPULATION aus.  
  
 [In diesem Thema](#top)NACH OBEN  
  
##  <a name="examples"></a> Beispiele zum Auffüllen von Volltextindizes  
  
> [!NOTE]  
>  In den Beispielen in diesem Abschnitt wird die `Production.Document`-Tabelle oder die `HumanResources.JobCandidate`-Tabelle der `AdventureWorks`-Beispieldatenbank verwendet.  
  
### A. Erstellen eines Volltextindexes ohne Ausführung der vollständigen Auffüllung  
 Im folgenden Beispiel wird ein Volltextindex für die `Production.Document`-Tabelle der `AdventureWorks`-Beispieldatenbank erstellt. In diesem Beispiel wird WITH CHANGE_TRACKING OFF, NO POPULATION verwendet, um die erste vollständige Auffüllung zu verzögern.  
  
```  
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
  
### B. Ausführen einer vollständigen Auffüllung einer Tabelle  
 Im folgenden Beispiel wird eine vollständige Auffüllung der `Production.Document`-Tabelle der `AdventureWorks`-Beispieldatenbank ausgeführt.  
  
```  
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
  
### C. Erstellen eines Volltextindexes mit manueller Änderungsnachverfolgung  
 Im folgenden Beispiel wird ein Volltextindex mit Änderungsnachverfolgung und manueller Auffüllung für die `HumanResources.JobCandidate`-Tabelle der `AdventureWorks`-Beispieldatenbank erstellt.  
  
```  
USE AdventureWorks;  
GO  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH CHANGE_TRACKING=MANUAL;  
GO  
```  
  
### D. Ausführen einer manuellen Auffüllung  
 Im folgenden Beispiel wird eine manuelle Auffüllung des Volltextindexes mit Änderungsnachverfolgung für die `HumanResources.JobCandidate`-Tabelle der `AdventureWorks`-Beispieldatenbank ausgeführt.  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
GO  
```  
  
### E. Umstellen eines Volltextindexes auf die automatische Änderungsnachverfolgung  
 Im folgenden Beispiel wird der Volltextindex für die `HumanResources.JobCandidate`-Tabelle der `AdventureWorks`-Beispieldatenbank so geändert, dass dieser die automatische Auffüllung mit Änderungsnachverfolgung verwendet.  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
GO   
```  
  
 [In diesem Thema](#top)NACH OBEN  
  
##  <a name="create"></a> Erstellen oder Ändern eines Zeitplans für inkrementelle Auffüllung  
  
#### So erstellen oder ändern Sie einen Zeitplan für inkrementelle Auffüllung in Management Studio  
  
1.  Erweitern Sie im Objekt-Explorer den Server.  
  
2.  Erweitern Sie **Datenbanken**, und erweitern Sie dann die Datenbank, die den Volltextindex enthält.  
  
3.  Erweitern Sie **Tabellen**.  
  
 Klicken Sie mit der rechten Maustaste auf die Tabelle, für die der Volltextindex definiert ist. Wählen Sie **Volltextindex**, und klicken Sie dann im Kontextmenü **Volltextindex** auf **Eigenschaften**. Das Dialogfeld **Volltextindexeigenschaften** wird geöffnet.  
  
1.  Wählen Sie im Bereich **Seite auswählen** die Option Zeitpläne aus.  
  
     Verwenden Sie diese Seite, um Zeitpläne für einen SQL Server-Agent-Auftrag zu erstellen oder zu verwalten, der eine inkrementelle Tabellenauffüllung für die Basistabelle oder indizierte Sicht eines Volltextindex beginnt.  
  
    > [!IMPORTANT]  
    >  Wenn die Basistabelle oder Sicht keine Spalte für den Datentyp **timestamp** enthält, wird eine vollständige Auffüllung ausgeführt.  
  
     Folgende Optionen stehen zur Verfügung:  
  
    -   Um einen neuen Zeitplan zu erstellen, klicken Sie auf **Neu**.  
  
         Das Dialogfeld **Neuer Zeitplan für Tabellen-Volltextindizierung** wird geöffnet und erlaubt das Erstellen eines neuen Zeitplans. Klicken Sie auf **OK**, um den Zeitplan zu speichern.  
  
        > [!IMPORTANT]  
        >  Einem neuen Zeitplan wird ein SQL Server-Agent-Auftrag (Start Incremental Table Population on *database_name*.*table_name*) zugeordnet, sobald Sie das Dialogfeld **Volltextindexeigenschaften** schließen. Wenn Sie mehrere Zeitpläne für den Volltextindex erstellen, verwenden alle denselben Auftrag.  
  
    -   Um einen Zeitplan zu ändern, wählen Sie ihn aus, und klicken Sie auf **Bearbeiten**.  
  
         Das Dialogfeld **Neuer Zeitplan für Tabellen-Volltextindizierung** wird geöffnet und erlaubt das Bearbeiten des Zeitplans.  
  
        > [!NOTE]  
        >  Informationen zum Bearbeiten eines Auftrags finden Sie unter [Ändern eines Auftrags](../../ssms/agent/modify-a-job.md).  
  
    -   Um einen Zeitplan zu entfernen, wählen Sie ihn aus, und klicken Sie auf **Löschen**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 [In diesem Thema](#top)NACH OBEN  
  
##  <a name="crawl"></a> Beheben von Fehlern in einer Volltextauffüllung (Durchforstung)  
 Tritt während eines Durchforstungsvorgangs ein Fehler auf, wird von der Durchforstungsprotokollfunktion der Volltextsuche ein Durchforstungsprotokoll erstellt und gewartet. Dabei handelt es sich um eine Nur-Text-Datei. Jedes Durchforstungsprotokoll gehört zu einem bestimmten Volltextkatalog. Standardmäßig befinden sich Durchforstungsprotokolle für eine bestimmte Instanz, in diesem Fall die erste Instanz, im Ordner „%ProgramFiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\LOG“. Das Benennungsschema für Durchforstungsprotokolldateien lautet folgendermaßen:  
  
 SQLFT\<DatabaseID>\<FullTextCatalogID>.LOG[\<n>]  
  
 \<**DatabaseID**>  
 Die ID einer Datenbank. \<**dbid**> ist eine fünfstellige Zahl mit führenden Nullen.  
  
 \<**FullTextCatalogID**>  
 Volltextkatalog-ID. \<**catid**> ist eine fünfstellige Zahl mit führenden Nullen.  
  
 \<**n**>  
 Ist eine ganze Zahl, die angibt, dass mindestens ein Durchforstungsprotokoll desselben Volltextkatalogs vorhanden ist.  
  
 SQLFT0000500008.2 ist z. B. die Durchforstungsprotokolldatei für eine Datenbank mit der Datenbank-ID = 5 und der Volltextkatalog-ID = 8. Die 2 am Ende des Dateinamens gibt an, dass zwei Durchforstungsprotokolldateien für dieses Datenbank-Katalog-Paar vorhanden sind.  
  
 [In diesem Thema](#top)NACH OBEN  
  
## Siehe auch  
 [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)   
 [Erste Schritte mit der Volltextsuche](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  