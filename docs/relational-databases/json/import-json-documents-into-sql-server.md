---
title: Importieren von JSON-Dokumenten in SQL Server | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e908ec0-7173-4cd2-8f48-2700757b53a5
caps.latest.revision: "5"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 59b8b667a9a895b9e95388ac781ec6bb46923920
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="import-json-documents-into-sql-server"></a>Importieren von JSON-Dokumenten in SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Dieses Thema beschreibt das Importieren von JSON-Dateien in SQL Server. Zurzeit werden viele JSON-Dokumente in Dateien gespeichert. Anwendungen protokollieren Informationen in JSON-Dateien, Sensoren generieren Informationen, die in JSON-Dateien gespeichert werden, usw. Es ist wichtig, in der Lage zu sein, die in Dateien gespeicherten JSON-Daten zu lesen, in SQL Server zu laden und sie zu analysieren.

## <a name="import-a-json-document-into-a-single-column"></a>Importieren eines JSON-Dokuments in eine einzelne Spalte
**OPENROWSET(BULK)** ist eine Tabellenwertfunktion, die Daten aus einer beliebigen Datei auf dem lokalen Laufwerk oder im Netzwerk lesen kann, wenn SQL Server über Lesezugriff für diesen Speicherort verfügt. Sie gibt eine Tabelle mit einer einzelnen Spalte zurück, die den Inhalt der Datei enthält. Es gibt verschiedene Optionen, die Sie mit der OPENROWSET(Bulk)-Funktion verwenden können, z.B. Trennzeichen. Im einfachsten Fall können Sie einfach den gesamten Inhalt einer Datei als Textwert laden. (Dieser einzelne große Wert wird als ein „Single Character Large Object“ oder SINGLE_CLOB bezeichnet.) 

Hier finden Sie ein Beispiel für die **OPENROWSET(BULK)**-Funktion, die den Inhalt einer JSON-Datei liest und als einzelnen Wert an den Benutzer zurückgibt:

```sql
SELECT BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

OPENROWSET(BULK) liest den Inhalt der Datei und gibt ihn in `BulkColumn` zurück.

Sie können auch den Inhalt der Datei in eine lokale Variable oder in eine Tabelle laden, wie im folgenden Beispiel gezeigt:

```sql
-- Load file contents into a variable
SELECT @json = BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j

-- Load file contents into a table 
SELECT BulkColumn
 INTO #temp 
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

Nachdem Sie den Inhalt der JSON-Datei geladen haben, können Sie den JSON-Text in einer Tabelle speichern.

## <a name="import-multiple-json-documents"></a>Importieren mehrerer JSON-Dokumente
Diese Vorgehensweise kann auch zum Laden eines Satzes von JSON-Dateien aus dem Dateisystem in lokale Variablen (nacheinander) verwendet werden. Nehmen wir an, dass die Dateien `book<index>.json` heißen.
  
```sql
DECLARE @i INT = 1
DECLARE @json AS NVARCHAR(MAX)

WHILE(@i < 10)
BEGIN
    SET @file = 'C:\JSON\Books\book' + cast(@i AS VARCHAR(5)) + '.json';
    SELECT @json = BulkColumn FROM OPENROWSET (BULK (@file), SINGLE_CLOB) AS j
    SELECT * FROM OPENJSON(@json) AS json
    -- Optionally, save the JSON text in a table.
    SET @i = @i + 1 ;
END
```

## <a name="import-json-documents-from-azure-file-storage"></a>Importieren von JSON-Dokumenten aus Azure File Storage
Sie können auch wie oben beschrieben OPENROWSET(BULK) zum Lesen von JSON-Dateien aus anderen Dateispeicherorten verwenden, auf die SQL Server zugreifen kann. Azure File Storage unterstützt z.B. das SMB-Protokoll. Daher können Sie der Azure File Storage-Freigabe mithilfe der folgenden Vorgehensweise eine virtuelle Festplatte zuordnen:
1.  Erstellen Sie mithilfe des Azure-Portals oder Azure PowerShell ein Dateispeicherkonto (z.B. `mystorage`), eine Dateifreigabe (z.B. `sharejson`) und einen Ordner in Azure File Storage.
2.  Laden Sie einige JSON-Dateien in die Dateispeicherfreigabe hoch.
3.  Erstellen Sie auf Ihrem Computer eine ausgehende Firewallregel in Windows-Firewall, die Port 445 zulässt. Beachten Sie, dass Ihr Internetdienstanbieter diesen Port möglicherweise blockiert. Wenn ein DNS-Fehler (Fehler 53) im folgenden Schritt auftritt, haben Sie Port 445 nicht geöffnet, oder Ihr Internetdienstanbieter blockiert ihn.
4. Binden Sie die Azure File Storage-Dateifreigabe als lokales Laufwerk (z.B. `T:`) ein.

    Hier finden Sie die Befehlssyntax:

    ```dos
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    Hier finden Sie ein Beispiel, in dem der lokale Laufwerkbuchstabe `T:` der Azure File Storage-Dateifreigabe zugewiesen wird:

    ```dos
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    Der Speicherkontoschlüssel und der primäre und sekundäre Speicherkonto-Zugriffsschlüssel befinden sich im Abschnitt „Schlüssel“ unter „Einstellungen“ im Azure-Portal.

