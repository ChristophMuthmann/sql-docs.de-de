---
title: "Volltextsuche | Microsoft Docs"
ms.custom: ""
ms.date: "07/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Volltextsuche [SQL Server]"
ms.assetid: a0ce315d-f96d-4e5d-b4eb-ff76811cab75
caps.latest.revision: 54
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 49
---
# Volltextsuche
  Mit der Volltextsuche in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] können Benutzer und Anwendungen Volltextabfragen für zeichenbasierte Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabellen ausführen. Bevor Sie Volltextabfragen für eine bestimmte Tabelle ausführen können, muss der Datenbankadministrator einen Volltextindex für die Tabelle erstellen. Der Volltextindex umfasst eine oder mehrere zeichenbasierte Spalten der Tabelle. Diese Spalten können jeden der folgenden Datentypen aufweisen: **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml** oder **varbinary(max)** und FILESTREAM. Jeder Volltextindex indiziert mindestens eine Spalte aus der Basistabelle. Für jede Spalte kann hierbei eine eigene Sprache verwendet werden.  
  
 Volltextabfragen führen linguistische Suchvorgänge für Textdaten in Volltextindizes durch. Dabei werden Wörter und Ausdrücke anhand von Regeln einer bestimmten Sprache (z. B. Englisch oder Japanisch) verarbeitet. Volltextabfragen können einfache Wörter und Ausdrücke oder mehrere Formen eines Worts bzw. Ausdrucks enthalten. Eine Volltextabfrage gibt alle Dokumente zurück, die mindestens eine Übereinstimmung (auch als *Treffer* bezeichnet) enthalten. Eine Übereinstimmung wird gefunden, wenn ein Zieldokument alle in der Volltextabfrage angegebenen Begriffe enthält und alle sonstigen Suchbedingungen erfüllt sind, z. B. der Abstand zwischen den übereinstimmenden Begriffen.  
  
> **HINWEIS** Die Volltextsuche ist eine optionale Komponente des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankmoduls. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md).  
  
##  <a name="queries"></a> Volltextsuche – Abfragen  
 Nachdem einem Volltextindex Spalten hinzugefügt wurden, können Benutzer und Anwendungen Volltextabfragen zum Text in diesen Spalten ausführen. Bei diesen Abfragen kann nach Folgendem gesucht werden:  
  
-   Mindestens ein Wort oder Ausdruck (*einfacher Begriff*)  
  
-   Ein Wort oder Ausdruck, bei dem die Wörter mit dem angegebenen Text beginnen (*Präfixbegriff*)  
  
-   Flexionsformen eines bestimmten Worts (*Generierungsbegriff*)  
  
-   Ein Wort oder Ausdruck in der Nähe eines anderen Worts oder Ausdrucks (*Näherungsbegriff*)  
  
-   Synonyme Formen eines bestimmten Worts (*Thesaurus*)  
  
-   Wörter oder Ausdrücke mit gewichteten Werten (*gewichteter Begriff*)  
  
 Bei Volltextabfragen wird die Groß- und Kleinschreibung nicht beachtet. Wenn Sie beispielsweise nach "Aluminium" oder "aluminium" suchen, werden dieselben Ergebnisse zurückgegeben.  
  
 Volltextabfragen verwenden eine geringe Anzahl von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prädikaten (CONTAINS und FREETEXT) und -Funktionen (CONTAINSTABLE und FREETEXTTABLE). Die Suchziele des jeweiligen Geschäftsszenarios beeinflussen jedoch die Struktur von Volltextabfragen. Beispiel:  
  
-   e-Business – Suchen nach einem Produkt auf einer Website:  
  
    ```  
    SELECT product_id   
    FROM products   
    WHERE CONTAINS(product_description, ”Snap Happy 100EZ” OR FORMSOF(THESAURUS,’Snap Happy’) OR ‘100EZ’)   
    AND product_cost < 200 ;  
    ```  
  
