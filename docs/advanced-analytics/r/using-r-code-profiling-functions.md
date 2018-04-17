---
title: Mithilfe von R-Code profilerstellung Funktionen (SQL Server-Machine Learning) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 05689ae356d415f9655b8709c619e40e6d8fa817
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-r-code-profiling-functions"></a>Mithilfe von R-Code, die profilerstellung für Funktionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neben SQL Server-Ressourcen und Tools zum Überwachen von R-Skriptausführung können Sie auch Leistungstools von anderen R-Paketen verwenden, um weitere Informationen zu internen Funktionsaufrufen zu erhalten. Dieses Thema enthält eine Übersicht über einige grundlegende Ressourcen, die Ihnen den Einstieg erleichtern. Für eine Anleitung durch einen Experten empfehlen wir das Kapitel über [Performance](http://adv-r.had.co.nz/Performance.html) (Leistung) im Buch „Advanced R“ von Hadley Wickham.

## <a name="using-rprof"></a>Verwenden von RPROF

Die *rprof*-Funktion ist im Basispaket **utils** enthalten, das standardmäßig geladen wird. Ein Vorteil von *rprof* ist, dass die Funktion Sampling durchführt und dadurch die Leistungsauslastung der Überwachung verringert wird.

Zur Verwendung der R-Profilerstellung in Ihrem Code rufen Sie diese Funktion auf und geben ihre Parameter an, darunter auch den Namen des Speicherorts der Protokolldatei, die geschrieben wird. Weitere Informationen finden Sie in der Hilfe zu *rprof*.

Im Allgemeinen schreibt die *rprof*-Funktion die Aufrufliste in bestimmten Intervallen in eine Datei. Anschließend können Sie die *summaryRprof*-Funktion verwenden, um die Ausgabedatei zu verarbeiten. 

Die Profilerstellung kann im Code aktiviert oder deaktiviert werden. Zum Aktivieren der Profilerstellung oder zum Anhalten und Neustarten der Profilerstellung verwenden Sie eine Sequenz von Aufrufen an *rprof*:

1. Ausgabedatei für die Profilerstellung angeben

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. Profilerstellung aktivieren
    ```R
    Rprof(NULL)
    ```
    
3. Profilerstellung neu starten
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE]
> Für die Verwendung dieser Funktion ist es erforderlich, dass Windows Perl auf dem Computer installiert ist, auf dem der Code ausgeführt wird. Deshalb wird empfohlen, dass Sie Code während der Entwicklung in einer R-Umgebung erstellen und dann den gedebuggten Code an SQL Server bereitstellen.  


## <a name="r-system-functions"></a>R-Systemfunktionen

Die R-Sprache umfasst viele Basispaketfunktionen für die Rückgabe des Inhalts von Systemvariablen. 

Als Teil des R-Codes können Sie zum Beispiel `Sys.timezone` zum Abrufen der aktuellen Zeitzone oder `Sys.Time` zum Abrufen der Systemzeit von R verwenden. 

Informationen zu einzelnen R-Systemfunktionen können Sie erhalten, indem Sie den Namen der Funktion als Argument für die R-`help()`-Funktion von einer R-Eingabeaufforderung aus eingeben.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>Debuggen und Profilerstellung in R

Die Dokumentation für Microsoft R Open, die standardmäßig installiert ist, enthält ein Handbuch zum Entwickeln von Erweiterungen für die R-Sprache, in dem Profilerstellung und Debuggen im Detail erläutert werden.

Das Kapitel ist auch online zur Verfügung: [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>Speicherort der R-Hilfedateien

C:\Programme\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\doc\manual



