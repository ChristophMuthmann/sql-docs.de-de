---
title: "Aktualisiert: Dokumentation zu SSDT für SQL Server | Microsoft-Dokumentation"
description: "Anzeigen von Codeausschnitten für aktualisierten Inhalt für kürzliche Änderungen in der Dokumentation zu SQL Server Data Tools (SSDT) für Microsoft SQL Server"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 8ae9a49443525524cf7f6ffceba4fb44984c7052
ms.contentlocale: de-de
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Neu und zuletzt kürzlich aktualisiert: SQL Server Data Tools (SSDT)



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich der Updates*: &nbsp; **18.7.2017** &nbsp; bis &nbsp; **11.9.2017**
- *Themenbereich:* &nbsp; **SQL Server Data Tools (SSDT)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu neuen Artikeln weiter, die kürzlich erstellt wurden.


1. [SQL Server Data Tools – Lizenzbedingungen](sql-server-data-tools-license-terms-vs2017.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu allen aktualisierten Artikeln, die im Abschnitt mit Auszügen aufgeführt sind.

1. [Änderungsprotokoll für SQL Server Data Tools (SSDT)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [Änderungsprotokoll für SQL Server Data Tools (SSDT)](changelog-for-sql-server-data-tools-ssdt.md)

*Aktualisiert: 23.08.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 23.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 536fe0fe41b023a4186f494a509fa14fcbafccf4 e5bc7b76c1755f5a1af77f6cd63d8e8691dafe7b  (PR=2927  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=71a2cbf181c94c4c1aff877614aadf890b2496e0) -->



**SSDT für Visual Studio 2017 (15.3.0, Vorschauversion)**

Buildnummer: 14.0.16121.0

**Neuigkeiten**


Diese Vorschauversion ist die erste Version von SSDT für Visual Studio 2017. Mit diesem Release wird für Projekte von SQL Server-Datenbank, Analysis Services, Reporting Services und Integration Services in Visual Studio 2017 15.3 oder höher eine eigenständige Benutzererfahrung für die Webinstallation eingeführt.


**Bekannte Probleme**

- Das Installationsprogramm ist nicht lokalisiert.
- SSIS ist nicht lokalisiert.
- Die SSIS-Aufgabe „Paket ausführen“ unterstützt kein Debuggen, wenn der Prozess *ExecuteOutofProcess* auf *TRUE* festgelegt ist. Dieses Problem gilt nur für das Debuggen. Das Speichern, Bereitstellen und Ausführen über „DTExec.exe“ oder den SSIS-Katalog wird nicht beeinträchtigt.
- Eine vollständige Liste aller Änderungen finden Sie unter [Änderungsprotokoll--changelog-for-sql-server-data-tools-ssdt.md).
- Melden Sie Fehler auf der Website [SSDT Connect Feedback](https://connect.microsoft.com/SQLServer/Feedback).
- SSIS-Pakete mit Drittanbietererweiterungen können nicht so geändert werden, dass sie sich an andere Serverversionen richten.


**SSDT 17.2 für Visual Studio 2015**

Buildnummer: 14.0.61707.300

**Neuigkeiten**



**AS-Projekte:**
- Die Sicherheit auf Objektebene kann nun im Dialogfeld *Rollen* konfiguriert werden, um erweiterte Sicherheit in tabellarischen Modellen mit Kompatibilitätsgrad 1400 zu gewährleisten.
- Neue AAD-Rollenmemberauswahl für Benutzer ohne E-Mail-Adressen in AS Azure-Modellen in SSDT AS-Projekten für VS2017.
- Neue Projekteigenschaft „Immer auffordern“ für tabellarische SSDT AS-Projekte in AS Azure, um das Verhalten der Zwischenspeicherung von Anmeldeinformationen in der ADAL anzupassen.


**Behebung von Programmfehlern**


**Allgemein**
- Aktualisierte Branding-Verweise für SQL Server 2017.

**AS-Projekte**
- Die Leistung wurde bedeutend verbessert, um die Benutzerfreundlichkeit bei der Weitergabe von Änderungen an DAX-Measures und anderen Modellbearbeitungen zu erhöhen.
- Es wurde eine Reihe von Problemen mit der Integration von Power Query in Analysis Services-Projekte, die tabellarische Modelle mit Kompatibilitätsgrad 1400 verwenden, behoben.
- Es wurde ein Problem mit mehrdimensionalen Projekten in VS2017 behoben, bei dem der Aggregation-Designer möglicherweise nicht lädt.







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für kürzlich aktualisierte Artikel in anderen Themenbereichen innerhalb unseres öffentlichen GitHub.com-Repositorys: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neu und aktualisiert (3+12): **Advanced Analytics für SQL** – Dokumentation](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neu und aktualisiert (5+0): **Herstellen einer Verbindung mit SQL** – Dokumentation](../connect/new-updated-connect.md)
- [Neu und aktualisiert (5+1): **Datenbankmodul für SQL** – Dokumentation](../database-engine/new-updated-database-engine.md)
- [Neu und aktualisiert (19+82): **Integration Services für SQL** – Dokumentation](../integration-services/new-updated-integration-services.md)
- [Neu und aktualisiert (1+8): **Linux für SQL** – Dokumentation](../linux/new-updated-linux.md)
- [Neu und aktualisiert (12+1): **Relationale Datenbanken für SQL** – Dokumentation](../relational-databases/new-updated-relational-databases.md)
- [Neu und aktualisiert (0+1): **Reporting Services für SQL** – Dokumentation](../reporting-services/new-updated-reporting-services.md)
- [Neu und aktualisiert (7+1): **Microsoft SQL Server** – Dokumentation](../sql-server/new-updated-sql-server.md)
- [Neu und aktualisiert (1+1): **SQL Server Data Tools (SSDT)** – Dokumentation](../ssdt/new-updated-ssdt.md)
- [Neu und aktualisiert (0+2): **SQL Server Migration Assistant (SSMA)** – Dokumentation](../ssma/new-updated-ssma.md)
- [Neu und aktualisiert (1+4): **SQL Server Management Studio (SSMS)** – Dokumentation](../ssms/new-updated-ssms.md)
- [Neu und aktualisiert (4+1): **Transact-SQL** – Dokumentation](../t-sql/new-updated-t-sql.md)
- [Neu und aktualisiert (0+1): **Tools für SQL** – Dokumentation](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [Neu und aktualisiert (0+0): **Analysis Services für SQL** – Dokumentation](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [Neu und aktualisiert (0+0): **Master Data Services (MDS) für SQL** – Dokumentation](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)



