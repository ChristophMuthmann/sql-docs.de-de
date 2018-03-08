---
title: 'Schritt 9: Testen des Tutorialpakets aus Lektion 1 | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5fe1c97344edd6b5893fee1873df89a1ca37444c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-1-9---testing-the-lesson-1-tutorial-package"></a>Lektion 1-9: Testen des Tutorialpakets aus Lektion 1
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Ausführung von Projekten und Paketen](https://msdn.microsoft.com/library/ms141708(v=sql.110).aspx) 
  
  
  
