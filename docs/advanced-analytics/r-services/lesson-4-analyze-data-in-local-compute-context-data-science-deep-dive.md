---
title: "Lektion 4: Analysieren von Daten in einem lokalen Computekontext (Tieferer Einblick in Data Science) | Microsoft Docs"
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
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Lektion 4: Analysieren von Daten in einem lokalen Computekontext (Tieferer Einblick in Data Science)
Obwohl es in der Regel viel schneller geht, komplexen R-Code mithilfe des Serverkontexts auszuführen, ist es manchmal bequemer, die Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abzurufen und sie auf Ihrer privaten Arbeitsstation zu analysieren.  
  
In diesem Abschnitt erfahren Sie, wie Sie zurück zu einem lokalen Computekontext wechseln und Daten zwischen den Kontexten zum Optimieren der Leistung verschieben können.  
  
## Erstellen eines lokales Verzeichnisses  
  
1.  Ändern Sie den Computekontext, damit all Ihre Arbeit lokal ausgeführt wird.  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
2.  Beim Extrahieren von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], erhalten Sie häufig eine bessere Leistung durch Erhöhen der Anzahl von Zeilen, die bei jedem Lesevorgang extrahiert werden.  Erhöhen Sie hierzu den Wert für den Parameter *rowsPerRead* in der Datenquelle.  
  
    ```R  
    sqlServerDS1 <- RxSqlServerData(  
       connectionString = sqlConnString,        
       table = sqlFraudTable,   
       colInfo = ccColInfo,   
       rowsPerRead = 10000)  
    ```  
  
    Zuvor war der Wert von *rowsPerRead* auf 5000 festgelegt.  
  
3.  Rufen Sie nun *rxSummary* für die neue Datenquelle auf.  
  
    ```R  
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)    
    ```  
  
    Die tatsächlichen Ergebnisse sollten denen entsprechen, die beim Ausführen von *rxSummary* im Kontext des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computers ausgegeben werden.  Der Vorgang kann jedoch schneller oder langsamer sein. Dies hängt hauptsächlich von der Verbindung zu Ihrer Datenbank ab, da die Daten für die Analyse auf Ihren lokalen Computer übertragen werden.  
  

## Nächster Schritt  
[Move Data between SQL Server and XDF File &#40;Data Science Deep Dive&#41; (Verschieben von Daten zwischen SQL Server und einer XDF-Datei (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Ausführen einer Block erstellenden Analyse mithilfe von rxDataStep &#40;Tieferer Einblick in Data Science&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
  
  
