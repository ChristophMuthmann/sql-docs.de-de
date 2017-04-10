---
title: "Erstellen von Graphen und Diagrammen mit R (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 5f70f0a6-fd4a-410f-9f44-1605503f77ec
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Erstellen von Graphen und Diagrammen mit R (Exemplarische Data Science Ende-zu-Ende-Vorgehensweise)
In dieser Lektion lernen Sie Techniken für die Generierung von Diagrammen und Karten mithilfe von R mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten kennen.  Sie sehen, wie einfach es ist, Diagramme anzuzeigen, die auf dem Server erstellt werden und wie Sie Grafikobjekte an den Server übergeben können.  
  
## <a name="creating-graphics"></a>Erstellen von Grafiken
In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] werden Grafikobjekte sowie Modelle und Ergebnisse zwischen Ihrem Computer und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computekontext serialisiert.

Wenn Sie einen SQL Server-Computekontext verwenden, können Sie möglicherweise die Darstellung der Karte nicht herunterladen, da die meisten Datenbankserver in Produktionsumgebungen den Internetzugriff vollständig blockieren.  Darum generieren Sie zum Erstellen der zweiten Gruppe von Diagrammen die Kartendarstellung im Client und legen anschließend die Punkte in der Datenbank über die Karte, die als Attribute in der Tabelle *nyctaxi_sample* gespeichert sind.   

Dazu erstellen Sie zunächst die Kartendarstellung, indem Sie Google Maps aufrufen und anschließend die Kartendarstellung an den SQL-Kontext übergeben.  
  
Dies ist ein Muster, das Sie möglicherweise als hilfreich erachten, wenn Sie Ihre eigenen Anwendung entwickeln.   
  
### <a name="create-a-histogram"></a>Erstellen eines Histogramms  
Um ein Histogramm zu erstellen, verwenden Sie die zuvor erstellte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle zusammen mit der in R Services bereitgestellten `rxHistogram` -Funktion.  
  
1.  Erstellen Sie die erste Zeichnung mithilfe der *rxHistogram*-Funktion.  Die *rxHistogram*-Funktion bietet ähnliche Funktionen wie Open-Source-R-Pakete, kann aber in einem Remoteausführungskontext ausgeführt werden. 
  
    ```R  
    #Plot fare amount on SQL Server and return the plot  
    start.time <- proc.time()  
    rxHistogram(~fare_amount, data = inDataSource, title = "Fare Amount Histogram")  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2), " seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```         
  
2.  Das Bild wird im Grafikgerät von R für Ihre Entwicklungsumgebung zurückgegeben.  Klicken Sie z.B. in RStudio auf das Fenster **Plot** (Diagramm).  In [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]wird ein separates Grafikfenster geöffnet.  
  
    ![using rxHistogram to plot fare amounts](../../advanced-analytics/r-services/media/rsql-e2e-rxhistogramresult.png "using rxHistogram to plot fare amounts")  
  
    > [!NOTE]  Da die Reihenfolge der Zeilen, die TOP ohne eine ORDER BY-Klausel verwenden, nicht deterministisch ist, werden Ihnen sehr unterschiedliche Ergebnisse angezeigt. Wir empfehlen daher, mit einer unterschiedlichen Anzahl von Zeilen zu experimentieren, um verschiedene Diagramme zu erhalten. Beachten Sie, wie lange es dauert, bis die Ergebnisse in Ihrer Umgebung zurückgegeben werden.  Dieses bestimmte Bild wurde mithilfe von ca. 10.000 Datenzeilen generiert.
  
### <a name="create-a-map-plot"></a>Erstellen einer Kartenzeichnung  
In diesem Beispiel generieren Sie ein Diagrammobjekt mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz als Computekontext und übergeben anschließend das Diagrammobjekt an den lokalen Computekontext für das Rendering.  
   
