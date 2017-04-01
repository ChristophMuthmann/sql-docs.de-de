---
title: "Mithilfe von R-Code Profiling-Funktionen | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 132db249-b9f1-48f5-a63e-c9806cacc4af
caps.latest.revision: 6
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# Mithilfe von R-Code Profiling-Funktionen
Zusätzlich zur Verwendung von SQL Server-Ressourcen und Tools zum Ausführen von R-Skripts zu überwachen, können Sie Leistungstools, die von anderen R-Pakete bereitgestellt und Weitere Informationen über interne Funktionsaufrufe erhalten. Dieses Thema enthält eine Liste der grundlegenden Ressourcen können Ihnen den Einstieg erleichtern. Für Experten, empfehlen wir die Kapitel auf [Leistung](http://adv-r.had.co.nz/Performance.html) im Buch "" Erweiterte R"", indem Hadley Wickham.

## <a name="using-rprof"></a>Verwenden von RPROF

*Rprof* ist eine Funktion in das Basispaket **Utils**, die standardmäßig geladen wird. Ein Vorteil von *Rprof* dass Sampling, verringern daher die leistungsauslastung von der Überwachung ausgeführt wird.

Wenn R profiling in Ihrem Code verwenden möchten, rufen Sie diese Funktion und geben Sie die Parameter, einschließlich des Namens des Speicherorts der Protokolldatei, die geschrieben werden. Finden Sie in der Hilfe für *Rprof* für Details.

Im Allgemeinen die *Rprof* -Funktion vorgeht durch Schreiben der Aufrufliste in einer Datei, in angegebenen Intervallen. Anschließend können Sie die *SummaryRprof* Funktion, um die Ausgabedatei zu verarbeiten. 

Die profilerstellung kann ein- oder ausschalten im Code festgelegt werden. Aktivieren Sie die profilerstellung Anhalten der profilerstellung und ihn dann neu starten, verwenden Sie eine Sequenz von Aufrufen an *Rprof*:

1. Geben Sie die Profilerstellungsdaten Ausgabedatei.

    ```R
    varOutputFile <- "C:/TEMP/run001.log")
    Rprof(varOutputFile)
    ```
2. Deaktivieren Sie die profilerstellung
    ```R
    Rprof(NULL)
    ```
    
3. Starten Sie die profilerstellung
    ```R
    Rprof(append=TRUE)
    ```


> [!NOTE] Mit dieser Funktion muss Windows Perl werden installiert, auf dem Computer, auf dem Code ausgeführt wird. Aus diesem Grund wird empfohlen, dass Sie Code während der Entwicklung in ein R-Umgebung ein Profil erstellen und anschließend den gedebuggten Code mit SQL Server bereitstellen.  


## <a name="r-system-functions"></a>R-Systemfunktionen

Die Sprache "R" umfasst viele Basispaket-Funktionen für die Rückgabe des Inhalts von Systemvariablen. 

Angenommen, im Rahmen des R-Codes können `Sys.timezone` zum Abrufen der aktuellen Zeitzone oder `Sys.Time` abzurufenden die Systemzeit aus r ein. 

Zum Abrufen von Informationen über einzelne R-Systemfunktionen geben Sie den Namen der Funktion als Argument für die R `help()` Funktion einer R-Eingabeaufforderung aus.

```R
help("Sys.time")
```

## <a name="debugging-and-profiling-in-r"></a>Debuggen und Profilerstellung in R

Die Dokumentation für Microsoft R Open, die standardmäßig installiert ist, enthält eine manuelle zum Entwickeln von Erweiterungen für die Sprache "R", die profilerstellung und debugging im Detail erläutert.

Das Kapitel ist auch online verfügbar: [https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging](https://cran.r-project.org/doc/manuals/r-release/R-exts.html#Debugging)

### <a name="location-of-r-help-files"></a>Speicherort der R-Hilfedateien

C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\doc\manual


