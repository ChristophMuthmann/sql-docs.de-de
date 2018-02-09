---
title: Aktualisiert - T-SQL-Dokumentation | Microsoft Docs
description: "Aktualisierter Inhalt in zuletzt geänderten Dokumentation für Transact-SQL-Codeausschnitte anzeigen"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: t-sql
ms.date: 02/03/2018
ms.openlocfilehash: c1f1ce751bd4bca781644e7e2f5282320c8c88a8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>Neue und zuletzt aktualisiert: Transact-SQL-Dokumente



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-12-03** &nbsp; - zu - &nbsp; **2018-02-03**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **T-SQL-**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


***Dieses Mal sind keine neuen Artikel aufgeführt.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [CREATE STATISTICS (Transact-SQL)](#TitleNum_1)
2. [UPDATE STATISTICS (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-statistics-transact-sqlstatementscreate-statistics-transact-sqlmd"></a>1. &nbsp; [CREATE STATISTICS (Transact-SQL)](statements/create-statistics-transact-sql.md)

*Aktualisiert: 2018-01-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 200.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 384e68493597bcc36876a3c7bada2630106256e2 c22168ea59b6020e8ebe1ccac5fa6a6049e6db4d  (PR=4460  ,  Filename=create-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *Max_degree_of_parallelism*
**betrifft**: SQL Server (SQL Server 2017 CU3 ab).

 Überschreibt die **Max. Grad an Parallelität** Konfigurationsoption für die Dauer des Vorgangs Statistik. Weitere Informationen finden Sie unter [Configure the max degree of parallelism Server Configuration Option](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.

 *Max_degree_of_parallelism* sind möglich:

 1 unterdrückt parallelen Pläne generiert.

 \>1 beschränkt die maximale Anzahl der Prozessoren, die in einer parallelen Statistik Operation auf die angegebene Anzahl verwendet oder weniger basierend auf der aktuellen systemarbeitsauslastung.

 0 (Standard) verwendet, die tatsächliche Anzahl von Prozessoren oder weniger basierend auf der aktuellen systemarbeitsauslastung.

 \<Update_stats_stream_option > nur zu Informationszwecken identifiziert. Nicht unterstützt. Zukünftige Kompatibilität wird nicht sichergestellt.




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-update-statistics-transact-sqlstatementsupdate-statistics-transact-sqlmd"></a>2. &nbsp; [UPDATE STATISTICS (Transact-SQL)](statements/update-statistics-transact-sql.md)

*Aktualisiert: 2018-01-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1))

<!-- Source markdown line 167.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5721e21a9f43fa784fe9357c47cb2a814385e63d 24ae47c553635f389a182e5e643bf9bd6bf59e78  (PR=4460  ,  Filename=update-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*

**Gilt für**: SQLServer (beginnend mit SQL Server 2017 CU3).

 Überschreibt die **Max. Grad an Parallelität** Konfigurationsoption für die Dauer des Vorgangs Statistik. Weitere Informationen finden Sie unter [Configure the max degree of parallelism Server Configuration Option](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Sie können mit MAXDOP die Anzahl der Prozessoren begrenzen, die bei der Ausführung paralleler Pläne verwendet werden. Maximal sind 64 Prozessoren zulässig.

 *Max_degree_of_parallelism* sind möglich:

 1 unterdrückt parallelen Pläne generiert.

 \>1 beschränkt die maximale Anzahl der Prozessoren, die in einer parallelen Statistik Operation auf die angegebene Anzahl verwendet oder weniger basierend auf der aktuellen systemarbeitsauslastung.

 0 (Standard) verwendet, die tatsächliche Anzahl von Prozessoren oder weniger basierend auf der aktuellen systemarbeitsauslastung.








## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel Informationen zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Bereiche für die Themenbereichsdatenbank, *führen* wurden neue oder vor kurzem aktualisiert Artikel


- [Neue und aktualisierte (1 + 3):&nbsp; **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **Analyseplattformsystem für SQL** Docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (12 + 1): **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (6 + 2):&nbsp; **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (15 + 0): **PowerShell für SQL** Docs](../powershell/new-updated-powershell.md)
- [Neue und aktualisierte (2 + 9):&nbsp; **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (1 + 0):&nbsp; **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (1 + 1):&nbsp; **SQL Operations Studio** Docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neue und aktualisierte (1 + 1):&nbsp; **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (0 + 2):&nbsp; **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Bereiche, die für die Themenbereichsdatenbank *nicht* haben eine neue oder vor kurzem aktualisiert Artikel


- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [Neue und aktualisierte (0 + 0): **ActiveX Data Objects (ADO) für SQL** Docs](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (0 + 0): **Samples for SQL** Docs](../sample/new-updated-sample.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)


