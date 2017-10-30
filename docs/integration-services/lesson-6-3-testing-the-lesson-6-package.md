---
title: 'Schritt 3: Testen des Pakets aus Lektion 6 | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0b97045d3916f7e3831bc1711e8657eecc58bdc0
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-6-3---testing-the-lesson-6-package"></a>Lektion 6 – 3: Testen des Lektion 6-Pakets
Zur Laufzeit erhält Ihr Paket den Wert für die Eigenschaft "Verzeichnis" vom VarFolderName-Parameter.  
  
Um zu überprüfen, ob vom Paket die Directory-Eigenschaft während der Laufzeit auf den neuen Wert aktualisiert wird, führen Sie das Paket einfach aus. Weil nur drei Beispieldatendateien in das neue Verzeichnis kopiert werden, wird der Datenfluss nur drei Mal ausgeführt, statt durch 14 Dateien im ursprünglichen Ordner zu iterieren.  
  
## <a name="checking-the-package-layout"></a>Überprüfen des Paketlayouts  
Bevor Sie das Paket testen, sollten Sie überprüfen, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 6 die in den folgenden Diagrammen gezeigten Objekte enthalten. Die Ablaufsteuerung sollte mit der Ablaufsteuerung in Lektion 5 übereinstimmen. Der Datenfluss sollte mit dem Datenfluss in Lektion 5 übereinstimmen.  
  
**Ablaufsteuerung**  
  
![Ablaufsteuerung](../integration-services/media/task3lesson6control.jpg "Ablaufsteuerung")  
  
**Datenfluss**  
  
![Datenfluss](../integration-services/media/task3lesson6data.jpg "Datenfluss")  
  
### <a name="to-test-the-lesson-6-tutorial-package"></a>So testen Sie das Lektion 6-Lernprogrammpaket  
  
1.  Klicken Sie im Menü "Debuggen" auf "Debuggen starten".  
  
2.  Klicken Sie nach Ausführen des Pakets im Menü "Debuggen" auf "Debuggen beenden".  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Schritt 4: Bereitstellen des Pakets aus Lektion 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
  

