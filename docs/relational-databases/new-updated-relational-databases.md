---
title: Aktualisiert – Dokumentation zu relationalen Datenbanken | Microsoft-Dokumentation
description: Zeigen Sie Codeausschnitte von aktualisierten Inhalten in der zuletzt geänderten Dokumentation zu relationale Datenbanken an.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 02/03/2018
ms.openlocfilehash: f30e38adef7faedb273dbd1b22c4ac9d3e8223b4
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Neu und zuletzt aktualisiert: Dokumentation zu relationalen Datenbanken



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **3.12.2017** &nbsp; bis &nbsp; **3.2.2018**
- *Themenbereich:* &nbsp; **Relationale Datenbanken**




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Speichern von JSON-Dokumenten in SQL Server oder SQL-Datenbank](json/store-json-documents-in-sql-tables.md)
2. [Sicherheitsrisikobewertung mit der SQL](security/sql-vulnerability-assessment.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Datenbankdatei-Initialisierung](#TitleNum_1)
2. [tempdb-Datenbank](#TitleNum_2)
3. [JSON-Daten in SQL Server](#TitleNum_3)
4. [Lektion 1: Herstellen einer Verbindung mit dem Datenbankmodul](#TitleNum_4)
5. [Verwalten der Größe der Transaktionsprotokolldatei](#TitleNum_5)
6. [bcp_bind](#TitleNum_6)
7. [Handbuch zum SQL Server Indexentwurf](#TitleNum_7)
8. [sp_execute_external_script (Transact-SQL)](#TitleNum_8)
9. [Erstellen von Primärschlüsseln](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-database-file-initializationdatabasesdatabase-instant-file-initializationmd"></a>1. &nbsp; [Datenbankdatei-Initialisierung](databases/database-instant-file-initialization.md)

*Aktualisiert: 23.1.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 81.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5f2aa53a8b43d4c43e0602cf945cb7c7028a27d 04c261c6588af1f53cda2fce3e9a86167c50b686  (PR=4702  ,  Filename=database-instant-file-initialization.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=3206a31870f8febab7d1718fa59fe0590d4d45db) -->



```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**Gilt für:** SQL Server (ab SQL Server 2012 SP4, SQL Server 2014 SP2 und von SQL Server 2016 bis SQL Server 2017)

**Überlegungen zur Sicherheit**

Da bei Verwendung der schnellen Dateiinitialisierung (Instant File Initialization, IFI) der gelöschte Datenträgerinhalt nur überschrieben wird, wenn neue Daten in die Dateien geschrieben werden, kann ein nicht autorisierter Prinzipal möglicherweise so lange auf den gelöschten Inhalt zugreifen, bis andere Daten in diesen Bereich der Datendatei geschrieben werden. Während die Datenbankdatei an die Instanz von SQL Server angefügt ist, wird diese Gefahr einer Offenlegung von Informationen durch die besitzerverwaltete Zugriffssteuerungsliste (Discretionary Access Control List, DACL) in der Datei verringert. Diese DACL gewährt den Dateizugriff nur für das SQL Server-Dienstkonto und den lokalen Administrator. Wenn die Datei jedoch getrennt wird, kann möglicherweise ein Benutzer oder Dienst darauf zugreifen, der nicht über SE\_MANAGE\_VOLUME_NAME verfügt. Eine ähnliche Betrachtung ergibt sich bei der Sicherung der Datenbank: Der gelöschte Inhalt kann für einen nicht autorisierten Benutzer oder Dienst verfügbar werden, wenn die Sicherungsdatei nicht mit einer entsprechenden DACL geschützt wird.

Außerdem kann es sein, dass ein SQL Server-Administrator Zugriff auf die grundlegenden Inhalte der Seite und bereits gelöschte Inhalte erhält, wenn eine Datei über die schnelle Dateiinitialisierung erstellt wird.

Wenn die Datenbankdateien auf einem Storage Area Network gehostet werden, kann es außerdem sein, dass das Storage Area Network neue Seiten immer als vorinitialisiert anzeigt und die Vorinitialisierung der Seiten durch das Betriebssystem würde einen unnötigen zeitlichen Mehraufwand bedeuten.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>2. &nbsp; [tempdb-Datenbank](databases/tempdb-database.md)

*Aktualisiert: 17.1.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Vorheriger](#TitleNum_1) | [Nächster](#TitleNum_3))

<!-- Source markdown line 100.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d 3257c92d6e2a88968fc44e5f6262c02cd0624635  (PR=0  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



 Eine Beschreibung dieser Datenbankoptionen finden Sie unter [ALTER DATABASE SET-Optionen (Transact-SQL)](databases/../../t-sql/statements/alter-database-transact-sql-set-options.md).

**tempdb-Datenbank in SQL-Datenbank**


|SLO|Maximale Dateigröße für tempdb-Daten (MB)|Anzahl von tempdb-Datendateien|Maximale Datengröße für tempdb (MB)|
|---|---:|---:|---:|
|Standard|14,225|1|14,225|
|S0|14,225|1|14,225|
|S1|14,225|1|14,225|
|S2|14,225| 1|14,225|
|S3|32,768|1|32,768|
|S4|32,768|2|65,536|
|S6|32,768|3|98,304|
|S7|32,768|6|196,608|
|S9|32,768|12|393,216|
|S12|32,768|12|393,216|
|P1|32,768|12|393,216|
|P2|32,768|12|393,216|
|P4|32,768|12|393,216|
|P6|32,768|12|393,216|
|P11|32,768|12|393,216|
|P15|32,768|12|393,216|
|Elastischer Premium-Pool (alle DTU-Konfigurationen)|14,225|12|170,700|
|Elastischer Standard-Pool (alle DTU-Konfigurationen)|14,225|12|170,700|
|Elastischer Basic-Pool (alle DTU-Konfigurationen)|14,225|12|170,700|
||||




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>3. &nbsp; [JSON-Daten in SQL Server](json/json-data-sql-server.md)

*Aktualisiert: 1.2.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Vorheriger](#TitleNum_2) | [Nächster](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 62dd9c68d8cb72d6bf51b941a0731224514f0a7f 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5  (PR=4783  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=73f18ae24a9a48234bf997ee9a2ef441bc4918b9) -->



-   [Load GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/)

**Analysieren von JSON-Daten mit SQL-Abfragen**

Wenn Sie JSON-Daten für Berichtszwecke filtern oder aggregieren müssen, können Sie JSON mithilfe von **OPENJSON** in ein relationales Format transformieren. Sie können dann Standard-Transact-SQL-Funktionen oder integrierte Funktionen verwenden, um die Berichte vorzubereiten.

```
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM   SalesOrderRecord AS Tab
          CROSS APPLY
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')
           WITH (
              Number   varchar(200) N'$.Order.Number',
              Date     datetime     N'$.Order.Date',
              Customer varchar(200) N'$.AccountNumber',
              Quantity int          N'$.Item.Quantity'
           )
  AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified
```



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-lesson-1-connecting-to-the-database-enginelesson-1-connecting-to-the-database-enginemd"></a>4. &nbsp; [Lektion 1: Herstellen einer Verbindung mit der Datenbank-Engine](lesson-1-connecting-to-the-database-engine.md)

*Aktualisiert: 13.12.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Vorheriger](#TitleNum_3) | [Nächster](#TitleNum_5))

<!-- Source markdown line 79.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c070935895450fd2ea054e2be9e1c48f7dc2b6c 0c386e3d47fb7f8f1e63b9301f0cafec2bc88ab0  (PR=4282  ,  Filename=lesson-1-connecting-to-the-database-engine.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=6e016a4ffd28b09456008f40ff88aef3d911c7ba) -->



2.  Wählen Sie **Datenbankmodul**aus.

    ![Objekt-Explorer](../relational-databases/media/object-explorer.png)

3.  Geben Sie im Feld **Servername** den Namen der Instanz der Datenbank-Engine ein. Bei der Standardinstanz von SQL Server ist der Servername der Name des Computers. Bei einer benannten Instanz von SQL Server ist der Servername der *<Computername>***\\***<Instanzname>*, wie z.B. **ACCTG_SRVR\SQLEXPRESS**. Der folgende Screenshot zeigt das Herstellen einer Verbindung mit der (unbenannten) Standardinstanz von SQL Server auf einem Computer namens „PracticeComputer“. Der Benutzer, der bei Windows angemeldet ist, ist Mary aus der Domain „Contoso“. Bei Verwendung der Windows-Authentifizierung können Sie den Benutzernamen nicht ändern.

    ![Verbindung-mit-Server-herstellen](../relational-databases/media/connect-to-server.png)

4.  Klicken Sie auf **Verbinden**.

> [!NOTE]
> In diesem Tutorial wird davon ausgegangen, dass Sie noch keine Vorkenntnisse zu SQL Server besitzen und keine besonderen Probleme beim Herstellen einer Verbindung haben. Dies sollte für die meisten Benutzer ausreichen, und so wird das Tutorial einfach gehalten. Detaillierte Schritte zur Fehlerbehebung finden Sie unter [Beheben von Verbindungsfehlern mit dem SQL Server-Datenbankmodul](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

**<a name="additional"></a>Autorisieren zusätzlicher Verbindungen**

Nachdem Sie als Administrator eine Verbindung mit SQL Server hergestellt haben, besteht eine Ihrer ersten Aufgaben darin, andere Benutzer zum Herstellen einer Verbindung zu autorisieren. Dazu erstellen Sie eine Anmeldung und erteilen dieser Anmeldung die Berechtigung, als Benutzer auf eine Datenbank zuzugreifen. Anmeldungen können über die Windows-Authentifizierung erfolgen, die Windows-Anmeldeinformationen verwendet, oder über die SQL Server-Authentifizierung, die Authentifizierungsinformationen in SQL Server speichert und von Ihren Windows-Anmeldeinformationen unabhängig ist. Verwenden Sie nach Möglichkeit immer Windows-Authentifizierung.



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-manage-the-size-of-the-transaction-log-filelogsmanage-the-size-of-the-transaction-log-filemd"></a>5. &nbsp; [Verwalten der Größe der Transaktionsprotokolldatei](logs/manage-the-size-of-the-transaction-log-file.md)

*Aktualisiert: 17.1.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Vorheriger](#TitleNum_4) | [Nächster](#TitleNum_6))

<!-- Source markdown line 105.  ms.author= "jhubbard".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5847b31cf8f6003a380f0c8aaa289efdc55be678 84e45320d81db218cde17fbf8b9668a9ac3805a7  (PR=0  ,  Filename=manage-the-size-of-the-transaction-log-file.md  ,  Dirpath=docs\relational-databases\logs\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



-   Ein kleines Vergrößerungsinkrement könnte dazu führen, dass zu viele kleine [VLFs](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) generiert werden und die Leistung beeinträchtigt wird. Informationen darüber, wie Sie die optimale VLF-Verteilung für die aktuelle Größe des Transaktionsprotokolls aller Datenbanken in einer bestimmten Instanz sowie die benötigten Wachstumsinkremente zum Erreichen der erforderlichen Größe ermitteln, finden Sie in [diesem Skript](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).

-   Ein großes Vergrößerungsinkrement könnte dazu führen, dass wenige große [VLFs](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) generiert werden und darüber hinaus die Leistung beeinträchtigt. Informationen darüber, wie Sie die optimale VLF-Verteilung für die aktuelle Größe des Transaktionsprotokolls aller Datenbanken in einer bestimmten Instanz sowie die benötigten Wachstumsinkremente zum Erreichen der erforderlichen Größe ermitteln, finden Sie in [diesem Skript](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).

-   Auch bei aktiviertem autogrow-Inkrement können Sie eine Meldung erhalten, dass das Transaktionsprotokoll voll ist, wenn es nicht schnell genug wachsen kann, um die Anforderungen Ihrer Abfrage zu erfüllen. Weitere Informationen zum Ändern des Vergrößerungsinkrements finden Sie unter [ALTER DATABASE-Optionen FILE und FILEGROUP &#40;Transact-SQL&#41;](logs/../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

-   Durch die Verwaltung von mehreren Protokolldateien in einer Datenbank wird die Leistung in keiner Weise verbessert, da die Transaktionsprotokolldateien nicht wie Datendateien eine [proportionale Füllung](logs/../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill) in derselben Dateigruppe durchführen.

-   Für Protokolldateien kann eine automatische Verkleinerung durchgeführt werden. Dies wird jedoch **nicht empfohlen**, und die Datenbankeigenschaft **auto_shrink** ist standardmäßig auf FALSE festgelegt. Wenn **auto_shrink** auf TRUE festgelegt ist, wird die Größe einer Datei nur dann automatisch verkleinert, wenn mehr als 25 Prozent des Speicherplatzes ungenutzt sind.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-bcpbindnative-client-odbc-extensions-bulk-copy-functionsbcp-bindmd"></a>6. &nbsp; [bcp_bind](native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)

*Aktualisiert: 30.1.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Vorheriger](#TitleNum_5) | [Nächster](#TitleNum_7))

<!-- Source markdown line 127.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d50791cef948ce8b3066438e317ab4d34d535258 e6f70559e7237cfc86dfc5746d218c08bec52af6  (PR=4762  ,  Filename=bcp-bind.md  ,  Dirpath=docs\relational-databases\native-client-odbc-extensions-bulk-copy-functions\  ,  MergeCommitSha40=60006e90d03fdb75b282bbc0dad3d40571bacacc) -->



 Die folgende Tabelle führt gültige enumerierte Datentypen und die entsprechenden ODBC-C-Datentypen auf.

|eDataType|C-Typ|
|-----------------------|------------|
|SQLTEXT|char *|
|SQLNTEXT|wchar_t *|
|SQLCHARACTER|char *|
|SQLBIGCHAR|char *|
|SQLVARCHAR|char *|
|SQLBIGVARCHAR|char *|
|SQLNCHAR|wchar_t *|
|SQLNVARCHAR|wchar_t *|
|SQLBINARY|unsigned char *|
|SQLBIGBINARY|unsigned char *|
|SQLVARBINARY|unsigned char *|
|SQLBIGVARBINARY|unsigned char *|
|SQLBIT|char|
|SQLBITN|char|
|SQLINT1|char|
|SQLINT2|short int|
|SQLINT4|ssNoversion|
|SQLINT8|_int64|
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|
|SQLFLT4|FLOAT|
|SQLFLT8|FLOAT|
|SQLFLTN|*cbIndicator*<br /> 4: SQLFLT4<br /> 8: SQLFLT8|
|SQLDECIMALN|SQL_NUMERIC_STRUCT|
|SQLNUMERICN|SQL_NUMERIC_STRUCT|
|SQLMONEY|DBMONEY|
|SQLMONEY4|DBMONEY4|
|SQLMONEYN|*cbIndicator*<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|
|SQLTIMEN|SQL_SS_TIME2_STRUCT|
|SQLDATEN|SQL_DATE_STRUCT|
|SQLDATETIM4|DBDATETIM4|
|SQLDATETIME|DBDATETIME|
|SQLDATETIMN|*cbIndicator*<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|
|SQLIMAGE|unsigned char *|
|SQLUDT|unsigned char *|
|SQLUNIQUEID|SQLGUID|
|SQLVARIANT|*Jeder Datentyp außer:*<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|
|SQLXML|*Unterstützte C-Datentypen:*<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-sql-server-index-design-guidesql-server-index-design-guidemd"></a>7. &nbsp; [Handbuch zum SQL Server-Indexentwurf](sql-server-index-design-guide.md)

*Aktualisiert: 2.1.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Vorheriger](#TitleNum_6) | [Nächster](#TitleNum_8))

<!-- Source markdown line 700.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bd09c9e66cd3cf5f3ebebe7ffa6e937978353169 8e5cbbf0063971676a8bafefba75aa5c7c28be61  (PR=0  ,  Filename=sql-server-index-design-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=74daee358fef75a25d75c69d971d08536c5bd2be) -->



Ab SQL Server 2016 können Sie einen aktualisierbaren, **nicht gruppierten Columnstore-Index für eine Rowstore-Tabelle** erstellen. Der Columnstore-Index speichert eine Kopie der Daten, sodass Sie keinen zusätzlichen Speicher benötigen. Allerdings werden die Daten in den Columnstore-Index komprimiert, auf eine kleinere Größe als die Rowstore-Tabelle es erfordert.  Durch dieses Vorgehen können Sie Analysen mit dem Columnstore-Index und Transaktionen mit dem Rowstore-Index zur gleichen Zeit ausführen. Der Spaltenspeicher wird aktualisiert, wenn sich die Daten in der Rowstore-Tabelle ändern, daher arbeiten beide Indizes auf den gleichen Daten.

Ab SQL Server 2016 können Sie über **mehrere nicht gruppierte Rowstore-Indizes in einem Columnstore-Index** verfügen. Auf diese Weise können effiziente Tabellensuchvorgänge im zugrundeliegenden Columnstore ausgeführt werden. Auch weitere Optionen werden dadurch verfügbar. Beispielsweise können Sie eine Primärschlüsseleinschränkung durchsetzen, indem Sie eine UNIQUE-Bedingung auf die Rowstore-Tabelle anwenden. Da ein nicht eindeutiger Wert nicht in die Rowstore-Tabelle eingefügt werden kann, kann SQL Server den Wert nicht in den Columnstore einfügen.

**Überlegungen zur Leistung**


-   Die Definition des nicht gruppierten Columnstore-Index unterstützt gefilterte Bedingungen. Um die Auswirkung auf die Leistung beim Hinzufügen eines Columnstore-Indexes in eine OLTP-Tabelle zu verringern, verwenden Sie eine gefilterte Bedingung, um einen nicht gruppierten Columnstore-Index anhand der kalten Daten Ihrer Betriebsworkload zu erstellen.

-   Eine In-Memory-Tabelle kann nur über einen Columnstore-Index verfügen. Sie können ihn bei Erstellung der Tabelle generieren oder später mit [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md) hinzufügen. Vor SQL Server 2016 konnte nur eine datenträgerbasierte Tabelle über einen Columnstore-Index verfügen.

Weitere Informationen finden Sie unter [Columnstore-Indizes: Abfrageleistung](../relational-databases/indexes/columnstore-indexes-query-performance.md).

**Leitfaden zum Entwurf**


-   Eine Rowstore-Tabelle kann über einen aktualisierbaren nicht gruppierten Columnstore-Index verfügen. Vor SQL Server 2014 war der nicht gruppierte Columnstore-Index schreibgeschützt.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-spexecuteexternalscript-transact-sqlsystem-stored-proceduressp-execute-external-script-transact-sqlmd"></a>8. &nbsp; [sp_execute_external_script (Transact-SQL)](system-stored-procedures/sp-execute-external-script-transact-sql.md)

*Aktualisiert: 23.1.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Vorheriger](#TitleNum_7) | [Nächster](#TitleNum_9))

<!-- Source markdown line 207.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0ee4d591ae9d9a5c015eec98aad9ccbb86268761 ac9b439c23ffae5fcc77639de6ff955763cf5844  (PR=4696  ,  Filename=sp-execute-external-script-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=d7dcbcebbf416298f838a39dd5de6a46ca9f77aa) -->



Um ein ähnliches Modell mithilfe von Python zu generieren, ändern Sie die Sprachen-ID von `@language=N'R'` zu `@language = N'Python'` und nehmen die notwendigen Änderungen im `@script`-Argument vor. Alle anderen Parameter funktionieren genauso wie bei R.

**C. Erstellen eines Python-Modells und Generieren von Bewertungen daraus**


Dieses Beispiel veranschaulicht, wie Sie „sp\_execute\_external\_script“ verwenden, um Bewertungen in einem einfachen Python-Modell zu generieren.

```
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

**Input query to generate the customer data**

DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders`

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

**Get data from input query**

customer_data = my_input_data

**Define the model**

n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

In Python-Code verwendete Spaltenüberschriften werden nicht an SQL Server ausgegeben; geben Sie daher mit der WITH RESULTS-Anweisung die Spaltennamen und Datentypen an, die SQL verwenden soll.

Zur Bewertung können Sie auch die native [PREDICT](system-stored-procedures/../../t-sql/queries/predict-transact-sql.md)-Funktion verwenden, die in der Regel schneller ist, weil sie die Python- bzw. R-Laufzeit nicht aufrufen muss.




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-create-primary-keystablescreate-primary-keysmd"></a>9. &nbsp; [Erstellen von Primärschlüsseln](tables/create-primary-keys.md)

*Aktualisiert: 18.01.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Vorheriger](#TitleNum_8))

<!-- Source markdown line 102.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d18b485f314cc005d624cab8a51650d3b8f55f89 9bd2e9453206e8940d30b0a01c43f9d8e1aed606  (PR=4652  ,  Filename=create-primary-keys.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**So erstellen Sie einen Primärschlüssel mit einem nicht gruppierten Index in einer neuen Tabelle**


1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz der Datenbank-Engine her.

2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.

3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im Beispiel wird eine Tabelle erstellt sowie ein Primärschlüssel für die Spalte `CustomerID` und ein gruppierter Index für `TransactionID` definiert.

```
    USE AdventureWorks2012;
    GO
    CREATE TABLE Production.TransactionHistoryArchive1
    (
       CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID(),
       TransactionID int IDENTITY (1,1) NOT NULL,
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY NONCLUSTERED (uniqueidentifier)
    );
    GO

    -- Now add the clustered index
    CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
    GO
```







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die *über* neue oder kürzlich aktualisierte Artikel verfügen


- [Neu und aktualisiert (1+3):&nbsp;Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Analytics Platform System für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zur **Datenbank-Engine für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu und aktualisiert (12+1): Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu und aktualisiert (6+2):&nbsp;Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu und aktualisiert (15+0): Dokumente zu **PowerShell für SQL**](../powershell/new-updated-powershell.md)
- [Neu und aktualisiert (2+9):&nbsp;Dokumente zu **relationalen Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu und aktualisiert (1+0):&nbsp;Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zu **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Neu und aktualisiert (1+2):&nbsp;Dokumente zu **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Neu und aktualisiert (0+2):&nbsp;Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Themenbereiche, die *nicht* über neue oder kürzlich aktualisierte Artikel verfügen


- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../samples/new-updated-samples.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