-   Einstellungsszenario – Suchen nach Jobkandidaten, die bereits mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gearbeitet haben:  
  
    ```  
    SELECT candidate_name,SSN   
    FROM candidates   
    WHERE CONTAINS(candidate_resume,”SQL Server”) AND candidate_division =DBA;  
    ```  
  
 Weitere Informationen finden Sie unter [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md).  
  
##  <a name="like"></a> Vergleichen von LIKE und der Volltextsuche  
 Im Gegensatz zur Volltextsuche verarbeitet das [LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]-Prädikat ausschließlich Zeichenmuster. Darüber hinaus können Sie mit dem LIKE-Prädikat keine formatierten Binärdaten abfragen. Eine LIKE-Abfrage in umfangreichen unstrukturierten Textdaten ist sehr viel langsamer als eine entsprechende Volltextabfrage in denselben Daten. Eine LIKE-Abfrage für Millionen von Zeilen von Textdaten kann Minuten in Anspruch nehmen; eine Volltextabfrage kann dagegen in Sekunden oder weniger für dieselben Daten ein Ergebnis liefern, je nach Anzahl der zurückgegebenen Zeilen.  
  
##  <a name="architecture"></a> Komponenten und Architektur  
 Die Architektur der Volltextsuche besteht aus den folgenden Prozessen:  
  
-   Dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess (sqlservr.exe)  
  
-   Dem Filterdaemon-Hostprozess (fdhost.exe)  
  
     Aus Sicherheitsgründen werden Filter von separaten Prozessen geladen, die als Filterdaemonhosts bezeichnet werden. Die fdhost.exe-Prozesse werden von einem FDHOST-Startprogrammdienst (MSSQLFDLauncher) erstellt und unter den Sicherheitsanmeldeinformationen des FDHOST-Startprogrammdiensts ausgeführt. Daher muss der FDHOST-Startprogrammdienst ausgeführt werden, damit die Volltextindizierung und Volltextabfragen funktionieren. Informationen zum Festlegen des Dienstkontos für diesen Dienst finden Sie unter [Festlegen des Dienstkontos für das Startprogramm des Volltextfilterdaemons](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md).  
  
 Diese beiden Prozesse enthalten die Komponenten, aus denen die Architektur der Volltextsuche besteht. Die Komponenten und ihre Beziehungen sind in der folgenden Abbildung zusammengefasst. Auf die Abbildung folgt eine Beschreibung der Komponenten.  
  
 ![Architektur der Volltextsuche](../../relational-databases/search/media/ifts-arch.gif "Architektur der Volltextsuche")  
  
###  <a name="sqlprocess"></a> SQL Server-Prozess  
 Für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess werden die folgenden Komponenten für die Volltextsuche verwendet:  
  
-   **Benutzertabellen** Diese Tabellen enthalten die Daten, für die ein Volltextindex erstellt werden soll.  
  
-   **Volltext-Gatherer** Der Volltext-Gatherer verwendet die Volltextdurchforstungsthreads. Er ist für das Planen und Antreiben der Auffüllung von Volltextindizes sowie für das Überwachen von Volltextkatalogen verantwortlich.  
  
-   **Thesaurusdateien** Diese Dateien enthalten Synonyme von Suchbegriffen. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
-   **Stopplistenobjekte** Stopplistenobjekte enthalten eine Liste häufig auftretender Wörter, die nicht nützlich für die Suche sind. Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abfrageprozessor** Der Abfrageprozessor kompiliert SQL-Abfragen und führt diese aus. Wenn eine SQL-Abfrage eine Volltextsuchabfrage enthält, wird die Abfrage sowohl während der Kompilierung als auch während der Ausführung an das Volltextsuchmodul gesendet. Das Abfrageergebnis wird mit dem Volltextindex verglichen.  
  
-   **Volltextmodul** Das Volltextsuchmodul in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist vollständig in den Abfrageprozessor integriert. Das Volltextsuchmodul kompiliert Volltextabfragen und führt diese aus. Im Rahmen der Abfrageausführung empfängt das Volltextsuchmodul möglicherweise Eingaben vom Thesaurus und von der Stoppliste.  
  
