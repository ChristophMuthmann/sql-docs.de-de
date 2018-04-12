---
title: Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a684f719495083d5ca4e79a2fbc0213ab83a95a6
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten
Erfahren Sie, was Sie von dem Import/Export-Assistenten von SQL Server im Hinblick auf alltägliche Szenarios erwarten können. In diesem Artikel geht es um das Importieren von Daten aus einem Excel-Arbeitsblatt in eine SQL Server-Datenbank. Selbst wenn Sie planen, eine andere Quelle und ein anderes Ziel zu verwenden, werden Ihnen trotzdem in diesem Artikel nützliche Informationen zum Ausführen des Assistenten zur Verfügung gestellt.

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Voraussetzung: Installation des Assistenten auf dem Computer
Wenn Sie den Assistenten ausführen möchten, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber nicht auf Ihrem Computer installiert ist, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten mit den SQL Server Data Tools (SSDT) installieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="heres-the-excel-source-data-for-this-example"></a>In diesem Beispiel verwendete Excel-Quelldaten
In der folgenden Abbildung werden die Quelldaten dargestellt, die kopiert werden sollen. Dabei handelt es sich um eine kleine Tabelle mit zwei Spalten im WizardWalkthrough-Arbeitsblatt der Excel-Arbeitsmappe „WizardWalkthrough.xlsx“.

