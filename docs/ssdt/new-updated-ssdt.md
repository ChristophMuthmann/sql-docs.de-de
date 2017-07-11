---
title: "Aktualisiert: SSDT für SQL Server-Dokumentation | Microsoft-Dokumentation"
description: "Anzeigen von Codeausschnitten für aktualisierten Inhalt für kürzliche Änderungen in der Dokumentation für SQL Server Data Tools (SSDT) für Microsoft SQL Server"
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
ms.date: 06/30/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 5e43cb76dac922b3c43318b2a9f539ab19ec7bfe
ms.contentlocale: de-de
ms.lasthandoff: 07/03/2017

---
<a id="new-and-recently-updated-sql-server-data-tools-ssdt" class="xliff"></a>

# Neu und zuletzt kürzlich aktualisiert: SQL Server Data Tools (SSDT)



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **17.5.2017** &nbsp; bis &nbsp; **30.6.2017**
- *Themenbereich:* &nbsp; **SQL Server Data Tools (SSDT)**.




&nbsp;

<a id="new-articles-created-recently" class="xliff"></a>

## Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


*Dieses Mal sind keine neuen Artikel aufgeführt.*



&nbsp;

<a id="updated-articles-with-excerpts" class="xliff"></a>

## Aktualisierte Artikel mit Auszüge

Dieser Abschnitt zeigt die Auszüge von Updates, die vom Artikel, die vor kurzem eine große Aktualisierung aufgetreten sind.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

<a id="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd" class="xliff"></a>

### 1. &nbsp; [Änderungsprotokoll für SQL Server Data Tools (SSDT)](changelog-for-sql-server-data-tools-ssdt.md)

*Aktualisiert: 19.5.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 21.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cf17883ce0daf75fdf88881171bf4042558b1cf4 536fe0fe41b023a4186f494a509fa14fcbafccf4  (PR=1777  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=5bd0e1d3955d898824d285d28979089e2de6f322) -->



