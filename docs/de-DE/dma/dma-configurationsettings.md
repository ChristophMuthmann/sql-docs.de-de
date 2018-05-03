---
title: Konfigurationseinstellungen (SQL Server Data Migration Assistant) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: b0cc5dc0b34e740034b6e0852163c70c9de9b09b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configuration-settings-for-data-migration-assistant"></a>Konfigurationseinstellungen für Data-Migrations-Assistent

Sie können bestimmte Verhalten der Migration Assistant Daten anhand der Konfigurationswerte in der Datei dma.exe.config optimieren. Dieser Artikel beschreibt wichtige Konfigurationswerte.

Sie finden die dma.exe.config-Datei für die Data Migration Assistant desktop-Anwendung und das Befehlszeilen-Hilfsprogramm in den folgenden Ordnern auf Ihrem Computer.

- Desktop-Anwendung

  "% ProgramFiles%"\\Migrations-Assistenten von Microsoft Data\\dma.exe.config

- Befehlszeilen-Hilfsprogramm

  "% ProgramFiles%"\\Migrations-Assistenten von Microsoft Data\\dmacmd.exe.config 

Achten Sie darauf, dass Sie eine Kopie der ursprünglichen Konfigurationsdatei zu speichern, bevor Sie Änderungen vorzunehmen. Starten Sie nach Änderungen vorgenommen wurden, Data Migration Assistant für die neuen Konfigurationswerte wirksam wird.

## <a name="number-of-databases-to-assess-in-parallel"></a>Anzahl der Datenbanken parallel bewerten

Data Migration Assistant bewertet mehrere Datenbanken gleichzeitig. Während der Bewertung extrahiert Daten Migration Assistant datenebenenanwendung (DACPAC-Datei), das Datenbankschema zu verstehen. Dieser Vorgang kann Timeout, wenn mehrere Datenbanken auf demselben Server parallel bewertet werden. 

Mit Data Migration Assistant v2. 0 beginnen, können Sie Controll dies durch Festlegen der ParallelDatabases Konfigurationswert. Standardwert ist 8.

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>Anzahl der Datenbanken gleichzeitig migriert.

Daten-Migrations-Assistent migriert mehrere Datenbanken gleichzeitig, vor dem Migrieren von Anmeldungen. Während der Migration wird Daten Migration Assistant erstellen Sie eine Sicherung der Quelldatenbank, kopieren Sie optional die Sicherung und anschließend wiederherstellen, auf dem Zielserver. Timeout-Fehler können auftreten, wenn mehrere Datenbanken für die Migration ausgewählt werden. 

Beginnend mit Data Migration Assistant v2. 0, falls dieses Problem auftritt, können Sie den Konfigurationswert ParallelDatabases reduzieren. Sie können den Wert, um verringern Sie die Gesamtdauer der Migration erhöhen.

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX-Einstellungen

Während der Bewertung extrahiert Daten Migration Assistant datenebenenanwendung (DACPAC-Datei), das Datenbankschema zu verstehen. Dieser Vorgang kann fehlschlagen, mit Timeouts für sehr große Datenbanken oder wenn der Server ausgelastet ist. Mit der Datenmigration v1. 0 beginnen, können Sie die folgenden Konfigurationswerte zur Vermeidung von Fehlern ändern. 

> [!NOTE]
> Die gesamte &lt;Dacfx&gt; Eintrag ist standardmäßig auskommentiert. Entfernen Sie die Kommentare, und ändern Sie den Wert an, nach Bedarf.

- CommandTimeout

   Damit wird die Eigenschaft IDbCommand.CommandTimeout in *Sekunden*. (Standard = 60)

- databaseLockTimeout

   Dies entspricht dem [SPERRE festgelegt\_TIMEOUT Timeout\_Zeitraum ](../t-sql/statements/set-lock-timeout-transact-sql.md) in *Millisekunden*. (Standard = 5000)

- maxDataReaderDegreeOfParallelism

   Anzahl der SQL-Verbindung-Pool-Verbindungen zu verwenden. (Standard = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```


## <a name="stretch-database-recommendation-threshold"></a>Stretch-Datenbank: Empfehlung Schwellenwert

Mit [SQL Server Stretch-Datenbank](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database), können Sie dynamisch Ausdehnung von warmen und kalte Transaktionsdaten von Microsoft SQL Server 2016 auf Azure erweitern. Stretch-Datenbank ist auf Transaktionsdatenbanken mit großen Mengen von kalten Daten. Die Empfehlung Stretch-Datenbank unter Speicher Feature Empfehlung, identifiziert zunächst Tabellen, wahrscheinlich profitieren von der dieses Feature ist, und klicken Sie dann identifiziert es Änderungen, die vorgenommen werden, um die Tabelle für diese Funktion aktivieren müssen.

Mit Data Migration Assistant v2. 0 beginnen, können Sie diesen Schwellenwert für eine Tabelle für die Funktion Stretch-Datenbank mit dem Konfigurationswert RecommendedNumberOfRows qualifizieren steuern. Standardwert ist 100.000 Zeilen. Wenn Sie die Stretch-Funktionen für noch kleinere Tabellen analysieren möchten, setzen Sie den Wert entsprechend.

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL-Verbindungstimeout

Sie können steuern, die [SQL-Verbindungstimeout](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx) für Quell- und Instanzen während der Ausführung einer Bewertung oder die Migration durch Festlegen der Wert für das Verbindungstimeout auf eine angegebene Anzahl von Sekunden. Der Standardwert beträgt 15 Sekunden.

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>Siehe auch

[Herunterladen von Daten Migrations-Assistent](https://www.microsoft.com/download/details.aspx?id=53595)
