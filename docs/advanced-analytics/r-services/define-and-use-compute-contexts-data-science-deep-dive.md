---
title: "Definieren und Verwenden von berechneten Kontexten (Tieferer Einblick in Data Science) | Microsoft Docs"
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
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Definieren und Verwenden von berechneten Kontexten (Tieferer Einblick in Data Science)
Sie haben sich entschieden, dass einige der komplexeren Berechnungen auf dem Server statt auf dem lokalen Computer ausgeführt werden sollen. Zu diesem Zweck müssen Sie einen Computekontext erstellen, mit dem Sie R-Code auf dem Server ausführen können.  
  
Die [RxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver)-Funktion ist eine der erweiterten R-Funktionen im [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)-Paket. Die Funktion behandelt die Aufgaben bei der Erstellung der Datenbank-Verbindung und das Übergeben von Objekten zwischen dem lokalen Computer und dem Remote-Ausführungskontext.  
  
In diesem Schritt erfahren Sie, wie Sie die *RxInSqlServer*-Funktion zur Definition eines Computekontexts in Ihrem R-Code verwenden.  


  
## Erstellen und Festlegen eines Computekontexts  
Um einen Computerkontext zu erstellen, benötigen Sie die folgenden grundlegenden Informationen über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz:  
  
-   Die Verbindungszeichenfolge für die Instanz  
-   Eine Spezifikation für die Verarbeitung der Ausgabe  
-   Optionale Argumente für das Aktivieren der Ablaufverfolgung oder für die Angabe eines freigegebenen Verzeichnisses


 Fangen wir an.

1.  Geben Sie die Verbindungszeichenfolge für die Instanz an, in der Berechnungen stattfinden sollen.  Dies ist nur eine der vielen Variablen, die Sie der *RxInSqlServer*-Funktion zum Erstellen des Computekontexts übergeben. 

    **Verwenden einer SQL-Anmeldung**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>" 
      ```

    **Verwenden der integrierten Windows-Authentifizierung**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"" 
      ```
2.  Geben Sie an, wie die Ausgabe behandelt werden soll. Im folgenden Code geben Sie an, dass die R-Sitzung auf der Arbeitsstation immer auf R-Auftragsergebnisse warten soll, aber keine Konsolenausgaben aus Remoteberechnungen zurückgegeben werden sollen.  
  
    ```R  
    sqlWait <- TRUE   
    sqlConsoleOutput <- FALSE   
    ```  
  
    Das Argument *wait* für *RxInSqlServer* unterstützt diese Optionen:  
  
    -   **TRUE**. Der Auftrag wird blockiert und nicht zurückgegeben, bis er abgeschlossen wurde oder ein Fehler aufgetreten ist.  Weitere Informationen zu blockierenden und nicht-blockierenden Aufträgen finden Sie unter 
  
    -   **FALSE**. Aufträge werden nicht blockierend und sofort zurückgegeben, sodass Sie weiterhin anderen R-Code ausführen können. Jedoch auch im nicht blockierenden Modus muss die Clientverbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrechterhalten werden, während der Auftrag ausgeführt wird.  

3. Optional können Sie ein lokales Verzeichnis angeben, das für den freigegebenen Gebrauch von der lokale R-Sitzung und vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Remotecomputer und dessen Konten gemeinsam genutzt wird.
    
    ```R  
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")   
    
    ## Add this line to create directory if it does not exist
    dir.create(sqlShareDir, recursive = TRUE) 
    ```  
    Sie sollten das standardmäßig angegebene Verzeichnis verwenden, anstatt manuell einen Ordner für dieses Argument anzugeben. Weitere Informationen finden Sie unter [RxInSqlServer (in englischer Sprache)](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver).
    
    Wenn Sie nur wissen möchten, welcher Ordner verwendet wird, können Sie `rxGetComputeContext` ausführen, um Details zum aktuellen Computekontext anzuzeigen. 
  

