---
title: PolyBase-Abfragen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: polybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: ''
ms.topic: article
keywords:
- PolyBase
helpviewer_keywords:
- PolyBase, import and export
- Hadoop, import with PolyBase
- Hadoop, export with PolyBase
- Azure blob storage, import with PolyBase
- Azure blob storage, export with PolyBase
ms.assetid: 2c5aa2bd-af7d-4f57-9a28-9673c2a4c07e
caps.latest.revision: 18
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6544e06a8b0d07e4a2eda1f8371cd0440c172f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="polybase-queries"></a>PolyBase-Abfragen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieser Artikel bietet Beispiele für Abfragen mit dem [PolyBase](../../relational-databases/polybase/polybase-guide.md)-Feature von SQL Server (ab 2016). Bevor Sie diese Beispiele verwenden können, müssen Sie zudem die T-SQL-Anweisungen zum Einrichten von PolyBase verstehen (siehe [PolyBase T-SQL objects](../../relational-databases/polybase/polybase-t-sql-objects.md) [PolyBase T-SQL-Objekte]).
  
## <a name="queries"></a>Abfragen  
 Führen Sie Transact-SQL-Anweisungen für externe Tabellen aus, oder verwenden Sie BI-Tools, um externe Tabellen abzufragen.
  
## <a name="select-from-external-table"></a>Auswählen aus einer externen Tabelle mit der SELECT-Anweisung  
 Eine einfache Abfrage, die Daten aus einer definierten externen Tabelle zurückgibt.  
  
```sql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```
  
 Eine einfache Abfrage, die ein Prädikat enthält.

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65;
```

## <a name="join-external-tables-with-local-tables"></a>Externe Tabellen mit dem Befehl JOIN mit lokalen Tabellen verknüpfen

```
SELECT InsuranceCustomers.FirstName,   
                           InsuranceCustomers.LastName,   
                           SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  
  
## <a name="pushdown-computation-to-hadoop"></a>Weitergabeberechnung in Hadoop

Varianten der Weitergabe werden hier angezeigt.

### <a name="pushdown-for-selecting-a-subset-of-rows"></a>Weitergabe für die Auswahl einer Teilmenge von Zeilen

Verwenden Sie die Prädikatweitergabe zum Verbessern der Leistung für eine Abfrage, die eine Teilmenge von Zeilen aus einer externen Tabelle auswählt.

In diesem Beispiel initiiert SQL Server 2016 einen map-reduce-Auftrag zum Abrufen der Zeilen, die dem Prädikat `customer.account_balance < 200000` auf Hadoop entsprechen. Da die Abfrage nicht erfolgreich abschließen kann, ohne alle Zeilen der Tabelle zu scannen, werden nur die Zeilen, die den Prädikatskriterien entsprechen, in SQL Server kopiert. Dies spart Zeit und erfordert weniger temporären Speicherplatz, wenn die Anzahl der Debitorensalden < 200000 im Vergleich mit der Anzahl der Kunden mit Kontensalden >= 200000 klein ist.

```
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="pushdown-for-selecting-a-subset-of-columns"></a>Weitergabe für die Auswahl einer Teilmenge von Spalten

Verwenden Sie die Prädikatweitergabe zum Verbessern der Leistung für eine Abfrage, die eine Teilmenge von Spalten aus einer externen Tabelle auswählt.

In dieser Abfrage initiiert SQL Server einen map-reduce-Auftrag, um die auf Hadoop begrenzte Textdatei vorab zu verarbeiten, sodass nur die Daten der zwei Spalten customer.name und customer.zip_code in SQL Server PDW kopiert werden.

```
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Weitergabe für grundlegende Ausdrücke und Operatoren

SQL Server erlaubt die folgenden grundlegenden Ausdrücke und Operatoren für Prädikatweitergabe.

+ Binäre Vergleichsoperatoren (\<, >, =, !=, <>, >=, <=) für die numerischen, Datums- und Zeitwerte.

+ Arithmetische Operatoren (+, -, *, /, %).

+ Logische Operatoren (AND, OR).

+ Unäroperatoren (NOT, IS NULL, IS NOT NULL).

