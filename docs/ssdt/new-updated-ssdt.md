---
title: "Aktualisiert: Dokumentation zu SSDT für SQL Server | Microsoft-Dokumentation"
description: "Anzeigen von Codeausschnitten für aktualisierten Inhalt für kürzliche Änderungen in der Dokumentation zu SQL Server Data Tools (SSDT) für Microsoft SQL Server"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: ssdt
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.openlocfilehash: 07bfbac52cdd7d118ffd58842fe2085d52265e6f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Neu und zuletzt kürzlich aktualisiert: SQL Server Data Tools (SSDT)



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates*: &nbsp; **28.09.2017** &nbsp; – bis – &nbsp; **02.12.2017**
- *Themenbereich:* &nbsp; **SQL Server Data Tools (SSDT)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


***Dieses Mal sind keine neuen Artikel aufgeführt.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Änderungsprotokoll für SQL Server Data Tools (SSDT)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [Änderungsprotokoll für SQL Server Data Tools (SSDT)](changelog-for-sql-server-data-tools-ssdt.md)

*Aktualisiert: 20.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7700cae7cafe1dac95c240b014f14d9c83e32be4 6416949beaee91da2f77dfebb9eb5ed363db4cb7  (PR=4032  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->




**SSDT für Visual Studio 2017 (15.4.0, Vorschauversion)**

Buildnummer: 14.0.16134.0

**Neuigkeiten**


Dieses Release bietet einen eigenständigen Webinstaller für Projekte von SQL Server-Datenbank, Analysis Services, Reporting Services und Integration Services in Visual Studio 2017 15.4 und höher.

**Installationsprogramm**


- Der Benutzer kann nun einen Spitznamen bei der Installation einer neuen SSDT-Instanz (SQL Server Data Tools) für Visual Studio 2017 angeben.
- Das Kontrollkästchen „Funktionsauswahl“ des Installationsprogramms wird ausgeblendet, wenn keine Instanz von Visual Studio ausgewählt ist.
- Einige Meldungen des Installationsprogramms wurden basierend auf Kundenfeedback verfeinert.
- Ein Problem wurde behoben, bei dem das Installationsprogramm keine Upgrades unterstützt hat.


**SSIS**


- Ein Problem wurde behoben, bei dem der Assistent für Import/Export keine Datenquellen auflisten konnte, wenn Azure Feature Pack installiert ist.
- Ein Problem wurde behoben, bei dem das Bearbeiten einer SSIS Analysis Services-Prozessaufgabe eine Ausnahme auslöst, wenn die Verbindung gewechselt wird.
- Ein Problem wurde behoben, bei dem CDC-Komponenten unterbrochen wurden, nachdem die SQL-Problembehebung angewendet wurde, die die Spalte „__$command_id“ hinzufügt.
- Ein Problem wurde behoben, bei dem Drittanbieterpakete nicht bearbeitet und ausgeführt werden konnten, wenn eine ältere Version von SQL Server angezielt wurde.
- Ein Problem wurde behoben, bei dem das Dialogfeld „Konfigurieren“ der Flatfilequelle nicht ordnungsgemäß angezeigt wurde, wenn doppelt auf „DTSWizard.exe“ geklickt und „Flatfilequelle“ ausgewählt wurde.
- Ein Problem wurde behoben, bei dem ein Paket, das Azure Feature Pack-Aufgaben und -Komponenten enthält, nicht ausgeführt werden konnte, wenn SQL Server 2017 angezielt wurde.


**Bekannte Probleme**

- Das Installationsprogramm ist nicht lokalisiert.
- Die SSIS-Aufgabe „Paket ausführen“ unterstützt kein Debuggen, wenn der Prozess *ExecuteOutOfProcess* auf TRUE festgelegt ist. Dieses Problem gilt nur für das Debuggen. Das Speichern, Bereitstellen und Ausführen über „DTExec.exe“ oder den SSIS-Katalog wird nicht beeinträchtigt.


**SSDT 17.3 für Visual Studio 2015**

Buildnummer: 14.0.61709.290

**Neuigkeiten**


**Analysis Services (AS)**

- Cosmos DB und HDI Spark werden in 1400-Modellen aktiviert
- Tabellarische Datenquelleneigenschaften
- Die „Leere Abfrage“ ist nun eine unterstützte Option zum Erstellen einer neuen Abfrage im Abfrage-Editor für Modelle des Kompatibilitätsgrads 1400.
- Der Abfrage-Editor für Modelle im Modus 1400 erlaubt nun das Speichern von Abfragen, ohne das neue Tabellen automatisch verarbeitet werden.







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neu + Aktualisiert (3+14): Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (1+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (1+0): Analysis Services für SQL-Dokumente)](../analysis-services/new-updated-analysis-services.md)
- [Neu + Aktualisiert (87+0): Dokumente zu **Analyseplattformsystem für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu + Aktualisiert (5+4): Dokumente zu **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu + Aktualisiert (0+1): Dokumente zum **Datenbankmodul für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu + Aktualisiert (2+2):Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu + Aktualisiert (10+9): Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu + Aktualisiert (2+4): Dokumente zu **Relationale Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu + Aktualisiert (4+2): Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu + Aktualisiert (0+1): Dokumente zu **Beispiele für SQL**](../sample/new-updated-sample.md)
- [Neu + Aktualisiert (21+0): Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu + Aktualisiert (5+1): Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+1): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+1): SQL Server Data Tools-Dokumente (SSDT))](../ssdt/new-updated-ssdt.md)
- [Neu + Aktualisiert (1+0): Dokumente zu **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [New + Updated (0+1): **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): SQL Server Management Studio-Dokumente (SSMS))](../ssms/new-updated-ssms.md)
- [Neu + Aktualisiert (0+2): Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