-   **Indexschreiber (Indexer)** Der Indexschreiber erstellt die Struktur, die zum Speichern der indizierten Token verwendet wird.  
  
-   **Filterdaemon-Manager** Der Filterdaemon-Manager ist für die Überwachung des Status des Filterdaemonhosts des Volltextsuchmoduls verantwortlich.  
  
##  <a name="fdhostprocess"></a> Filterdaemon-Hostprozess  
 Der Filterdaemonhost ist ein Prozess, der vom Volltextsuchmodul gestartet wird. Er führt die folgenden Komponenten der Volltextsuche aus, die für den Zugriff auf, die Filterung von und die Wörtertrennung für Daten aus Tabellen sowie für die Wörtertrennung und Wortstammerkennung für Abfrageeingaben verantwortlich sind.  
  
 Der Filterdaemonhost umfasst die folgenden Komponenten:  
  
-   **Protokollhandler** Diese Komponente ruft die Daten aus dem Arbeitsspeicher zur weiteren Verarbeitung ab und greift auf Daten aus einer Benutzertabelle in einer angegebenen Datenbank zu. Zu ihren Aufgaben gehört das Erfassen von Daten aus den volltextindizierten Spalten sowie deren Übergabe an den Filterdaemonhost, der bei Bedarf die Filterung und die Wörtertrennung anwendet.  
  
-   **Filter.** Bei einigen Datentypen ist eine Filterung erforderlich, bevor die Daten in einem Dokument volltextindiziert werden können. Dazu zählen Daten in **varbinary**-, **varbinary(max)**-, **image**- oder **xml**-Spalten. Welcher Filter für ein bestimmtes Dokument verwendet wird, ist vom Dokumenttyp abhängig. Beispielsweise werden für Microsoft Word-Dokumente (DOC), Microsoft Excel-Dokumente (XLS) und XML-Dokumente unterschiedliche Filter verwendet. Anschließend extrahiert der Filter Textabschnitte aus dem Dokument. Dabei werden eingebettete Formatierungen entfernt, der Text und ggf. Informationen über seine Position werden beibehalten. Das Ergebnis ist ein Datenstrom von Textinformationen. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
-   **Wörtertrennung und Wortstammerkennung** Die Wörtertrennung ist eine sprachspezifische Komponente, die anhand von lexikalischen Regeln einer bestimmten Sprache Wortgrenzen erkennt (*Wörtertrennung*). Jede Wörtertrennung ist einer sprachspezifischen Wortstammerkennungskomponente zugeordnet, die Verben konjugiert und flektierende Erweiterungen vornimmt. Bei der Indizierung verwendet der Filterdaemonhost die Wörtertrennung und die Wortstammerkennung, um eine linguistische Analyse der Textdaten aus einer angegebenen Tabellenspalte durchzuführen. Die Sprache, die einer Tabellenspalte im Volltextindex zugeordnet ist, bestimmt, welche Wörtertrennung und Wortstammerkennung zum Indizieren der Spalte verwendet wird. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
##  <a name="processing"></a> Verarbeitung der Volltextsuche  
 Die Volltextsuche beruht auf dem Volltextmodul. Das Volltextmodul erfüllt zwei Funktionen: Unterstützung der Indizierung und Unterstützung von Abfragen.  
  
