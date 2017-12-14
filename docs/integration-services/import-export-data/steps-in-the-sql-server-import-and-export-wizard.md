---
title: Schritte im SQL Server-Import/Export-Assistenten | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aed445a4a884aa07f1fa93a0f27cfe2763bfe4b4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>Schritte im SQL Server-Import/Export-Assistenten
Dieses Thema beschreibt die Abfolge der Schritte zum Importieren und Exportieren von Daten mit dem SQL Server-Import/Export-Assistenten. Es enthält auch Links zu den einzelnen Seiten der Dokumentation, die die Seiten bzw. Dialogfelder des Assistenten im Einzelnen beschreiben.

Dieses Thema beschreibt nur die im Assistenten durchzuführenden **Schritte**. Wenn Sie andere Themen interessieren, lesen Sie die Seite [Verwandte Tasks und Inhalte](#related).

## <a name="steps-for-importing-and-exporting-data"></a>Schritte zum Importieren und Exportieren von Daten  
 Die folgende Tabelle enthält die Schritte zum Importieren und Exportieren von Daten und die entsprechenden Seiten des Assistenten. Abhängig von den Optionen, die Sie im Assistenten auswählen, werden in der Regel nicht alle diese Seiten angezeigt.  

Um einen schnellen Überblick über die verschiedenen Bildschirme in einer typischen Sitzung zu erhalten, sehen Sie sich ein einfaches vollständiges Beispiel auf der Seite [Get started with this simple example of the Import and Export Wizard (Erste Schritte mit diesem einfachen Beispiel für den Import/Export-Assistenten)](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md) an.

|Schritt|Seiten des Assistenten|  
|----------|------------------|  
|**Willkommen**<br />Sie müssen auf dieser Seite keine Aktionen durchführen.|[Willkommen beim SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**Wählen Sie die Quelle** der Daten.|[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**Wählen Sie das Ziel** der Daten.|[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**Konfigurieren des Ziels** (optionale Schritte)<br /><br /> – Erstellen Sie eine neue Zieldatenbank.<br />– Wenn Sie Daten in eine Textdatei kopieren, konfigurieren Sie zusätzliche Einstellungen.|[Erstellen einer Datenbank](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[Konfigurieren eines Flatfileziels](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**Angeben der zu kopierenden Inhalte**|[Kopieren von Tabellen oder Abfragen von Datenbanken](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[Auswählen von Quelltabellen und -sichten](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[Angeben einer Quellabfrage](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**Konfigurieren des Kopiervorgangs** (optionale Schritte)<br /><br /> – Erstellen Sie eine neue Zieltabelle.<br />– Legen Sie fest, was zu tun ist, wenn der Assistent nicht weiß, wie Datentypen zwischen der ausgewählten Quelle und dem Ziel zugeordnet werden können.<br />– Überprüfen Sie die Spaltenzuordnungen zwischen Quelle und Ziel.<br />– Behandeln Sie Probleme bei der Konvertierung von Datentypen zwischen Quelle und Ziel.<br />– Zeigen Sie eine Vorschau der Daten an, die kopiert werden sollen.|[SQL-Anweisung CREATE TABLE](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[Typen ohne Konvertierungsprüfung konvertieren](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[Datentypzuordnung überprüfen](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[Dialogfeld „Spaltenkonvertierungsdetails“](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[Dialogfeld „Datenvorschau“](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**Kopieren Sie die Daten.**<br /><br /> Speichern Sie optional Ihre Einstellungen als SSIS-Paket (SQL Server Integration Services).|[Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[Assistenten abschließen](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[Vorgang wird ausgeführt](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> Drücken Sie auf einer beliebigen Seite oder in einem beliebigen Dialogfeld des Assistenten F1, um die Dokumentation für die aktuelle Seite anzuzeigen.

## <a name="related"></a> Verwandte Tasks und Inhalte  
Im Folgenden werden einige weitere grundlegenden Tasks aufgelistet.
-   **Sehen Sie sich ein kurzes Beispiel zur Funktionsweise des Assistenten an.**

    -   **Wenn Sie lieber mit Screenshots arbeiten:** Sehen Sie sich das folgende einfache vollständige Beispiel auf der Seite [Get started with this simple example of the Import and Export Wizard (Erste Schritte mit diesem einfachen Beispiel für den Import/Export-Assistenten)](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md) an.

    -   **Wenn Sie sich lieber ein Video ansehen möchten:** Sehen Sie sich dieses vierminütige YouTube-Video an, in dem der Assistent vorgestellt wird und klar und deutlich erklärt wird, wie Daten nach Excel exportiert werden können: [Using the SQL Server Import and Export Wizard to Export to Excel (Verwenden des SQL Server-Import/Export-Assistenten zum Exportieren nach Excel)](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Weitere Informationen zur Funktionsweise des Assistenten:**

    -   **Weitere Informationen zum Assistenten:** Wenn Sie eine Übersicht über den Assistenten suchen, lesen Sie [Importieren und Exportieren von für SQL Server unterstützten Datenquellen](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Weitere Informationen zum Herstellen einer Verbindung zwischen Datenquellen und -zielen:** Um weitere Informationen zum Herstellen einer Verbindung mit Ihren Daten zu erhalten, wählen Sie aus der folgenden Liste die Seite aus, die Sie besonders interessiert: [Connect to data sources with the SQL Server Import and Export Wizard (Herstellen einer Verbindung mit Datenquellen mit dem SQL Server Import/Export-Assistenten)](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Es sind separate Dokumentationsseiten für verschiedene, häufig verwendete Datenquellen verfügbar. 

-   **Starten des Assistenten:** Wenn Sie bereit sind, den Assistenten auszuführen, und nur wissen möchten, wie Sie ihn starten, lesen Sie [Starten des SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

-     **So erhalten Sie den Wizard.** Wenn Sie den Assistenten ausführen möchten, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber nicht auf Ihrem Computer installiert ist, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten mit den SQL Server Data Tools (SSDT) installieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).


