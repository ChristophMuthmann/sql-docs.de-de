---
title: "Verschieben von Daten zwischen SQL Server und einer XDF-Datei (Tieferer Einblick in Data Science) | Microsoft Docs"
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
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Verschieben von Daten zwischen SQL Server und einer XDF-Datei (Tieferer Einblick in Data Science)
Wenn Sie in einem lokalen Computekontext arbeiten, haben Sie sowohl Zugriff auf lokale Datendateien als auch auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank (als eine *RxSqlServerData*-Datenquelle definiert).  
  
In diesem Abschnitt erfahren Sie, wie Daten abgerufen und in einer Datei auf dem lokalen Computer gespeichert werden, sodass Sie die Daten transformieren können. Wenn Sie fertig sind, verwenden Sie die Daten in der Datei, um eine neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle mithilfe von *rxDataStep* zu erstellen.  
  
## Erstellen einer SQL Server-Tabelle aus einer XDF-Datei  

Mit der Funktion *rxImport* können Sie Daten aus einer beliebigen unterstützten Datenquelle in eine lokale XDF-Datei importieren. Die Verwendung einer lokalen Datei eignet sich, wenn Sie verschiedene Analysen der in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank gespeicherten Daten ausführen oder verhindern möchten, dass dieselbe Abfrage immer wieder ausgeführt wird.  
  
Verwenden Sie für diese Übung wieder die Daten über Kreditkartenbetrug. In diesem Szenario wurden Sie gebeten, zusätzliche Analysen für Benutzer in den US-Bundesstaaten Kalifornien, Oregon und Washington durchzuführen. Sie haben sich der Effizienz halber dazu entschieden, Daten nur für diese Bundesstaaten auf Ihrem lokalen Computer zu speichern und mit den Variablen „gender“ (Geschlecht), „cardholder“ (Karteninhaber/in), „state“ (Bundesstaat) und „balance“ (Kontostand) zu arbeiten.  
  
1.  Verwenden Sie erneut den Vektor *stateAbb*, den Sie vorher erstellt haben, um die einzuschließenden Ebenen zu identifizieren und die neue Variable *statesToKeep* anschließend in der Konsole auszugeben.  
  
    ```  
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)   
  
    statesToKeep  
  
    ```  
 **Ergebnisse**
CA |  OR  | WA 
-- | -- | --
 5 |  38  | 48 
  
2.  Nun definieren Sie die Daten, die mithilfe einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage von SQL Server übermittelt werden sollen.  Später verwenden Sie diese Variable als das *inData*-Argument für *rxImport*.  
  
    ```R  
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")  
  
    ```  
  
    Stellen Sie sicher, dass keine ausgeblendeten Zeichen, wie z. B. Zeilenvorschübe oder Registerkarten, in der Abfrage vorhanden sind.  
  
3.  Als Nächstes definieren Sie die Spalten, die beim Arbeiten mit Daten in R verwenden werden sollen.  
  Im kleineren Dataset benötigen Sie z.B. nur drei Faktorebenen, da die Abfrage nur Daten für drei Bundesstaaten zurückgeben wird.  Sie können die *statesToKeep*-Variable erneut verwenden, um die richtigen Ebenen zu identifizieren, die eingeschlossen werden sollen.  
  
    ```R  
    importColInfo <- list(   
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),       
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),     
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))   
            )  
  
    ```  
  
4.  Legen Sie den Computekontext auf **local** fest, da Sie möchten, dass alle Daten auf Ihrem lokalen Computer verfügbar sind.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
5.  Erstellen Sie das Datenquellenobjekt, indem Sie alle Variablen, die Sie soeben als Argumente definiert haben, an *RxSqlServerData* übergeben.  
  
    ```R  
    sqlServerImportDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        sqlQuery = importQuery,   
        colInfo = importColInfo)  
  
    ```  
  
6.  Rufen Sie anschließend *rxImport* auf, um die Daten im aktuellen Arbeitsverzeichnis in einer Datei namens `ccFraudSub.xdf` zu speichern.  
  
    ```R  
    localDS <- rxImport(inData = sqlServerImportDS,   
        outFile = "ccFraudSub.xdf",    
        overwrite = TRUE)  
  
    ```  
  
    Das Objekt *localDs*, das von der Funktion *rxImport* zurückgegeben wird, ist ein kompaktes *RxXdfData*-Datenquellenobjekt, das die „ccFraud.xdf“-Datendatei darstellt, die lokal auf dem Datenträger gespeichert ist.  
  
7.  Rufen Sie *rxGetVarInfo* für die XDF-Datei auf, um zu überprüfen, ob das Schema identisch ist.  
  
    ```R  
    rxGetVarInfo(data = localDS)   
    ```  
    **Ergebnisse**
    
    *rxGetVarInfo(data = localDS)*    
    *Var 1: gender, Type: factor, no factor levels available*    
    *Var 2: cardholder, Type: factor, no factor levels available*    
    *Var 3: balance, Type: integer, Low/High: (0, 22463)*    
    *Var 4: state, Type: factor, no factor levels available*
  
8.  Sie können nun verschiedene R-Funktionen aufrufen, um das *localDs*-Objekt zu analysieren, so Sie wie die auch mit den Quelldaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfahren würden. Beispiel:  
  
    ```R  
    rxSummary(~gender + cardholder + balance + state, data = localDS)    
    ```  
  
Da Sie nun wissen, wie Computekontexte verwendet werden und die Arbeit mit verschiedenen Datenquellen kennen, ist es an der Zeit, etwas lustiges auszuprobieren.  
  
In der nächsten, finalen Lektion, werden Sie eine einfache Simulation mit einer benutzerdefinierten R-Funktion erstellen und sie auf dem Remoteserver ausführen.  
  
## Nächster Schritt  
[Lektion 5: Create a Simple Simulation &#40;Data Science Deep Dive&#41; (Erstellen einer einfachen Simulation (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Lektion 4: Analyze Data in Local Compute Context &#40;Data Science Deep Dive&#41; (Analysieren von Daten in einem lokalen Computekontext (Tieferer Einblick in Data Science))](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## Siehe auch  
[Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
