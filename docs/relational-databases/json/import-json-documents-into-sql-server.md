---
title: Importieren von JSON-Dokumenten in SQL Server | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e908ec0-7173-4cd2-8f48-2700757b53a5
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 1c842fde925e89901971a525c3e171ffce050269
ms.contentlocale: de-de
ms.lasthandoff: 06/09/2017

---
# <a name="import-json-documents-into-sql-server"></a>Importieren von JSON-Dokumenten in SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

In diesem Thema wird beschrieben, wie zum Importieren von JSON-Dateien in SQL Server. Aktuell sind viele der JSON-Dokumente, die in Dateien gespeichert. Anwendungen Protokollinformationen in JSON-Dateien, Sensoren, generieren Informationen, die in JSON-Dateien usw. gespeichert ist. Es ist wichtig, in der Lage zu sein, die in Dateien gespeicherten JSON-Daten zu lesen, in SQL Server zu laden und sie zu analysieren.

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

Nach dem Laden den Inhalt des JSON-Datei, können Sie die JSON-Text in einer Tabelle speichern.

## <a name="import-multiple-json-documents"></a>Importieren mehrerer JSON-Dokumente
Den gleichen Ansatz können Sie um einen Satz von JSON-Dateien aus dem Dateisystem in eine lokale Variable zu einem Zeitpunkt zu laden. Nehmen wir an, dass die Dateien `book<index>.json` heißen.
  
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
Sie können auch OPENROWSET(Bulk)-Funktion. verwenden wie oben beschrieben, um JSON-Dateien von anderen Speicherorten zu lesen, die auf SQL Server zugreifen können. Azure File Storage unterstützt z.B. das SMB-Protokoll. Daher können Sie der Azure File Storage-Freigabe mithilfe der folgenden Vorgehensweise eine virtuelle Festplatte zuordnen:
1.  Erstellen Sie mithilfe des Azure-Portals oder Azure PowerShell ein Dateispeicherkonto (z.B. `mystorage`), eine Dateifreigabe (z.B. `sharejson`) und einen Ordner in Azure File Storage.
2.  Laden Sie einige JSON-Dateien in die Dateispeicherfreigabe hoch.
3.  Erstellen Sie auf Ihrem Computer eine ausgehende Firewallregel in Windows-Firewall, die Port 445 zulässt. Beachten Sie, dass Ihr Internetdienstanbieter diesen Port möglicherweise blockiert. Wenn ein DNS-Fehler (Fehler 53) im folgenden Schritt auftritt, haben Sie Port 445 nicht geöffnet, oder Ihr Internetdienstanbieter blockiert ihn.
4. Bereitstellen die Azure-Dateispeicher Freigabe als einem lokalen Laufwerk (z. B. `T:`).

    Hier ist die Befehlssyntax:

    ```
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    Hier ist ein Beispiel, die lokalen Laufwerkbuchstaben zuweist `T:` auf die Freigabe des Azure-Dateispeicher:

    ```
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    Der Speicherkontoschlüssel und der primäre und sekundäre Speicherkonto-Zugriffsschlüssel befinden sich im Abschnitt „Schlüssel“ unter „Einstellungen“ im Azure-Portal.

5.  Jetzt können Sie Ihre JSON-Dateien aus dem Azure-Dateispeicher der Netzwerkfreigabe zugreifen mit das zugeordnete Laufwerk wie im folgenden Beispiel gezeigt:

    ```sql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

Weitere Informationen zu Azure File Storage finden Sie unter [File Storage](https://azure.microsoft.com/en-us/services/storage/files/).

## <a name="import-json-documents-from-azure-blob-storage"></a>Importieren von JSON-Dokumenten aus Azure BLOB-Speicher

Dateien können direkt in Azure SQL-Datenbank aus Azure Blob-Speicher mit der T-SQL BULK INSERT-Befehl oder die OPENROWSET-Funktion geladen werden.

Erstellen Sie eine externe Datenquelle zunächst, wie im folgenden Beispiel gezeigt.

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

Weitere Informationen und ein Beispiel für die Verwendung von OPENROWSET finden Sie unter [Laden von Dateien aus dem Azure-Blob-Speicher in Azure SQL-Datenbank](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/02/23/loading-files-from-azure-blob-storage-into-azure-sql-database/).

## <a name="parse-json-documents-into-rows-and-columns"></a>Analysieren von JSON-Dokumenten in Zeilen und Spalten
Anstatt beim Lesen einer vollständigen JSON-Datei in einen einzelnen Wert enthält, empfiehlt es sich analysieren und die Bücher in der Datei und deren Eigenschaften in Zeilen und Spalten zurückgeben. Im folgenden Beispiel wird eine JSON-Datei aus [Websiteansicht](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json) mit einer Liste von Büchern.

### <a name="example-1"></a>Beispiel 1
Im einfachsten Beispiel können Sie einfach die gesamte Liste aus der Datei laden. 

```sql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

### <a name="example-2"></a>Beispiel 2
OPENROWSET liest einen einzelnen Textwert aus der Datei, gibt ihn als BulkColumn zurück und übergibt ihn an die Funktion OPENJSON. OPENJSON durchläuft das Array von JSON-Objekten im BulkColumn Array und gibt ein Buch in jeder Zeile wird als JSON formatiert:

```
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

Jetzt können Sie die Tabelle an den Benutzer zurückgeben oder die Daten in eine andere Tabelle laden.

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Für viele spezifische Lösungen Fälle und Empfehlungen zu verwenden, finden Sie unter der [Blogeinträge von jovan zur integrierten JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server und Azure SQL-Datenbank von Microsoft Program Manager Jovan Popovic.
  
## <a name="see-also"></a>Siehe auch
[Konvertieren von JSON-Daten in Zeilen und Spalten mit OPENJSON](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)


