---
title: "Lektion 5: Erstellen einer einfachen Simulation (Tieferer Einblick in Data Science) | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
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
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Lektion 5: Erstellen einer einfachen Simulation (Tieferer Einblick in Data Science)
Bisher haben Sie R-Funktionen verwendet, die von SQL Server R Services bereitgestellt wurden und besonders für das Verschieben von Daten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und einem lokalen Computekontext konzipiert sind. Angenommen jedoch, Sie schreiben eine eigene benutzerdefinierte R-Funktion und möchten sie im Serverkontext ausführen.  
  
Sie können eine beliebige Funktion im Kontext des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computers aufrufen, indem Sie die *rxExec*-Funktion verwenden. Sie können auch *rxExec* verwenden, um explizit Arbeit über die Kerne eines Serverknotens zu verteilen.  
  
In dieser Lektion verwenden Sie den Remoteserver, um eine einfache Simulation zu erstellen. Die Simulation erfordert keinerlei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Daten. Das Beispiel demonstriert nur, wie Sie eine benutzerdefinierte Funktion entwerfen und sie anschließend mithilfe von *rxExec* aufrufen.  
  
Ein komplexeres Beispiel der Verwendung von *rxExec* finden Sie in diesem Artikel in englischer Sprache: [http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)  
  
## Erstellen der Funktion  
Ein bekanntes Spiel im Casino ist das Würfeln mit folgenden Regeln:  
  
-   Wenn Sie eine 7 oder 11 beim ersten Wurf würfeln, gewinnen Sie.  
  
-   Wenn Sie eine 2, 3 oder 12 würfeln, verlieren Sie.  
  
-   Wenn Sie eine 4, 5, 6, 8, 9 oder 10 würfeln, wird diese Zahl zu Ihrem Point, und Sie würfeln weiter, bis Sie entweder noch einmal Ihren Point würfeln (dann gewinnen Sie) oder eine 7 würfeln, was bedeutet, dass Sie verlieren.  
  
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
                { result <- "Loss" }    
                else if (count > 1 && roll == 7 )   
                { result <- "Loss" }    
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
  
## Erstellen der Simulation  
Um eine beliebige Funktion im Kontext des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computers auszuführen, rufen Sie die *rxExec*-Funktion auf. Obwohl *rxExec* auch die verteilte, gleichzeitige Ausführung einer Funktion auf Knoten oder Kernen eines Serverkontexts unterstützt, verwenden Sie die Funktion, um nur Ihre benutzerdefinierte Funktion auf dem Server auszuführen.  
  
1.  Rufen Sie die benutzerdefinierte Funktion als Argument für *rxExec* und einige andere Parameter auf, die die Simulation ändern.  
  
    ```R  
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")   
    length(sqlServerExec)   
    ```  
  
    -   Verwenden Sie das *timesToRun*-Argument, um anzugeben, wie oft die Funktion ausgeführt werden soll.  In diesem Fall würfeln Sie 20 Mal.  
  
    -   Die Argumente *RNGseed* und *RNGkind* können dazu verwendet werden, die Generierung von Zufallszahlen zu steuern. Wenn *RNGseed* auf **automatisch** festgelegt ist, wird ein paralleler Stream von Zufallszahlen auf jedem Worker initialisiert.  
  
2.  Die Funktion *rxExec* erstellt bei jeder Ausführung eine Liste mit einem Element, es passiert jedoch nicht viel, bis die Liste vollständig ist. Wenn alle Iterationen abgeschlossen sind, gibt die Zeile, die mit `length` beginnt, einen Wert zurück.  
  
    Sie können anschließend den nächsten Schritt ausführen, um eine Zusammenfassung Ihrer Bilanz aus gewonnenen und verlorenen Spielen abzurufen.  
  
3.  Konvertieren Sie die zurückgegebene Liste mithilfe der *unlist*-Funktion von R zu einem Vektor, und fassen Sie die Ergebnisse mithilfe der *table*-Funktion zusammen.  
  
    ```R  
    table(unlist(sqlServerExec))  
    ```  
  
    Ihre Ergebnisse sollten in etwa wie folgt aussehen:  
  
     *Verlust – Gewinn*   
     *12 – 8*  
  
## Schlussfolgerungen  
In diesem Tutorial haben Sie die folgenden Aufgaben geübt:  
  
-   Abrufen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Daten, die in Analysen verwendet werden  
  
-   Erstellen und Ändern von Datenquellen in R  
  
-   Übergeben von Modellen, Daten und Diagrammen zwischen Ihrer Arbeitsstation und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Server  
  
>  [!TIP]
> 
> Wenn Sie mit dieser Technik mithilfe eines größeren Datensatzes von 10 Millionen Beobachtungen weiter experimentieren möchten, finden Sie hier die Datendateien: [http://packages.revolutionanalytics.com/datasets](http://packages.revolutionanalytics.com/datasets).  
>   
> Um diese exemplarische Vorgehensweise mit den umfangreicheren Datendateien erneut zu verwenden, laden Sie einfach die Daten herunter, und ändern Sie die Datenquellen wie folgt:   
>  -   Legen Sie die Variablen *ccFraudCsv* und *ccScoreCsv* fest, um auf die neuen Datendateien zu verweisen     
>  -   Ändern Sie den Namen der Tabelle, auf von *sqlFraudTable* verwiesen wird, in *ccFraud10*    
>  -   Ändern Sie den Namen der Tabelle, auf von * sqlScoreTable* verwiesen wird, in *ccFraudScore10*   
  
## Vorheriger Schritt  
[Move Data between SQL Server and XDF File &#40;Data Science Deep Dive&#41; (Verschieben von Daten zwischen SQL Server und einer XDF-Datei (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
  
  
