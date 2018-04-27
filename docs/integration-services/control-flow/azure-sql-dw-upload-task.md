---
title: Azure SQL DW-Uploadtask | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPDWUPTASK.F1
- sql14.dts.designer.afpdwuptask.f1
ms.assetid: eef82c89-228a-4dc7-9bd0-ea00f57692f5
caps.latest.revision: 5
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bff2df8d44cf8406a507fb764cb409f766f15bab
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="azure-sql-dw-upload-task"></a>Azure SQL DW-Uploadtask
Der **Azure SQL DW-Uploadtask** ermöglicht einem SSIS-Paket, lokale Daten in eine Tabelle in Azure SQL Data Warehouse (DW) hochzuladen. Das gegenwärtig unterstützte Quelldatenformat ist Text mit Trennzeichen in UTF8-Codierung. Der Hochladevorgang folgt dem effizienten PolyBase-Ansatz gemäß Beschreibung im Artikel [Azure SQL Data Warehouse Loading Patterns and Strategies](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/)(Azure SQL Data Warehouse: Muster und Strategien zum Laden). Insbesondere werden Daten zunächst in Azure Blob Storage und dann in Azure SQL Data Warehouse hochgeladen. Darum ist ein Azure Blob Storage-Konto erforderlich, um diesen Task zu verwenden.

Der **Azure SQL DW-Uploadtask** ist eine Komponente des [SQL Server Integration Services-Feature Packs (SSIS) für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Um einen **Azure SQL DW-Uploadtask**hinzuzufügen, ziehen Sie ihn mittels Drag &amp; Drop aus der SSIS-Toolbox auf den Designercanvas, und doppelklicken Sie, oder klicken Sie mit der rechten Maustaste darauf, und klicken Sie anschließend auf **Bearbeiten** , um das Dialogfeld des Task-Editors anzuzeigen.

Konfigurieren Sie auf der Seite **Allgemein** die folgenden Eigenschaften.

Feld|Description
-----|-----------
LocalDirectory|Gibt das lokale Verzeichnis mit den Datendateien an, die hochgeladen werden sollen.
Rekursiv|Gibt an, ob Unterverzeichnisse rekursiv durchsucht werden sollen.
FileName|Geben Sie einen Namensfilter zum Auswählen von Dateien mit einem bestimmten Namensmuster an. Beispiel: „MeinArbeitsblatt*.xsl\* “ schließt „MeinArbeitsblatt001.xsl“ und „MeinArbeitsblattABC.xslx“ ein.
RowDelimiter|Gibt ein oder mehrere Zeichen an, die das Ende jeder Zeile markieren.
ColumnDelimiter|Gibt ein oder mehrere Zeichen an, die das Ende jeder Spalte markieren. Beispiel: &#124; (senkrechter Strich), \t (Tabulator), ' (einfaches Anführungszeichen), " (doppeltes Anführungszeichen) und 0x5c (umgekehrter Schrägstrich).
IsFirstRowHeader|Gibt an, ob die erste Zeile in jeder Datendatei Spaltennamen statt tatsächlicher Daten enthält.
AzureStorageConnection|Gibt einen Azure Storage-Verbindungs-Manager an.
BlobContainer|Gibt den Namen des Blobcontainers an, zu dem lokale Daten hochgeladen und über PolyBase an Azure DW weitergeleitet werden. Falls noch nicht vorhanden ist, wird ein neuer Container erstellt.
BlobDirectory|Gibt das Blobverzeichnis an (virtuelle Hierarchiestruktur), zu dem lokale Daten hochgeladen und über PolyBase an Azure DW weitergeleitet werden.
RetainFiles|Gibt an, ob die zu Azure Storage hochgeladenen Dateien beibehalten werden sollen.
CompressionType|Gibt an, welches Komprimierungsformat beim Hochladen von Dateien in Azure Storage verwendet werden soll. Die lokale Quelle ist nicht betroffen.
CompressionLevel|Gibt an, welcher Komprimierungsgrad für das Komprimierungsformat verwendet werden soll.
AzureDwConnection|Gibt einen ADO.NET-Verbindungs-Manager für Azure SQL Data Warehouse an.
TableName|Gibt den Namen der Zieltabelle an. Wählen Sie entweder einen vorhandenen Tabellennamen, oder erstellen Sie einen neuen durch Auswahl von **\<<Neue Tabelle...>**.
TableDistribution|Gibt die Verteilungsmethode für die neue Tabelle an. Gilt, wenn für **TableName**ein neuer Tabellenname angegeben wird.
HashColumnName|Gibt an, welche Spalte für die Verteilung der Hashtabelle verwendet werden soll. Gilt, wenn **HASH** für **TableDistribution**angegeben wird.

Je nachdem, ob Sie zu einer neuen oder einer vorhandenen Tabelle hochladen, sehen Sie eine andere Seite **Zuordnungen** . Konfigurieren Sie im ersten Fall, welche Quellspalten zugeordnet werden sollen, sowie ihre entsprechenden Namen in der zu erstellenden Zieltabelle. Konfigurieren Sie im letzten Fall die Zuordnungsbeziehungen zwischen Quell- und Zielspalten.

Konfigurieren Sie auf der Seite **Spalten** die Datentypeigenschaften für jede Quellspalte.

Die Seite **T-SQL** zeigt das zum Laden von Daten aus Azure Blob Storage in Azure SQL Data Warehouse verwendete T-SQL an. Das T-SQL wird automatisch von Konfigurationen auf den anderen Seiten generiert und als Teil der Taskausführung ausgeführt. Um das generierte T-SQL wahlweise nach Ihren speziellen Bedürfnissen manuell zu bearbeiten, klicken Sie auf die Schaltfläche **Bearbeiten** . Sie können später durch Klicken auf die Schaltfläche **Zurücksetzen** das automatisch generierte wiederherstellen.

