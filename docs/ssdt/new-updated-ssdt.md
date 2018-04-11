---
title: 'Aktualisiert: Dokumentation zu SSDT für SQL Server | Microsoft-Dokumentation'
description: Anzeigen von Codeausschnitten für aktualisierten Inhalt für kürzliche Änderungen in der Dokumentation zu SQL Server Data Tools (SSDT) für Microsoft SQL Server
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 02/03/2018
ms.openlocfilehash: ad139f5ff9389c1a04a7f077d61facc7643db323
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Neu und zuletzt kürzlich aktualisiert: SQL Server Data Tools (SSDT)



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **3.12.2017** &nbsp; bis &nbsp; **3.2.2018**
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

*Aktualisiert: 18.1.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6416949beaee91da2f77dfebb9eb5ed363db4cb7 de18314845cffa197b3fd2ed868f2c330760bedb  (PR=4652  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**SSDT für Visual Studio 2017 (15.5.1)**

Buildnummer: 14.0.16148.0

**Neuigkeiten**


Bei Version 15.5.1 von Visual Studio 2017 handelt es sich, abgesehen von folgenden Fehlerkorrekturen beim Installer, um das gleiche Release wie Version 15.5.0:

1.  Korrigiert: Der Installer reagiert nach der Installation von SQL Server Integration Services nicht mehr.
2.  Korrigiert: Das Setup schlägt mit der folgenden Fehlermeldung fehl: „The requested metafile operation is not support (0x800707D3)“ (Der angeforderte Metadateivorgang wird nicht unterstützt (0x800707D3)).

Neben diesen beiden Fehlerbehebungen gelten folgende Angaben zu 15.5.0 auch weiterhin für 15.5.1:

**SSDT für Visual Studio 2017 (15.5.0)**

Buildnummer: 14.0.16146.0

**Neuigkeiten**


SSDT für Visual Studio 2017 (15.5.0) befindet sich nicht mehr in der Vorschauphase sondern ist nun allgemein verfügbar.

**Installationsprogramm**
1. Die Benutzeroberfläche des Setups wurde lokalisiert.
1. Die Qualität des Symbols wurde verbessert.

**Integration Services (IS)**
1. Im Bereitstellungsassistenten wurde ein Schritt zur Paketvalidierung hinzugefügt, wenn eine Bereitstellung an Azure SSIS IR in ADF durchgeführt wird, wobei mögliche Kompatibilitätsprobleme in SSIS-Paketen bei der Ausführung in Azure SSIS IR erkannt werden. Weitere Informationen finden Sie unter [Überprüfen von in Azure bereitgestellten SSIS-Paketen](..\integration-services\lift-shift\ssis-azure-validate-packages.md).
1. Die SSIS-Erweiterung wurde lokalisiert.

**Behebung von Programmfehlern**


**Integration Services (IS)**
1. Korrigiert: Das Layout des Verbindungs-Managers von OLE DB und ADO.NET ist beschädigt.
2. Korrigiert: Beim Bearbeiten einer Aufgabe zum Verarbeiten von Dimensionen wird der Fehler „Assembly nicht gefunden“ ausgegeben.

**Bekannte Probleme**


Die SSIS-Aufgabe „Paket ausführen“ (**Integration Services (IS)**) unterstützt kein Debuggen, wenn ExecuteOutOfProcess auf TRUE festgelegt ist. Dieses Problem gilt nur für das Debuggen. Das Speichern, Bereitstellen und Ausführen über „DTExec.exe“ oder den SSIS-Katalog wird nicht beeinträchtigt.



**SSDT 17.4 für Visual Studio 2015**

Buildnummer: 14.0.61712.050

**Neuigkeiten**


**Analysis Services-Projekte**
- Es wurden drei neue Optionen zu tabellarischen Projekten hinzugefügt (unter „Optionen“ > „Analysis Services tabellarisch“ > „Datenimport“):







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die *über* neue oder kürzlich aktualisierte Artikel verfügen


- [Neu und aktualisiert (1+3):&nbsp;Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Analytics Platform System für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zur **Datenbank-Engine für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu und aktualisiert (12+1): Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu und aktualisiert (6+2):&nbsp;Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu und aktualisiert (15+0): Dokumente zu **PowerShell für SQL**](../powershell/new-updated-powershell.md)
- [Neu und aktualisiert (2+9):&nbsp;Dokumente zu **relationalen Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu und aktualisiert (1+0):&nbsp;Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zu **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Neu und aktualisiert (1+2):&nbsp;Dokumente zu **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Neu und aktualisiert (0+2):&nbsp;Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Themenbereiche, die *nicht* über neue oder kürzlich aktualisierte Artikel verfügen


- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../samples/new-updated-samples.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