1.  Definieren Sie zuerst die Funktion, die das Diagrammobjekt erstellt.  

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
    + Die benutzerdefinierte R-Funktion *mapPlot* erstellt ein Punktdiagramm, das die Abholorte des Taxis verwendet, um die Anzahl der Fahrten von jedem Abholort aus zu zeichnen. Die Funktion verwendet die Pakete **ggplot2** und  **ggmap** , die bereits installiert und geladen sein sollten.  
    + Die benutzerdefinierte Funktion *mapPlot* hat zwei Argumente: ein vorhandenes Datenobjekt, das Sie zuvor mit *RxSqlServerData* definiert haben, sowie die Kartendarstellung, die vom Client übergeben wurde.    
    + Beachten Sie, dass die Variable *ds* zum Laden von Daten aus der zuvor erstellten Datenquelle *inDataSource* verwendet wird.  Wenn Sie Open Source-Funktionen von R verwenden, müssen Daten in Datenrahmen im Arbeitsspeicher geladen werden. Verwenden Sie dazu die *rxImport*-Funktion im **RevoScaleR**-Paket.  Diese Funktion wird jedoch im Arbeitsspeicher im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kontext ausgeführt, der zuvor definiert wurde. Das bedeutet, dass die Funktion nicht den Arbeitsspeicher Ihres lokalen Arbeitsbereichs verwendet.  
  
2.  Laden Sie als Nächstes die Bibliotheken, die für das Erstellen der Karten in Ihrer lokalen R-Umgebung benötigt werden.  
  
    ```R  
    library(ggmap)  
    library(mapproj)  
    gc <- geocode("Times Square", source = "google")  
    googMap <- get_googlemap(center = as.numeric(gc), zoom = 12, maptype = 'roadmap', color = 'color';    
    ```  
    + Dieser Code wird auf dem R-Client ausgeführt. Achten Sie auf den wiederholten Aufruf der Bibliotheken **ggmap** und **mapproj**. Der Grund dafür ist, dass die vorherige Funktionsdefinition im Serverkontext ausgeführt wurde und die Bibliotheken nie lokal geladen wurden. Den Zeichenvorgang führen Sie nun wieder auf Ihrer Arbeitsstation aus.  
  
    -   Die Variable *gc* speichert mehrere Koordinaten für den Times Square in New York City.  
  
    -   Die Zeile, die mit *googmap* beginnt, generiert eine Karte mit den angegebenen Koordinaten in der Mitte.  
          
  
3.  Führen Sie die Zeichenfunktion aus, und rendern Sie die Ergebnisse in Ihrer lokalen R-Umgebung. Umschließen Sie zu diesem Zweck die Diagrammfunktion in *rxExec* so wie hier gezeigt.  Die *rxExec*-Funktion wird im **RevoScaleR**-Paket eingeschlossen und unterstützt die Ausführung beliebiger R-Funktionen in einem Remotecomputekontext. 
  
    ```R  
    myplots <- rxExec(mapPlot, inDataSource, googMap, timesToRun = 1)  
    plot(myplots[[1]][["myplot"]]);  
  
    ```  
    + In der ersten Zeile können Sie sehen, dass die Kartendaten als Argument (*googMap*) an die remote ausgeführte *mapPlot*-Funktion übergeben werden. Das liegt daran, dass die Karten in Ihrer lokalen Umgebung generiert wurden und an die Funktion übergeben werden müssen, damit das Diagramm im Kontext von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellt werden kann.   
  
        Die gerenderten Daten werden anschließend zurück an die lokale R-Umgebung serialisiert, sodass Sie sie mithilfe des Fensters **Zeichnen** in RStudio oder anderen R-Grafikgeräten anzeigen können.  
  
  
4.  Hier sehen Sie das ausgegebene Diagramm, auf dem die Abholorte auf der Karte als rote Punkte markiert sind.  
  
    ![plotting taxi rides using a custom R function](../../advanced-analytics/r-services/media/rsql-e2e-mapplot.png "plotting taxi rides using a custom R function")  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 3: Erstellen der Datenfunktionen &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
