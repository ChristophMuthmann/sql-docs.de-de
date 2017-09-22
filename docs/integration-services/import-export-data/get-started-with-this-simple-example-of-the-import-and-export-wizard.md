---
title: Erste Schritte mit diesem einfachen Beispiel des Import / Export-Assistenten | Microsoft Docs
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 1b59268e884d3e797a74ef65d9e75c405d75a0d5
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>Erste Schritte mit diesem einfachen Beispiel des Import / Export-Assistenten
Erfahren Sie, was Sie erwartet in der SQL Server-Import / Export-Assistenten, indem ein häufiges Szenario – Importieren von Daten aus einem Excel-Arbeitsblatt mit einer SQL Server-Datenbank durchlaufen. Auch wenn Sie eine andere Quelle und ein anderes Ziel verwenden möchten, in diesem Thema werden die meisten der gesuchte kennen, den Assistenten ausführen.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Voraussetzung - ist der Assistent auf dem Computer installiert werden?
Wenn Sie den Assistenten ausführen möchten, aber Sie verfügen nicht über [! UMFASSEN[MsCoName](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt).

## <a name="heres-the-excel-source-data-for-this-example"></a>Hier wird die Excel-Quelldaten für dieses Beispiel
So sieht die Quelldaten, die Sie die offensichtlichen kopieren - eine kleine zweispaltige Tabelle im Arbeitsblatt WizardWalkthrough der WizardWalkthrough.xlsx Excel-Arbeitsmappe aus.

![Excel-Quelldaten](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>Hier ist die SQL Server-Zieldatenbank für dieses Beispiel
Hier ist (in SQL Server Management Studio) die SQL Server-Zieldatenbank zu der Sie also die Quelldaten zu kopieren. Die Zieltabelle nicht vorhanden ist – Sie sind im Begriff, die der Assistent die Tabelle für Sie erstellen können.

![SQL Server-Zieldatenbank](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>Schritt 1: Starten des Assistenten
Sie können den Assistenten starten, aus der Microsoft SQL Server 2016-Gruppe auf Windows-Startmenü.

![Starten des Assistenten](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> In diesem Beispiel wählen Sie den 32-Bit-Assistenten aus, da Sie die 32-Bit-Version von Microsoft Office installiert haben. Daher müssen Sie die 32-Bit-Datenanbieter für die Verbindung in Excel verwenden. Für viele andere Datenquellen können Sie in der Regel die 64-Bit-Assistenten auswählen.
>
> Um die 64-Bit-Version von den SQL Server-Import / Export-Assistenten verwenden zu können, müssen Sie SQL Server installieren. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen, und nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten installieren.

Weitere Informationen finden Sie unter [Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

## <a name="step-2---view-the-welcome-page"></a>Schritt 2: Anzeigen der Seite "Willkommen"
Die erste Seite des Assistenten ist die **Willkommen** Seite. 

Wahrscheinlich möchten finden auf dieser Seite erneut, also fahren Sie fort und klicken Sie auf **nicht diese Anfangsseite nicht mehr anzeigen**.

![Willkommen beim Assistenten](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>Schritt 3: Auswählen von Excel als Datenquelle
Auf der nächsten Seite **wählen Sie eine Datenquelle**, Sie Microsoft Excel als Datenquelle auswählen. Klicken Sie dann durchsuchen Sie die Excel-Datei und wählen Sie aus. Geben Sie Sie schließlich die Excel-Version, mit denen Sie die Datei zu erstellen.

![Wählen Sie die Excel-Datenquelle](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

Weitere Informationen zum Verbinden mit Excel finden Sie unter [Herstellen einer Verbindung mit einer Excel-Datenquelle](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md). Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md).

## <a name="step-4---pick-sql-server-as-your-destination"></a>Schritt 4 – SQL-Server als Ziel auswählen
Auf der nächsten Seite **wählen Sie ein Ziel**, Sie Microsoft SQL Server auswählen, wie Ihr Ziel von Kommissionierung an einem der Datenanbieter in der Liste, eine Verbindung mit SQL Server herstellt. Wählen Sie in diesem Beispiel wird die **.Net Framework-Datenanbieter für SQL Server**.

Die Seite zeigt eine Liste von Anbietereigenschaften. Viele davon werden ungeeignete Namen und Einstellungen nicht vertraut. Zum Enterprise-Datenbank herstellen, müssen Sie Glücklicherweise in der Regel nur drei Arten von Informationen bereitstellen. Sie können die Standardwerte für die anderen Einstellungen ignorieren.

|Erforderliche Informationen|.NET Framework-Datenanbieter für SQL Server-Eigenschaft|
|---|---|
|Servername|**Datenquelle**|
|Authentifizierungsinformationen (Anmeldenamen)|**Integrierte Sicherheit von**; oder **Benutzer-ID** und **Kennwort**<br/>Wenn Sie eine Dropdownliste mit Datenbanken auf dem Server anzeigen möchten, müssen Sie zunächst gültige Anmeldeinformationen bereitstellen.|
|Datenbankname|**Anfangskatalog**|

![Wählen Sie das SQL Server-Ziel](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

Weitere Informationen zum Verbinden mit SQL Server finden Sie unter [Herstellen einer Verbindung mit einer SQL Server-Datenquelle](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md). Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>Schritt 5: anstatt das Schreiben einer Abfrage eine Tabelle kopieren
Auf der nächsten Seite **geben Tabelle kopieren oder Datenbank Abfragen**, Sie angeben, dass die gesamte Tabelle der Datenquelle kopiert werden soll. Sie möchten nicht in der SQL-Sprache zur Auswahl der Daten so kopieren Sie eine Abfrage schreiben.

![Gibt an, dass eine Tabelle kopieren](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [geben Tabelle kopieren oder Datenbank Abfragen](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).

## <a name="step-6---pick-the-table-to-copy"></a>Schritt 6: Wählen Sie die zu kopierende Tabelle
Auf der nächsten Seite **wählen Quelltabellen und-Sichten**, Sie wählen Sie die Tabelle oder Tabellen, die aus der Datenquelle kopiert werden sollen. Anschließend ordnen Sie jeder ausgewählten Quelltabelle in einer neuen oder vorhandenen Zieltabelle.

In diesem Beispiel wird standardmäßig der Assistent wurde zugeordnet der **WizardWalkthrough$** Arbeitsblatt in der **Quelle** Spalte in eine neue Tabelle mit demselben Namen beim SQL Server-Ziel. (Die Excel-Arbeitsmappe enthält nur ein einzelnes Arbeitsblatt).
-   Das Dollarzeichen ($) auf den Namen der Quelltabelle gibt ein Excel-Arbeitsblatt an. (Einen benannten Bereich in Excel wird nur mit dem Namen dargestellt.)
-   Der Stern auf das Symbol "Tabelle Ziel" gibt an, dass der Assistent zum Erstellen einer neuen Zieltabelle abgelaufen ist.

![Wählen Sie die Tabelle (vor dem Umbenennen)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

Sie möchten möglicherweise so entfernen Sie das Dollarzeichen ($) nicht mit dem Namen der neuen Zieltabelle.

![Wählen Sie die Tabelle (nach dem Umbenennen)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [wählen Quelltabellen und-Sichten](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).

## <a name="optional-step-7---review-the-column-mappings"></a>Optionaler Schritt 7: Überprüfen Sie die spaltenzuordnungen
Bevor Sie lassen die **Quelltabellen und Sichten auswählen** Seite klicken Sie optional auf die **Zuordnungen bearbeiten** zu öffnen die **Spaltenzuordnungen** (Dialogfeld). Hier in der **Zuordnungen** Tabelle sehen Sie, wie der Assistent Spalten im Quellarbeitsblatt den Spalten in die neue Zieltabelle zuordnen soll.

![Anzeigen von spaltenzuordnungen](../../integration-services/import-export-data/media/view-column-mappings.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

## <a name="optional-step-8---review-the-create-table-statement"></a>Optionaler Schritt 8: Überprüfen Sie die CREATE TABLE-Anweisung
Während der **Spaltenzuordnungen** Dialogfeld geöffnet ist, klicken Sie optional auf die **SQL bearbeiten** zu öffnen die **SQL-Anweisung für Create Table** (Dialogfeld). Hier sehen Sie die **CREATE TABLE** Anweisung, die vom Assistenten zum Erstellen der neuen Zieltabelle generiert. In der Regel müssen Sie die Anweisung zu ändern.

![View, CREATE TABLE-Anweisung](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [SQL-Anweisung für Create Table](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).

## <a name="optional-step-9---preview-the-data-to-copy"></a>Optionaler Schritt 9 – Vorschau anzeigen, die zu kopierenden Daten
Nachdem Sie auf **OK** zu schließen die **Table SQL-Anweisung erstellen** Dialogfeld Feld, und klicken Sie auf **OK** zu schließen die **Spaltenzuordnungen** (Dialogfeld), Sie sind, wieder auf die **wählen Quelltabellen und-Sichten** Seite. Klicken Sie optional auf die **Vorschau** Schaltfläche, um eine Stichprobe der Daten anzuzeigen, die wird der Assistent zum kopieren soll. In diesem Beispiel sucht sie OK.

![Die zu kopierenden Vorschaudaten.](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Vorschaudaten](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>Schritt von 10 – Ja, den Import / Export-Vorgang ausgeführt werden soll
Auf der nächsten Seite **speichern und Paket ausführen**, lassen Sie **sofort ausführen** aktiviert, um die Daten zu kopieren, sobald Sie klicken Sie auf **Fertig stellen** auf der nächsten Seite. Sie können die nächste Seite überspringen, indem Sie auf **Fertig stellen** auf die **speichern und Paket ausführen** Seite.

![Führen Sie das Paket](../../integration-services/import-export-data/media/run-the-package.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [speichern und Paket ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>Schritt 11: Beenden Sie den Assistenten, und führen Sie den Import / Export-Vorgang
Wenn Sie geklickt haben **Weiter** anstelle von **Fertig stellen** auf die **speichern und Paket ausführen** Seite klicken Sie dann auf die nächste Seite **Abschließen des Assistenten**, daraufhin einen Überblick darüber, was der Assistent führen soll. Klicken Sie auf **Fertig stellen** beim Ausführen des Import / Export-Vorgangs.

![Assistenten abschließen](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Abschließen des Assistenten](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).

## <a name="step-12---review-what-the-wizard-did"></a>Schritt 12: Überprüfen Sie, welche Schritte des Assistenten ausgeführt wurden
Klicken Sie auf der letzten Seite sehen Sie sich beim Abschließen jeder Aufgabe durch des Assistenten, und überprüfen Sie die Ergebnisse. Die hervorgehobene Zeile zeigt an, dass der Assistent die Daten erfolgreich kopiert. Sie sind fertig!

![Der Assistent wurde erfolgreich abgeschlossen](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [ausführen](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md).

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>Hier wird die neue Tabelle mit Daten, die in SQL Server kopiert
Hier sehen (in SQL Server Management Studio) die neue Zieltabelle, die der Assistent in SQL Server erstellt.

![Daten, die in SQL Server kopiert](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

Hier sehen (erneut in SSMS) die Daten, die der Assistent in SQL Server kopiert.

![Daten, die in SQL Server 2 kopiert](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>Weitere Informationen  
Weitere Informationen zur Funktionsweise des Assistenten.
-   **Erfahren Sie mehr über den Assistenten.** Wenn Sie eine Übersicht über den Assistenten suchen, lesen Sie [Importieren und Exportieren von für SQL Server unterstützten Datenquellen](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

-   **Weitere Informationen Sie zu den Schritten im Assistenten.** Wenn Sie Informationen zu den Schritten im Assistenten suchen, wählen Sie die gewünschte Seite aus der Liste hier - [Schritte in der SQL Server-Import / Export-Assistenten](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Es gibt auch eine separate Seite der Dokumentation für jede Seite des Assistenten.

-   **Informationen Sie zur Verbindung mit Datenquellen und Ziele.** Wenn Sie Informationen zum Herstellen einer Verbindung mit Ihren Daten suchen, wählen Sie die gewünschte Seite aus der Liste hier - [Herstellen einer Verbindung mit Datenquellen mit der SQL Server-Import / Export-Assistenten](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Es gibt eine separate Seite der Dokumentation für jede der verschiedenen häufig verwendeten Datenquellen.



