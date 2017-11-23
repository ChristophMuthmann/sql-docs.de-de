---
title: Verwenden von Daten aus OLAP-Cubes in R | Microsoft Docs
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1c55a5b834cd91478a87ded7ebb86884117c7bfb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>Verwenden von Daten aus OLAP-Cubes in R

Die **OlapR** Paket ist ein R-Paket bereitgestellt von Microsoft für die Verwendung mit Machine Learning-Server und SQL Server R Services, die Sie MDX-Abfragen zum Abrufen von Daten aus OLAP-Cubes ausführen können. Mit diesem Paket müssen Sie das Erstellen von Verbindungsservern oder bereinigen Sie die vereinfachte Rowsets; Sie können OLAP-Daten direkt in r verwenden.

Dieser Artikel beschreibt die API, zusammen mit einer Übersicht über fo OLAP und MDX für R-Benutzer, die möglicherweise noch nicht mit mehrdimensionale Cubedatenbanken.

## <a name="what-is-an-olap-cube"></a>Was ist ein OLAP-Cube?

OLAP wird kurz für Online Analytical Processing. OLAP-Lösungen werden häufig zum Erfassen und Speichern von wichtigen Geschäftsdaten mit der Zeit verwendet. OLAP-Daten werden von einer Vielzahl von Tools, Dashboards und Visualisierungen für Business Analytics genutzt. Weitere Informationen finden Sie unter [Online analytical Processing](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft bietet [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), die ermöglicht, entwerfen, bereitstellen und Abfragen von OLAP-Daten in Form von _Cubes_ oder _Tabellenmodelle_. Ein Cube ist eine mehrdimensionale Datenbank an. _Dimensionen_ ähneln Facets der Daten-oder Faktoren in R: Sie Dimensionen verwenden, um eine bestimmte Teilmenge der Daten zu identifizieren, die Sie zusammenfassen oder analysieren möchten. Beispielsweise ist Zeit eine wichtige Dimension, ein derartiger Umfang, sodass viele OLAP-Lösungen mehrere Kalender definiert standardmäßig zu verwendende Aufteilen in Slices und Zusammenfassen von Daten enthalten. 

Aus Gründen der Leistung eine OLAP-Datenbank häufig Zusammenfassungen berechnet (oder _Aggregationen_) im voraus, und speichert sie schneller abrufen. Zusammenfassungen basieren auf *Measures*, die darstellen, dass Formeln, die auf numerische Daten angewendet werden können. Sie verwenden Sie die Dimensionen, um eine Teilmenge der Daten zu definieren, und berechnen Sie das Measure, auf diese Daten. Beispielsweise würden Sie ein Measure verwenden, berechnet den Gesamtumsatz für eine bestimmte Produktlinie über mehrere Quartale minus steuern, um die durchschnittliche Versandkosten für einen bestimmten Lieferanten, Jahr-bis-heute kumulative Gehälter bezahlt usw. zu melden.

MDX, kurz für mehrdimensionale Ausdrücke, ist die Sprache für die Abfrage von Cubes verwendet. Eine MDX-Abfrage in der Regel enthält eine Datendefinition, die eine oder mehrere Dimensionen und mindestens ein Measure enthält, Thogh MDX-Abfragen abrufen wesentlich komplexer und parallelen Windows, kumulierte Mittelwerte oder Summen, Quantile enthalten können. 

Hier sind einige andere Begriffe, die möglicherweise hilfreich, wenn Sie zum Erstellen von MDX-Abfragen starten:

+ *Aufteilen in Slices* nimmt eine Teilmenge des Cubes mithilfe von Werten aus einer einzelnen Dimension.

+ *Dicing* (Teilwürfel) erstellt einen Teilwürfel durch Angabe eines Wertebereichs für mehrere Dimensionen.

+ *Drilldown* navigiert von einer Zusammenfassung zu Detailinformationen.

+ *Drillup* bezeichnet die Bewegung von Details zu einer höheren Aggregationsstufe.

+ *Rollup* fasst die Daten für eine Dimension zusammen.

+ Beim*Pivotieren* wird der Würfel oder die Datenauswahl gedreht.

Dieses Thema enthält weitere Beispiele für die grundlegende Syntax für Abfragen für einen Cube: 

+ [Vorgehensweise: Erstellen von MDX-Abfragen mithilfe von R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>OlapR API

Das **olapR** -Paket unterstützt zwei Methoden zum Erstellen von MDX-Abfragen:

- **Verwenden Sie die MDX-Generator.** Verwenden Sie die R-Funktionen im Paket, um eine einfache MDX-Abfrage zu generieren, indem Sie einen Cube und Einstellung Achsen und Slicer auswählen. Dies ist eine einfache Möglichkeit, eine gültige MDX-Abfrage zu erstellen, wenn Sie keinen Zugriff auf die herkömmliche OLAP-Tools oder keine umfassenden Kenntnisse der MDX-Sprache.

    Nicht alle mögliche MDX-Abfragen können mit dieser Methode erstellt werden, da MDX komplex sein kann. Diese API unterstützt jedoch die meisten der am häufigsten häufige und sinnvolle Vorgänge, einschließlich Slice, Datenwürfel aufgeteilt, Drilldown, Rollup und Pivot in N-Dimensionen.

+ **Wohlgeformte MDX kopieren und einfügen.** Erstellen Sie manuell, und fügen Sie in einer MDX-Abfrage. Diese Option ist am besten bei vorhandenen MDX-Abfragen, die Sie wiederverwenden möchten, oder wenn die Abfrage zu erstellenden zu komplex für **OlapR** behandelt. 

    Erstellen Sie Ihrer MDX über alle Client-Dienstprogramm, z. B. SSMS oder Excel, und speichern Sie dann die Zeichenfolge, die die MDX-Abfrage definiert. Geben Sie diese MDX-Zeichenfolge als Argument an die *SSAS Abfrage Handler* in der **OlapR** Paket. Die Funktion die Abfrage mit dem angegebenen Analysis Services-Server sendet, und übergibt der R, vorausgesetzt, dass Sie berechtigt, den Cube natürlich Abfragen die Ergebnisse.

Beispiele zum Erstellen einer MDX Abfragen oder eine vorhandene MDX-Abfrage ausführen, finden Sie unter [Erstellen von MDX-Abfragen mithilfe von R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Bekannte Probleme

### <a name="tabular-models-not-supported"></a>Tabellarische Modelle nicht unterstützt.

+ Wenn das Herstellen einer Verbindung mit einer tabellarischen Instanz von Analysis Services, die `explore` -Funktion meldet Erfolg mit einem Rückgabewert von "true". Allerdings tabellenmodellobjekte sind keinen kompatiblen Typ und können nicht durchsucht werden.

+ Tabellarische Modelle können mit DAX oder MDX abgefragt werden. Wenn Sie eine gültige MDX-Abfrage für ein tabellarisches Modell mithilfe eines externen Tools entwerfen und fügen Sie die Abfrage in dieser API, die Abfrage gibt ein NULL-Ergebnis zurück, und meldet keine Fehler.

## <a name="resources"></a>Ressourcen

Wenn Sie neu in OLAP oder MDX-Abfragen einsteigen, lesen Sie diese Wikipedia-Artikel: [OLAP Cubes (OLAP-Cubes)](https://en.wikipedia.org/wiki/OLAP_cube)
[MDX queries (MDX-Abfragen)](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>Beispiele

Wenn Sie mehr über Cubes erfahren möchten, können Sie den Cube, der in diesen Beispielen verwendet wird, erstellen, indem Sie dem Analysis Services-Tutorial bis zur Lektion 4: [Erstellen eines OLAP-Cubes](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)folgen

Sie können auch einen vorhandenen Cube als Sicherung herunterladen und ihn in einer Instanz von Analysis Services wiederherstellen. Beispielsweise können Sie einen vollständig verarbeiteten Cube für das [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)im komprimierten ZIP-Format herunterladen und ihn in Ihrer SSAS-Instanz wiederherstellen. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)oder [Restore-ASDatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md).
