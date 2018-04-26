---
title: Konsolidieren Bewertungsberichte (SQL Server Data Migration Assistant) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 30399ddacff6c84ea1f5d914f87b11dac02167b4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="consolidate-assessment-reports-data-migration-assistant"></a>Konsolidieren Sie Bewertungsberichte (Data Migration Assistant)

Die Befehlszeile können Sie die Migrations-Bewertungen im unbeaufsichtigten Modus ausführen Data Migration Assistant v2. 1 ab. Dieses Feature erleichtert die Bewertungen Größenordnungen ausführen. Die Bewertung von Ergebnissen in Form einer JSON- oder CSV-Datei.

Mehrere Datenbanken in eine einzelne Instanziierung Data Migration Assistant Befehlszeilen-Hilfsprogramm zu bewerten können und alle Bewertungen Ergebnisse in einer einzelnen JSON-Datei exportieren. Alternativ können Sie bewerten Sie eine Datenbank zum Zeitpunkt und später die Ergebnisse aus diesen mehrere JSON-Dateien in einer SQL-Datenbank konsolidieren können.

Informationen zum Migrations-Assistenten Daten über die Befehlszeile ausführen, finden Sie unter [ausführen Data Migration Assistant über Befehlszeile](../dma/dma-commandline.md). 


## <a name="import-assessment-results-into-a-sql-server-database"></a>Assessment-Ergebnisse in einer SQL Server-Datenbank importieren

Verwenden Sie das PowerShell-Skript zur Verfügung, in diesem [Github-Repository](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant) die Bewertungsergebnisse aus JSON-Dateien in einer SQL Server-Datenbank zu importieren.

> [!NOTE]
> PowerShell-v5 oder höher erforderlich.

Wenn Sie das Skript ausführen, müssen Sie die folgenden Informationen bereitstellen: 

- **ServerName**: SQL Server-Instanzname, dass Sie die Bewertung importieren möchten, die aus der JSON-Dateien resultiert.

- **DatabaseName**: den Datenbanknamen, die die Ergebnisse in importiert abrufen.

- **JsonDirectory**: der Ordner, der die Bewertungsergebnisse, in einer oder mehreren JSON-Dateien gespeichert.

- **ProcessTo**: SQL Server

Fügen Sie die vorherigen Werte wie folgt im Abschnitt "Funktionen ausführen" hinzu.

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

Das PowerShell-Skript erstellt die folgenden Objekte in der SQL-Instanz, die Sie angegeben haben, die Wenn die Objekte nicht bereits vorhanden sind:

- **Datenbank** – in der PowerShell-Parameter angegebene Name

  - Wichtigstes repository

- **Tabelle** – ReportData

  - Daten für die Berichterstattung

- **Tabelle** -BreakingChangeWeighting

  - Verweistabelle für alle Änderungen. Hier können Sie Ihre eigenen Werte Gewichtung, um zu beeinflussen, eine genauere Prozentsatz (%) Upgrade Erfolg Rangfolge definieren.

- **Ansicht** – UpgradeSuccessRanking\_lokal

  - Ansicht Anzeigen einer Erfolgsfaktor für jede Datenbank migrierte lokal sein.

- **Ansicht** – UpgradeSuccessRanking\_Azure

  - Ansicht Anzeigen einer Erfolgsfaktor für jede Datenbank migrierte lokal sein.

- **Gespeicherte Prozedur** – JSONResults\_einfügen

  - Zum Importieren von Daten aus einer JSON-Datei in SQL Server verwendet.

- **Gespeicherte Prozedur** – AzureFeatureParityResults\_einfügen

  - Zum Importieren von Azure Feature Parität Ergebnisse aus einer JSON-Datei in SQL Server verwendet.

- **Tabellentyp** – JSONResults

  - Halten die JSON-Ergebnisse für lokalen Bewertungen und übergeben Sie an der JSONResults zum\_gespeicherte Prozedur Insert

- **Tabellentyp** – AzureFeatureParityResults

  - Halten das Azure Feature Parität Ergebnisse für Azure-Bewertungen und übergeben Sie an der AzureFeatureParityResults zum\_gespeicherte Prozedur Insert

Das PowerShell-Skript erstellt eine **verarbeitete** Verzeichnis im angegebenen Verzeichnis, das JSON-Dateien enthält, die verarbeitet werden sollen.

