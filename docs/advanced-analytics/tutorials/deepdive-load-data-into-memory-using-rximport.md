---
title: Laden von Daten in den Arbeitsspeicher mit RxImport (SQL und R deep Dive) | Microsoft Docs
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 68e9533509c731b9cddff737a4db120be0dc86b8
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="load-data-into-memory-using-rximport-sql-and-r-deep-dive"></a>Laden von Daten in den Arbeitsspeicher mit RxImport (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

Die [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) -Funktion kann verwendet werden, um Daten aus einer Datenquelle in einem Datenrahmen im Arbeitsspeicher der Sitzung oder in einer XDF-Datei auf dem Datenträger zu verschieben. Wenn Sie keine Datei als Ziel angeben, werden die Daten als Datenrahmen in den Arbeitsspeicher abgelegt.

In diesem Schritt erfahren Sie, wie beim Abrufen von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und verwenden Sie dann die **RxImport** Funktion, die zu überwachenden Daten in einer lokalen Datei zu versetzen. Auf diese Weise können Sie sie wiederholt im lokalen Computekontext analysieren, ohne die Datenbank erneut abfragen zu müssen.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extrahieren Sie eine Teilmenge der Daten aus SQL Server in den lokalen Speicher

Sie haben sich entschieden, dass Sie nur die hohes Risiko Personen ausführlicher untersuchen möchten. Die Quelltabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] groß ist, damit die Informationen nur mit hohem Risiko Kunden abgerufen werden soll. Sie laden dann diese Daten in einem Datenrahmen im Speicher des lokalen Arbeitsstation.

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

3. Rufen Sie die Funktion [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) zum Lesen der Daten in einem Datenrahmen in der lokalen R-Sitzung.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Wenn der Vorgang erfolgreich war, sollte eine Statusmeldung an, wie die folgende angezeigt: "Zeilen lesen: 35, insgesamt Zeilen verarbeitet: 35, Segment Gesamtzeit: 0.036 Sekunden"

4. Mit hohem Risiko Beobachtungen in einer in-Memory-Datenrahmen sind, können Sie verschiedene R-Funktionen, die Datenrahmen zu bearbeiten. Sie können z. B. Kunden nach ihrer risikobewertung sortieren und Drucken eine Liste der Kunden, die das höchste Risiko darstellen.

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

Sie können **rxImport** nicht nur zum Verschieben von Daten verwenden, sondern auch, um Daten während des Auslesens zu transformieren. Beispielsweise können Sie die Anzahl von Zeichen für Spalten mit fester Breite angeben, eine Beschreibung der Variablen bereitstellen, Ebenen für Faktorspalten festlegen und sogar neue Ebenen für die Verwendung nach dem Import erstellen.

Die **RxImport** Funktion weist Variablennamen zu Spalten während des Importvorgangs, aber Sie können neue Variablennamen angeben, mit der *ColInfo* -Parameters an, oder Ändern von Datentypen mithilfe von der *ColClasses* Parameter.

Durch die Angabe zusätzlicher Vorgänge im Parameter *transforms* können Sie jeden Datenblock, der gelesen wird, elementar verarbeiten.

## <a name="next-step"></a>Nächster Schritt

[Erstellen einer neuen SQL Server-Tabelle mit rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Umwandeln von Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

