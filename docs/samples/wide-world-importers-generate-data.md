---
title: "\"Wideworldimporters\" Generieren von Daten - SQL-Beispieldatenbank | Microsoft Docs"
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be472ed5594a523497244c25264e16530e2a12ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimporters-data-generation"></a>"Wideworldimporters" Datengenerierungsplan
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Versionen der Datenbanken "wideworldimporters" und WideWorldImportersDW enthält Daten, die ab dem 1. Januar 2013 bis zu dem Tag, die diese Datenbanken erstellt wurden.

Wenn Sie die Beispieldatenbanken zu verwenden, kann es auch hilfreich, die neuere Daten enthalten sein.

## <a name="data-generation-in-wideworldimporters"></a>Generieren von Daten in "wideworldimporters"

Gehen Sie folgendermaßen vor, um das Generieren von Beispieldaten bis zum aktuellen Datum:

1. Wenn Sie dies noch nicht getan haben, installieren Sie eine saubere Version der Datenbank "wideworldimporters". Anweisungen zur Installation **"wideworldimporters" Installation und Konfiguration**.
2. Führen Sie die folgende Anweisung in der Datenbank an:

```
    EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
        @AverageNumberOfCustomerOrdersPerDay = 60,
        @SaturdayPercentageOfNormalWorkDay = 50,
        @SundayPercentageOfNormalWorkDay = 0,
        @IsSilentMode = 1,
        @AreDatesPrinted = 1;
```

Diese Anweisung fügt Beispiel Sales und Purchase Daten in der Datenbank bis zum aktuellen Datum. Er gibt den Status der Daten auf Generation--Tag. Es kann einmal im Jahr bis zu 10 Minuten dauern, die Daten benötigt. Es gibt einige Unterschiede in den Daten zwischen ausgeführt wird, da es ein Zufallsfaktor in die datengenerierung wird generiert.

Erhöhen oder verringern die Menge der Daten, die generiert werden, im Hinblick auf Aufträge pro Tag, ändern Sie den Wert für den Parameter `@AverageNumberOfCustomerOrdersPerDay`. Die Parameter `@SaturdayPercentageOfNormalWorkDay` und `@SundayPercentageOfNormalWorkDay` werden verwendet, um das Volume Reihenfolge für Wochenendtage zu ermitteln.

## <a name="importing-generated-data-in-wideworldimportersdw"></a>Importieren von generierten Daten in WideWorldImportersDW

Gehen Sie folgendermaßen vor, um Beispieldaten vor dem aktuellen Datum in der OLAP-Datenbank WideWorldImportersDW zu importieren:

1. Führen Sie Logik zur Generierung in der WideWorldImporters-OLTP-Datenbank, die mit den oben beschriebenen Schritten.
2. Wenn Sie dies noch nicht getan haben, installieren Sie eine saubere Version der Datenbank WideWorldImportersDW. Anweisungen zur Installation **"wideworldimporters" Installation und Konfiguration**.
3. Als Ausgangswert für die OLAP-Datenbank durch Ausführen der folgenden Anweisung in der Datenbank:

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. Führen Sie das SSIS-Paket **tägliche ETL.ispac** zum Importieren der Daten in der OLAP-Datenbank. Informationen zum Ausführen des ETL-Auftrags finden Sie unter **"wideworldimporters" ETL-Workflows**.

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>Generieren von Daten in WideWorldImportersDW aber für Leistungstests

WideWorldImportersDW hat die Möglichkeit, nach dem Zufallsprinzip Erhöhen der Größe der spaltensegmentdaten für die Leistungstests, z. B. mit gruppierten Columnstore.

Eine der Herausforderungen ist die Größe des Downloads klein genug für die lang herunterladen genug, um SQL Server-Leistung-Funktionen veranschaulichen einfach zu halten. Z. B. vorkommen bedeutende Vorteile für columnstore-Indizes nur beim Arbeiten mit einer größeren Anzahl von Zeilen. 

Die Prozedur `Application.Configuration_PopulateLargeSaleTable` können verwendet werden, um deutlich erhöhen der Anzahl der Zeilen in der `Fact.Sale` Tabelle. Beachten Sie, dass die Zeilen in das Kalenderjahr 2012, um zu vermeiden, vorhandene Wide World Importers Daten beginnend ab dem 1. Januar 2013 implementierungsgrenzen eingefügt werden.

### <a name="procedure-details"></a>Prozedur-Details

#### <a name="name"></a>Name: 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parameter:

  `@EstimatedRowsFor2012` **"bigint"** (hat den Standardwert 12000000)

#### <a name="result"></a>Ergebnis:

In etwa die erforderliche Anzahl von Zeilen eingefügt werden die `Fact.Sale` Tabelle im Jahr 2012. Die Prozedur beschränkt die Standardanzahl der Anzahl der Zeilen pro Tag auf 50000. Diese Einschränkung kann geändert werden, jedoch handelt es sich um eine versehentliche Overinflations der Tabelle zu vermeiden.

Darüber hinaus angewendet wird die Prozedur gruppierten columnstore-Index, wenn es nicht bereits angewendet wurde.