Nach Abschluss des Skripts werden die Ergebnisse in der Tabelle ReportData importiert.

### <a name="viewing-the-results-in-sql-server"></a>Anzeigen der Ergebnisse in SQL Server

Nachdem die Daten geladen wurden, verbinden Sie sich mit Ihrer SQL Server-Instanz. Ihr Bildschirm sollte angezeigt werden, wie in der folgenden Abbildung gezeigt:

![Konsolidierte Berichte in SQL Server-Datenbank](../dma/media/DMAReportingDatabase.png)

Das "Dbo". ReportData-Tabelle enthält den Inhalt des JSON-Datei in seiner Rohform an.

## <a name="on-premises-upgrade-success-ranking"></a>Lokaler upgrade Erfolg Rangfolge

Um eine Liste der Datenbanken und ihren Erfolg Rang (%) angezeigt wird, wählen Sie das "Dbo" ein. UpgradeSuccessRanking_OnPrem anzeigen:

![Anzeige von Daten im UpgradeSuccessRaning_OnPrem](../dma/media/UpgradeSuccessRankingView.png)

Hier können Sie für eine bestimmte Datenbank sehen, was das Upgrade erfolgreich Risiko für verschiedene Kompatibilitätsgraden funktionsfähig ist. Daher wurde beispielsweise Datenbank der Personalabteilung gegen Kompatibilitätsgraden 100, 110, 120 und 130 bewertet. Dieser Bewertung können Sie visuell zu sehen, wie viel Aufwand bei der Migration auf eine höhere Version von SQL Server aus der aktuellen Version, der die Datenbank derzeit auf ist beteiligt ist.

In der Regel ist die Metrik, der Sie interessieren, wie viele Änderungen gibt es für eine bestimmte Datenbank sind. Im vorherigen Beispiel sehen Sie sich, dass die Datenbank der Personalabteilung ein 50 % Upgrade Erfolgsfaktor für Kompatibilitätsgraden 100, 110, 120 und 130 hat.

Diese Metrik kann beeinflusst werden, durch die Gewichtung-Werte in das "Dbo" ändern. BreakingChangeWeighting-Tabelle.

Im folgenden Beispiel der erforderliche Aufwand in der Syntax-Problem behoben ist in der Datenbank der Personalabteilung ist als hoch eingestuft, sodass der Wert 3 zugewiesen wird **Aufwand**. Da es zur Behebung des Problems Syntax lange dauern würde nicht, wird der Wert 1 zugewiesen **FixTime**. Da einige Kosten der Änderung beteiligt sein würde, wird ein Wert von 2 zugewiesen **Kosten**. Verwendung dieses Werts wird die kombinierten Changerank auf 2 geändert.

> [!NOTE]
> Die Bewertung wird auf einer Skala von 1 bis 5.  1 niedrig und 5 hoch. Darüber hinaus ist die ChangeRank eine berechnete Spalte.

![Aufwand, FixTime und Kosten für die Syntax Problem Werte](../dma/media/SyntaxIssueEffort.png)

Jetzt in diesem Beispiel, wenn Sie das "Dbo" Abfragen. UpgradeSuccessRanking_OnPrem anzeigen, wurde das Upgrade Erfolgsfaktor für die Datenbank der Personalabteilung für wichtige Änderungen gelöscht.

![Aktualisieren von Erfolgsfaktor für Personaldatenbank](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Rangfolge von Azure-Upgrade-Erfolg

Um eine Liste der Datenbanken zum Migrieren zu Azure SQL-Datenbank und ihren Erfolg QUANTILSRANG anzuzeigen, wählen Sie das "Dbo" ein. UpgradeSuccessRanking_Azure anzeigen.

![Anzeige von Daten im UpgradeSuccessRanking_Azure](../dma/media/UpgradeSuccessRankingView_Azure.png)

Hier können Sie den Wert MigrationBlocker interessiert. 100,00 bedeutet, dass 100 % Erfolg Rang für das Verschieben einer Datenbank auf Azure SQL-Datenbank v12 vorhanden ist.

Der Unterschied in dieser Ansicht ist, dass derzeit keine Überschreibung für die Gewichtung für die Migration Blocker Regeln ändern.

Informationen zur Meldung von auf diese Daten mithilfe von Power BI finden Sie unter [melden Ihre konsolidierten Bewertungen mit Power BI](../dma/dma-powerbiassesreport.md).
