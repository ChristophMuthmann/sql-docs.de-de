---
title: "Laden von Daten in den Arbeitsspeicher mit rxImport (Tieferer Einblick in Data Science) | Microsoft Docs"
ms.custom: ""
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
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Laden von Daten in den Arbeitsspeicher mit rxImport (Tieferer Einblick in Data Science)
Mithilfe der *rxImport*-Funktion können Daten aus einer Datenquelle in einen Datenrahmen im Arbeitsspeicher einer R-Sitzung oder in eine XDF-Datei auf einem Datenträger verschoben werden. Wenn Sie keine Datei als Ziel angeben, werden die Daten als Datenrahmen in den Arbeitsspeicher abgelegt.  
  
In diesem Schritt erfahren Sie, wie Sie Daten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abrufen und anschließend die Funktion *rxImport* verwenden, um die zu überwachenden Daten in einer lokalen Datei abzulegen. Auf diese Weise können Sie sie wiederholt im lokalen Computekontext analysieren, ohne die Datenbank erneut abfragen zu müssen.  
  
## Extrahieren einer Teilmenge von Daten von SQL Server in den lokalen Arbeitsspeicher  
Sie haben sich dazu entschieden, nur die Hochrisiko-Personen genauer zu untersuchen. Die Quelltabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist groß. Sie erhalten daher nur die Informationen über die Hochrisiko-Kunden und laden diese in einen Datenrahmen im Arbeitsspeicher der lokalen Arbeitsstation.  
  
1.  Setzen Sie den Computekontext zurück auf die lokale Arbeitsstation.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  Erstellen Sie ein neues SQL Server-Datenquellenobjekt, indem Sie eine gültige SQL­-Anweisung im *sqlQuery*-Parameter bereitstellen. In diesem Beispiel wird eine Teilmenge der Beobachtungen mit den höchsten Risikobewertungen abgerufen. Auf diese Weise werden nur die wirklich benötigten Daten im lokalen Arbeitsspeicher abgelegt.  
  
    ```R    
    sqlServerProbDS <- RxSqlServerData(       
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",  
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)   
    ```  
  
3.  Verwenden Sie die Funktion *rxImport*, um die Daten tatsächlich in einen Datenrahmen in der lokalen R-Sitzung zu laden.  
  
    ```R  
    highRisk <- rxImport(sqlServerProbDS)   
    ```  
     Wenn der Vorgang erfolgreich war, sollte eine Statusmeldung angezeigt werden: Rows Read: 35, Total Rows Processed: 35, Total Chunk Time: 0.036 seconds. 
   
4.  Da sich nun die risikoreichsten Beobachtungen in einem Datenrahmen im Arbeitsspeicher befinden, können Sie verschiedene R-Funktionen verwenden, um den Datenrahmen zu bearbeiten. Sie können Kunden z.B. nach ihrer Risikobewertung sortieren und die Informationen über jene Kunden ausgeben, die das größte Risiko darstellen.  
  
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
  
## Weitere Informationen zu rxImport  
Sie können *rxImport* nicht nur zum Verschieben von Daten verwenden, sondern auch, um Daten während des Auslesens zu transformieren. Beispielsweise können Sie die Anzahl von Zeichen für Spalten mit fester Breite angeben, eine Beschreibung der Variablen bereitstellen, Ebenen für Faktorspalten festlegen und sogar neue Ebenen für die Verwendung nach dem Import erstellen.  
  
Die Funktion *rxImport* weist den Spalten während des Importprozesses Variablennamen zu. Sie können jedoch auch neue Variablennamen angeben, indem Sie den *colInfo*-Parameter verwenden oder Datentypen mithilfe des *colClasses*-Parameters ändern.  
  
Durch die Angabe zusätzlicher Vorgänge im Parameter *transforms* können Sie jeden Datenblock, der gelesen wird, elementar verarbeiten.  
  
## Nächster Schritt  
[Create New SQL Server Table using rxDataStep &#40;Data Science Deep Dive&#41; (Erstellen einer neuen SQL Server-Tabelle mit rxDataStep (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/create-new-sql-server-table-using-rxdatastep-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Lektion 3: Transform Data Using R &#40;Data Science Deep Dive&#41; (Umwandeln von Daten mithilfe von R (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## Siehe auch  
[SQL Server R Services-Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