Ausführliche Beiträge zu den Neuigkeiten und Änderungen finden Sie auf dem [SSDT-Team-Blog](https://blogs.msdn.microsoft.com/ssdt/)

**SSDT 17.1**

Buildnummer: 14.0.61705.170

**Neuigkeiten**

**AS-Projekte:**
- Benutzer können Hinweise auf Spalten in der Benutzeroberfläche auf 1400 Modelle Codierung festlegen.
- Nicht-Modell-bezogenen IntelliSense steht jetzt im Offlinemodus
- Tabellarische Modell-Explorer enthält jetzt einen Knoten zum Darstellen von benannten M Ausdrücke verfügbar über das Modell (1400 Kompatibilitätsgrad Tabellenmodelle)
- Azure Active Directory Personenauswahl ähnlich wie Microsoft Azure-Portal IAM jetzt verfügbar, wenn Sie Mitglieder einer Benutzerrolle in tabellarischen Modellen einrichten

**Datenbankprojekte:**
- Dacfx 17.1 aktualisiert

**Behebung von Programmfehlern**

- Das Problem behoben wurde der Name der Business Intelligence-Designer nicht ordnungsgemäß in Visual Studio-Optionen in VS2017 Anzeige
- Es wurde ein Problem, in denen ein Absturz (Crash) kann auftreten, generieren eine Code Map für eine Projektmappe mit einem Berichtsprojekt oder als Projekt
- Eine Reihe von Problemen mit PowerQuery-Integration für tabellarische Modelle von Analysis Services 1400/Compat-Ebene wurde behoben.
- Es wurde ein Problem in der neuen DAX-Editor Toolfenster, in dem der Zuweisungsoperator nicht in einer separaten Zeile bei sein könnte ein Measure definieren
- Es wurde ein Problem, das verhindert, dass die tabellarischen Measure Anzeige beim Umbenennen des Measures in der Perspektive aktualisieren
- Aktualisierte Analysis Services-Arbeitsbereich "integrierte"-Modul und tabellarischen Objektmodell, das eine Regression, die Projekten für tabellarische Modelle mit Übersetzungen behebt auf ein Fehler auf 1200 verursacht bereitstellen auf SQL Server 2016 Analysis Services-server
- Feste ein leistungsbezogenes Problem vorliegt, die Creation\deletion neue 1400 tabellarische Datenquellen sehr langsam vorgenommen.
- Es wurde ein Problem im Datenquellensicht-Diagramm in mehrdimensionalen Modellen konnte, auf dem Rendering beendet, wenn die Ansicht schnell zwischen verschiedenen DSVs ändern

**DacFx 17.1**

- Es wurde ein Problem beim Verschlüsseln einer Spalteninhalts mit speicheroptimierten Tabellen mit anderen Identity-Spalten
- SQLDOM-Unterstützung für CATALOG_COLLATION-Option für CREATE DATABASE





&nbsp;

<a name="compactupdatedlist"/>

<a id="compact-list-of-articles-updated-recently" class="xliff"></a>

## Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese compact Liste enthält Links zu den aktualisierten Artikeln, die im vorherigen Abschnitt aufgeführt sind.

1. [Änderungsprotokoll für SQL Server Data Tools (SSDT)](#TitleNum_1)




<a name="sisters2"/>

&nbsp;

<a id="sister-articles" class="xliff"></a>

## Schwester Artikel

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen, innerhalb des gleichen GitHub-Repository: [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170630-1150  -->

<a id="subject-areas-which-do-have-new-or-recently-updated-articles" class="xliff"></a>

#### Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen.

- [New + Updated (12+2): **Advanced Analytics for SQL** docs (Neu + Aktualisiert (12+2): Erweiterte Analysen für SQL-Dokumente)](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (1+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (1+0): Analysis Services für SQL-Dokumente)](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+2): **Connect to SQL** docs (Neu + Aktualisiert (0+2): Herstellung einer Verbindung mit SQL-Dokumenten)](../connect/new-updated-connect.md)
- [New + Updated (3+0): **Database Engine for SQL** docs (Neu + Aktualisiert (3+0): Datenbankmodul für SQL-Dokumente)](../database-engine/new-updated-database-engine.md)
- [New + Updated (1+2): **Integration Services for SQL** docs (Neu + Aktualisiert (1+2): Integration Services für SQL-Dokumente)](../integration-services/new-updated-integration-services.md)
- [New + Updated (2+8): **Linux for SQL** docs (Neu + Aktualisiert (2+8): Linux für SQL-Dokumente)](../linux/new-updated-linux.md)
- [New + Updated (1+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (1+0): Master Data Services (MDS) für SQL-Dokumente)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (5+5): **Relational Databases for SQL** docs (Neu + Aktualisiert (5+5): Relationale Datenbanken für SQL-Dokumente)](../relational-databases/new-updated-relational-databases.md)
- [New + Updated (2+0): **Reporting Services for SQL** docs (Neu + Aktualisiert (2+0): Reporting Services für SQL-Dokumente)](../reporting-services/new-updated-reporting-services.md)
- [New + Updated (0+4): **Microsoft SQL Server** docs (Neu + Aktualisiert (0+4): Microsoft SQL Server-Dokumente)](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+1): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+1): SQL Server Data Tools-Dokumente (SSDT))](../ssdt/new-updated-ssdt.md)
- [New + Updated (0+1): **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): SQL Server Management Studio-Dokumente (SSMS))](../ssms/new-updated-ssms.md)
- [New + Updated (1+0): **Tools for SQL** docs (Neu + Aktualisiert (1+0): Tools für SQL-Dokumente)](../tools/new-updated-tools.md)


<a id="subject-areas-which-have-no-new-or-recently-updated-articles" class="xliff"></a>

#### Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [New + Updated (0+0): **Transact-SQL** docs (Neu + Aktualisiert (0+0): Transact-SQL-Dokumente)](../t-sql/new-updated-t-sql.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


&nbsp;


