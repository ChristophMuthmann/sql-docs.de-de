---
title: "Aktivieren der semantischen Suche in Tabellen und Spalten | Microsoft Docs"
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
  - "Semantische Suche [SQL Server], aktivieren"
ms.assetid: 895d220c-6749-4954-9dd3-2ea4c6a321ff
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 20
---
# Aktivieren der semantischen Suche in Tabellen und Spalten
  Beschreibt, wie die statistische semantische Indizierung für ausgewählte Spalten, die Dokumente oder Text enthalten, aktiviert bzw. deaktiviert wird.  
  
 Die statistische semantische Suche verwendet die Indizes, die von der Volltextsuche erstellt werden, und erstellt zusätzliche Indizes. Als Ergebnis dieser Abhängigkeit von der Volltextsuche erstellen Sie einen neuen semantischen Index, wenn Sie einen neuen Volltextindex definieren oder einen vorhandenen Volltextindex ändern. Einen neuen semantischen Index können Sie mit [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen oder mit dem Volltextindizierungs-Assistenten und anderen Dialogfeldern in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen, wie in diesem Thema beschrieben.  
  
##  <a name="BasicEnabling"></a> Erstellen eines semantischen Indexes  
  
###  <a name="reqenable"></a> Anforderungen und Einschränkungen beim Erstellen eines semantischen Indexes  
  
-   Sie können einen Index für alle Datenbankobjekte erstellen, die für Volltextindizierung unterstützt werden, einschließlich Tabellen und indizierte Sichten.  
  
-   Bevor Sie die semantische Indizierung für bestimmte Spalten aktivieren können, müssen die folgenden Anforderungen erfüllt werden:  
  
    -   Für die Datenbank muss ein Volltextkatalog vorhanden sein.  
  
    -   Die Tabelle muss über einen Volltextindex verfügen.  
  
    -   Die ausgewählten Spalten müssen Teil des Volltextindexes sein.  
  
     Diese Anforderungen können alle gleichzeitig erstellt und aktiviert werden.  
  
-   Sie können einen semantischen Index für Spalten erstellen, die einen der für Volltextindizierung unterstützten Datentypen aufweisen. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md).  
  
