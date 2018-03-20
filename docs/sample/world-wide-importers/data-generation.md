---
title: Der datengenerierung | Microsoft Docs
ms.custom: 
ms.date: 01/30/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology:
- " database-engine "
ms.topic: article
ms.assetid: f387273b-8b5f-4687-b033-09499ea2d68f
caps.latest.revision: 
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: 20db5f20256fb4b545482b29b0c5cc41c6ba231e
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters data generation
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Versionen der Datenbanken "wideworldimporters" und WideWorldImportersDW enthält Daten, die beginnend am 1. Januar-2013, bis zu dem Tag, die diese Datenbanken erstellt wurden.

Wenn die Beispieldatenbanken zu einem späteren Zeitpunkt, für Demonstrations- oder Abbildung, verwendet werden, kann es vorteilhaft, neuere Beispieldaten in der Datenbank enthalten sein.

## <a name="data-generation-in-wideworldimporters"></a>Data Generation in WideWorldImporters

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

Diese Anweisung fügt Beispiel Sales und Purchase Daten in der Datenbank bis zum aktuellen Datum. Er gibt den Status der Daten auf Generation--Tag. M/s dauert für jedes Jahr beträgt 10 Minuten, die Daten benötigt. Beachten Sie, dass es einige Unterschiede in den Daten zwischen ausgeführt wird gibt, da es ein Zufallsfaktor in die datengenerierung wird generiert.

Erhöhen oder verringern die Menge der Daten, die generiert werden, im Hinblick auf Aufträge pro Tag, ändern Sie den Wert für den Parameter `@AverageNumberOfCustomerOrdersPerDay`. Die Parameter `@SaturdayPercentageOfNormalWorkDay` und `@SundayPercentageOfNormalWorkDay` werden verwendet, um das Volume Reihenfolge für Wochenendtage zu ermitteln.

## <a name="importing-generated-data-in-wideworldimportersdw"></a>Importieren von generierten Daten in WideWorldImportersDW

Gehen Sie folgendermaßen vor, um Beispieldaten vor dem aktuellen Datum in der OLAP-Datenbank WideWorldImportersDW zu importieren:

1. Führen Sie Logik zur Generierung in der WideWorldImporters-OLTP-Datenbank, die mit den oben beschriebenen Schritten.
2. Wenn Sie dies noch nicht getan haben, installieren Sie eine saubere Version der Datenbank WideWorldImportersDW. Anweisungen zur Installation **"wideworldimporters" Installation und Konfiguration**.
3. Als Ausgangswert für die OLAP-Datenbank durch Ausführen der folgenden Anweisung in der Datenbank:

```
    EXECUTE [Application].Configuration_ReseedETL
```

4. Führen Sie das SSIS-Paket **tägliche ETL.ispac** zum Importieren der Daten in der OLAP-Datenbank. Informationen zum Ausführen des ETL-Auftrags finden Sie unter **"wideworldimporters" ETL-Workflows**.

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>Generieren von Daten in WideWorldImportersDW aber für Leistungstests

WideWorldImportersDW hat die Möglichkeit, nach dem Zufallsprinzip Erhöhen der Größe der spaltensegmentdaten für die Leistungstests, z. B. mit gruppierten Columnstore.

Eine der Herausforderungen beim Protokollversand ein Beispiel, wie Wide World Importers ist die Größe des Downloads klein genug für die verteilbaren jedoch groß genug ist, um SQL Server-Leistung-Funktionen veranschaulichen zu können, werden beibehalten. Ein Bereich, in denen dies ist, eine besondere Herausforderung ist bei der Arbeit mit columnstore-Indizes. Bedeutende Vorteile sind nur beim Arbeiten mit einer größeren Anzahl von Zeilen. 

Die Prozedur `Application.Configuration_PopulateLargeSaleTable` können verwendet werden, um deutlich erhöhen der Anzahl der Zeilen in der `Fact.Sale` Tabelle. Beachten Sie, dass die Zeilen in das Kalenderjahr 2012, um zu vermeiden, vorhandene Wide World Importers Daten beginnend ab dem 1. Januar 2013 implementierungsgrenzen eingefügt werden.

### <a name="procedure-details"></a>Prozedur-Details

#### <a name="name"></a>Name: 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parameter:

  `@EstimatedRowsFor2012` **"bigint"** (hat den Standardwert 12000000)

#### <a name="result"></a>Ergebnis:

In etwa die erforderliche Anzahl von Zeilen eingefügt werden die `Fact.Sale` Tabelle im Jahr 2012. Die Prozedur beschränkt die Standardanzahl der Anzahl der Zeilen pro Tag auf 50000. Dies kann geändert werden, jedoch handelt es sich um es versehentlich Overinflations der Tabelle zu vermeiden.

Darüber hinaus angewendet wird die Prozedur gruppierten columnstore-Index, wenn es nicht bereits angewendet wurde.
