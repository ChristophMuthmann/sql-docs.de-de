---
title: 'Schritt 3: Testen des Lektion 3-Tutorialpakets | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
caps.latest.revision: "27"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa344530396b13defc44680a1232a3d6a1c39b42
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-3-3---testing-the-lesson-3-tutorial-package"></a>Lektion 3-3: Testen des Lektion 3-Tutorialpakets
In dieser Aufgabe führen Sie das Paket Lesson 3.dtsx aus. Beim Ausführen des Pakets werden im Fenster Protokollereignisse die Protokolleinträge aufgelistet, die in die Protokolldatei geschrieben werden. Nachdem vom Paket die Ausführung abgeschlossen wurde, überprüfen Sie den Inhalt der Protokolldatei, die vom Protokollanbieter generiert worden ist.  
  
## <a name="checking-the-package-layout"></a>Überprüfen des Paketlayouts  
Bevor Sie das Paket testen, sollten Sie überprüfen, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 3 die in den folgenden Diagrammen gezeigten Objekte enthalten. Die Ablaufsteuerung sollte mit der Ablaufsteuerung in Lektion 2 übereinstimmen. Der Datenfluss sollte mit dem Datenfluss in den Lektionen 1 und 2 übereinstimmen.  
  
**Ablaufsteuerung**  
  
![Ablaufsteuerung im Paket](../integration-services/media/task4lesson2control.gif "Ablaufsteuerung im Paket")  
  
**Datenfluss**  
  
![Datenfluss im Paket](../integration-services/media/task9lesson1data.gif "Datenfluss im Paket")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>So führen Sie das Lernprogrammpaket aus Lektion 4 aus  
  
1.  Klicken Sie im Menü SSIS auf Protokollereignisse.  
  
2.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
3.  Klicken Sie nach Ausführen des Pakets im Menü **Debuggen** auf **Debuggen beenden**.  
  
### <a name="to-examine-the-generated-log-file"></a>So überprüfen Sie die generierte Protokolldatei  
  
-   Öffnen Sie mithilfe von Editor oder einem anderen Text-Editor die Datei TutorialLog.log.  
  
-   Obwohl dieses Tutorial die Semantik der Informationen, die für die Ereignisse **PipelineExecutionPlan** und **PipelineExecutionTrees** generiert wurden, nicht abdeckt, können Sie erkennen, dass in der ersten Zeile die Informationsfelder aufgeführt sind, die auf der Registerkarte **Details** des Dialogfelds **SSIS-Protokolle konfigurieren** angegeben wurden. Darüber hinaus können Sie überprüfen, dass die zwei von Ihnen ausgewählten Ereignisse (PipelineExecutionPlan und PipelineExecutionTrees) für jede Iteration der Foreach-Schleife protokolliert worden sind.  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 4: Hinzufügen der Fehlerflussumleitung mit SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  
