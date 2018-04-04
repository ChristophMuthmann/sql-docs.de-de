---
title: Erstellen von Diagrammen und Darstellungen, die mithilfe von SQL und R (Exemplarische Vorgehensweise) | Microsoft Docs
ms.date: 11/10/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: e7c40d76a585e021fac13094a524e32ff4da0a45
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="create-graphs-and-plots-using-sql-and-r-walkthrough"></a>Erstellen von Diagrammen und Darstellungen, die mithilfe von SQL und R (Exemplarische Vorgehensweise)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Teil der exemplarischen Vorgehensweise lernen Sie die Techniken zum Generieren von Zeichnungen und Zuordnungen, die mithilfe von R mit SQL Server-Daten. Erstellen Sie ein einfache Histogramm angezeigt, und um, vertraut zu machen und entwickeln Sie eine komplexere Zuordnung zeichnen.

### <a name="create-a-histogram"></a>Erstellt ein Histogramm

1. Erstellen Sie die erste Zeichnung mithilfe der [rxHistogram](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource) -Funktion.  Die RxHistogram-Funktion in open Source-R-Paketen, die ähnliche Funktionen bietet, aber Sie können in einem Kontext Remoteausführung ausführen.

    ```R
    # Plot fare amount on SQL Server and return the plot
    start.time <- proc.time()
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate plot.", sep=""))
    ```

2. Das Bild wird im Grafikgerät von R für Ihre Entwicklungsumgebung zurückgegeben.  Klicken Sie z.B. in RStudio auf das Fenster **Plot** (Diagramm).  In [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]wird ein separates Grafikfenster geöffnet.

    ![Verwenden von rxHistogramm zum Darstellen von Fahrpreisen](media/rsql-e2e-rxhistogramresult.png "using rxHistogram to plot fare amounts")

    > [!NOTE]
    > Aussehen das Diagramm anders?
    >  
    > Grund hierfür ist, _InDataSource_ nur die Top 1000 Zeilen verwendet. Die Reihenfolge der Zeilen mit TOP ist nicht deterministisch in Abwesenheit einer ORDER BY-Klausel so, dass die Daten und das resultierende Diagramm variieren erwartet wird.
    > Dieses bestimmte Bild wurde mithilfe von ca. 10.000 Datenzeilen generiert. Wir empfehlen daher, mit einer unterschiedlichen Anzahl von Zeilen zu experimentieren, um verschiedene Diagramme zu erhalten. Beachten Sie, wie lange es dauert, bis die Ergebnisse in Ihrer Umgebung zurückgegeben werden.

### <a name="create-a-map-plot"></a>Erstellen Sie eine Zuordnung Zeichnungsfläche

In der Regel Sperren Datenbankserver Zugang zum Internet. Dies kann unpraktisch sein, wenn R-Pakete zu verwenden, die müssen zum Herunterladen von Zuordnungen oder anderen Bildern um Darstellungen zu generieren. Allerdings ist dieses Problem zu umgehen, die Sie hilfreich finden könnten bei der Entwicklung eigener Anwendungen. Im Grunde die Darstellung der Karte auf dem Client zu generieren und dann Überlagerung auf der Karte die Punkte, die als Attribute in der SQL Server-Tabelle gespeichert sind.

