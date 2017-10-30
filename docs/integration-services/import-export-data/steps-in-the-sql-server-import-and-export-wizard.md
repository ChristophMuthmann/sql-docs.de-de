---
title: Die Schritte in der SQL Server-Import / Export-Assistent | Microsoft Docs
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 22d1f4b78fadab6d7b6659104b54a564f11da308
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>Schritte in der SQL Server-Import / Export-Assistent
Dieses Thema beschreibt die Abfolge der Schritte zum Importieren und Exportieren von Daten mit der SQL Server-Import / Export-Assistenten. Es enthält auch Links zu den einzelnen Seiten eines Dokumentation, die jede Seite beschreiben oder (Dialogfeld), die im Assistenten angezeigt.

Dieses Thema beschreibt nur die **Schritte** im Assistenten. Wenn Sie für ein anderes Element suchen, finden Sie unter [Aufgaben und den Inhalt im Zusammenhang mit](#related).

## <a name="steps-for-importing-and-exporting-data"></a>Schritte zum Importieren und Exportieren von Daten  
 Die folgende Tabelle enthält die Schritte zum Importieren und Exportieren von Daten und die entsprechenden Seiten des Assistenten. Abhängig von den Optionen, die Sie im Assistenten auswählen, nicht in der Regel alle Seiten angezeigt werden.  

Für einen kurzen Blick auf die mehrere Bildschirme in eine typische Sitzung angezeigt werden soll, sehen Sie sich diesem einfachen End-to-End-Beispiel auf einer Seite - [beginnen Sie mit diesem einfachen Beispiel des Import / Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

|Schritt|Seiten des Assistenten|  
|----------|------------------|  
|**Willkommen**<br />Sie müssen auf dieser Seite keine Aktionen durchführen.|[Willkommen beim SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**Wählen Sie die Quelle** der Daten.|[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**Wählen Sie das Ziel** der Daten.|[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**Konfigurieren des Ziels**. (optionaler Schritt)<br /><br /> – Erstellen Sie eine neue Zieldatenbank.<br />– Wenn Sie Daten in eine Textdatei kopieren, konfigurieren Sie zusätzliche Einstellungen.|[Datenbank erstellen](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[Flatfileziel konfigurieren](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**Geben Sie an, was Sie kopieren möchten.**|[Tabelle kopieren oder Datenbank Abfragen](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[Quelltabellen und-Sichten auswählen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[Quellabfrage angeben](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**Konfigurieren Sie den Kopiervorgang**. (optionaler Schritt)<br /><br /> – Erstellen Sie eine neue Zieltabelle.<br />-Entscheiden Sie, was Sie tun, wenn der Assistent nicht weiß Zuordnen von Datentypen zwischen Quelle und Ziel, das Sie ausgewählt haben.<br />– Überprüfen Sie die Spaltenzuordnungen zwischen Quelle und Ziel.<br />– Behandeln Sie Probleme bei der Konvertierung von Datentypen zwischen Quelle und Ziel.<br />– Zeigen Sie eine Vorschau der Daten an, die kopiert werden sollen.|[SQL-Anweisung CREATE Table](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[Typen ohne Konvertierungsprüfung konvertieren](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[Datentypzuordnung überprüfen](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[Spalte Konvertierung Details (Dialogfeld)](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[Vorschau Daten (Dialogfeld)](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**Kopieren Sie die Daten an.**<br /><br /> Speichern Sie die Einstellungen optional als SQL Server Integration Services (SSIS)-Paket.|[Speichern und Paket ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[Abschließen des Assistenten](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[Vorgang](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> Drücken Sie auf einer beliebigen Seite oder in einem beliebigen Dialogfeld des Assistenten F1, um die Dokumentation für die aktuelle Seite anzuzeigen.

## <a name="related"></a>Verwandte Aufgaben und Inhalt  
Hier sind einige andere grundlegende Aufgaben aus.
-   **Finden Sie ein kurzes Beispiel der Funktionsweise des Assistenten aus.**

    -   **Wenn Sie es vorziehen, Screenshots finden Sie unter.** Sehen Sie sich diesem einfachen End-to-End-Beispiel auf einer Seite - [beginnen Sie mit diesem einfachen Beispiel des Import / Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Wenn Sie ein Video ansehen möchten.** In diesem vierminütigen Video aus YouTube, die der Assistent zeigt und erklärt eindeutig und einfach Gewusst wie: Exportieren von Daten in Excel - [mithilfe der SQL Server-Import / Export-Assistenten, um nach Excel exportieren,](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Weitere Informationen zur Funktionsweise des Assistenten.**

    -   **Erfahren Sie mehr über den Assistenten.** Wenn Sie eine Übersicht über den Assistenten suchen, lesen Sie [Importieren und Exportieren von für SQL Server unterstützten Datenquellen](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Informationen Sie zur Verbindung mit Datenquellen und Ziele.** Wenn Sie Informationen zum Herstellen einer Verbindung mit Ihren Daten suchen, wählen Sie die gewünschte Seite aus der Liste hier - [Herstellen einer Verbindung mit Datenquellen mit der SQL Server-Import / Export-Assistenten](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Es gibt eine separate Seite der Dokumentation für jede der verschiedenen häufig verwendeten Datenquellen. 

-   **Starten Sie den Assistenten.** Wenn Sie bereit sind, den Assistenten auszuführen, und nur wissen möchten, wie Sie ihn starten, lesen Sie [Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

-     **So erhalten Sie den Wizard.** Wenn Sie den Assistenten ausführen möchten, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber nicht auf Ihrem Computer installiert ist, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten mit den SQL Server Data Tools (SSDT) installieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).



