---
title: "Abfragen und &#196;ndern der SQL Server-Daten (Tieferer Einblick in Data Science) | Microsoft Docs"
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
ms.assetid: 8c7007a9-9a8f-4dcd-8068-40060d4f6444
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Abfragen und &#196;ndern der SQL Server-Daten (Tieferer Einblick in Data Science)
Nachdem Sie die Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geladen haben, können Sie die Datenquellen, die Sie als Argumente für R-Funktionen in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] erstellt haben, nun dazu verwenden, um grundlegende Informationen zu Variablen abzurufen und Übersichten und Histogramme zu generieren.  
  
In diesem Schritt verwenden Sie erneut die Datenquellen, um einige schnelle Analysen durchzuführen und die Daten zu verbessern:  
  
## Abfragen der Daten  
Rufen Sie zunächst eine Liste der Spalten und ihrer Datentypen ab.  
  
1.  Verwenden Sie die Funktion *rxGetVarInfo*, und geben Sie die Datenquelle an, die Sie analysieren möchten:  
  
    ```R  
    rxGetVarInfo(data = sqlFraudDS)   
    ```  
  
  
**Ergebnisse**  
*Var 1: custID, Type: integer*  
*Var 2: gender, Type: integer*  
*Var 3: state, Type: integer*  
*Var 4: cardholder, Type: integer*  
*Var 5: balance, Type: integer*  
*Var 6: numTrans, Type: integer*  
*Var 7: numIntlTrans, Type: integer*  
*Var 8: creditLine, Type: integer*  
*Var 9: fraudRisk, Type: integer*  
  
## Ändern von Metadaten  
Alle Variablen werden als Integer gespeichert, einige Variablen können aber Kategoriedaten darstellen. Diese werden in R als *Faktorvariablen* bezeichnet. Die Spalte *State* enthält beispielsweise Zahlen, die für Bezeichner für die 50 US-Bundesstaaten sowie Washington D.C. verwendet werden.  Um das Verständnis der Daten zu erleichtern, ersetzen Sie die Zahlen durch eine Liste der Abkürzungen der US-Bundesstaaten.  
  
In diesem Schritt stellen Sie einen Zeichenfolgenvektor bereit, der die Abkürzungen enthält. Anschließend ordnen Sie diese kategorischen Werte den ursprünglichen Integerbezeichnern zu. Wenn diese Variable bereit ist, verwenden Sie das Argument *colInfo*, um anzugeben, dass diese Spalte als Faktor behandelt werden soll. Danach werden die Abkürzungen verwendet, und die Spalte wird als Faktor behandelt, wann immer diese Daten analysiert oder importiert werden.  
  
1.  Beginnen Sie folgendermaßen, indem Sie eine R-Variable, *stateAbb*, erstellen und den Zeichenfolgenvektor definieren, der ihr zugeordnet werden soll:  
  
    ```R  
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",     
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",   
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",   
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",   
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")  
  
    ```  
  
2.  Als Nächstes erstellen Sie ein Spaltenobjekt namens *ccColInfo*, das die Zuordnung der vorhandenen Integer-Werte zu den Kategorieebenen angibt (Abkürzungen der US-Bundesstaaten).  
  
    Diese Anweisung erstellt auch Faktorvariablen für „gender“ (Geschlecht) und „cardholder“ (Karteninhaber).  
  
    ```R  
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"), 
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51), 
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )  

    ```  
  
3.  Um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenquelle zu erstellen, die die aktualisierten Daten verwendet, rufen Sie die Funktion *RxSqlServerData* wie zuvor auf, fügen Sie jedoch das Argument *colInfo* hinzu.  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,  
    table = sqlFraudTable, colInfo = ccColInfo,  
    rowsPerRead = sqlRowsPerRead)   
    ```  
  
    -   Übergeben Sie für den *table*-Parameter die Variable *sqlFraudTable*, die die zuvor erstellte Datenquelle enthält.    
    -   Übergeben Sie für den *colInfo*-Parameter die Variable *ccColInfo*, die die Spaltendatentypen und Faktorebenen enthält.
    -   Wenn die Spalte vor der Verwendung als Faktor zu Abkürzungen zugeordnet wird, verbessert dies auch die Leistung. Weitere Informationen finden Sie unter [R und Datenoptimierung (R-Services)](https://msdn.microsoft.com/library/mt723575.aspx).  
  
4.  Sie können die *rxGetVarInfo*-Funktion nun dazu verwenden, um die Variablen in der neuen Datenquelle anzuzeigen.  
  
    ```R  
    rxGetVarInfo(data = sqlFraudDS)   
    ```  
  
**Ergebnisse**  
  
*Var 1: custID, Type: integer*  
*Var 2: gender       2 factor levels: Male Female*  
*Var 3: state       51 factor levels: AK AL AR AZ CA ... VT WA WI WV WY*  
*Var 4: cardholder       2 factor levels: Principal Secondary*  
*Var 5: balance, Type: integer*  
*Var 6: numTrans, Type: integer*  
*Var 7: numIntlTrans, Type: integer*  
*Var 8: creditLine, Type: integer*  
*Var 9: fraudRisk, Type: integer*  
  
Die drei von Ihnen angegebenen Variablen (_gender_, _state_ und _cardholder_) werden nun wie Faktoren verarbeitet.  
  
## Nächster Schritt  
[Define and Use Compute Contexts &#40;Data Science Deep Dive&#41; (Definieren und Verwenden von Computekontexten (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/define-and-use-compute-contexts-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData](../../advanced-analytics/r-services/create-sql-server-data-objects-using-rxsqlserverdata.md)  
  
## Siehe auch  
[Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