4.  Nachdem alle Variablen vorbereitet sind, stellen Sie diese als Argumente für den `RxInSqlServer`-Konstruktor bereit, um das Computekontext-Objekt zu definieren.  
  
    ```R  
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,        
         #shareDir = sqlShareDir,       
         wait = sqlWait,   
         consoleOutput = sqlConsoleOutput)  
    ```  
  
    Sie beobachten möglicherweise, dass die Syntax für *RxInSqlServer* fast identisch mit der Syntax der Funktion *RxSqlServerData* ist, die Sie zuvor zum Definieren der Datenquelle verwendet haben. Es gibt jedoch auch wichtige Unterschiede.  
  
    -   Das Datenquellenobjekt (mithilfe der Funktion *RxSqlServerData* definiert) gibt an, wo die Daten gespeichert werden.  
  
    -   Im Gegensatz dazu gibt der Computekontext (mit der Funktion *RxInSqlServer* definiert) an, wo Aggregationen und andere Berechnungen durchgeführt werden.  
  
    Das Definieren eines Computekontexts wirkt sich nicht auf andere generische R-Berechnungen aus, die Sie auf Ihrer Arbeitsstation ausführen können, und ändert nicht die Quelle der Daten. Sie können z.B. eine lokale Textdatei als Datenquelle definieren, aber SQL Server als Computekontext verwenden und alle Lesevorgänge und Zusammenfassungen der Daten auf dem SQL Server-Computer ausführen. 
  
## Aktivieren der Ablaufverfolgung für den Computekontext  
Es kann vorkommen, dass bei Vorgängen, die auf Ihren lokalen Kontext zugreifen, Probleme auftreten, wenn die Ausführung in einem spezifischen Remotecomputekontext erfolgt. Wenn Sie Probleme analysieren möchten oder die Leistung überwachen möchten, können Sie die Ablaufverfolgung im Computekontext aktivieren, um die Problembehandlung der Laufzeit zu unterstützen.  
  
1. Erstellen Sie einen neuen Computekontext, der die gleiche Verbindungszeichenfolge verwendet, aber fügen Sie dem *RxInSqlServer*-Konstruktor die Argumente *traceEnabled* und *traceLevel* hinzu.  
  
    ```R  
    sqlComputeTrace <- RxInSqlServer(   
        connectionString = sqlConnString,        
        #shareDir = sqlShareDir,  
        wait = sqlWait,   
        consoleOutput = sqlConsoleOutput,       
        traceEnabled = TRUE,
        traceLevel = 7)  
    ```  
  
    In diesem Beispiel ist *traceLevel* auf 7 gesetzt, d.h. „alle Ablaufverfolgungsinformationen anzeigen“.  

2. Um jederzeit zu diesem Computekontext zu wechseln, verwenden Sie die Funktion *rxSetComputeContext*, und geben Sie den Kontext anhand des Namens an.

    ```R  
    rxSetComputeContext( sqlComputeTrace)
    ```

    In diesem Tutorial verwenden Sie den Computekontext, bei dem die Ablaufverfolgung nicht aktiviert ist. Die Leistung für die Option, für die die Ablaufverfolgung aktiviert ist, wurde nicht für alle Vorgänge getestet, und Ihre Funktion kann entsprechend der Netzwerkkonnektivität variieren.  
  
Da Sie nun einen Remotecomputekontext erstellt haben, lernen Sie, wie Sie Computerkontexte ändern können, um R-Code lokal auf dem Server auszuführen.  
  
## Nächster Schritt  
[Lektion 2: Create and Run R Scripts &#40;Data Science Deep Dive&#41; (Erstellen und Ausführen von R-Skripts (Tieferer Einstieg in Data Science))](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## Vorheriger Schritt  
[Abfragen und Ändern der SQL Server-Daten &#40;Tieferer Einblick in Data Science&#41;](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## Siehe auch  
[Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
