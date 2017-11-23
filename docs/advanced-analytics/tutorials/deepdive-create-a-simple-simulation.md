---
title: 'Lektion 5: Erstellen einer einfachen Simulation (Tieferer Einblick in Data Science) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c6bad3a92aa3bf5c1e52d34b5c9f9e981c96bd87
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-simple-simulation"></a>Erstellen Sie eine einfache Simulation

Bis jetzt haben wurde Verwendung von R-Funktionen, die entwickelt wurden speziell für das Verschieben von Daten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und ein lokalen computekontext. Angenommen jedoch, Sie schreiben eine eigene benutzerdefinierte R-Funktion und möchten sie im Serverkontext ausführen.

Sie können eine beliebige Funktion im Kontext des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computers aufrufen, indem Sie die **rxExec** -Funktion verwenden. RxExec können auch explizit über Kerne in einem einzelnen Server-Knoten verteilt.

In dieser Lektion verwenden Sie den Remoteserver, um eine einfache Simulation zu erstellen. Die Simulation erfordert eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten nur wird veranschaulicht, wie eine benutzerdefinierte Funktion entwerfen, und rufen Sie anschließend mithilfe der RxExec-Funktion.

Ein komplexeres Beispiel der Verwendung von RxExec, finden Sie im Artikel: [grobe Granularität Parallelität mit Foreach und RxExec](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-function"></a>Erstellen der Funktion

Ein bekanntes Spiel im Casino ist das Würfeln mit folgenden Regeln:

- Wenn Sie eine 7 oder 11 beim ersten Wurf würfeln, gewinnen Sie.
- Wenn Sie eine 2, 3 oder 12 würfeln, verlieren Sie.
- Wenn Sie eine 4, 5, 6, 8, 9 oder 10 würfeln, wird diese Zahl zu Ihrem Point, und Sie würfeln weiter, bis Sie entweder noch einmal Ihren Point würfeln (dann gewinnen Sie) oder eine 7 würfeln, was bedeutet, dass Sie verlieren.

Das Spiel wird in R einfach simuliert, indem Sie eine benutzerdefinierte Funktion erstellen und diese anschließend mehrmals ausführen.

1.  Erstellen Sie die benutzerdefinierte Funktion mit dem folgenden R-Code:
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result \<- "Loss" }
                else if (count > 1 && roll == 7 )
                { result \<- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  Führen Sie die Funktion aus, um ein einzelnes Würfelspiel zu simulieren.
  
    ```R
    rollDice()
    ```
  
    Haben Sie gewonnen oder verloren?
  
Jetzt sehen wir uns an, wie Sie die Funktion mehrmals ausführen können, um eine Simulation zu erstellen, die dabei hilft, die Wahrscheinlichkeit eines Gewinns zu bestimmen.

## <a name="create-the-simulation"></a>Erstellen der Simulation

Eine beliebige Funktion im Kontext des auszuführenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer, rufen Sie die RxExec-Funktion. Obwohl RxExec auch verteilte Ausführung einer Funktion parallel über Knoten oder Kerne in einem Serverkontext unterstützt, verwenden hier es Sie nur für die benutzerdefinierte Funktion auf dem Server ausgeführt.

1. Rufen Sie die benutzerdefinierte Funktion als Argument für RxExec, zusammen mit einigen anderen Parametern, die die Simulation zu ändern.
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - Verwenden Sie das *timesToRun* -Argument, um anzugeben, wie oft die Funktion ausgeführt werden soll.  In diesem Fall würfeln Sie 20 Mal.
  
    - Die Argumente *RNGseed* und *RNGkind* können dazu verwendet werden, die Generierung von Zufallszahlen zu steuern. Wenn *RNGseed* auf **automatisch**festgelegt ist, wird ein paralleler Stream von Zufallszahlen auf jedem Worker initialisiert.
  
2. Die RxExec-Funktion erstellt eine Liste mit je einem Element für jede Ausführung. Sie wird nicht jedoch angezeigt, viel häufiger, bis die Liste vollständig ist. Wenn alle Iterationen abgeschlossen sind, gibt die Zeile, die mit `length` beginnt, einen Wert zurück.
  
    Sie können anschließend den nächsten Schritt ausführen, um eine Zusammenfassung Ihrer Bilanz aus gewonnenen und verlorenen Spielen abzurufen.
  
3. Konvertieren Sie die zurückgegebene Liste mithilfe der `unlist` -Funktion von R zu einem Vektor, und fassen Sie die Ergebnisse mithilfe der `table` -Funktion verwenden.
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    Ihre Ergebnisse sollten in etwa wie folgt aussehen:
  
     *Verlust Win* *12 8*

## <a name="conclusions"></a>Schlussfolgerungen

In diesem Tutorial haben Sie die folgenden Aufgaben geübt:
  
-   Abrufen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten, die in Analysen verwendet werden
  
-   Erstellen und Ändern von Datenquellen in R
  
-   Übergeben von Modellen, Daten und Diagrammen zwischen Ihrer Arbeitsstation und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Server
  
>  [!TIP]
> 
> Wenn Sie mit diesen Verfahren unter Verwendung eines größeren Datasets von 10 Millionen von Beobachtungen experimentieren möchten, stehen die Datendateien von der Website von Revolution Analytics: [Index des Datasets](http://packages.revolutionanalytics.com/datasets)
>   
> Um dieser exemplarischen Vorgehensweise mit den größeren Data-Dateien erneut zu verwenden, die Daten herunter, und ändern Sie jede der Datenquellen wie folgt:
>  - Legen Sie die Variablen *ccFraudCsv* und *ccScoreCsv* fest, um auf die neuen Datendateien zu verweisen
>  - Ändern Sie den Namen der Tabelle, auf von *sqlFraudTable* verwiesen wird, in *ccFraud10*
>  - Ändern Sie den Namen der Tabelle, auf von *sqlScoreTable* verwiesen wird, in *ccFraudScore10*

## <a name="previous-step"></a>Vorheriger Schritt

[Verschieben von Daten zwischen SQLServer und XDF-Datei](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)


