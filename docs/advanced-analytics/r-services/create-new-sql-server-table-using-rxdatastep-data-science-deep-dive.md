---
title: "Erstellen einer neuen SQL Server-Tabelle mit rxDataStep (Tieferer Einblick in Data Science) | Microsoft Docs"
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
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Erstellen einer neuen SQL Server-Tabelle mit rxDataStep (Tieferer Einblick in Data Science)
In dieser Lektion erfahren Sie, wie Sie Daten zwischen In-Memory-Datenrahmen, dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Kontext und lokale Dateien verschieben.  
  
> [!NOTE]  
> In dieser Lektion verwenden Sie ein anderes Dataset. Das Dataset der Verspätungen der Fluggesellschaft ist ein öffentliches Dataset, das hauptsächlich für Experimente im maschinellen Lernen verwendet wird. Wenn Sie gerade erst mit R beginnen, ist dieses Dataset nützlich, um es für Tests zur Hand zu haben, denn es wird in verschiedenen Produktbeispielen für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] verwendet, die unter [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] veröffentlicht wurden. Die Datendateien, die Sie für dieses Beispiel benötigen, sind in demselben Verzeichnis wie die anderen Produktbeispiele verfügbar.  
  
## Erstellen einer SQL Server-Tabelle aus den lokalen Daten  
In der ersten Lektion dieses Tutorials verwendeten Sie die Funktion *RxTextData* zum Importieren von Daten aus einer Textdatei in R und anschließend die Funktion *RxDataStep* zum Verschieben der Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
In dieser Lektion verwenden Sie eine andere Herangehensweise und rufen Daten aus einer Datei ab, die im [XDF-Format](https://en.wikipedia.org/wiki/Extensible_Data_Format) gespeichert ist. Das XDF-Format ist ein XML-Standard für mehrdimensionale Daten. Dies ist ein binäres Dateiformat mit einer R-Schnittstelle, die die Verarbeitung und Analyse von Zeilen und Spalten optimiert.  Sie können es für das Verschieben von Daten verwenden, um Teilmengen von Daten zu speichern, die für Analysen hilfreich sind.
  
Nach einigen einfachen Transformationen der Daten mithilfe der XDF-Datei, speichern Sie die transformierten Daten in eine neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle.  
  
> [!NOTE]  
> Sie benötigen DDL-Berechtigungen für diesen Schritt.  
  
1.  Legen Sie den Computekontext auf die lokale Arbeitsstation fest.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  Definieren Sie ein neues Datenquellenobjekt mithilfe der *RxXdfData*-Funktion. Für eine XDF-Datenquelle geben Sie einfach den Pfad zur Datendatei an.  Sie können den Pfad zu der Datei mit einer Textvariablen angeben, aber in diesem Fall besteht eine praktische Kurzform, da sich die Datei mit den Beispieldaten (AirlineDemoSmall.xdf) in dem Verzeichnis befindet, das von *rxGetOption* zurückgegeben wird.
  
    ```R  
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))   
    ```  
  
  
3.  Rufen Sie *rxGetVarInfo* für die Daten im Arbeitsspeicher auf, um eine Zusammenfassung des Datasets anzuzeigen.  
  
    ```R  
    rxGetVarInfo(xdfAirDemo)    
    ```  
  
**Ergebnisse**  
  
*Var 1: ArrDelay, Typ: ganze Zahl, Min/Max: (-86, 1490)*   
*Var 2: CRSDepTime, Typ: numerisch, Speicher: float32, Min/Max: (0.0167, 23.9833)*   
*Var 3: DayOfWeek 7 Faktorebenen: Montag Dienstag Mittwoch Donnerstag Freitag Samstag Sonntag*  

> [!NOTE]
> 
> Haben Sie bemerkt, dass Sie keine anderen Funktionen aufrufen mussten, um die Daten in die XDF-Datei zu laden, und die Funktion *rxGetVarInfo* sofort auf die Daten anwenden konnten? Das liegt daran, dass XDF die Standardmethode für die Zwischenspeicherung für RevoScaleR ist. Weitere Informationen zu XDF-Dateien finden Sie im [Leitfaden für die ersten Schritte mit ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform#using-the-data-step-to-create-an-xdf-file-from-a-data-frame). 
  
4.  Nun fügen Sie diese Daten in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle, speichern _DayOfWeek_ als ganze Zahl mit Werten von 1 bis 7.  
  
    Zu diesem Zweck müssen Sie zunächst eine SQL Server-Datenquelle definieren.  
  
    ```R  
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)   
    ```  
  
5.  Überprüft, ob eine Tabelle mit dem gleichen Namen vorhanden ist und löscht diese Tabelle, falls vorhanden.  
  
    ```R  
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)    
    ```  
  
6.  Tabelle erstellen und Daten laden mithilfe von `rxDataStep`.  
  
    ```R  
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,    
            transforms = list( DayOfWeek = as.integer(DayOfWeek),   
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),   
            overwrite = TRUE )    
    ```  
  
7.  Setzt den Computekontext auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Computer zurück.  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
8.  Definiert eine Teilmenge der Daten mithilfe einer einfachen SQL­Anweisung.  
  
    ```R    
    SqlServerAirDemo <- RxSqlServerData(  
        sqlQuery = "SELECT * FROM AirDemoSmallTest",      
        connectionString = sqlConnString,   
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))    
    ```  
  
9. Ruf *rxSummary* auf, um eine Zusammenfassung der Daten in der Abfrage zu überprüfen.  
  
    ```R  
    rxSummary(~., data = sqlServerAirDemo)   
    ```  
  
## Nächster Schritt  
[Ausführen einer Block erstellenden Analyse mithilfe von rxDataStep &#40;Tieferer Einblick in Data Science&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Laden von Daten in den Arbeitsspeicher mit rxImport &#40;Tieferer Einblick in Data Science&#41;](../../advanced-analytics/r-services/load-data-into-memory-using-rximport-data-science-deep-dive.md)  
  
## Siehe auch  
[Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
