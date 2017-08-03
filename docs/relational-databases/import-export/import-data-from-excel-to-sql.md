---
title: Importieren von Daten aus Excel in SQL | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.assetid: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 70a1fd4dbec68d22187585de69a1d603c39e259e
ms.openlocfilehash: 3a978076b9776b57ffc996404c5f7773d7cf9094
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>Importieren von Daten aus Excel in SQL Server oder Azure SQL-Datenbank
Es gibt verschiedene Möglichkeiten, Daten aus Excel in SQL Server oder Azure SQL-Datenbank zu importieren.
-   Sie können Daten direkt aus Excel importieren, indem Sie den SQL Server-Import/Export-Assistenten, Integration Services (SSIS) oder die OPENROWSET-Funktion verwenden. 
-   Sie können Ihre Excel-Daten als Text speichern und dann die BULK INSERT-Anweisung, BCP oder Azure Data Factory verwenden. Hier finden Sie eine Übersicht über die Optionen sowie Links zu detaillierten Anweisungen.

> [!NOTE]
> Eine vollständige Beschreibung der komplexen Tools wie SSIS oder Azure Data Factory würde den Rahmen dieser Übersicht sprengen. Um mehr über die Lösung zu erhalten, für die Sie sich interessieren, folgen Sie den Links zu Tutorials und weiteren Informationen.

## <a name="sql-server-import-and-export-wizard"></a>SQL Server-Import/Export-Assistent

Importen Sie Daten direkt aus Excel-Dateien, indem Sie den Schritten des Assistenten folgen. Optional können Sie die Import-/Exporteinstellungen als SQL Server Integration Services-Paket (SSIS) speichern, das Sie anpassen und wiederverwenden können.

![Herstellen einer Verbindung mit einer Excel-Datenquelle](media/excel-connection.png)

