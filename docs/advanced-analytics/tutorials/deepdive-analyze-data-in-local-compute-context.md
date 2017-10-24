---
title: Analysieren von Daten im lokalen Computekontext | Microsoft Docs
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1efbf5b6d3835759ccce74c820ea2829e6fa41dc
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="analyze-data-in-local-compute-context-data-science-deep-dive"></a>Analysieren von Daten im lokalen Computekontext (Data Science Deep Dive)

Dennoch ist es schneller möglicherweise komplexe R-Code unter Verwendung des Serverkontexts ausführen, manchmal ist es einfach bequemer zum Abrufen der Daten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und analysieren Sie ihn auf Ihrer privaten Arbeitsstation.

In diesem Abschnitt erfahren Sie, wie Sie zurück zu einem lokalen Computekontext wechseln und Daten zwischen den Kontexten zum Optimieren der Leistung verschieben können.

## <a name="create-a-local-summary"></a>Erstellen eines lokales Verzeichnisses

1. Ändern Sie den Computekontext, damit all Ihre Arbeit lokal ausgeführt wird.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Beim Extrahieren von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], erhalten Sie häufig eine bessere Leistung durch Erhöhen der Anzahl von Zeilen, die bei jedem Lesevorgang extrahiert werden.  Erhöhen Sie hierzu den Wert für den Parameter *rowsPerRead* in der Datenquelle.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```
  
    Zuvor war der Wert von *rowsPerRead* auf 5000 festgelegt.
  
3. Rufen Sie nun **rxSummary** für die neue Datenquelle auf.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    Die tatsächlichen Ergebnisse sollten beim Ausführen von RxSummary im Kontext der identisch sein der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer.  Der Vorgang kann jedoch schneller oder langsamer sein. Dies hängt hauptsächlich von der Verbindung zu Ihrer Datenbank ab, da die Daten für die Analyse auf Ihren lokalen Computer übertragen werden.


## <a name="next--step"></a>Nächster Schritt

[Verschieben von Daten zwischen SQLServer und XDF-Datei](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Führen Sie die Segmentierung Analysen mit RxDataStep aus](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)



