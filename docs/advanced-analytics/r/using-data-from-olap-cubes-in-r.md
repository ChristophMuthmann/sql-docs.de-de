---
title: Verwenden von Daten aus OLAP-Cubes in R | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 8fe9d54e1d635b5c8f1dd6e00e33bd92136343b4
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="using-data-from-olap-cubes-in-r"></a>Verwenden von Daten aus OLAP-Cubes in R

Das **olapR** -Paket ist ein neues R-Paket, das in Microsoft R Server und SQL Server R Services zum Ausführen von MDX-Abfragen und Verwenden der Daten aus OLAP-Cubes in Ihrer R-Lösung bereitsteht.

Mit diesem Paket brauchen Sie keine verknüpften Server zu erstellen oder vereinfachten Rowsets zu bereinigen; OLAP-Daten können direkt in R verwendet werden.

## <a name="overview"></a>Übersicht

Ein OLAP-Cube ist eine mehrdimensionale Datenbank, die vorausberechnete Aggregationen für *Measures*enthält, die normalerweise wichtige Geschäftsmetriken erfassen, wie etwa den Umsatz, die Verkaufszahlen oder andere numerische Werte. OLAP-Cubes werden in großem Umfang zum Erfassen und Speichern wichtiger Unternehmensdaten in der zeitlichen Abfolge verwendet. OLAP-Daten werden von einer Vielzahl von Tools, Dashboards und Visualisierungen für Business Analytics genutzt. Weitere Informationen finden Sie unter [Analytische Onlineverarbeitung (OLAP)](https://en.wikipedia.org/wiki/Online_analytical_processing)

Das **olapR** -Paket unterstützt zwei Methoden zum Erstellen von MDX-Abfragen: 

- Sie können eine einfache MDX-Abfrage erstellen, indem Sie eine API nach R-Art verwenden, um einen Cube, Achsen und Datenschnitte auszuwählen. Mithilfe dieser Funktion können Sie auch ohne Zugang zu herkömmlichen OLAP-Tools oder tiefgreifende Kenntnis der MDX-Sprache gültige MDX-Abfragen erstellen.

  Beachten Sie, dass nicht alle möglichen MDX-Abfragen mithilfe dieser Methode im **olapR** -Paket erstellt werden können, da MDX sehr komplex sein kann. Die gebräuchlichsten und nützlichsten Operationen werden jedoch ausnahmslos unterstützt, einschließlich Slice, Dice, Drilldown, Rollup und Pivotieren in N Dimensionen.

+ Sie können MDX-Abfragen manuell erstellen und dann einfügen. Diese Option ist nützlich, wenn Sie vorhandene MDX-Abfragen erneut verwenden möchten oder die Abfrage, die Sie erstellen möchten, zu komplex für **olapR** ist. 

  Bei diesem Ansatz erstellen Sie Ihre MDX-Abfrage mithilfe beliebiger Clienthilfsprogramme wie SSMS oder Excel und verwenden sie dann als Zeichenfolgenargument für den *SSAS-Abfragehandler* , der von diesem Paket bereitgestellt wird. Die **olapR** -Funktion sendet die Abfrage an den angegebenen Analysis Services-Server und übergibt die Ergebnisse dann zurück an R.

Beispiele zum Erstellen von MDX-Abfragen oder zum Ausführen vorhandener MDX-Abfragen finden Sie unter [Erstellen von MDX-Abfragen mithilfe von R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md).


## <a name="mdx-basics"></a>MDX-Grundlagen

Die Daten in einem Cube können mithilfe der MDX-Abfragesprache (MultiDimensional Expression) abgerufen werden. Da die Daten in einem OLAP-Cube (oder in einer Analysis Services-Datenbank) mehrdimensional anstatt tabellarisch gespeichert sind, unterstützt MDX eine komplexe Syntax und eine Vielzahl von Operationen zum Filtern und Slicen von Daten:

+ Beim*Slicing* (Datenschnitt) wird eine Teilmenge des Cubes erstellt, indem ein Wert für eine Dimension ausgewählt wird, was zu einem um eine Dimension kleineren Cube führt. 

+ *Dicing* (Teilwürfel) erstellt einen Teilwürfel durch Angabe eines Wertebereichs für mehrere Dimensionen.

+ *Drilldown* navigiert von einer Zusammenfassung zu Detailinformationen.

+ *Drillup* bezeichnet die Bewegung von Details zu einer höheren Aggregationsstufe.

+ *Rollup* fasst die Daten für eine Dimension zusammen.

+ Beim*Pivotieren* wird der Würfel oder die Datenauswahl gedreht.

Dieses Thema enthält im Anschluss an die Beispiele mit der grundlegenden Syntax zum Abfragen eines Cubes weitere Beispiele.
[Erstellen von MDX-Abfragen mit R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)


## <a name="known-issues"></a>Bekannte Probleme

### <a name="tabular-models-not-supported-currently"></a>Tabellarische Modelle werden zurzeit nicht unterstützt

Sie können eine Verbindung mit einer Tabelleninstanz von Analysis Services herstellen, und die `explore` -Funktion gibt den Rückgabewert WAHR zurück, die Objekte des Tabellenmodells gehören aber keinem kompatiblen Typ an und können nicht durchsucht werden. 

Tabellenmodelle unterstützen MDX-Abfragen, eine gültige MDX-Abfrage eines Tabellenmodells gibt aber ein NULL-Ergebnis zurück und führt nicht zur Meldung eines Fehlers.

## <a name="resources"></a>Ressourcen

Wenn Sie neu in OLAP oder MDX-Abfragen einsteigen, lesen Sie diese Wikipedia-Artikel: [OLAP Cubes (OLAP-Cubes)](https://en.wikipedia.org/wiki/OLAP_cube)
[MDX queries (MDX-Abfragen)](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>Beispiele

Wenn Sie mehr über Cubes erfahren möchten, können Sie den Cube, der in diesen Beispielen verwendet wird, erstellen, indem Sie dem Analysis Services-Tutorial bis zur Lektion 4: [Erstellen eines OLAP-Cubes](/sql-docs/docs/analysis-services/multidimensional-modeling-adventure-works-tutorial)folgen

Sie können auch einen vorhandenen Cube als Sicherung herunterladen und ihn in einer Instanz von Analysis Services wiederherstellen. Beispielsweise können Sie einen vollständig verarbeiteten Cube für das [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)im komprimierten ZIP-Format herunterladen und ihn in Ihrer SSAS-Instanz wiederherstellen. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)oder [Restore-ASDatabase Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md).

## <a name="see-also"></a>Siehe auch
[Erstellen von MDX-Abfragen mit R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

[MDX-Abfrage-Designer für Analysis Services](http://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)



