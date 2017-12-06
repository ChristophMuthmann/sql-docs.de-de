---
title: "Abfragen und ändern Sie die SQL Server-Daten | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 8c7007a9-9a8f-4dcd-8068-40060d4f6444
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 66543db80e1d4c6255f6ac64077bfdc10b28dc5d
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="query-and-modify-the-sql-server-data"></a>Abfragen und Ändern der SQL Server-Daten

Nachdem Sie die Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geladen haben, können Sie die Datenquellen, die Sie als Argumente für R-Funktionen in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]erstellt haben, nun dazu verwenden, um grundlegende Informationen zu Variablen abzurufen und Übersichten und Histogramme zu generieren.

In diesem Schritt verwenden Sie erneut die Datenquellen zum einige schnelle Analysen durchführen und dann die Daten erweitern.

## <a name="query-the-data"></a>Abfragen der Daten

Rufen Sie zunächst eine Liste der Spalten und ihrer Datentypen ab.

1.  Verwenden Sie die Funktion **von RxGetVarInfo** , und geben Sie die Datenquelle, die Sie analysieren möchten.
  
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


## <a name="modify-metadata"></a>Ändern von Metadaten

Alle Variablen werden als Integer gespeichert, einige Variablen können aber Kategoriedaten darstellen. Diese werden in R als *Faktorvariablen* bezeichnet. Die Spalte *State* enthält beispielsweise Zahlen, die für Bezeichner für die 50 US-Bundesstaaten sowie Washington D.C. verwendet werden.  Um das Verständnis der Daten zu erleichtern, ersetzen Sie die Zahlen durch eine Liste der Abkürzungen der US-Bundesstaaten.

In diesem Schritt stellen Sie einen Zeichenfolgenvektor bereit, der die Abkürzungen enthält. Anschließend ordnen Sie diese kategorischen Werte den ursprünglichen Integerbezeichnern zu. Wenn diese Variable bereit ist, verwenden Sie das Argument *colInfo* , um anzugeben, dass diese Spalte als Faktor behandelt werden soll. Danach werden die Abkürzungen verwendet, und die Spalte wird als Faktor behandelt, wann immer diese Daten analysiert oder importiert werden.

1. Beginnen Sie folgendermaßen, indem Sie eine R-Variable, *stateAbb*, erstellen und den Zeichenfolgenvektor definieren, der ihr zugeordnet werden soll:
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. Als Nächstes erstellen Sie ein Spaltenobjekt namens *ccColInfo*, das die Zuordnung der vorhandenen Integer-Werte zu den Kategorieebenen angibt (Abkürzungen der US-Bundesstaaten).
  
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
  
3. Um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle zu erstellen, die die aktualisierten Daten verwendet, rufen Sie die Funktion *RxSqlServerData* wie zuvor auf, fügen Sie jedoch das Argument *colInfo* hinzu.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - Übergeben Sie für den *table* -Parameter die Variable *sqlFraudTable*, die die zuvor erstellte Datenquelle enthält.
    - Übergeben Sie für den *colInfo* -Parameter die Variable *ccColInfo* , die die Spaltendatentypen und Faktorebenen enthält.
    - Wenn die Spalte vor der Verwendung als Faktor zu Abkürzungen zugeordnet wird, verbessert dies auch die Leistung. Weitere Informationen finden Sie unter [R und Datenoptimierung (R-Services)](https://msdn.microsoft.com/library/mt723575.aspx).
  
4.  Die Funktion von RxGetVarInfo können jetzt die Variablen in der neuen Datenquelle anzeigen.
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **Ergebnisse**
    
    *Var 1: custID, Type: integer*
    
    *Var 2: gender-2-Faktor-Ebenen: Männlich Weiblich*
    
    *Var 3: Status 51 Faktor Ebenen: AK AL AR AZ Zertifizierungsstelle... VT WA WI WV WY*
    
    *Var 4: Karteninhabern 2-Faktor-Ebenen: Prinzipal sekundäre Datenbank*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*

Die drei von Ihnen angegebenen Variablen (_gender_, _state_und _cardholder_) werden nun wie Faktoren verarbeitet.

## <a name="next-step"></a>Nächster Schritt

[Definieren Sie und verwenden Sie Rechenkontexte](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)



