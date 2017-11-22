---
title: Laden von Daten in den Arbeitsspeicher mit RxImport | Microsoft Docs
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
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85d6174686be113ff9a23985b1d5b5763783c986
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="load-data-into-memory-using-rximport"></a>Laden von Daten in den Arbeitsspeicher mit rxImport

Mithilfe der **rxImport** -Funktion können Daten aus einer Datenquelle in einen Datenrahmen im Arbeitsspeicher einer R-Sitzung oder in eine XDF-Datei auf einem Datenträger verschoben werden. Wenn Sie keine Datei als Ziel angeben, werden die Daten als Datenrahmen in den Arbeitsspeicher abgelegt.

In diesem Schritt erfahren Sie, wie beim Abrufen von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und klicken Sie dann die RxImport-Funktion verwenden, die zu überwachenden Daten in einer lokalen Datei zu versetzen. Auf diese Weise können Sie sie wiederholt im lokalen Computekontext analysieren, ohne die Datenbank erneut abfragen zu müssen.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extrahieren einer Teilmenge von Daten von SQL Server in den lokalen Arbeitsspeicher

Sie haben sich dazu entschieden, nur die Hochrisiko-Personen genauer zu untersuchen. Die Quelltabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist groß. Sie erhalten daher nur die Informationen über die Hochrisiko-Kunden und laden diese in einen Datenrahmen im Arbeitsspeicher der lokalen Arbeitsstation.

1. Setzen Sie den Computekontext zurück auf die lokale Arbeitsstation.

    ```R
    rxSetComputeContext("local")
    ```

2. Erstellen Sie ein neues SQL Server-Datenquellenobjekt, indem Sie eine gültige SQL­-Anweisung im *sqlQuery* -Parameter bereitstellen. In diesem Beispiel wird eine Teilmenge der Beobachtungen mit den höchsten Risikobewertungen abgerufen. Auf diese Weise werden nur die wirklich benötigten Daten im lokalen Arbeitsspeicher abgelegt.

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. Verwenden Sie die Funktion **rxImport** , um die Daten tatsächlich in einen Datenrahmen in der lokalen R-Sitzung zu laden.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Wenn der Vorgang erfolgreich war, sollte eine Statusmeldung angezeigt werden: Rows Read: 35, Total Rows Processed: 35, Total Chunk Time: 0.036 seconds.

4. Da sich nun die risikoreichsten Beobachtungen in einem Datenrahmen im Arbeitsspeicher befinden, können Sie verschiedene R-Funktionen verwenden, um den Datenrahmen zu bearbeiten. Sie können Kunden z.B. nach ihrer Risikobewertung sortieren und die Informationen über jene Kunden ausgeben, die das größte Risiko darstellen.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**Ergebnisse**

*ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*

*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*

*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*

*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*

*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*

*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*

*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*

## <a name="more-about-rximport"></a>Weitere Informationen zu rxImport

Sie können RxImport nicht nur zum Verschieben von Daten, aber zum Transformieren von Daten beim Lesen es verwenden. Beispielsweise können Sie die Anzahl von Zeichen für Spalten mit fester Breite angeben, eine Beschreibung der Variablen bereitstellen, Ebenen für Faktorspalten festlegen und sogar neue Ebenen für die Verwendung nach dem Import erstellen.

Die Funktion RxImport weist Variablennamen Spalten während des Importvorgangs, aber Sie können neue Variablennamen angeben, mit der *ColInfo* angeben, und Sie ändern von Datentypen mithilfe der *ColClasses* Parameter.

Durch die Angabe zusätzlicher Vorgänge im Parameter *transforms* können Sie jeden Datenblock, der gelesen wird, elementar verarbeiten.

## <a name="next-step"></a>Nächster Schritt

[Erstellen Sie neue SQL Server-Tabelle mit rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Transformieren von Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="see-also"></a>Siehe auch

[Machine Learning-Lernprogramme](../../advanced-analytics/tutorials/machine-learning-services-tutorials.md)