5.  Sie können jetzt über die Azure File Storage-Dateifreigabe auf die JSON-Dateien zugreifen, indem Sie das zugeordnete Laufwerk verwenden, wie im folgenden Beispiel gezeigt:

    ```sql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

Weitere Informationen zu Azure File Storage finden Sie unter [File Storage](https://azure.microsoft.com/services/storage/files/).

## <a name="import-json-documents-from-azure-blob-storage"></a>Importieren von JSON-Dokumenten aus Azure BLOB-Speicher

Sie können Dateien mit dem Befehl T-SQL BULK INSERT oder der OPENROWSET-Funktion direkt aus Azure Blob Storage in die Azure SQL-Datenbank laden.

Erstellen Sie zunächst eine externe Datenquelle, wie im folgenden Beispiel gezeigt.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
 WITH ( TYPE = BLOB_STORAGE,
        LOCATION = 'https://myazureblobstorage.blob.core.windows.net',
        CREDENTIAL= MyAzureBlobStorageCredential);
```

Führen Sie anschließend einen BULK INSERT-Befehl mit der Option DATA_SOURCE aus.

```sql
BULK INSERT Product
FROM 'data/product.dat'
WITH ( DATA_SOURCE = 'MyAzureBlobStorage');
```

Weitere Informationen und ein Beispiel für OPENROWSET finden Sie unter [Loading files from Azure Blob Storage into Azure SQL Database (Laden von Dateien aus Azure Blob Storage in die Azure SQL-Datenbank)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/02/23/loading-files-from-azure-blob-storage-into-azure-sql-database/).

## <a name="parse-json-documents-into-rows-and-columns"></a>Analysieren von JSON-Dokumenten in Zeilen und Spalten
Möglicherweise möchten Sie eine JSON-Datei analysieren und die Bücher in der Tabelle sowie die Eigenschaften in Reihen und Zeilen zurückgeben, anstatt die gesamte JSON-Datei als einzelnen Wert zu lesen. Im folgenden Beispiel wird eine JSON-Datei mit einer Liste von Büchern von [dieser Website](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json) verwendet.

### <a name="example-1"></a>Beispiel 1
Im einfachsten Beispiel können Sie einfach die gesamte Liste aus der Datei laden. 

```sql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

### <a name="example-2"></a>Beispiel 2
OPENROWSET liest einen einzelnen Textwert aus der Datei, gibt ihn als BulkColumn zurück und übergibt ihn an die Funktion OPENJSON. OPENJSON durchläuft das Array von JSON-Objekten im BulkColumn-Array und gibt in jeder Zeile ein Buch zurück, das als JSON-Datei formatiert ist:

```json
{"id":"978-0641723445″, "cat":["book","hardcover"], "name":"The Lightning Thief", … 
{"id":"978-1423103349″, "cat":["book","paperback"], "name":"The Sea of Monsters", … 
{"id":"978-1857995879″, "cat":["book","paperback"], "name":"Sophie’s World : The Greek … 
{"id":"978-1933988177″, "cat":["book","paperback"], "name":"Lucene in Action, Second … 
```

### <a name="example-3"></a>Beispiel 3
Die OPENJSON-Funktion kann den JSON-Inhalt analysieren und ihn in eine Tabelle oder ein Resultset transformieren. Im folgenden Beispiel wird der Inhalt geladen, die geladene JSON-Datei analysiert und die fünf Felder als Spalten zurückgegeben:

```sql
SELECT book.*
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
 WITH( id nvarchar(100), name nvarchar(100), price float,
 pages_i int, author nvarchar(100)) AS book
```

In diesem Beispiel liest OPENROWSET(BULK) den Inhalt der Datei und übergibt den Inhalt mit einem definierten Schema für die Ausgabe an die OPENJSON-Funktion. OPENJSON vergleicht Eigenschaften in JSON-Objekten mithilfe der Spaltennamen. Die Eigenschaft `price` wird z.B. als `price`-Spalte zurückgegeben und in den float-Datentyp konvertiert. Dies sind die Ergebnisse:

|ID|Name|Preis|Seiten_i|Autor
|---|---|---|---|---|
978-0641723445|The Lightning Thief (Diebe im Olymp)|12.5|384|Rick Riordan| 
978-1423103349|The Sea of Monsters (Im Bann des Zyklopen)|6.49|304|Rick Riordan| 
978-1857995879|Sophie’s World : The Greek Philosophers (Sofies Welt: Roman über die Geschichte der Philosophie)|3.07|64|Jostein Gaarder| 
978-1933988177|Lucene in Action, Zweite Auflage (nur englisch)|30.5|475|Michael McCandless|
||||||

Jetzt können Sie die Tabelle an den Benutzer zurückgeben oder die Daten in eine andere Tabelle laden.

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Viele spezifische Lösungen, Anwendungsfälle und Empfehlungen finden Sie in SQL Server und in der Azure SQL-Daten im [Blogbeitrag über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) von Jovan Popovic, Program Manager bei Microsoft.
  
## <a name="see-also"></a>Siehe auch
[Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)

