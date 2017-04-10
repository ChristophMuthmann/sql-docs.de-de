---
title: "Schritt 9: Testen des Lektion 1-Lernprogrammpakets | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Schritt 9: Testen des Lektion 1-Lernprogrammpakets
In dieser Lektion haben Sie die folgenden Aufgaben ausgeführt:  
  
-   Ein neues [!INCLUDE[ssIS](../includes/ssis-md.md)] -Projekt erstellt.  
  
-   Die Verbindungs-Manager konfiguriert, die vom Paket zum Herstellen einer Verbindung mit den Quell- und Zieldaten benötigt werden.  
  
-   Einen Datenfluss hinzugefügt, der Daten aus einer Flatfilequelle abruft, die notwendigen Transformationen zum Suchen in den Daten ausführt und die Daten für das Ziel konfiguriert.  
  
Ihr Paket ist jetzt vollständig. Testen Sie jetzt Ihr Paket.  
  
## Überprüfen des Paketlayouts  
Bevor Sie das Paket testen, sollten Sie überprüfen, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 1 die in den folgenden Diagrammen gezeigten Objekte enthalten.  
  
**Ablaufsteuerung**  
  
![Control flow in package](../integration-services/media/task9lesson1control.gif "Control flow in package")  
  
**Datenfluss**  
  
![Data flow in package](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### So führen Sie das Lernprogrammpaket aus Lektion 1 aus  
  
1.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
    Das Paket wird ausgeführt, wobei der **FactCurrency** -Faktentabelle in **AdventureWorksDW2012**1.097 Zeilen erfolgreich hinzugefügt werden.  
  
2.  Klicken Sie nach Ausführen des Pakets im Menü **Debuggen** auf **Debuggen beenden**.  
  
## Nächste Lektion  
[Lesson 2: Adding Looping with SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## Siehe auch  
[Ausführung von Projekten und Paketen](../Topic/Execution%20of%20Projects%20and%20Packages.md)  
  
  
  