###  <a name="indexing"></a> Der Vorgang der Volltextindizierung  
 Wenn eine Volltextauffüllung (auch als "Durchforstung" bezeichnet) initiiert wird, werden vom Volltextmodul große Batches von Daten in den Arbeitsspeicher geladen, und der Filterdaemonhost wird benachrichtigt. Der Host führt Filterung und Wörtertrennung aus und konvertiert die Daten in invertierte Wortlisten. Die konvertierten Daten werden dann von der Volltextsuche aus den Wortlisten abgerufen, Stoppwörter werden entfernt, und die Wortlisten werden für einen Batch in einem oder mehreren invertierten Indizes gespeichert.  
  
 Sind die Indizierungsdaten in einer **varbinary(max)**- oder **image**-Spalte gespeichert, extrahiert der Filter, der die **IFilter**-Schnittstelle implementiert, Text basierend auf dem angegebenen Dateiformat für diese Daten (z.B. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word). In manchen Fällen erfordern die Filterkomponenten, dass die **varbinary(max)**- oder **image**-Daten statt in den Arbeitsspeicher in den Filterdatenordner geschrieben werden.  
  
 Im Rahmen der Verarbeitung durchlaufen die gesammelten Textdaten eine Wörtertrennung, die den Text in einzelne Token oder Schlüsselwörter zerlegt. Die Sprache für die Zerlegung in Token wird auf Spaltenebene angegeben oder kann in **varbinary(max)**-, **image**- oder **xml**-Daten durch die Filterkomponente identifiziert werden.  
  
 Unter Umständen werden weitere Verarbeitungsschritte ausgeführt, um Stoppwörter zu entfernen und Token zu normalisieren, bevor sie im Volltextindex oder einem Indexfragment gespeichert werden.  
  
 Nach dem Ende einer Auffüllung wird ein abschließender Mergeprozess ausgelöst, der die Indexfragmente zu einem Mastervolltextindex zusammenführt. Dies ermöglicht eine verbesserte Abfrageleistung, da statt mehrerer Indexfragmente nur der Masterindex abgefragt werden muss. Zudem können bessere Bewertungsstatistiken zum Erstellen der Relevanzrangfolge verwendet werden.  
  
###  <a name="querying"></a> Der Vorgang der Volltextabfrage  
 Der Abfrageprozessor übergibt die Volltextteile einer Abfrage zur Verarbeitung an das Volltextmodul. Das Volltextmodul führt Worttrennungen sowie optional Thesauruserweiterungen, Wortstammerkennung und Stoppwort-/Füllwortverarbeitung durch. Die Volltextteile der Abfrage werden dann in Form von SQL-Operatoren dargestellt, vorrangig als Streaming-Tabellenwertfunktionen. Während der Abfrageausführung greifen diese Streaming-Tabellenwertfunktionen auf den invertierten Index zu, um die richtigen Ergebnisse abzurufen. Die Ergebnisse werden entweder zu diesem Zeitpunkt an den Client zurückgegeben oder vor der Rückgabe an den Client weiter verarbeitet.  
  
##  <a name="components"></a> Linguistische Komponenten und Sprachunterstützung in Volltextsuche  
 Die Volltextsuche unterstützt fast 50 verschiedene Sprachen, z. B. Englisch, Spanisch, Chinesisch, Japanisch, Arabisch, Bangla und Hindi. Eine vollständige Liste der unterstützten Volltextsprachen finden Sie unter [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md). Jeder Spalte, die im Volltextindex enthalten ist, ist ein Microsoft Windows-Gebietsschemabezeichner (LCID) zugeordnet, der einer von der Volltextsuche unterstützten Sprache entspricht. Der LCID 1033 entspricht beispielsweise US-Englisch, und der LCID 2057 steht für britisches Englisch. Für jede unterstützte Volltextsprache bietet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] linguistische Komponenten, die die Indizierung und Abfrage von in dieser Sprache gespeicherten Volltextdaten unterstützen.  
  
 Sprachspezifische Komponenten umfassen Folgendes:  
  
