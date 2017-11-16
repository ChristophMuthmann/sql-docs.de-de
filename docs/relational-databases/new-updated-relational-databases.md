---
title: "Aktualisiert – Dokumentation zu relationalen Datenbanken | Microsoft-Dokumentation"
description: "Zeigen Sie Codeausschnitte von aktualisierten Inhalten in der zuletzt geänderten Dokumentation zu relationale Datenbanken an."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: relational-databases-misc
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 70cb071dc7b6f4ff15c5c7dee3f24bb352d6eb61
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Neu und zuletzt aktualisiert: Dokumentation zu relationalen Datenbanken
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates*: &nbsp; **11.9.2017** &nbsp; bis &nbsp; **27.9.2017**
- *Themenbereich:* &nbsp; **Relationale Datenbanken**




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Importieren und Exportieren von Daten des SQL Servers und der Azure SQL-Datenbank](import-export/overview-import-export.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Übersicht über räumliche Datentypen](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-spatial-data-types-overviewspatialspatial-data-types-overviewmd"></a>1. &nbsp; [Übersicht über räumliche Datentypen](spatial/spatial-data-types-overview.md)

*Aktualisiert: 26.9.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 27.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96dd44cf49e96d1d543a629d49de297dba9c1753 2e9629f852ea42a213c7c24831bcfa53e40358f2  (PR=0  ,  Filename=spatial-data-types-overview.md  ,  Dirpath=docs\relational-databases\spatial\  ,  MergeCommitSha40=b33976cf92f23fbb13cee0c353fd40608d002d94) -->



 -  Es gibt zwei Typen von räumlichen Daten. Der **geometry** -Datentyp unterstützt planare bzw. euklidische Daten (flache Erdabbildung). Der **geometry** -Datentyp entspricht der Version 1.1.0. der Simple Features for SQL-Spezifikation des Open Geospatial Consortium (OGC) und ist auch mit SQL MM (ISO-Standard) kompatibel.
 -
 - Zudem unterstützt ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] den **geography**-Datentyp, der ellipsenförmige Daten (runde Erdabbildung) wie GPS-Breiten- und -Längenkoordinaten speichert.
 -
 -> [!IMPORTANT]
 ->  Laden Sie das folgende Whitepaper herunter, um eine ausführliche Beschreibung und Beispiele der in ..!NCLUDE-NotShown--ssSQL11--../../includes/sssql11-md.md)] eingeführten räumlichen Funktionen (u.a. Erweiterungen der räumlichen Datentypen) zu erhalten: [New Spatial Features in SQL Server Code-Named „Denali“ (Neue räumliche Funktionen in SQL Server Codename „Denali“)](http://go.microsoft.com/fwlink/?LinkId=226407).
 -
 -##  <a name="objects"></a> Räumliche Datenobjekte
 - Der **geometry** -Datentyp und der **geography** -Datentyp unterstützen 16 räumliche Datenobjekte bzw. Instanztypen. Nur elf dieser Instanztypen sind jedoch *instanziierbar*. Sie können diese Instanzen erstellen und Sie in einer Datenbanken bearbeiten (oder instanziieren). Diese Instanzen leiten bestimmte Eigenschaften von ihren übergeordneten Datentypen ab, die sie als **Points**, **LineStrings, CircularStrings**, **CompoundCurves**, **Polygons**, **CurvePolygons** oder als mehrere Instanzen von **geometry** oder **geography** in einer **GeometryCollection**auszeichnen. Der**Geography** -Typ verfügt über einen zusätzlichen Instanztyp **FullGlobe**.
 -
 - Die nachfolgende Abbildung stellt die **geometry** -Hierarchie dar, auf der der **geometry** -Datentyp und der **geography** -Datentyp basieren. Die instanziierbaren Typen von **geometry** und **geography** sind in Blau dargestellt.
 -
 - ![geom_hierarchy--../../relational-databases/spatial/media/geom-hierarchy.gif)
 -
 - Wie aus der Abbildung hervorgeht, handelt es sich bei den zehn instanziierbaren Typen der Datentypen **geometry** und **geography** **Point**, **MultiPoint**, **LineString**, **CircularString**, **MultiLineString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **MultiPolygon**und **GeometryCollection**. Es gibt einen zusätzlichen instanziierbaren Typen für den geography-Datentyp: **FullGlobe**. Die Typen **geometry** und **geography** können eine spezifische Instanz erkennen, wenn es sich um eine wohlgeformte Instanz handelt. Dies gilt auch, wenn die Instanz nicht explizit definiert ist. Wenn Sie beispielsweise eine **Point** -Instanz explizit mit der STPointFromText()-Methode definieren, erkennen **geometry** und **geography** die Instanz als **Point**, sofern die Methodeneingabe wohlgeformt ist. Wenn Sie die gleiche Instanz mit der `STGeomFromText()` -Methode definieren, erkennen sowohl der **geometry** - als auch der **geography** -Datentyp die Instanz als **Point**.







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [New + Updated (0+1): **Advanced Analytics for SQL** docs (Neu + Aktualisiert (0+1): Dokumentation zu Advanced Analytics für SQL)](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (0+1): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+1): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (4+1): **Database Engine for SQL** docs (Neu + Aktualisiert (4+1): Dokumentation zum Datenbankmodul für SQL)](../database-engine/new-updated-database-engine.md)
- [New + Updated (17+0):  **Integration Services for SQL** docs (Neu + Aktualisiert (17+0):Dokumentation zu Integration Services für SQL)](../integration-services/new-updated-integration-services.md)
- [New + Updated (3+0): **Linux for SQL** docs (Neu + Aktualisiert (3+0): Dokumentation zu Linux für SQL)](../linux/new-updated-linux.md)
- [New + Updated (1+1): **Relational Databases for SQL** docs (Neu + Aktualisiert (1+1): Dokumentation zu relationalen Datenbanken für SQL)](../relational-databases/new-updated-relational-databases.md)
- [New + Updated (2+0): **Reporting Services for SQL** docs (Neu + Aktualisiert (2+0): Dokumentation zu Reporting Services für SQL](../reporting-services/new-updated-reporting-services.md)
- [New + Updated (0+1): **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): Dokumentation zu SQL Server Management Studio (SSMS) Dokumentation](../ssms/new-updated-ssms.md)
- [New + Updated (0+1): **Transact-SQL** docs (Neu + Aktualisiert (0+1): Dokumentation zu Transact-SQL](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Connect to SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zum Herstellen einer Verbindung mit SQL](../connect/new-updated-connect.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **Microsoft SQL Server** docs (Neu + Aktualisiert: Dokumentation zu Microsoft SQL Server)](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+0): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+0): Dokumentation zu SQL Server Data Tools (SSDT))](../ssdt/new-updated-ssdt.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [New + Updated (0+0): **Tools for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Tools für SQL)](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)



