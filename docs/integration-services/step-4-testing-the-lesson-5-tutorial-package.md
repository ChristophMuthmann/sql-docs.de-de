---
title: "Schritt 4: Testen des Lektion 5-Lernprogrammpakets | Microsoft Docs"
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
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Schritt 4: Testen des Lektion 5-Lernprogrammpakets
Zur Laufzeit erhält Ihr Paket den Wert für die **Directory** -Eigenschaft von einer zur Laufzeit aktualisierten Variable. Es wird also nicht der ursprüngliche Verzeichnisname verwendet, den Sie beim Erstellen des Pakets angegeben haben. Der Wert der Variablen wird durch die Datei SSISTutorial.dtsConfig aufgefüllt.  
  
Um zu überprüfen, ob vom Paket die Directory-Eigenschaft während der Laufzeit auf den neuen Wert aktualisiert wird, führen Sie das Paket einfach aus. Weil nur drei Beispieldatendateien in das neue Verzeichnis kopiert werden, wird der Datenfluss nur drei Mal ausgeführt, statt durch 14 Dateien im ursprünglichen Ordner zu iterieren.  
  
## Überprüfen des Paketlayouts  
Bevor Sie das Paket testen, sollten Sie überprüfen, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 5 die in den folgenden Diagrammen gezeigten Objekte enthalten. Die Ablaufsteuerung sollte mit der Ablaufsteuerung in Lektion 4 übereinstimmen. Der Datenfluss sollte mit dem Datenfluss in Lektion 4 übereinstimmen.  
  
**Ablaufsteuerung**  
  
![Control flow in package](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Datenfluss**  
  
![Data flow in package](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### So testen Sie das Lernprogrammpaket aus Lektion 5  
  
1.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
2.  Klicken Sie nach dem Ausführen des Pakets im Menü **Debuggen** auf **Debuggen beenden**.  
  
## Nächste Lektion  
[Lesson 6: Using Parameters with the Project Deployment Model in SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
