---
title: Aktualisierte Dokumentation zu Datenbankmodulen | Microsoft-Dokumentation
description: "Anzeigen von Codeausschnitten aktualisierter Inhalte in der zuletzt geänderten Dokumentation für Datenbankmodule."
services: na
documentationcenter: 
author: MightyPen
manager: craigg
editor: barbkess
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: database-engine
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: cbf472ba2b8d2d7abad095992895b56940a82d92
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="new-and-recently-updated-database-engine-docs"></a>Neue und kürzlich aktualisierte Dokumentation zu Datenbankmodulen



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates*: &nbsp; **28.09.2017** &nbsp; – bis – &nbsp; **02.12.2017**
- *Themenbereich:* &nbsp; **Datenbankmodul**.




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

1. [Für Ad-hoc-Arbeitsauslastungen optimieren (Serverkonfigurationsoption)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-optimize-for-ad-hoc-workloads-server-configuration-optionconfigure-windowsoptimize-for-ad-hoc-workloads-server-configuration-optionmd"></a>1. &nbsp; [Für Ad-hoc-Arbeitsauslastungen optimieren (Serverkonfigurationsoption)](configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)

*Aktualisiert: 20.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 38.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6ca71358f13780b930e6fd10e431d4df2bb96441 221306c4554ebd383ab68ed67cdaeca390f57106  (PR=4032  ,  Filename=optimize-for-ad-hoc-workloads-server-configuration-option.md  ,  Dirpath=docs\database-engine\configure-windows\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



**Empfehlungen**

Wenn die Anzahl von einmal genutzten Plänen einen beträchtlichen Teil des Speichers für „..!NCLUDE-NotShown--ssDEnoversion--../../includes/ssdenoversion-md.md)]“ in einem OLTP-Server beansprucht, und wenn diese Pläne Ad-hoc-Pläne sind, verwenden Sie diese Serveroption, um die Speichernutzung mit diesen Objekten zu verringern.
Um die Anzahl von zwischengespeicherten einmal genutzten Plänen zu ermitteln, führen Sie die folgende Abfrage aus:

```
SELECT objtype, cacheobjtype,
  AVG(usecounts) AS Avg_UseCount,
  SUM(refcounts) AS AllRefObjects,
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> Wenn **Optimieren für Ad-hoc-Arbeitsauslastungen** auf 1 festgelegt wird, wirkt sich dies ausschließlich auf neue Pläne aus. Pläne, die sich bereits im Plancache befinden, sind davon nicht betroffen.
> Sollen auch bereits zwischengespeicherte Abfragepläne sofort betroffen sein, muss der Plancache mit [ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE--../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) gelöscht werden, oder ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] muss neu gestartet werden.







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


