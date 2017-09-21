---
title: Aktualisierte Dokumentation zu Datenbankmodulen | Microsoft-Dokumentation
description: "Anzeigen von Codeausschnitten aktualisierter Inhalte in der zuletzt geänderten Dokumentation für Datenbankmodule."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: barbkess
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: database-engine
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: ce80496cdf82c2bc2df2447ed043216e6c78ad7e
ms.contentlocale: de-de
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-database-engine-docs"></a>Neue und kürzlich aktualisierte Dokumentation zu Datenbankmodulen



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates*: &nbsp; **18.07.2017** &nbsp; –bis– &nbsp; **11.09.2017**
- *Themenbereich:* &nbsp; **Datenbankmodul**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [SQL Server-Installation](install-windows/installation-for-sql-server.md)
2. [Unterstützte Versions- und Editionsupgrades in SQL Server 2017](install-windows/supported-version-and-edition-upgrades-2017.md)
3. [SQL Server-Datenbankmodul](sql-server-database-engine-overview.md)
4. [Neues im Datenbankmodul – SQL Server 2016](whats-new-in-sql-server-2016.md)
5. [Neues im Datenbankmodul – SQL Server 2017](whats-new-in-sql-server-2017.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Automatisches Seeding für sekundäre Replikate](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-automatic-seeding-for-secondary-replicasavailability-groupswindowsautomatic-seeding-secondary-replicasmd"></a>1. &nbsp; [Automatisches Seeding für sekundäre Replikate](availability-groups/windows/automatic-seeding-secondary-replicas.md)

*Updated: 21.08.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 55.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0b7b6a23f38bfe5959ccd170527a9bbdb308dc4b dc51fdf69649ed6cae03584cff7bc900d5b72149  (PR=2896  ,  Filename=automatic-seeding-secondary-replicas.md  ,  Dirpath=docs\database-engine\availability-groups\windows\  ,  MergeCommitSha40=80642503480add90fc75573338760ab86139694c) -->



Bis SQL Server 2016 muss der Ordner, in dem die Datenbank durch das automatische Seeding erstellt wird, bereits vorhanden und mit dem Pfad auf dem primären Replikat identisch sein.

In SQL Server 2017 empfiehlt Microsoft, denselben Pfad für Daten und Protokolldateien für alle Replikate zu verwenden, die in einer Verfügbarkeitsgruppe enthalten sind. Sie können jedoch bei Bedarf unterschiedliche Pfade verwenden. In einer plattformübergreifenden Verfügbarkeitsgruppe kann sich beispielsweise eine Instanz von SQL Server unter Windows und eine weitere Instanz von SQL Server unter Linux befinden. Die unterschiedlichen Plattformen verfügen über unterschiedliche Standardpfade. SQL Server 2017 unterstützt Verfügbarkeitsgruppenreplikate auf Instanzen von SQL Server mit unterschiedlichen Standardpfaden.

Die folgende Tabelle enthält Beispiele für die unterstützten Datenträgerlayouts, die automatisches Seeding unterstützen können:

|Primäre Instanz</br>Standarddatenpfad|Sekundäre Instanz</br>Standarddatenpfad|Primäre Instanz</br>Quelldateispeicherort|Sekundäre Instanz</br> Zieldateispeicherort
|:------|:------|:------|:------
|C:\\Daten\\ |/var/opt/mssql/data/ |C:\\Daten\\ |/var/opt/mssql/data/|
|C:\\Daten\\ |/var/opt/mssql/data/ |C:\\Daten\\group1\\ |/var/opt/mssql/data/group1/|
|C:\\Daten\\ |D:\\Daten\\ |C:\\Daten\\ |D:\\Daten\\
|C:\\Daten\\ |D:\\Daten\\ |C:\\Daten\\group1\\ |D:\\Daten\\group1\

Szenarios, bei denen der Speicherort der Datenbank der primären und sekundären Replikate nicht dem Standardpfad der Instanz entspricht, sind von dieser Änderung nicht betroffen. Die Anforderung, dass die Dateipfade von sekundären Replikaten mit denen der primären Replikate übereinstimmen müssen, besteht weiterhin.

|Primäre Instanz</br>Standarddatenpfad|Sekundäre Instanz</br>Standarddatenpfad|Primäre Instanz</br>Dateispeicherort|Sekundäre Instanz</br> Dateispeicherort
|:------|:------|:------|:------
|C:\\Daten\\ |C:\\Daten\\ |D:\\group1\\ |D:\\group1\\
|C:\\Daten\\ |C:\\Daten\\ |D:\\Daten\\ |D:\\Daten\\
|C:\\Daten\\ |C:\\Daten\\ |D:\\Daten\\group1\\ |D:\\Daten\\group1\\

Beim Kombinieren von Standard- und Nicht-Standardpfaden auf den primären und sekundären Replikaten verhält sich SQL Server 2017 anders als die vorherigen Versionen. In der folgenden Tabelle wird das Verhaltensmuster von SQL Server 2017 veranschaulicht.







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [New + Updated (3+12): **Advanced Analytics for SQL** docs (Neu + Aktualisiert (3+12): Dokumentation zu Advanced Analytics für SQL)](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (5+0): **Connect to SQL** docs (Neu + Aktualisiert (1+2): Dokumentation zur Herstellung einer Verbindung mit SQL)](../connect/new-updated-connect.md)
- [New + Updated (5+1): **Database Engine for SQL** docs (Neu + Aktualisiert (6+0): Dokumentation zum Datenbankmodul für SQL)](../database-engine/new-updated-database-engine.md)
- [New + Updated (19+82): **Integration Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu SSIS für SQL)](../integration-services/new-updated-integration-services.md)
- [New + Updated (1+8): **Linux for SQL** docs (Neu + Aktualisiert (13+2): Dokumentation zu Linux für SQL)](../linux/new-updated-linux.md)
- [New + Updated (12+1): **Relational Databases for SQL** docs (Neu + Aktualisiert (8+4): Dokumentation zu relationalen Datenbanken für SQL)](../relational-databases/new-updated-relational-databases.md)
- [New + Updated (0+1): **Reporting Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Reporting Services für SQL)](../reporting-services/new-updated-reporting-services.md)
- [New + Updated (7+1): **Microsoft SQL Server** docs (Neu + Aktualisiert (2+2): Dokumentation zu Microsoft SQL Server)](../sql-server/new-updated-sql-server.md)
- [New + Updated (1+1): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+0): Dokumentation zu SQL Server Data Tools (SSDT))](../ssdt/new-updated-ssdt.md)
- [New + Updated (0+2): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [New + Updated (1+4): **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): Dokumentation zu SQL Server Management Studio (SSMS))](../ssms/new-updated-ssms.md)
- [New + Updated (4+1): **Transact-SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zu Transact-SQL)](../t-sql/new-updated-t-sql.md)
- [New + Updated (0+1): **Tools for SQL** docs (Neu + Aktualisiert (0+1): Dokumentation zu Tools für SQL)](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)



