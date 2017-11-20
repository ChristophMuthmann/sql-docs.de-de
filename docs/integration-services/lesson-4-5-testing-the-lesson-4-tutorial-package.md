---
title: 'Schritt 5: Testen des Lektion 4-Lernprogrammpakets | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 68e4545ee2eae96664007a8dc69c9953c0351107
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-4-5---testing-the-lesson-4-tutorial-package"></a>Lektion 4-5: Testen des Lektion 4-Lernprogrammpakets
Die beschädigte Datei Currency_BAD.txt kann in der Currency Key-Transformation keine Übereinstimmung generieren. Weil die Fehlerausgabe von Currency Key Lookup jetzt so konfiguriert wurde, dass fehlerhafte Zeilen zum neuen Ziel für fehlerhafte Dateien umgeleitet werden, erzeugt die Komponente keinen Fehler, und das Paket wird erfolgreich ausgeführt. Alle fehlgeschlagenen Zeilen werden in die Datei ErrorOutput.txt geschrieben.  
  
In dieser Aufgabe testen Sie die überarbeitete Fehlerausgabekonfiguration, indem Sie das Paket ausführen. Bei einer erfolgreichen Paketausführung zeigen Sie dann den Inhalt der Datei ErrorOutput.txt an.  
  
> [!NOTE]  
> Wenn Sie keine Fehlerzeilen in der Datei ErrorOutput.txt anhäufen möchten, sollten Sie den Dateiinhalt zwischen Paketausführungen manuell löschen.  
  
## <a name="checking-the-package-layout"></a>Überprüfen des Paketlayouts  
Bevor Sie das Paket testen, sollten Sie überprüfen, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 4 die in den folgenden Diagrammen gezeigten Objekte enthalten. Die Ablaufsteuerung sollte mit der Ablaufsteuerung in den Lektionen 2 bis 4 übereinstimmen.  
  
**Ablaufsteuerung**  
  
![Ablaufsteuerung im Paket](../integration-services/media/task4lesson2control.gif "Ablaufsteuerung im Paket")  
  
**Datenfluss**  
  
![Datenfluss im Paket](../integration-services/media/task5lesson5data.gif "Datenfluss im Paket")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>So führen Sie das Lernprogrammpaket aus Lektion 4 aus  
  
1.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
2.  Klicken Sie nach Ausführen des Pakets im Menü **Debuggen** auf **Debuggen beenden**.  
  
### <a name="to-verify-the-contents-of-the-erroroutputtxt-file"></a>So überprüfen Sie den Inhalt der Datei ErrorOutput.txt  
  
-   Öffnen Sie in Editor oder einem anderen Texteditor die Datei ErrorOutput.txt. Die standardmäßige Spaltenreihenfolge ist: AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn und ErrorDescription.  
  
    Beachten Sie, dass alle in der Datei enthaltenen Zeilen den nicht übereinstimmenden CurrencyID-Wert BAD, den ErrorCode-Wert -1071607778, den ErrorColumn-Wert 0 und den ErrorDescription-Wert "Die Zeile ergab bei der Suche keine Übereinstimmung" enthalten. Der Wert für ErrorColumn ist auf 0 festgelegt, da der Fehler nicht spaltenspezifisch ist. Es ist der Suchvorgang, der fehlerhaft ist. .  
  
  
  