![Excel-Quelldaten](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>In diesem Beispiel verwendete SQL Server-Zieldatenbank
In der folgenden Abbildung wird die SQL Server-Zieldatenbank (in SQL Server Management Studio) dargestellt, in die die Quelldaten kopiert werden sollen. Zu diesem Zeitpunkt gibt es noch keine Zieltabelle, da der Assistent diese für Sie erstellen soll.

![SQL Server-Zieldatenbank](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>Schritt 1: Starten des Assistenten
Starten Sie den Assistenten über die Microsoft SQL Server 2016-Gruppe im Windows-Startmenü.

![Starten des Assistenten](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> In diesem Beispiel wird der 32-Bit-Assistent ausgewählt, da die 32-Bit-Version von Microsoft Office installiert ist. Aus diesem Grund muss auch der 32-Bit-Datenanbieter verwendet werden, um eine Verbindung mit Excel herzustellen. Für viele andere Datenquellen kann in der Regel auch der 64-Bit-Assistent ausgewählt werden.
>
> Sie müssen SQL Server installieren, um die 64-Bit-Version des Import/Export-Assistenten von SQL Server verwenden zu können. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen und installieren daher auch nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten.

Weitere Informationen finden Sie unter [Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

## <a name="step-2---view-the-welcome-page"></a>Schritt 2: Anzeigen der Startseite
Die erste Seite des Assistenten ist die **Startseite**. 

Wenn Sie diese Seite nicht mehr anzeigen lassen möchten, klicken Sie einfach auf **Diese Anfangsseite nicht mehr anzeigen**.

![Willkommen beim Assistenten](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>Schritt 3: Auswählen von Excel als Datenquelle
Wählen Sie auf der nächsten Seite (**Datenquelle auswählen**) Microsoft Excel als Ihre Datenquelle aus. Suchen Sie dann die Excel-Datei, die Sie auswählen möchten. Geben Sie dann die Excel-Version an, die Sie zum Erstellen der Datei verwendet haben.

> [!IMPORTANT]
> Ausführliche Informationen über das Herstellen einer Verbindung mit Excel-Dateien sowie Einschränkungen und bekannte Probleme beim Laden von Daten aus oder in Excel-Dateien finden Sie unter [Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md).

![Auswählen der Excel-Datenquelle](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Choose a Data Source (Auswählen einer Datenquelle)](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md).

## <a name="step-4---pick-sql-server-as-your-destination"></a>Schritt 4: Auswählen von SQL Server als Ziel
Wählen Sie auf der nächsten Seite (**Ziel auswählen**) Microsoft SQL Server als Ziel aus, indem Sie einen der Datenanbieter aus der Liste auswählen, die eine Verbindung mit SQL Server herstellen. Wählen Sie für dieses Beispiel **.NET Framework-Datenanbieter für SQL Server** aus.

Auf der Seite wird eine Liste mit Anbietereigenschaften angezeigt. Darunter befinden sich viele ungeeignete Namen und ungewöhnliche Einstellungen. Damit Sie eine Verbindung mit einer Unternehmensdatenbank herstellen können, benötigen Sie in der Regel nur drei Informationen. Die Standardwerte für die anderen Einstellungen können Sie ignorieren.

|Erforderliche Informationen|Eigenschaft „.NET Framework-Datenanbieter für SQL Server“|
|---|---|
|Servername|**Datenquelle**|
|Authentifizierungsinformationen (Anmeldung)|**Integrierte Sicherheit**, oder **Benutzer-ID** und **Kennwort**<br/>Wenn eine Dropdownliste mit den Datenbanken auf dem Server angezeigt werden soll, müssen Sie zunächst gültige Anmeldeinformationen eingeben.|
|Datenbankname|**Anfangskatalog**|

![Auswählen des SQL Server-Ziels](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

Weitere Informationen zum Herstellen einer Verbindung mit SQL Server finden Sie unter [Connect to an SQL Server Data Source (Herstellen einer Verbindung mit einer SQL Server-Datenquelle)](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md). Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Choose a Destination (Auswählen eines Ziels)](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>Schritt 5: Kopieren einer Tabelle anstelle des Schreibens einer Abfrage
Geben Sie auf der nächsten Seite (**Tabelle kopieren oder Datenbank abfragen**) an, dass Sie die ganze Tabelle aus der Datenquelle kopieren möchten. So können Sie es vermeiden, eine Abfrage in der SQL-Sprache schreiben zu müssen, um die Daten auszuwählen, die kopiert werden sollen.

![Angeben zum Kopieren einer Tabelle](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Specify Table Copy or Query (Angeben einer Tabellenkopie oder Abfrage)](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).

## <a name="step-6---pick-the-table-to-copy"></a>Schritt 6: Auswählen der Tabelle, die kopiert werden soll
Wählen Sie auf der nächsten Seite (**Quelltabellen und -sichten auswählen**) die Tabelle(n) aus, die Sie aus der Datenquelle kopieren möchten. Anschließend ordnen Sie jede ausgewählte Quelltabellen einer neuen oder vorhandenen Zieltabelle zu.

In diesem Beispiel ist das **WizardWalkthrough$**-Arbeitsblatt in der **Quellspalte** standardmäßig einer neuen Tabelle mit demselben Namen im SQL Server-Ziel zugeordnet. (Die Excel-Arbeitsmappe enthält nur ein einziges Arbeitsblatt.)
-   Das Dollarzeichen ($) im Namen der Quelltabelle deutet auf ein Excel-Arbeitsblatt hin. (In Excel wird ein benannter Bereich nur mit seinem Namen dargestellt.)
-   Der Stern auf dem Symbol der Zieltabelle deutet darauf hin, dass der Assistent eine neue Zieltabelle erstellen wird.

![Wählen Sie die Tabelle aus (bevor Sie sie umbenennen)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

Wahrscheinlich möchten Sie das Dollarzeichen ($) aus dem Namen der neuen Zieltabelle löschen.

![Wählen Sie die Tabelle aus (nachdem Sie sie umbenennen)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Select Source Tables and Views (Auswählen von Quelltabellen und -sichten)](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).

## <a name="optional-step-7---review-the-column-mappings"></a>Schritt 7 (optional): Überprüfen der Spaltenzuordnungen
Bevor Sie die Seite **Quelltabellen und -sichten auswählen** verlassen, können Sie auf die Schaltfläche **Zuordnungen bearbeiten** klicken, um das Dialogfeld **Spaltenzuordnungen** zu öffnen. In der Tabelle **Zuordnungen** können Sie dabei sehen, wie der Assistent Spalten im ursprünglichen Arbeitsblatt Spalten in der neuen Zieltabelle zuordnet.

![Ansicht der Spaltenzuordnungen](../../integration-services/import-export-data/media/view-column-mappings.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Column Mappings (Spaltenzuordnungen)](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

## <a name="optional-step-8---review-the-create-table-statement"></a>Schritt 8 (optional): Überprüfen der CREATE TABLE-Anweisung
Wenn das Dialogfeld **Spaltenzuordnungen** geöffnet ist, können Sie auf die Schaltfläche **SQL bearbeiten** klicken, um das Dialogfeld **SQL-Anweisung CREATE TABLE** zu öffnen. Dann wird die Anweisung **CREATE TABLE** angezeigt, die der Assistent generiert hat, um die neue Zieltabelle zu erstellen. In der Regel müssen Sie die Anweisung nicht ändern.

![Ansicht der CREATE TABLE-Anweisung](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Create Table SQL Statement (Erstellen einer SQL-Tabellenanweisung)](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).

## <a name="optional-step-9---preview-the-data-to-copy"></a>Schritt 9 (optional): Überprüfen der Daten, die kopiert werden sollen
Nachdem Sie auf **OK** geklickt haben, um das Dialogfeld **SQL-Anweisung CREATE TABLE** zu schließen, klicken Sie erneut auf **OK**, um das Dialogfeld **Spaltenzuordnungen** zu schließen. So gelangen Sie zurück auf die Seite **Quelltabellen und -sichten auswählen**. Sie können auf die Schaltfläche **Vorschau** klicken, damit ein Beispiel der Daten angezeigt wird, die vom Assistenten kopiert werden. In diesem Beispiel scheinen die Daten in Ordnung zu sein.

![Vorschau der Daten, die kopiert werden sollen](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Preview Data (Vorschau der Daten)](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>Schritt 10: Ausführen des Import/Export-Vorgangs
Die Aktivierung von **Sofort ausführen** auf der nächsten Seite (**Paket speichern und ausführen**) sollte bestehen bleiben, damit die Daten kopiert werden, sobald Sie auf der nächsten Seite auf **Fertig stellen** klicken. Stattdessen können Sie diesen Schritt auch überspringen, indem Sie auf der Seite **Paket speichern und ausführen** auf **Fertig stellen** klicken.

![Ausführen des Pakets](../../integration-services/import-export-data/media/run-the-package.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Save and Run Package (Paket speichern und ausführen)](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>Schritt 11: Beenden des Assistenten und Ausführen des Import/Export-Vorgangs
Wenn Sie anstatt auf **Fertig stellen** auf der Seite **Paket speichern und ausführen** auf **Weiter** geklickt haben, wird auf der nächsten Seite (**Assistenten abschließen**) eine Zusammenfassung der Aufgaben des Assistenten angezeigt. Klicken Sie auf **Fertig stellen**, um den Import/Export-Vorgang auszuführen.

![Assistenten abschließen](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Complete the Wizard (Abschließen des Assistenten)](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).

## <a name="step-12---review-what-the-wizard-did"></a>Schritt 12: Überprüfen der Ergebnisse
Sehen Sie auf der letzten Seite dabei zu, wie der Assistent seine Aufgaben fertig stellt, und prüfen Sie dann die Ergebnisse. In der hervorgehobenen Zeile wird darauf hingedeutet, dass der Assistent Ihre Daten erfolgreich kopiert hat. Sie sind jetzt fertig!

![Der Assistent war erfolgreich](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

Weitere Informationen zu dieser Seite des Assistenten finden Sie unter [Performing Operation (Ausführen eines Vorgangs)](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md).

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>Die neue Tabelle von Daten, die in SQL Server kopiert wurden
An dieser Stelle wird (in SQL Server Management Studio) die neue Zieltabelle angezeigt, die der Assistent in SQL Server erstellt hat.

![In SQL Server kopierte Daten](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

An dieser Stelle (wieder in SQL Server Management Studio) werden die Daten angezeigt, die der Assistent in SQL Server kopiert hat.

![In SQL Server kopierte Daten 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>Weitere Informationen  
Weitere Informationen zu den Funktionen des Assistenten.
-   **Weitere Informationen zum Assistenten:** Wenn Sie eine Übersicht über den Assistenten suchen, lesen Sie [Importieren und Exportieren von für SQL Server unterstützten Datenquellen](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

-   **Weitere Informationen zu den Schritten des Assistenten:** Wählen Sie für weitere Informationen zu den einzelnen Schritten des Assistenten die Seite aus der Liste aus, die Sie besonders interessiert: [Steps in the SQL Server Import and Export Wizard (Schritte des SQL Server Import/Export-Assistenten)](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Es ist außerdem eine eigene Dokumentationsseite für jede Seite des Assistenten verfügbar.

-   **Weitere Informationen zum Herstellen einer Verbindung zwischen Datenquellen und -zielen:** Wählen Sie für weitere Informationen zum Herstellen einer Verbindung mit Ihren Daten die Seite aus der Liste aus, die Sie besonders interessiert: [Connect to data sources with the SQL Server Import and Export Wizard (Herstellen einer Verbindung mit Datenquellen mit dem SQL Server Import/Export-Assistenten)](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Es sind separate Dokumentationsseiten für verschiedene, häufig verwendete Datenquellen verfügbar.

-   **Weitere Informationen zum Laden von Daten aus und in Excel.** Informationen über das Herstellen einer Verbindung mit Excel-Dateien und Einschränkungen und bekannte Probleme beim Laden von Daten aus oder in Excel-Dateien finden Sie unter [Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md).