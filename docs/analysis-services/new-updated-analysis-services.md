---
title: "Aktualisiert - Analysis Services für SQL Server-Dokumentation | Microsoft Docs"
description: "Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für Analysis Services für Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: analysis-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: a21f82dd5a0bd4ef59abc639d9441be25191a21b
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-analysis-services-for-sql-server"></a>Neue und kürzlich aktualisierte: Analysis Services für SQLServer



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-09-11** &nbsp; - zu - &nbsp; **2017-09-27**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Analysis Services für SQL Server**.




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

1. [Was &#39; s neu in SQL Server 2017 Analysis Services](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-what39s-new-in-sql-server-2017-analysis-serviceswhat-s-new-in-sql-server-analysis-services-2017md"></a>1. &nbsp;[Was &#39; s neu in SQL Server 2017 Analysis Services](what-s-new-in-sql-server-analysis-services-2017.md)

*Aktualisiert: 2017-09-22* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 143.  ms.author= "owend".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c8d75883f07e6e32859728d09139920eb9bf65c5 d206e83413d15a6e6116120e4a98dda9c8ce81d8  (PR=3278  ,  Filename=what-s-new-in-sql-server-analysis-services-2017.md  ,  Dirpath=docs\analysis-services\  ,  MergeCommitSha40=656e62f36446db4ef5b232129130a0253d2aebdf) -->



**Sicherheit auf Objektebene**

Ab dieser Version steht [Objektebene-Sicherheit –... / analysis-services/tabular-models/object-level-security.md) für Tabellen und Spalten. Zusätzlich zum Einschränken des Zugriffs auf Tabellen-und Spaltendaten, können sensible Tabellen- und Spaltennamen gesichert werden. Dadurch wird verhindert, dass ein böswilliger Benutzer entdeckt, dass eine solche Tabelle vorhanden ist.

Sicherheit auf Nachrichtenebene Objekt muss mit der JSON-basierte Metadaten, Tabular Model Scripting Language (TMSL) oder tabellarisches Objekt Model (TOM) festgelegt werden.

Der folgende Code schützt beispielsweise die Produkttabelle im Beispieltabellenmodell von Adventure Works, indem die **MetadataPermission** -Eigenschaft der **TablePermission** -Klasse auf **Keine**gesetzt wird.

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```

**Dynamische Verwaltungssichten (DMVs)**

[DMVs--... / analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md) sind Abfragen in SQL Server Profiler, Informationen zu lokalen Servervorgängen und Serverzustand zurückgeben.
Diese Version bietet Verbesserungen an [dynamische Verwaltungssichten](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMVS) für tabellarische Modelle mit Kompatibilitätsgrad 1200 und 1400.







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (0 + 1): **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (0 + 1): **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (4 + 1): **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (17 + 0): **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (3 + 0): **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (1 + 1): **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (2 + 0): **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (0 + 1): **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (0 + 1): **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [Neue und aktualisierte (0 + 0): **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [Neue und aktualisierte (0 + 0): **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+0): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+0): Dokumentation zu SQL Server Data Tools (SSDT))](../ssdt/new-updated-ssdt.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (0 + 0): **-Tools für SQL** Docs](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)