-   Sie können einen beliebigen Dokumenttyp angeben, der für Volltextindizierung für **varbinary(max)**-Spalten unterstützt wird. Weitere Informationen finden Sie unter [Vorgehensweise: Ermitteln, welche Dokumenttypen indiziert werden können](#doctypes) .  
  
-   Bei der semantischen Indizierung werden zwei Typen von Indizes für die ausgewählten Spalten erstellt – ein Index mit Schlüsselausdrücken und ein Index für Dokumentähnlichkeit. Wenn Sie die semantische Indizierung aktivieren, können Sie nur einen Indextyp auswählen. Sie können diese beiden Indizes jedoch unabhängig voneinander abfragen. Weitere Informationen finden Sie unter [Suchen von Schlüsselausdrücken in Dokumenten mit der semantischen Suche](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) und [Suchen von ähnlichen und verwandten Dokumenten mit semantischer Suche](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
-   Wenn Sie nicht explizit eine LCID für einen semantischen Index angeben, werden nur die primäre Sprache und ihre zugeordneten Sprachstatistiken für die semantische Indizierung verwendet.  
  
-   Wenn Sie eine Sprache für eine Spalte angeben, für die das Sprachmodell nicht verfügbar ist, schlägt die Erstellung des Indexes fehl, und es wird eine Fehlermeldung zurückgegeben.  
  
###  <a name="HowToEnableCreate"></a> Vorgehensweise: Erstellen eines semantischen Indexes, wenn kein Volltextindex vorhanden ist  
 Wenn Sie einen neuen Volltextindex mit der **CREATE FULLTEXT INDEX**-Anweisung erstellen, können Sie die semantische Indizierung auf Spaltenebene aktivieren, indem Sie das Schlüsselwort **STATISTICAL_SEMANTICS** als Teil der Spaltendefinition angeben. Sie können die semantische Indizierung auch aktivieren, wenn Sie einen neuen Volltextindex mithilfe des Volltextindizierungs-Assistenten erstellen.  
  
 **Erstellen eines neuen semantischen Indexes mit Transact-SQL**  
 Rufen Sie die **CREATE FULLTEXT INDEX**-Anweisung auf, und geben Sie **STATISTICAL_SEMANTICS** für jede Spalte an, in der Sie einen semantischen Index erstellen möchten. Weitere Informationen zu allen Optionen für diese Anweisung finden Sie unter [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
 **Beispiel 1: Erstellen eines eindeutigen Indexes, eines Volltextindexes und eines semantischen Indexes**  
  
 Im folgenden Beispiel wird der Standardvolltextkatalog **ft** erstellt. Im folgenden Beispiel wird ein eindeutiger Index für die **JobCandidateID**-Spalte der **HumanResources.JobCandidate**-Tabelle der AdventureWorks2012-Beispieldatenbank erstellt. Dieser eindeutige Index ist als Schlüsselspalte für einen Volltextindex erforderlich. Im Beispiel werden dann ein Volltextindex und ein semantischer Index in der **Resume**-Spalte erstellt.  
  
```tsql  
CREATE FULLTEXT CATALOG ft AS DEFAULT  
GO  
  
CREATE UNIQUE INDEX ui_ukJobCand  
    ON HumanResources.JobCandidate(JobCandidateID)  
GO  
  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate  
    (Resume  
        Language 1033  
        Statistical_Semantics  
    )   
    KEY INDEX JobCandidateID   
    WITH STOPLIST = SYSTEM  
GO  
```  
  
 **Beispiel 2: Erstellen eines Volltextindexes und eines semantischen Indexes in mehreren Spalten mit verzögerter Indexauffüllung**  
  
 Im folgenden Beispiel wird ein Volltextkatalog **documents_catalog** in der AdventureWorks2012-Beispieldatenbank erstellt. Im Beispiel wird dann ein Volltextindex erstellt, der diesen neuen Katalog verwendet. Der Volltextindex wird in den Spalten **Title**, **DocumentSummary** und **Document** der Tabelle **Production.Document** erstellt, wohingegen der semantische Index nur in der Spalte **Document** erstellt wird. Dieser Volltextindex verwendet den neu erstellten Volltextkatalog und den vorhandenen eindeutigen Schlüsselindex **PK_Document_DocumentID**. Wie empfohlen, wird dieser Indexschlüssel in der ganzzahligen Spalte **DocumentID**erstellt. Im Beispiel ist die LCID für Englisch, 1033, angegeben. Dies entspricht der Sprache der Daten in den Spalten.  
  
 In diesem Beispiel wird auch angegeben, dass die Änderungsnachverfolgung ohne Auffüllung deaktiviert ist. Im Beispiel wird eine **ALTER FULLTEXT INDEX**-Anweisung verwendet, um außerhalb der Spitzenbetriebszeiten eine vollständige Auffüllung mit dem neuen Index zu beginnen und die automatische Änderungsnachverfolgung zu aktivieren.  
  
```tsql  
CREATE FULLTEXT CATALOG documents_catalog  
GO  
  
CREATE FULLTEXT INDEX ON Production.Document  
    (   
    Title  
        Language 1033,   
    DocumentSummary  
        Language 1033,   
    Document   
        TYPE COLUMN FileExtension  
        Language 1033  
        Statistical_Semantics  
    )  
    KEY INDEX PK_Document_DocumentID  
        ON documents_catalog  
        WITH CHANGE_TRACKING OFF, NO POPULATION  
GO  
```  
  
 Der Index wird später zu einem Zeitpunkt mit wenig Datenverkehr aufgefüllt:  
  
```tsql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO  
GO  
```  
  
 **Erstellen eines neuen semantischen Indexes mithilfe von SQL Server Management Studio**  
 Führen Sie den Volltextindizierungs-Assistenten aus, und aktivieren Sie für jede Spalte, in der Sie einen semantischen Index erstellen möchten, die Option **Statistische Semantik** auf der Seite **Tabellenspalten** auswählen. Weitere Informationen, einschließlich Informationen zum Starten des Volltextindizierungs-Assistenten, finden Sie unter [Verwenden des Volltextindizierungs-Assistenten](../../relational-databases/search/use-the-full-text-indexing-wizard.md).  
  
###  <a name="HowToEnableAlter"></a> Vorgehensweise: Erstellen eines semantischen Indexes, wenn ein Volltextindex vorhanden ist  
 Sie können die semantische Indizierung hinzufügen, wenn Sie einen vorhandenen Volltextindex mit der **ALTER FULLTEXT INDEX**-Anweisung ändern. Sie können die semantische Indizierung auch mithilfe verschiedener Dialogfelder in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] hinzufügen.  
  
 **Hinzufügen eines semantischen Indexes mit Transact-SQL**  
 Rufen Sie für jede Spalte, in der Sie einen semantischen Index hinzufügen möchten, die **ALTER FULLTEXT INDEX**-Anweisung mit den unten beschriebenen Optionen auf. Weitere Informationen zu allen Optionen für diese Anweisung finden Sie unter [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
 Sofern Sie nichts anderes angegeben haben, werden sowohl Volltext- als auch semantische Indizes nach einem Aufruf von **ALTER** erneut aufgefüllt.  
  
-   Um einer Spalte nur Volltextindizierung hinzuzufügen, verwenden Sie die **ADD**-Syntax.  
  
-   Um einer Spalte sowohl Volltext- als auch semantische Indizierung hinzuzufügen, verwenden Sie die **ADD**-Syntax mit der **STATISTICAL_SEMANTICS**-Option.  
  
-   Um einer Spalte, die bereits für Volltextindizierung aktiviert wurde, eine semantische Indizierung hinzuzufügen, verwenden Sie die **ADD STATISTICAL_SEMANTICS**-Option. In einer einzigen **ALTER** -Anweisung können Sie einer Spalte nur semantische Indizierung hinzufügen.  
  
 **Beispiel: Hinzufügen von semantischer Indizierung zu einer Spalte, die bereits eine Volltextindizierung aufweist**  
  
 Im folgenden Beispiel wird ein vorhandener Volltextindex für die **Production.Document**-Tabelle in der AdventureWorks2012-Beispieldatenbank geändert. Im Beispiel wird ein semantischer Index in der Spalte **Document** der Tabelle **Production.Document** hinzugefügt, die bereits einen Volltextindex hat. Das Beispiel gibt an, dass der Index nicht automatisch erneut aufgefüllt wird.  
  
```tsql  
ALTER FULLTEXT INDEX ON Production.Document  
    ALTER COLUMN Document  
        ADD Statistical_Semantics  
    WITH NO POPULATION  
GO  
```  
  
 **Hinzufügen eines semantischen Indexes mithilfe von SQL Server Management Studio**  
 Sie können die Spalten, die für die semantische Indizierung und die Volltextindizierung verfügbar sind, auf der Seite **Volltextindexspalten** des Dialogfelds **Volltextindex-Eigenschaften** ändern. Weitere Informationen finden Sie unter [Verwalten von Volltextindizes](../Topic/Manage%20Full-Text%20Indexes.md).  
  
###  <a name="addreq"></a> Anforderungen und Einschränkungen beim Ändern eines vorhandenen Indexes  
  
-   Sie können einen vorhandenen Index nicht ändern, während die Auffüllung des Indexes ausgeführt wird. Weitere Informationen zum Überwachen des Status der Indexauffüllung finden Sie unter [Verwalten und Überwachen der semantischen Suche](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
-   Sie können in einem einzigen Aufruf der **ALTER FULLTEXT INDEX** -Anweisung einer Spalte keine Indizierung hinzufügen und die Indizierung für dieselbe Spalte ändern oder löschen.  
  
##  <a name="dropping"></a> Löschen eines semantischen Indexes  
  
###  <a name="drophow"></a> Vorgehensweise: Löschen eines semantischen Indexes  
 Sie können die semantische Indizierung löschen, wenn Sie einen vorhandenen Volltextindex mit der **ALTER FULLTEXT INDEX**-Anweisung ändern. Sie können die semantische Indizierung auch mithilfe verschiedener Dialogfelder in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] löschen.  
  
 **Löschen eines semantischen Indexes mit Transact-SQL**  
 -   Rufen Sie zum ausschließlichen Löschen der semantischen Indizierung aus Spalten die **ALTER FULLTEXT INDEX**-Anweisung mit der Option **ALTER COLUMN***Spaltenname***DROP STATISTICAL_SEMANTICS** auf. Sie können die Indizierung in einer einzigen **ALTER** -Anweisung aus mehreren Spalten löschen.  
  
    ```tsql  
    USE database_name  
    GO  
  
    ALTER FULLTEXT INDEX  
        ALTER COLUMN column_name  
        DROP STATISTICAL_SEMANTICS  
    GO  
    ```  
  
-   Rufen Sie zum Löschen der Volltextindizierung und der semantischen Indizierung aus einer Spalte die **ALTER FULLTEXT INDEX**-Anweisung mit der Option **ALTER COLUMN***Spaltenname***DROP** auf.  
  
    ```tsql  
    USE database_name  
    GO  
  
    ALTER FULLTEXT INDEX  
        ALTER COLUMN column_name  
        DROP  
    GO  
    ```  
  
 **Löschen eines semantischen Indexes mithilfe von SQL Server Management Studio**  
 Sie können die Spalten, die für die semantische Indizierung und die Volltextindizierung verfügbar sind, auf der Seite **Volltextindexspalten** des Dialogfelds **Volltextindex-Eigenschaften** ändern. Weitere Informationen finden Sie unter [Verwalten von Volltextindizes](../Topic/Manage%20Full-Text%20Indexes.md).  
  
###  <a name="dropreq"></a> Anforderungen und Einschränkungen beim Löschen eines semantischen Indexes  
  
-   Sie können die Volltextindizierung nicht aus einer Spalte löschen, während Sie die semantische Indizierung beibehalten. Die semantische Indizierung ist für Dokumentähnlichkeitsergebnisse von der Volltextindizierung abhängig.  
  
-   Sie können die **NO POPULATION** -Option nicht angeben, wenn Sie die semantische Indizierung aus der letzten Spalte in einer Tabelle löschen, für die die semantische Indizierung aktiviert wurde. Zur Entfernung der Ergebnisse, die zuvor indiziert wurden, ist ein Auffüllungszyklus erforderlich.  
  
## Überprüfen, ob die semantische Suche für Datenbankobjekte aktiviert ist  
  
###  <a name="HowToCheckEnabled"></a> Vorgehensweise: Überprüfen, ob die semantische Suche für Datenbankobjekte aktiviert ist  
 **Ist die semantische Suche für eine Datenbank aktiviert?**  
 Fragen Sie die Eigenschaft **IsFullTextEnabled** der Metadatenfunktion [DATABASEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) ab.  
  
 Der Rückgabewert 1 gibt an, dass die Volltextsuche und die semantische Suche für die Datenbank aktiviert sind; der Rückgabewert 0 gibt an, dass sie nicht aktiviert sind.  
  
```tsql  
SELECT DATABASEPROPERTYEX('database_name', 'IsFullTextEnabled')  
GO  
```  
  
 **Ist die semantische Suche für eine Tabelle aktiviert?**  
 Fragen Sie die Eigenschaft **TableFullTextSemanticExtraction** der Metadatenfunktion [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md) ab.  
  
 Der Rückgabewert 1 gibt an, dass die semantische Suche für die Tabelle aktiviert ist; der Rückgabewert 0 gibt an, dass sie nicht aktiviert ist.  
  
```scr  
SELECT OBJECTPROPERTYEX(OBJECT_ID('table_name'), 'TableFullTextSemanticExtraction')  
GO  
```  
  
 **Ist die semantische Suche für eine Spalte aktiviert?**  
 So bestimmen Sie, ob die semantische Suche für eine bestimmte Spalte aktiviert ist:  
  
-   Fragen Sie die Eigenschaft **StatisticalSemantics** der Metadatenfunktion [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md) ab.  
  
     Der Rückgabewert 1 gibt an, dass die semantische Suche für die Spalte aktiviert ist; der Rückgabewert 0 gibt an, dass sie nicht aktiviert ist.  
  
    ```tsql  
    SELECT COLUMNPROPERTY(OBJECT_ID('table_name'), 'column_name', 'StatisticalSemantics')  
    GO  
    ```  
  
-   Fragen Sie die Katalogsicht [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) für den Volltextindex ab.  
  
     Der Wert 1 in der **statistical_semantics**-Spalte gibt an, dass die angegebene Spalte zusätzlich zur Volltextindizierung für die semantische Indizierung aktiviert ist.  
  
    ```tsql  
    SELECT * FROM sys.fulltext_index_columns WHERE object_id = OBJECT_ID('table_name')  
    GO  
    ```  
  
-   Klicken Sie im Objekt-Explorer in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] mit der rechten Maustaste auf eine Spalte, und wählen Sie **Eigenschaften** aus. Überprüfen Sie auf der Seite **Allgemein** des Dialogfelds **Spalteneigenschaften** den Wert der Eigenschaft **Statistical Semantics** .  
  
     Der Wert TRUE gibt an, dass die angegebene Spalte zusätzlich zur Volltextindizierung für die semantische Indizierung aktiviert ist.  
  
## Ermitteln der indizierbaren Objekte für die semantische Suche  
  
###  <a name="HowToCheckLanguages"></a> Vorgehensweise: Ermitteln der für die semantische Suche unterstützten Sprachen  
  
> [!IMPORTANT]  
>  Für die semantische Indizierung werden weniger Sprachen als für die Volltextindizierung unterstützt. Es gibt daher möglicherweise Spalten, die für die Volltextsuche, aber nicht für die semantische Suche indiziert werden können.  
  
 Fragen Sie die Katalogsicht [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md) ab.  
  
```tsql  
SELECT * FROM sys.fulltext_semantic_languages  
GO  
```  
  
 Für die semantische Indizierung werden die folgenden Sprachen unterstützt: Dieses Liste stellt die Ausgabe der Katalogsicht [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md) nach der LCID sortiert dar.  
  
|Sprache|LCID|  
|--------------|----------|  
|Deutsch|1031|  
|Englisch (USA)|1033|  
|Französisch|1036|  
|Italienisch|1040|  
|Portugiesisch (Brasilien)|1046|  
|Russisch|1049|  
|Schwedisch|1053|  
|Englisch (Großbritannien)|2057|  
|Portugiesisch (Portugal)|2070|  
|Spanisch|3082|  
  
###  <a name="doctypes"></a> Vorgehensweise: Ermitteln, welche Dokumenttypen indiziert werden können  
 Fragen Sie die Katalogsicht [sys.fulltext_document_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) ab.  
  
 Wenn der zu indizierende Dokumenttyp nicht in der Liste der unterstützten Typen aufgeführt wird, müssen Sie möglicherweise zusätzliche Filter suchen, herunterladen und installieren. Weitere Informationen finden Sie unter [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="BestPracticeFilegroup"></a> Bewährte Methode: Erwägen der Erstellung einer separaten Dateigruppe für Volltextindizes und semantische Indizes  
 Erwägen Sie, eine separate Dateigruppe für den Volltext- und den semantischen Index zu erstellen, wenn Sie Bedenken im Hinblick auf die Speicherplatzzuordnung haben. Die semantischen Indizes werden in derselben Dateigruppe wie der Volltextindex erstellt. Ein vollständig aufgefüllter semantischer Index kann eine große Datenmenge enthalten.  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="IssueNoResults"></a> Problem: Das Durchsuchen einer bestimmten Spalte gibt keine Ergebnisse zurück  
 **Wurde eine Nicht-Unicode-LCID für eine Unicode-Sprache angegeben?**  
 Es ist möglich, die semantische Indizierung für einen Nicht-Unicode-Spaltentyp mit einer LCID für eine Sprache zu aktivieren, die nur Unicode-Wörter aufweist, z. B. LCID 1049 für Russisch. In diesem Fall werden nie Ergebnisse von den semantischen Indizes in dieser Spalte zurückgegeben.  
  
  