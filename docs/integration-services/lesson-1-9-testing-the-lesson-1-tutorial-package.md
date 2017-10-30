---
title: 'Schritt 9: Testen des Lektion 1-Lernprogrammpakets | Microsoft Docs'
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca45e8e1ba02246eb5429bd7bfea125663f69f41
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-9---testing-the-lesson-1-tutorial-package"></a>Lektion 1 – 9: Testen des Lektion 1-Lernprogrammpakets
In dieser Lektion haben Sie die folgenden Aufgaben ausgeführt:  
  
-   Ein neues [!INCLUDE[ssIS](../includes/ssis-md.md)] -Projekt erstellt.  
  
-   Die Verbindungs-Manager konfiguriert, die vom Paket zum Herstellen einer Verbindung mit den Quell- und Zieldaten benötigt werden.  
  
-   Einen Datenfluss hinzugefügt, der Daten aus einer Flatfilequelle abruft, die notwendigen Transformationen zum Suchen in den Daten ausführt und die Daten für das Ziel konfiguriert.  
  
Ihr Paket ist jetzt vollständig. Testen Sie jetzt Ihr Paket.  
  
## <a name="checking-the-package-layout"></a>Überprüfen des Paketlayouts  
Bevor Sie das Paket testen, sollten Sie überprüfen, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 1 die in den folgenden Diagrammen gezeigten Objekte enthalten.  
  
**Ablaufsteuerung**  
  
![Ablaufsteuerung im Paket](../integration-services/media/task9lesson1control.gif "Ablaufsteuerung im Paket")  
  
**Datenfluss**  
  
![Datenfluss im Paket](../integration-services/media/task9lesson1data.gif "Datenfluss im Paket")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>So führen Sie das Lernprogrammpaket aus Lektion 1 aus  
  
1.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
    Das Paket wird ausgeführt, wobei der **FactCurrency** -Faktentabelle in **AdventureWorksDW2012**1.097 Zeilen erfolgreich hinzugefügt werden.  
  
2.  Klicken Sie nach Ausführen des Pakets im Menü **Debuggen** auf **Debuggen beenden**.  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lesson 2: Adding Looping with SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Siehe auch  
[Ausführung von Projekten und Paketen](https://msdn.microsoft.com/library/ms141708(v=sql.110).aspx) 
  
  
  