-   **Wörtertrennung und Wortstammerkennung** Die Wörtertrennung erkennt Wortgrenzen anhand der lexikalischen Regeln einer bestimmten Sprache (*Wörtertrennung*). Jeder Wörtertrennung ist eine Wortstammerkennung zugeordnet, die Verben für diese Sprache konjugiert. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
-   **Stopplisten** Eine Systemstoppliste enthält eine Reihe grundlegender Stoppwörter (Füllwörter). Ein *Stoppwort* ist ein Wort, das nicht zur Suche beiträgt und in Volltextabfragen ignoriert wird. Im deutschen Gebietsschema werden beispielsweise Wörter wie "ein", "und", "ist" und "der/die/das" als Stoppwörter betrachtet. In der Regel müssen Sie eine oder mehrere Thesaurusdateien und Stopplisten konfigurieren. Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
-   **Thesaurusdateien** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert außerdem eine Thesaurusdatei für jede Volltextsprache sowie eine globale Thesaurusdatei. Die installierten Thesaurusdateien sind im Wesentlichen leer, Sie können sie jedoch so bearbeiten, dass sie Synonyme für eine bestimmte Sprache oder Geschäftsszenarien definieren. Indem Sie einen Thesaurus entwickeln, der genau auf Ihre Volltextdaten abgestimmt ist, können Sie den Bereich der Volltextabfragen für diese Daten effektiv erweitern. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
-   **Filter (iFilters)**  Die Indizierung eines Dokuments in einer Spalte mit dem Datentyp **varbinary(max)**, **image** oder **xml** erfordert einen Filter für die Ausführung zusätzlicher Verarbeitungsschritte. Der Filter muss für den Dokumenttyp spezifisch sein (DOC, PDF, XLS, XML und so weiter). Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
 Wörtertrennung (und Wortstammerkennung) sowie Filter werden im Filterdaemon-Hostprozess (fdhost.exe) ausgeführt.  
  
##  <a name="reltasks"></a> Verwandte Aufgaben  
  
-   [Erste Schritte mit der Volltextsuche](../../relational-databases/search/get-started-with-full-text-search.md)  
  
-   **Schreiben von Volltextabfragen**  
  
    -   [Abfragen mit Volltextsuche](../../relational-databases/search/query-with-full-text-search.md)  
  
    -   [Suchen von Wörtern in der Nähe eines anderen Worts mit NEAR](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)  
  
    -   [Einschränken von Suchergebnissen mit RANK](../../relational-databases/search/limit-search-results-with-rank.md)  
  
    -   [Verbessern der Leistung von Volltextabfragen](../../relational-databases/search/improve-the-performance-of-full-text-queries.md)  
  
    -   [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
    -   [Suchen von Eigenschaftensatz-GUIDS und ganzzahligen Eigenschaft-IDs für Sucheigenschaften](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
-   **Verwalten von Katalogen und Indizes**  
  
    -   [Erstellen und Verwalten von Volltextkatalogen](../../relational-databases/search/create-and-manage-full-text-catalogs.md)  
  
    -   [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md)  
  
    -   [Auswählen einer Sprache beim Erstellen eines Volltextindex](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)  
  
    -   [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md)  
  
    -   [Verwalten von Volltextindizes](../Topic/Manage%20Full-Text%20Indexes.md)  
  
    -   [Verbessern der Leistung von Volltextindizes](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
    -   [Behandeln von Problemen mit der Volltextindizierung](../../relational-databases/search/troubleshoot-full-text-indexing.md)  
  
    -   [Sichern und Wiederherstellen von Volltextkatalogen und Indizes](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   **Verwalten der linguistischen Komponenten**  
  
    -   [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
    -   [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
    -   [Anzeigen oder Ändern von registrierten Filtern und Wörtertrennungen](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)  
  
    -   [Wiederherstellen der von der Suche verwendeten Wörtertrennungen auf die vorherige Version](../../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
    -   [Ändern der für Englisch (USA) und Englisch (Großbritannien) verwendeten Wörtertrennung](../../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
    -   [Anpassen des Verhaltens der Wörtertrennung mit einem Benutzerwörterbuch](../../relational-databases/search/customize-the-behavior-of-word-breakers-with-a-custom-dictionary.md)  
  
    -   [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
    -   [Konfigurieren und Verwalten von Thesaurusdateien für die Volltextsuche](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
-   **Verwalten der Volltextsuche**  
  
    -   [Verwalten und Überwachen der Volltextsuche auf einer Serverinstanz](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)  
  
    -   [Festlegen des Dienstkontos für das Startprogramm des Volltextfilterdaemon](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
  
-   [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md)Upgrade der Volltextsuche  
  
##  <a name="relcontent"></a> Verwandte Inhalte  
  
-   [DDL, Funktionen, gespeicherte Prozeduren und Sichten für Volltextsuche](../../relational-databases/search/full-text-search-ddl-functions-stored-procedures-and-views.md)  
  
  
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
