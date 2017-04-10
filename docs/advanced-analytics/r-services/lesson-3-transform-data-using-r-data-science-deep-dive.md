---
title: "Lektion 3: Umwandeln von Daten mithilfe von R (Tieferer Einblick in Data Science) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
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
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# Lektion 3: Umwandeln von Daten mithilfe von R (Tieferer Einblick in Data Science)
Das **RevoScaleR**-Paket stellt mehrere Funktionen zum Transformieren von Daten in verschiedenen Phasen der Analyse bereit:  
  
-   **rxDataStep** kann zum Erstellen und Transformieren von Datenteilmengen verwendet werden.  
  
-   **rxImport** unterstützt das Transformieren von Daten, da Daten in eine XDF-Datei importiert oder aus dieser exportiert oder in einen Datenrahmen im Arbeitsspeicher importiert werden.  
  
-   Obwohl die Funktionen **rxSummary**, **rxCube**, **rxLinMod** und **rxLogit** nicht speziell für die Datenverschiebung vorgesehen sind, unterstützen sie jedoch alle dynamische Datentransformationen.  
  
In diesem Abschnitt erfahren Sie, wie Sie diese Funktionen verwenden. Beginnen wir mit *rxDataStep*.  
  
## Verwenden von rxDataStep zum Transformieren von Variablen  
Die Funktion *rxDataStep* verarbeitet Daten abschnittsweise und liest aus einer Datenquelle und schreibt in eine andere. Sie können die Spalten angeben, die transformiert werden sollen, die zu ladenden Transformationen usw.  
  
Um dieses Beispiel interessant zu gestalten, verwenden Sie eine Funktion aus einem anderen R-Paket zum Transformieren Ihrer Daten.  Das Paket **boot** stellt eines der „empfohlenen“ Pakete dar, was bedeutet, dass **Start** in jeder Verteilung von R enthalten ist, jedoch nicht automatisch beim Starten geladen wird. Aus diesem Grund sollte das Paket schon auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verfügbar sein, die Sie mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verwenden.  
  
Aus dem Paket **boot** verwenden Sie die Funktion *inv.logit*, die die Umkehrfunktion eines Logit berechnet. Das bedeutet, dass die Funktion *inv.logit* ein Logit zurück zu einer Wahrscheinlichkeit auf der Skala [0,1] konvertiert.  
  
> [!TIP]  
> Eine andere Möglichkeit, Vorhersagen auf dieser Skala zu erhalten, wäre den Parameter *type* auf **response** im ursprünglichen Aufruf von *rxPredict* festzulegen.  
  
1.  Erstellen Sie zunächst eine Datenquelle, die die Daten aufnimmt, die für die Tabelle *ccScoreOutput* bestimmt sind.  
  
    ```R  
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )  
  
    ```  
  
2.  Fügen Sie eine weitere Datenquelle hinzu, um die Daten für die Tabelle ccScoreOutput2 aufzunehmen.  
  
    ```R  
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )  
  
    ```  
  
    In der neuen Tabelle erhalten Sie alle Variablen aus der vorherigen Tabelle *ccScoreOutput* sowie die neu erstellte Variable.  
  
3.  Legen Sie den Computekontext auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz fest.  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
  
    ```  
  
4.  Verwenden Sie die Funktion *rxSqlServerTableExists*, um zu überprüfen, ob die Ausgabetabelle *ccScoreOutput2* bereits vorhanden ist, und verwenden Sie, falls dies der Fall ist, die Funktion *rxSqlServerDropTable* zum Löschen der Tabelle.  
  
    ```R    
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")  
  
    ```  
  
5.  Rufen Sie die Funktion *rxDataStep* auf, und geben Sie die gewünschten Transformationen in einer Liste an.  
  
    ```R  
    rxDataStep(inData = sqlOutScoreDS,   
        outFile = sqlOutScoreDS2,         
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),        
        transformPackages = "boot",   
        overwrite = TRUE)    
    ```  
  
    Wenn Sie die Transformationen definieren, die für die einzelnen Spalten angewendet werden, können Sie auch alle zusätzlichen R-Pakete angeben, die für die Durchführung der Transformationen notwendig sind.  Weitere Informationen zu den Arten von Transformationen, die Sie ausführen können, finden Sie unter [Transforming and Subsetting Data (Transformieren von Daten und Erstellen von Teilmengen)](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform).
  
6.  Rufen Sie *rxGetVarInfo* auf, um eine Zusammenfassung der Variablen im neuen Dataset anzuzeigen.  
  
    ```R  
    rxGetVarInfo(sqlOutScoreDS2)  
    ```  
  
**Ergebnisse**  
  
*Var 1: ccFraudLogitScore, Type: numeric*  
*Var 2: state, Type: character*  
*Var 3: gender, Type: character*  
*Var 4: cardholder, Type: character*  
*Var 5: balance, Type: integer*  
*Var 6: numTrans, Type: integer*  
*Var 7: numIntlTrans, Type: integer*  
*Var 8: creditLine, Type: integer*  
*Var 9: ccFraudProb, Type: numeric*  
  
Die ursprünglichen Logit-Ergebnisse werden beibehalten, jedoch wurde eine neue Spalte, *ccFraudProb*, hinzugefügt, in der die Logit-Ergebnisse als Werte zwischen 0 und 1 dargestellt sind. 

Beachten Sie, dass die Faktorvariablen als Zeichendaten in die Tabelle *ccScoreOutput2* geschrieben wurden.  Um diese als Faktoren in nachfolgenden Analysen zu verwenden, geben Sie die Ebenen mit dem Parameter *colInfo* an.  

  
## Nächster Schritt  
[Laden von Daten in den Arbeitsspeicher mit rxImport &#40;Tieferer Einblick in Data Science&#41;](../../advanced-analytics/r-services/load-data-into-memory-using-rximport-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Lektion 2: Create and Run R Scripts &#40;Data Science Deep Dive&#41; (Erstellen und Ausführen von R-Skripts (Tieferer Einstieg in Data Science))](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
  
  
