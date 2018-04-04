---
title: Analysieren von Daten im lokalen computekontext (SQL und R deep Dive) | Microsoft Docs
ms.date: 12/18/2017
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
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: e521ae9ab359ac210383cfb56ded80da4ed181ff
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="analyze-data-in-local-compute-context-sql-and-r-deep-dive"></a>Analysieren von Daten im lokalen computekontext (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

In diesem Abschnitt erfahren Sie, wie an einen lokalen computekontext wechseln, und Verschieben von Daten zwischen den Kontexten zum Optimieren der Leistung.

Obwohl i komplexe R-Code unter Verwendung des Serverkontexts ausführen schneller sein kann, in einigen Fällen ist es sinnvoller zum Abrufen der Daten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und analysieren Sie ihn auf einer lokalen Arbeitsstation.

## <a name="create-a-local-summary"></a>Erstellen einer lokalen Zusammenfassung

1. Ändern Sie den Computekontext, damit all Ihre Arbeit lokal ausgeführt wird.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Beim Extrahieren von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], erhalten Sie häufig eine bessere Leistung durch Erhöhen der Anzahl von Zeilen, die bei jedem Lesevorgang extrahiert werden.  Erhöhen Sie hierzu den Wert für den Parameter *rowsPerRead* in der Datenquelle. Zuvor war der Wert von *rowsPerRead* auf 5000 festgelegt.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. Rufen Sie **RxSummary** für die neue Datenquelle.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    Die tatsächlichen Ergebnisse sollten denen entsprechen, die beim Ausführen von **rxSummary** im Kontext des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computers ausgegeben werden.  Der Vorgang kann jedoch schneller oder langsamer sein. Dies hängt hauptsächlich von der Verbindung zu Ihrer Datenbank ab, da die Daten für die Analyse auf Ihren lokalen Computer übertragen werden.

## <a name="next-step"></a>Nächster Schritt

[Verschieben von Daten zwischen SQL Server und XDF-Datei](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Blockweises Analysieren mithilfe von rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
