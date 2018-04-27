---
title: 'Schritt 5: Testen der aktualisierten Pakete | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7208df70732d42a24f41728e19847f61d6a57645
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="lesson-1-5---testing-the-updated-packages"></a>Lektion 1-5: Testen der aktualisierten Pakete
Bevor Sie mit der nächsten Lektion fortfahren, in der Sie das Bereitstellungspaket erstellen, das bei der Installation der Lernprogrammpakete auf dem Zielcomputer verwendet werden soll, sollten Sie die Pakete testen. In dieser Aufgabe führen Sie die Pakete DataTransfer.dtsx und LoadXMLData aus, die Sie dem Deployment Tutorial-Projekt hinzugefügt und dann mit Konfigurationen erweitert haben.  
  
Bei der Ausführung der Pakete wird jede ausführbare Datei im Paket, die erfolgreich abgeschlossen wurde, in Grün angezeigt. Werden alle ausführbaren Dateien in Grün angezeigt, wurde das Paket erfolgreich abgeschlossen. Sie können den Status der Paketausführung auch auf der Registerkarte **Status** verfolgen.  
  
Werden die Pakete nicht erfolgreich ausgeführt, müssen Sie das Problem beheben, bevor Sie mit der nächsten Lektion fortfahren.  
  
### <a name="to-run-the-datatransfer-package"></a>So führen Sie das DataTransfer-Paket aus  
  
1.  Klicken Sie im Projektmappen-Explorer auf DataTransfer.dtsx.  
  
2.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
3.  Klicken Sie nach Ausführen des Pakets im Menü **Debuggen** auf **Debuggen beenden**.  
  
### <a name="to-run-the-loadxmldata-package"></a>So führen Sie das LoadXMLData-Paket aus  
  
1.  Klicken Sie im Projektmappen-Explorer auf LoadXMLData.dtsx.  
  
2.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
3.  Klicken Sie nach Ausführen des Pakets im Menü **Debuggen** auf **Debuggen beenden**.  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lesson 2: Create the Deployment Bundle in SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
  
  