Ein Beispiel für die Verwendung des Assistenten zum Importieren von Daten aus Excel in SQL Server finden Sie unter [Erste Schritte mit diesem einfachen Beispiel für den Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

Wenn Sie mit SSIS vertraut sind und den SQL Server-Import/Export-Assistenten nicht ausführen möchten, erstellen Sie ein SSIS-Paket, das die Excel-Quelle und das SQL Server-Ziel im Datenfluss verwendet.

![Komponenten im Datenfluss](media/excel-to-sql-data-flow.png)

Weitere Informationen zu dieser SSIS-Komponente finden Sie in den folgenden Themen.
-   [Excel-Quelle](../../integration-services/data-flow/excel-source.md)
-   [SQL Server-Ziel](../../integration-services/data-flow/sql-server-destination.md)

Erste Informationen zum Erstellen von SSIS-Paketen finden Sie im Tutorial [Erstellen eines ETL-Pakets](../../integration-services/ssis-how-to-create-an-etl-package.md).

## <a name="openrowset-and-linked-servers"></a>OPENROWSET und Verbindungsserver
> [!NOTE]
> Der ACE-Anbieter (früher der Jet-Anbieter), der die Verbindung mit Excel-Dateien herstellt, ist für die interaktive Verwendung auf Clientseite vorgesehen. Wenn Sie den ACE-Anbieter auf dem Server verwenden – insbesondere in automatisierten oder parallel ausgeführten Prozessen –, kann dies zu unerwarteten Ergebnissen führen.

Importieren Sie Daten mithilfe der Funktion `OPENROWSET` oder `OPENDATASOURCE` direkt aus Excel-Dateien. Diese Nutzung wird als *verteilte Abfrage* bezeichnet.

Bevor Sie eine verteilte Abfrage ausführen können, müssen Sie die Serverkonfigurationsoption `ad hoc distributed queries` aktivieren, wie in folgendem Beispiel gezeigt. Weitere Informationen finden Sie unter [Ad Hoc Distributed Queries (Serverkonfigurationsoption)](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md).

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

Das folgende Codebeispiel importiert die Daten aus dem Excel-Arbeitsblatt `Customers` mit `OPENROWSET` in eine neue SQL Server-Tabelle.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=D:\Desktop\Data.xlsx', [Data$]);
GO
```

Hier sehen Sie das Beispiel mit `OPENDATASOURCE`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=D:\Desktop\Data.xlsx;Extended Properties=Excel 12.0')...[Data$];
GO
```

Um die importierten Daten an eine *vorhandene* Tabelle *anzufügen*, anstatt eine neue Tabelle zu erstellen, verwenden Sie die Syntax `INSERT INTO ... SELECT ... FROM ...` anstelle der Syntax `SELECT ... INTO ... FROM ...` aus den vorherigen Beispielen.

Um die Excel-Daten abzufragen, ohne sie zu importieren, verwenden Sie einfach die Syntax `SELECT ... FROM ...`.

Weitere Informationen zu verteilten Abfragen finden Sie in den folgenden Themen.
-   [Verteilte Abfragen](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx). (Verteilte Abfragen werden in SQL Server 2016 weiterhin unterstützt, aber die Dokumentation für dieses Feature wurde nicht aktualisiert.)
-   [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
-   [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

Sie können auch eine dauerhafte Verbindung zur Excel-Datei in Form eines *Verbindungsservers* konfigurieren. Das folgende Beispiel importiert die Daten aus dem Arbeitsblatt `Data` auf dem vorhandenen Excel-Verbindungsserver `EXCELLINK` in eine neue SQL Server-Tabelle mit der Bezeichnung `Data_ls`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_ls FROM EXCELLINK...[Data$];
GO
```

Sie können einen Verbindungsserver über SQL Server Management Studio oder durch Ausführen der gespeicherten Systemprozedur `sp_addlinkedserver` erstellen, wie im folgenden Beispiel gezeigt.

```sql
DECLARE @RC int

DECLARE @server     nvarchar(128)
DECLARE @srvproduct nvarchar(128)
DECLARE @provider   nvarchar(128)
DECLARE @datasrc    nvarchar(4000)
DECLARE @location   nvarchar(4000)
DECLARE @provstr    nvarchar(4000)
DECLARE @catalog    nvarchar(128)

-- Set parameter values
SET @server =     'EXCELLINK'
SET @srvproduct = 'Excel'
SET @provider =   'Microsoft.ACE.OLEDB.12.0'
SET @datasrc =    'D:\Desktop\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

Weitere Informationen zu Verbindungsservern finden Sie in den folgenden Themen.
-   [Erstellen von Verbindungsservern](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
-   [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

Weitere Beispiele und Informationen zu Verbindungsservern und verteilten Abfragen finden Sie in den folgenden Themen.
-   [Verwenden von Excel mit SQL Server-Verbindungsservern und verteilten Abfragen](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
-   [Importieren von Daten aus Excel in SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prerequisite---save-excel-data-as-text"></a>Voraussetzung: Speichern von Excel-Daten im Textformat
Für die restlichen auf dieser Seite beschriebenen Methoden – die BULK INSERT-Anweisung, das BCP-Tool und Azure Data Factory – müssen Sie Ihre Excel-Daten zuerst in eine Textdatei exportieren.

Wählen Sie in Excel die Optionen **Datei | Speichern unter**, und wählen Sie dann als Zieldateityp **Text (Tabstopp-getrennt) (\*.txt)** oder **CSV (Trennzeichen-getrennt) (\*.csv)** aus.

> [!TIP]
> Um mit Tools für den Datenimport die besten Ergebnisse zu erzielen, speichern Sie Tabellen, die nur die Spaltenüberschriften und die Datenzeilen enthalten. Wenn die gespeicherten Daten Seitentitel, Leerzeilen und Ähnliches enthalten, führt der spätere Import der Daten möglicherweise zu unerwarteten Ergebnissen.

## <a name="bulk-insert-command"></a>BULK INSERT-Befehl

`BULK INSERT` ist ein Befehl, den Sie in SQL Server Management Studio ausführen können. Das folgende Beispiel lädt die Daten aus der durch Trennzeichen getrennten Datei `Data.csv` in eine vorhandene Tabelle.

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'D:\Desktop\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

Weitere Informationen finden Sie in folgenden Themen.
-   [Importieren von Massendaten mithilfe von BULK INSERT oder OPENROWSET(BULK...)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
-   [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp-tool"></a>BCP-Tool

BCP ist eine SQL Server-Instanz, die Sie über die Eingabeaufforderung ausführen. Das folgende Beispiel lädt Daten aus der Datei `Data.csv` in die vorhandene Tabelle `Data_bcp` in SQL Server.

```sql
bcp.exe ImportFromExcel..Data_bcp in "D:\Desktop\data.csv" -T -c -t ,
```

Weitere Informationen finden Sie in folgenden Themen.
-   [Importieren und Exportieren von Massendaten mithilfe des Hilfsprogramms BCP](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
-   [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)
-   [Vorbereiten von Daten für den Massenexport oder -import](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="copy-wizard-azure-data-factory"></a>Kopier-Assistent (Azure Data Factory)
Importen Sie in Textdateien gespeicherte Daten, indem Sie den Schritten des Assistenten folgen. Weitere Informationen zum Kopier-Assistenten finden Sie in den folgenden Themen.
-   [Data Factory-Kopier-Assistent](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
-   [Tutorial: Erstellen einer Pipeline mit Kopieraktivität mithilfe des Data Factory-Kopier-Assistenten](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial)

## <a name="azure-data-factory"></a>Azure Data Factory
Wenn Sie mit Azure Data Factory vertraut sind und den Azure Data Factory-Kopier-Assistenten nicht ausführen möchten, erstellen Sie eine Pipeline mit einer Kopieraktivität, die Daten aus der Textdatei in einem Dateispeicherort nach SQL Server oder Azure SQL-Datenbank kopiert.

Weitere Informationen zu diesen Data Factory-Quellen und -Senken finden Sie in folgenden Themen.
-   [File system](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
-   [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
-   [Azure SQL-Datenbank](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

Informationen zum Kopieren von Daten mit Azure Data Factory finden Sie in folgenden Themen.
-   [Verschieben von Daten mit der Kopieraktivität](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
-   [Tutorial: Erstellen einer Pipeline mit Kopieraktivität mithilfe des Azure-Portals](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