Die Operatoren BETWEEN, NOT, IN und LIKE können möglicherweise weitergegeben werden. Das aktuelle Verhalten hängt davon ab, wie der Abfrageoptimierer die Operatorausdrücke als eine Reihe von Anweisungen neu schreibt, die grundlegende relationale Operatoren verwenden.

Die Abfrage in diesem Beispiel verfügt über mehrere Prädikate, die an Hadoop weitergegeben werden können. SQL Server kann map-reduce-Aufträge an Hadoop weitergeben, um das Prädikat `customer.account_balance <= 200000` auszuführen. Der Ausdruck `BETWEEN 92656 and 92677` besteht auch aus binären und logischen Operationen, die an Hadoop weitergegeben werden können. Das logische **AND** in `customer.account_balance and customer.zipcode` ist ein finaler Ausdruck.

Mit dieser Kombination von Prädikaten können also die map-reduce-Aufträge alle Bedingungen der WHERE-Klausel vollständig bearbeiten. Nur die Daten, die die Kriterien von SELECT erfüllen, werden in SQL Server PDW zurückkopiert.

```
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

### <a name="force-pushdown"></a>Weitergabe erzwingen

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>Weitergabe deaktivieren

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="import-data"></a>Importieren von Daten

Importieren Sie Daten aus Hadoop oder Azure Storage in SQL Server für den beständigen Speicher. Verwenden Sie SELECT INTO, um Daten, auf die eine externe Tabelle verweist, zu importieren und dauerhaft in SQL Server zu speichern. Erstellen Sie dynamisch eine relationale Tabelle, und erstellen Sie dann in einem zweiten Schritt einen Columnstore-Index am oberen Rand der Tabelle.

```sql
-- PolyBase scenario - import external data into SQL Server
-- Import data for fast drivers into SQL Server to do more in-depth analysis
-- Leverage columnstore technology
  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
```

## <a name="export-data"></a>Exportieren von Daten

Exportieren von Daten aus SQL Server in Hadoop oder Azure Storage 

Aktivieren Sie zunächst die Exportfunktion, indem Sie den Wert `sp_configure` von „allow polybase export“ auf 1 festlegen. Erstellen Sie anschließend eine externe Tabelle, die auf das Zielverzeichnis verweist. Die Anweisung CREATE EXTERNAL TABLE erstellt das Zielverzeichnis, wenn dieses noch nicht vorhanden ist. Verwenden Sie dann INSERT INTO zum Exportieren von Daten aus einer lokalen SQL Server-Tabelle in die externe Datenquelle. 

Die Ergebnisse der SELECT-Anweisung werden an die angegebene Position im angegebenen Dateiformat exportiert. Die externen Dateien heißen *QueryID_date_time_ID.format*, wobei *ID* ein inkrementeller Bezeichner ist und *Format* das Format der exportierten Daten. Beispielsweise kann ein Dateiname „QID776_20160130_182739_0.orc“ lauten.


> [!NOTE]
> Beim Exportieren von Daten nach Hadoop oder Azure Blob Storage über PolyBase werden nur die Daten exportiert, nicht die Spaltennamen (Metadaten), wie im CREATE EXTERNAL TABLE-Befehl definiert.

```sql  
-- PolyBase scenario  - export data from SQL Server to Hadoop
-- Create an external table
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
        [FirstName] char(25) NOT NULL,   
        [LastName] char(25) NOT NULL,   
        [YearlyIncome] float NULL,   
        [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
        LOCATION='/old_data/2009/customerdata',  
        DATA_SOURCE = HadoopHDP2,  
        FILE_FORMAT = TextFileFormat,  
        REJECT_TYPE = VALUE,  
        REJECT_VALUE = 0  
);  
  
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```

## <a name="new-catalog-views"></a>Neue Katalogsichten

Die folgenden neuen Katalogsichten zeigen externe Ressourcen an.
  
```sql
SELECT * FROM sys.external_data_sources;   
SELECT * FROM sys.external_file_formats;  
SELECT * FROM sys.external_tables;  
```
  
 Bestimmen Sie unter Verwendung von, ob eine Tabelle eine externe Tabelle ist. `is_external`  
  
```sql  
SELECT name, type, is_external FROM sys.tables WHERE name='myTableName'   
```  
  
## <a name="next-steps"></a>Nächste Schritte  

Weitere Informationen zur Problembehandlung finden Sie unter [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md)(PolyBase-Problembehandlung).
