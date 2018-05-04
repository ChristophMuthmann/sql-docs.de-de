---
title: Aktualisiert - SQL-Vorgänge Studio Docs | Microsoft Docs
description: Aktualisierter Inhalt in zuletzt geänderten Dokumentation für SQL-Vorgänge Studio Codeausschnitte anzeigen
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssops
ms.date: 04/28/2018
ms.openlocfilehash: 074ed6176480655d9d87a55eb87cbb76b3011b7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-operations-studio-docs"></a>Neue und zuletzt aktualisiert: SQL-Vorgänge Studio Docs



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2018-02-03** &nbsp; - zu - &nbsp; **2018-04-28**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **SQL Operations Studio**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


- [Erweitern der Funktionalität von SQL-Vorgänge Studio (Vorschau)](extensions.md)

<!-- GeneMi:  I MANUALLY replace the ugly !INCLUDE with the name from inside the includes file. -->


&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Herunterladen und Installieren von SQL-Vorgänge Studio (Vorschau)](#TitleNum_1)
2. [Versionshinweise für SQL-Vorgänge Studio (Vorschau)](#TitleNum_2)
3. [Lernprogramm: Hinzufügen der *fünf langsamsten Abfragen* Beispiel Widget auf die Datenbank-Dashboard](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-and-install-sql-operations-studio-previewdownloadmd"></a>1. &nbsp; [Herunterladen und Installieren von SQL-Vorgänge Studio (Vorschau)](download.md)

*Aktualisiert: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6b4f80ad54c599e4354303a736f62e9715f99a32 18b22f464bbd8676348248ba5717b71acbab1c0d  (PR=5676  ,  Filename=download.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



   **Debian-Installation:**
```
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
```

   **RPM-Installation:**
```
   cd ~
   yum install ./Downloads/sqlops-linux-<version string>.rpm

   sqlops
```

   **weswegen Installation:**



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-operations-studio-preview-release-notesrelease-notesmd"></a>2. &nbsp; [Versionshinweise für SQL-Vorgänge Studio (Vorschau)](release-notes.md)

*Aktualisiert: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e2901d8a197f375f7d10ec93cbc9320362bf9278 0dde1aceceb339cb4cacd744e469f3d85d589668  (PR=5676  ,  Filename=release-notes.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[April Public Preview herunterladen]**


**April 2018 (April öffentliche Vorschau)**


Veröffentlichungsdatum: 25 April 2018-Version: 0.28.6

Die *April Public Preview* enthält Fehlerbehebungen und Verbesserungen.

- Verbesserungen an der Erweiterung SQL Agent-Vorschau.
- Verbesserte dateiunterstützung für große und geschützte zum Speichern von Admin geschützt und > 256 MB-Dateien in Studio für SQL-Vorgänge.
- Integrierte Terminaldienste aufteilen, um gleichzeitig mit mehreren open Terminals arbeiten.
- Reduzierte Installation Datei auf dem Datenträger Anzahl Foot für schnellere Installationen und Startzeiten drucken.
- Den Vorgang fortzusetzen Sie, GitHub-Probleme zu beheben:
   - Beheben Sie [ausstellen 37](https://github.com/Microsoft/sqlopsstudio/issues/37): unerwartetes Verhalten tritt auf, wenn Benutzer einen Fehler auslöst,.
   - Beheben Sie [ausstellen 462](https://github.com/Microsoft/sqlopsstudio/issues/462): anfordern Funktion: Option für Servergruppen standardmäßig erweitert wird.
   - Beheben Sie [ausstellen 606](https://github.com/Microsoft/sqlopsstudio/issues/606): Intellisense - ungültige Vorschlag für den Befehl 'update'.
   - Beheben Sie [ausstellen 967](https://github.com/Microsoft/sqlopsstudio/issues/967): erwarten Abfrageplan Wenn XML-Showplan im Ergebnisraster auswählen.
   - Beheben Sie [ausstellen 1023](https://github.com/Microsoft/sqlopsstudio/issues/1023): eckige Klammern für Ms_foreachdb Aufruf aus Flyfishingdba hinzufügen.
   - Beheben Sie [ausstellen 1048](https://github.com/Microsoft/sqlopsstudio/issues/1048): vor der Anmeldung SSL/TLS-Handshake-Fehler.
   - Beheben Sie [1050 ausstellen](https://github.com/Microsoft/sqlopsstudio/issues/1050): Clear Einblicke anzuzeigen, vor dem Fehler anzeigen.
   - Beheben Sie [ausstellen 1057](https://github.com/Microsoft/sqlopsstudio/issues/1057): Wiederherstellen und neue Abfrageaktionen im Explorer-Widget werden unterbrochen.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboardtutorial-qds-sql-servermd"></a>3. &nbsp; [Lernprogramm: Hinzufügen der *fünf langsamsten Abfragen* Beispiel Widget auf die Datenbank-Dashboard](tutorial-qds-sql-server.md)

*Aktualisiert: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2))

<!-- Source markdown line 94.  ms.author= "erickang".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bc128acd966898cafc04381d7d83187d28466052 a47bf93ea4165618e0e514d7900ce1461f691aae  (PR=5676  ,  Filename=tutorial-qds-sql-server.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die *über* neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (11 + 6): &nbsp; &nbsp; **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (18 + 0): &nbsp; &nbsp; **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (218 + 14): **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (14 + 0): &nbsp; &nbsp; **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (3 + 2): &nbsp; &nbsp; **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (3 + 3): &nbsp; &nbsp; **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (7 + 10): &nbsp; &nbsp; **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (0 + 2): &nbsp; &nbsp; **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (1 + 3): &nbsp; &nbsp; **SQL Operations Studio** Docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neue und aktualisierte (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (0 + 2): &nbsp; &nbsp; **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)
- [Neue und aktualisierte (1 + 1): &nbsp; &nbsp; **-Tools für SQL** Docs](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Themenbereiche, die *nicht* über neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (0 + 0): **Analyseplattformsystem für SQL** Docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (0 + 0): **PowerShell für SQL** Docs](../powershell/new-updated-powershell.md)
- [Neue und aktualisierte (0 + 0): **Samples for SQL** Docs](../samples/new-updated-samples.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)

