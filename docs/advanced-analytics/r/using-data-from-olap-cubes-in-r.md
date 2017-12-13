---
title: Verwenden von Daten aus OLAP-Cubes in R | Microsoft Docs
ms.custom: 
ms.prod: sql-non-specified
ms.date: 12/08/2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: r-services
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 21bb48b26b7bf8e755ba85a16fb25676bbff4363
ms.sourcegitcommit: 05e2814fac4d308196b84f1f0fbac6755e8ef876
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>Verwenden von Daten aus OLAP-Cubes in R

Die **OlapR** Paket ist ein R-Paket aus, sofern von Microsoft für die Verwendung mit Machine Learning-Server und SQL Server, die Sie MDX-Abfragen zum Abrufen von Daten aus OLAP-Cubes ausführen können. Mit diesem Paket müssen Sie das Erstellen von Verbindungsservern oder bereinigen Sie die vereinfachte Rowsets; Sie können OLAP-Daten direkt aus r abrufen.

Dieser Artikel beschreibt die API, sowie eine Übersicht über OLAP- und MDX für R-Benutzer, die möglicherweise noch nicht mit mehrdimensionale Cubedatenbanken.

> [!IMPORTANT]
> Eine Instanz von Analysis Services konventionellen mehrdimensionalen Cubes oder tabellarische Modelle unterstützt, jedoch eine Instanz kann nicht beide Typen von Modellen unterstützen. Aus diesem Grund, bevor Sie versuchen, eine MDX-Abfrage für einen Cube zu erstellen, stellen Sie sicher, dass die Instanz von Analysis Services mehrdimensionale Modelle enthält.

## <a name="what-is-an-olap-cube"></a>Was ist ein OLAP-Cube?