1. Definieren Sie die Funktion, die die R-Plots-Objekt erstellt. Die benutzerdefinierte Funktion *MapPlot* erstellt ein Punktdiagramm, die die Taxi pickup-Speicherorte verwendet und zeichnet die Anzahl der Schlittenfahrten, die von jedem Standort gestartet. Die Funktion verwendet die Pakete **ggplot2** und  **ggmap** , die bereits installiert und geladen sein sollten.

    ```R
    mapPlot <- function(inDataSource, googMap){
        library(ggmap)
        library(mapproj)
        ds <- rxImport(inDataSource)
        p <- ggmap(googMap)+
        geom_point(aes(x = pickup_longitude, y =pickup_latitude ), data=ds, alpha =.5,
    color="darkred", size = 1.5)
        return(list(myplot=p))
    }
    ```

    + Die *MapPlot* Funktion akzeptiert zwei Argumente: ein vorhandenes Datenobjekt, das Sie zuvor mit RxSqlServerData definiert und die Darstellung der Karte, die vom Client übergeben.
    + In der Zeile ab, mit der *ds* Variable RxImport wird verwendet, um in den von Speicherdaten aus der zuvor erstellte Datenquelle geladen *InDataSource*. (Diese Datenquelle enthält nur 1000 Zeilen; Wenn Sie eine Zuordnung mit mehr Datenpunkte erstellen möchten, können Sie eine andere Datenquelle ersetzen)
    + Bei Verwendung **open-Source** R-Funktionen, Daten in Data Frames im lokalen Speicher geladen werden müssen. Allerdings durch Aufrufen der [RxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) -Funktion, die Sie ausführen können, im Arbeitsspeicher des remote-computekontext.

2. Ändern Sie des computekontexts lokalen, und Laden Sie die Bibliotheken, die zum Erstellen der Zuordnungen erforderlich sind.

    ```R
    rxSetComputeContext("local")
    library(ggmap)
    library(mapproj)
    gc <- geocode("Times Square", source = "google")
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color');
    ```

    + Die Variable `gc` speichert mehrere Koordinaten für den Times Square, NY.

    + Die Zeile, die mit `googmap` beginnt, generiert eine Karte mit den angegebenen Koordinaten in der Mitte.

3. Wechseln Sie zu der SQL Server-computekontext und die Ergebnisse durch wrapping in die Zeichnungsfläche-Funktion Rendern [RxExec](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexec) wie hier gezeigt. Die RxExec-Funktion ist Teil der **"revoscaler"** Paket und unterstützt die Ausführung von beliebige R-Funktionen in einem remote-computekontext.

    ```R
    rxSetComputeContext(sqlcc)
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)
    plot(myplots[[1]][["myplot"]]);
    ````

    + Die Kartendaten in `googMap` als Argument übergeben wird, die an die Remote ausgeführte Funktion *MapPlot*. Da die Zuordnungen in Ihrer lokalen Umgebung generiert wurden, müssen sie an die Funktion übergeben werden, um die Zeichnung im Kontext von SQL Server zu erstellen.

    + Wenn der Anfang der Zeile mit `plot` ausgeführt wird, der gerenderten Daten zurück an den lokalen R-Umgebung serialisiert wird, damit Sie ihn in Ihrem R-Client anzeigen können.

    > [!NOTE]
    > Wenn Sie SQL Server in virtuellen Azure-Computer verwenden, Sie erhalten möglicherweise einen Fehler an diesem Punkt. Grund hierfür eine Firewall-Standardregel in Azure Netzwerkzugriff durch R-Code blockiert ist. Weitere Informationen zum Beheben dieses Fehlers finden Sie unter [Installieren von R Services in einer Azure-VM](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

4. In der folgenden Abbildung ist das ausgegebene Diagramm dargestellt. Die Taxi-Abholorte wurden zur Karte als rote Punkte hinzugefügt. Ihr Bild stilistisch möglicherweise unterschiedlich, je nachdem, wie viele Speicherorte in der Datenquelle sind, die Sie verwendet.

    ![Zeichnen von Taxifahrten mithilfe einer benutzerdefinierten R-Funktion](media/rsql-e2e-mapplot.png "plotting taxi rides using a custom R function")

## <a name="next-lesson"></a>Nächste Lektion

[Erstellen Sie mithilfe von R und SQL Data-Funktionen](/walkthrough-create-data-features.md)

## <a name="previous-lesson"></a>Vorherige Lektion

[Zusammenfassen von Daten mithilfe von R](/walkthrough-view-and-summarize-data-using-r.md)
