---
title: "Schritt 3: Testen des Lektion 3-Tutorialpakets | Microsoft Docs"
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
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Schritt 3: Testen des Lektion 3-Tutorialpakets
In dieser Aufgabe führen Sie das Paket Lesson 3.dtsx aus. Beim Ausführen des Pakets werden im Fenster Protokollereignisse die Protokolleinträge aufgelistet, die in die Protokolldatei geschrieben werden. Nachdem vom Paket die Ausführung abgeschlossen wurde, überprüfen Sie den Inhalt der Protokolldatei, die vom Protokollanbieter generiert worden ist.  
  
## Überprüfen des Paketlayouts  
Bevor Sie das Paket testen, sollten Sie überprüfen, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 3 die in den folgenden Diagrammen gezeigten Objekte enthalten. Die Ablaufsteuerung sollte mit der Ablaufsteuerung in Lektion 2 übereinstimmen. Der Datenfluss sollte mit dem Datenfluss in den Lektionen 1 und 2 übereinstimmen.  
  
**Ablaufsteuerung**  
  
![Control flow in package](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Datenfluss**  
  
![Data flow in package](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### So führen Sie das Lernprogrammpaket aus Lektion 4 aus  
  
1.  Klicken Sie im Menü SSIS auf Protokollereignisse.  
  
2.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
3.  Klicken Sie nach Ausführen des Pakets im Menü **Debuggen** auf **Debuggen beenden**.  
  
### So überprüfen Sie die generierte Protokolldatei  
  
-   Öffnen Sie mithilfe von Editor oder einem anderen Text-Editor die Datei TutorialLog.log.  
  
-   Obwohl dieses Tutorial die Semantik der Informationen, die für die Ereignisse **PipelineExecutionPlan** und **PipelineExecutionTrees** generiert wurden, nicht abdeckt, können Sie erkennen, dass in der ersten Zeile die Informationsfelder aufgeführt sind, die auf der Registerkarte **Details** des Dialogfelds **SSIS-Protokolle konfigurieren** angegeben wurden. Darüber hinaus können Sie überprüfen, dass die zwei von Ihnen ausgewählten Ereignisse (PipelineExecutionPlan und PipelineExecutionTrees) für jede Iteration der Foreach-Schleife protokolliert worden sind.  
  
## Nächste Lektion  
[Lektion 4: Hinzufügen der Fehlerflussumleitung mit SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  