OLAP wird kurz für Online Analytical Processing. OLAP-Lösungen werden häufig zum Erfassen und Speichern von wichtigen Geschäftsdaten mit der Zeit verwendet. OLAP-Daten werden von einer Vielzahl von Tools, Dashboards und Visualisierungen für Business Analytics genutzt. Weitere Informationen finden Sie unter [Online analytical Processing](https://en.wikipedia.org/wiki/Online_analytical_processing).

Microsoft bietet [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), die ermöglicht, entwerfen, bereitstellen und Abfragen von OLAP-Daten in Form von _Cubes_ oder _Tabellenmodelle_. Ein Cube ist eine mehrdimensionale Datenbank an. _Dimensionen_ ähneln Facets der Daten-oder Faktoren in R: Sie Dimensionen verwenden, um eine bestimmte Teilmenge der Daten zu identifizieren, die Sie zusammenfassen oder analysieren möchten. Beispielsweise ist Zeit eine wichtige Dimension, ein derartiger Umfang, sodass viele OLAP-Lösungen mehrere Kalender definiert standardmäßig zu verwendende Aufteilen in Slices und Zusammenfassen von Daten enthalten. 

Aus Gründen der Leistung eine OLAP-Datenbank häufig Zusammenfassungen berechnet (oder _Aggregationen_) im voraus, und speichert sie schneller abrufen. Zusammenfassungen basieren auf *Measures*, die darstellen, dass Formeln, die auf numerische Daten angewendet werden können. Sie verwenden Sie die Dimensionen, um eine Teilmenge der Daten zu definieren, und berechnen Sie das Measure, auf diese Daten. Beispielsweise würden Sie ein Measure verwenden, berechnet den Gesamtumsatz für eine bestimmte Produktlinie über mehrere Quartale minus steuern, um die durchschnittliche Versandkosten für einen bestimmten Lieferanten, Jahr-bis-heute kumulative Gehälter bezahlt usw. zu melden.

MDX, kurz für mehrdimensionale Ausdrücke, ist die Sprache für die Abfrage von Cubes verwendet. Eine MDX-Abfrage enthält in der Regel eine Datendefinition, die eine oder mehrere Dimensionen und mindestens ein Measure enthält, obwohl MDX-Abfragen wesentlich komplexer abrufen und parallelen Windows, kumulierte Durchschnittswerte, Summen, Ränge oder Quantile enthalten können. 

Hier sind einige andere Begriffe, die möglicherweise hilfreich, wenn Sie zum Erstellen von MDX-Abfragen starten:

+ *Aufteilen in Slices* nimmt eine Teilmenge des Cubes mithilfe von Werten aus einer einzelnen Dimension.

+ *Dicing* (Teilwürfel) erstellt einen Teilwürfel durch Angabe eines Wertebereichs für mehrere Dimensionen.

+ *Drilldown* navigiert von einer Zusammenfassung zu Detailinformationen.

+ *Drillup* bezeichnet die Bewegung von Details zu einer höheren Aggregationsstufe.

+ *Rollup* fasst die Daten für eine Dimension zusammen.

+ Beim*Pivotieren* wird der Würfel oder die Datenauswahl gedreht.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Gewusst wie: OlapR zu verwenden, um MDX-Abfragen zu erstellen.

Der folgende Artikel enthält ausführliche Beispiele für die Syntax zum Erstellen oder Ausführen von Abfragen für einen Cube:

+ [Vorgehensweise: Erstellen von MDX-Abfragen mithilfe von R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>OlapR API

Das **olapR** -Paket unterstützt zwei Methoden zum Erstellen von MDX-Abfragen:

- **Verwenden Sie die MDX-Generator.** Verwenden Sie die R-Funktionen im Paket, eine einfache MDX-Abfrage zu generieren, indem Sie einen Cube auswählen sowie das anschließende festlegen, Achsen und Slicer. Dies ist eine einfache Möglichkeit, eine gültige MDX-Abfrage zu erstellen, wenn Sie keinen Zugriff auf die herkömmliche OLAP-Tools oder keine umfassenden Kenntnisse der MDX-Sprache.

    Nicht alle MDX-Abfragen können mit dieser Methode erstellt werden, da MDX komplex sein kann. Diese API unterstützt jedoch die meisten der am häufigsten häufige und sinnvolle Vorgänge, einschließlich Slice, Datenwürfel aufgeteilt, Drilldown, Rollup und Pivot in N-Dimensionen.

+ **Wohlgeformte MDX kopieren und einfügen.** Erstellen Sie manuell, und fügen Sie in einer MDX-Abfrage. Diese Option ist am besten bei vorhandenen MDX-Abfragen, die Sie wiederverwenden möchten, oder wenn die Abfrage zu erstellenden zu komplex für **OlapR** behandelt.

    Speichern Sie nach der Erstellung Ihrer MDX Client-Dienstprogramm, z. B. SSMS oder Excel, über die Abfragezeichenfolge. Geben Sie diese MDX-Zeichenfolge als Argument an die *SSAS Abfrage Handler* in der **OlapR** Paket. Der Anbieter sendet die Abfrage mit dem angegebenen Analysis Services-Server und übergibt der r die Ergebnisse 

Beispiele zum Erstellen einer MDX Abfragen oder eine vorhandene MDX-Abfrage ausführen, finden Sie unter [Erstellen von MDX-Abfragen mithilfe von R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Bekannte Probleme

Dieser Abschnitt listet einige bekannte Probleme und häufig gestellte Fragen über die **OlapR** Paket.

### <a name="tabular-model-support"></a>Tabellenmodell-Unterstützung

Wenn Sie eine Verbindung mit einer Instanz von Analysis Services herstellen, die ein tabellarisches Modell enthält die `explore` -Funktion meldet Erfolg mit einem Rückgabewert von "true". Allerdings tabellenmodellobjekte unterscheiden sich von mehrdimensionalen Objekten und die Struktur einer mehrdimensionalen Datenbank unterscheidet sich von denen für ein tabellarisches Modell.

Obwohl DAX (Data Analysis Expressions) der Sprache, die in der Regel mit tabellarischen Modellen verwendet wird, können Sie gültige MDX-Abfragen für ein tabellarisches Modell entwerfen, wenn Sie bereits mit MDX vertraut sind. Die OlapR Konstruktoren können keine um gültigen MDX-Abfragen für ein tabellarisches Modell zu erstellen.

MDX-Abfragen sind jedoch eine ineffiziente Möglichkeit zum Abrufen von Daten aus einem tabellarischen Modell. Wenn Sie zum Abrufen von Daten aus einem tabellarischen Modell für die Verwendung in R möchten, erwägen Sie stattdessen diese Methoden:

+ Aktivieren von DirectQuery für das Modell aus, und fügen Sie den Server als Verbindungsserver in SQL Server. 
+ Wenn das tabellarische Modell auf einem relationalen Datamart erstellt wurde, werden rufen Sie die Daten direkt aus der Quelle ab.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Gewusst wie: bestimmen, ob eine Instanz tabellarische oder mehrdimensionale Modelle enthält.

Eine einzelne Analysis Services-Instanz kann nur einen Typ von Modell enthalten, obwohl sie mehrere Modelle enthalten kann. Der Grund dafür ist, dass es grundlegende Unterschiede zwischen tabellarischen Modellen und mehrdimensionale Modelle, die die zu steuern, wie Daten gespeichert und verarbeitet werden. Beispielsweise tabellarische Modelle werden im Arbeitsspeicher gespeichert und Nutzen von columnstore-Indizes, um sehr schnelle Berechnungen durchzuführen. In mehrdimensionalen Modellen werden auf Datenträger gespeichert und Aggregationen im Voraus definiert und mithilfe von MDX-Abfragen abgerufen werden.

Wenn Sie eine Verbindung zu Analysis Services über einen Client wie SQL Server Management Studio herstellen, können Sie auf einen Blick erkennen, welcher Modelltyp unterstützt wird, durch einen Blick auf das Symbol für die Datenbank.

Sie können auch anzeigen, und Fragen Sie die Servereigenschaften, um zu bestimmen, welcher Typ von Modell die Instanz unterstützt. Die **Servermodus** Eigenschaft zwei Werte werden unterstützt: _mehrdimensionale_ oder _tabellarische_.

Finden Sie im folgenden Artikel allgemeine Informationen zu den zwei Typen von Modellen aus:

+ [Mehrdimensionale und tabellarische Modelle vergleichen](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Finden Sie im folgenden Artikel Informationen zum Abfragen von Servereigenschaften:

+ [OLE DB für OLAP-Schemarowsets](https://docs.microsoft.com/sql/analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>Das Rückschreiben wird nicht unterstützt.

Es ist nicht möglich, benutzerdefinierte R Berechnungsergebnisse des in den Cube schreiben.

Im Allgemeinen auch, wenn Sie ein Cube für das Rückschreiben aktiviert ist, wird nur eingeschränkte Vorgänge werden unterstützt, und möglicherweise zusätzliche Konfigurationsschritte erforderlich. Es wird empfohlen, dass Sie für solche Vorgänge MDX verwenden.

+ [Dimensionen mit aktiviertem Schreibzugriff](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Partitionen mit aktiviertem Schreibzugriff](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Festlegen von benutzerdefiniertem Zugriff auf Zellendaten](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Lang andauernde MDX-Abfragen blockiert, die Verarbeitung eines Cubes

Obwohl die **OlapR** Paket führt nur Lesevorgänge, lang andauernde MDX-Abfragen erstellen sperren, die verhindern, dass den Cube verarbeitet wird. Testen Sie MDX-Abfragen immer im voraus, damit Sie wissen, wie viele Daten zurückgegeben werden sollen.

Wenn Sie versuchen, eine Verbindung mit einem Cube, die gesperrt wird, erhalten Sie möglicherweise einen Fehler, den das SQL Server-Datawarehouse nicht erreicht werden kann. Vorgeschlagene Lösungen umfassen das Aktivieren von Remoteverbindungen, überprüfen den Server oder den Instanznamen usw.; sollten Sie aber die Möglichkeit, dass eine vorherige offene Verbindung.

Eine SSAS-Serveradministrator kann verhindern, dass Probleme identifizieren und Beenden von geöffneten Sitzungen sperren. Eine Timeouteigenschaft kann auch für MDX-Abfragen auf Serverebene für das erzwungene Beenden aller lang andauernde Abfragen angewendet werden.

## <a name="resources"></a>Ressourcen

Wenn Sie OLAP- oder MDX-Abfragen nicht vertraut sind, finden Sie unter folgenden Wikipedia-Artikeln: 

+ [OLAP-cubes](https://en.wikipedia.org/wiki/OLAP_cube)
+ [MDX-Abfragen](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
