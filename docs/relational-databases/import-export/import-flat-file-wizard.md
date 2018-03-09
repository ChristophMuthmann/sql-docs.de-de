---
title: Importieren von Flatfiles in SQL | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: import-export
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.importflatfile.f1
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db507927ac37d8f960f5090c774c6a52fa0d0243
ms.sourcegitcommit: 4a462c7339dac7d3951a4e1f6f7fb02a3e01b331
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="import-flat-file-to-sql-wizard"></a>Assistent zum Importieren von Flatfiles in SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
> Inhalte im Zusammenhang mit dem Import/Export-Assistenten finden Sie unter [SQL Server-Import/Export-Assistent](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).

Mit dem Assistenten zum Importieren von Flatfiles können Daten mühelos aus einer Flatfile (CSV, TXT) in ein Ziel kopiert werden. In dieser Übersicht werden die Gründe für die Verwendung dieses Assistenten beschrieben. Außerdem erfahren Sie, wie er zu finden ist, und erhalten ein einfaches Beispiel, dem Sie folgen können.

## <a name="why-would-i-use-this-wizard"></a>Warum sollte ich diesen Assistenten verwenden?
Dieser Assistent wurde erstellt, um die aktuelle Importoberfläche mithilfe eines intelligenten Frameworks zu verbessern: Program Synthesis using Examples ([PROSE](https://microsoft.github.io/prose/)). Für einen Benutzer ohne spezielle Domänenkenntnisse kann das Importieren von Daten oft eine komplexe, fehleranfällige und mühsame Aufgabe darstellen. Dieser Assistent optimiert und vereinfacht den Importvorgang, sodass es genügt, eine Eingabedatei und einen eindeutigen Tabellennamen auszuwählen. Das PROSE-Framework kümmert sich um den Rest.

PROSE analysiert Datenmuster in Ihrer Eingabedatei, um daraus Spaltennamen, Typen, Trennzeichen und vieles mehr abzuleiten. Dieses Framework erlernt die Struktur der Datei und übernimmt die gesamte Schwerarbeit, um unsere Benutzer zu entlasten.

Um noch mehr über die Verbesserung der Benutzerfreundlichkeit des Assistenten zum Importieren von Flatfiles zu erfahren, schauen Sie sich dieses Video an:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173/player]

## <a name="prerequisites"></a>Erforderliche Komponenten
Dieses Feature ist nur in SQL Server Management Studio (SSMS) v17.3 oder höher verfügbar. Stellen Sie sicher, dass Sie die neueste Version verwenden. Die neueste Version ist [hier](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) zu finden.
 
## <a id="started"></a>Erste Schritte
Um den Assistenten zum Importieren von Flatfiles aufzurufen, gehen Sie folgendermaßen vor:

1. Öffnen Sie **SQL Server Management Studio**.
2. Stellen Sie eine Verbindung mit einer Instanz des SQL Server-Datenbankmoduls oder mit localhost her.
3. Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf eine Datenbank („test“ im folgenden Beispiel), zeigen Sie auf **Aufgaben**, und klicken Sie oberhalb von „Daten importieren“ auf **Flatfile importieren**.

![Assistent: Menü](media/import-flat-file-wizard/importffmenu.png)

Weitere Informationen über die verschiedenen Funktionen des Assistenten finden Sie im folgenden Tutorial.

## <a name="tutorial"></a>Lernprogramm
Für den Zweck dieses Tutorials können Sie gerne Ihre eigene Flatfile verwenden. Andernfalls verwendet dieses Tutorial die folgende CSV-Datei aus Excel, die Sie kopieren können. Wenn Sie diese CSV-Datei verwenden, benennen Sie sie **example.csv**, und stellen Sie sicher, dass Sie sie als CSV-Datei an einem leicht zugänglichen Speicherort wie z.B. dem Desktop speichern.

![Assistent: Excel](media/import-flat-file-wizard/importffexample.png)

### <a name="step-1-access-wizard-and-intro-page"></a>Schritt 1: Öffnen Sie den Assistenten und die Einführungsseite.
Öffnen Sie den Assistenten, wie [hier](#started) beschrieben wird.

Die erste Seite des Assistenten ist die Startseite. Wenn Sie diese Seite nicht mehr anzeigen möchten, klicken Sie einfach auf **Diese Anfangsseite nicht mehr anzeigen**.

![Assistent: Einführung](media/import-flat-file-wizard/importffintro.png)

### <a name="step-2-specify-input-file"></a>Schritt 2: Geben Sie die Eingabedatei an.
Klicken Sie auf „Durchsuchen“, um die Eingabedatei auszuwählen. Der Assistent sucht standardmäßig nach CSV- und TXT-Dateien. 

Der neue Tabellenname muss eindeutig sein, andernfalls lässt der Assistent Sie nicht fortfahren.

![Assistent: Angabe](media/import-flat-file-wizard/importffspecify.png)

### <a name="step-3-preview-data"></a>Schritt 3: Zeigen Sie eine Vorschau der Daten an.
Der Assistent generiert eine Vorschau, die für die ersten 50 Zeilen angezeigt werden kann. Wenn Probleme auftreten, klicken Sie auf „Abbrechen“. Fahren Sie andernfalls mit der nächsten Seite fort.

![Assistent: Vorschau](media/import-flat-file-wizard/importffpreview.png)

### <a name="step-4-modify-columns"></a>Schritt 4: Ändern Sie Spalten.
Der Assistent identifiziert die richtigen Spaltennamen, Datentypen usw. Hier können Sie die Felder bearbeiten, wenn sie nicht korrekt sind (z.B. muss der Datentyp „float“ anstatt von „int“ lauten).

Fahren Sie fort, wenn Sie fertig sind.

![Assistent: Ändern](media/import-flat-file-wizard/importffmodify.png)

### <a name="step-5-summary"></a>Schritt 5: Zusammenfassung
Dies ist lediglich eine Übersichtsseite, auf der Ihre aktuelle Konfiguration angezeigt wird. Wenn Probleme vorliegen, können Sie zu den vorherigen Abschnitten zurückwechseln. Andernfalls wird durch Klicken auf „Fertig stellen“ der Importvorgang gestartet.

![Assistent: Zusammenfassung](media/import-flat-file-wizard/importffsummary.png)

### <a name="step-6-results"></a>Schritt 6: Ergebnisse
Diese Seite gibt an, ob der Import erfolgreich war. Wenn ein grünes Häkchen angezeigt wird, war er erfolgreich. Andernfalls müssen Sie möglicherweise Ihre Konfiguration oder Ihre Eingabedatei auf Fehler überprüfen.

![Assistent: Ergebnisse](media/import-flat-file-wizard/importffresults.png)

## <a name="learn-more"></a>Weitere Informationen

Weitere Informationen zum Assistenten.

- **Weitere Informationen zum Importieren anderer Quellen.** Wenn Sie außer Flatfiles noch andere Dateien importieren möchten, finden Sie weitere Informationen unter [SQL Server-Import/Export-Assistent](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).
- **Weitere Informationen zum Herstellen einer Verbindung mit Flatfilequellen.** Weitere Informationen zum Herstellen einer Verbindung mit Flatfilequellen finden Sie unter [Herstellen einer Verbindung mit einer Flatfile-Datenquelle](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard).
- **Weitere Informationen zu PROSE.** Eine Übersicht über das intelligente Framework, das von diesem Assistenten verwendet wird, finden Sie unter [PROSE SDK](https://microsoft.github.io/prose/).

